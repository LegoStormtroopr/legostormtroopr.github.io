---
title: WTF Django - Vol 1 - Converting a model to multi-table inheritance, with a many to many field and retaining your sanity
author: Samuel Spencer
layout: post
categories:
  - Python
  - Django
  - WTF Django
---

This isn't a post about how Django has WTFs, its about you doing a huge WTF withour code in django and trying to fix it.

If you've arrived on this page, I want to say this - Its ok - you tried, messed up your models design 6 months and many users ago,
you have a django model you actually need to inherit from something else,
and if you are like me you are trying to un-fuck it all up. And the good news, is you can. I did it too, and we can get through this.

But first the problem, you are making a simple app and want to associated users with planes they can fly, and a list of parking bays
that belong to a plane (lets assume a plane can have many bays). So we have a simple `models.py` like this:

```
# 0001_initial
class Plane(models.Model):
    registration=models.CharField(#some settings)
    pilots=models.ManyToManyField(User)

class ParkingBay(models.Model):
    plane=models.ForeignKey(Plane)
```

But... after 100 users have created 1000 aircraft, you've realised drones have become popular, but they don't have pilots.
But you want to be able to treat drones and planes in a similar way. What you've learned is you really want this:

```
# 0002_drones_ahoy
class Aircraft(models.Model):
    registration=models.CharField(#some settings)

class Plane(Aircraft):
    pilots=models.ManyToManyField(User)
```

Well, django doesn't like this because it needs to create a pointer on the child class back to its parent of the
form `<parent_model_name>_ptr` and its mandatory and needs a default - and you'll see this as soon as you try to migrate:

```
You are trying to add a non-nullable field 'aircraft_ptr' to plane without a default; we can't do that (the database needs something to populate existing rows).
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows)
 2) Quit, and let me add a default in models.py
```
Neither of these work! We don't want a default, and we *really, really* don't want to be altering primary keys.
So for now, set a default of 99999999999. Just so we can find it in our new migration:

```
class Migration(migrations.Migration):

    dependencies = [
        ('part1', '0001_initial'),
    ]

    operations = [
        migrations.CreateModel(
            name='Aircraft',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('registration', models.CharField(max_length=100)),
            ],
        ),
        migrations.RemoveField(
            model_name='plane',
            name='id',
        ),
        migrations.RemoveField(
            model_name='plane',
            name='registration',
        ),
        migrations.AddField(
            model_name='plane',
            name='aircraft_ptr',
            field=models.OneToOneField(auto_created=True, default=999999, on_delete=django.db.models.deletion.CASCADE, parent_link=True, primary_key=True, serialize=False, to='part1.Aircraft'),
            preserve_default=False,
        ),
    ]
```

Everything is is wrong - for starters you'll lose your id fields. So, lets start fixing the operations:

```
class Migration(migrations.Migration):
    #  trimmed ...
    operations = [
        migrations.CreateModel(
            name='Aircraft',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('registration', models.CharField(max_length=100)),
            ],
        ),
        migrations.RenameField(  # Don't remove, rename
            model_name='plane',
            old_name='id',
            new_name='aircraft_ptr'   # Make the id the pointer
        ),
        migrations.RemoveField(
            model_name='plane',
            name='registration',
        ),
        migrations.AlterField( # Don't add the field, Alter the existing one to fix it up
            model_name='plane',
            name='aircraft_ptr',
            field=models.OneToOneField(auto_created=True, default=999999, on_delete=django.db.models.deletion.CASCADE, parent_link=True, primary_key=True, serialize=False, to='part1.Aircraft'),
            preserve_default=False,
        ),
    ]
```

Ok, but we are still removing all of the registrations we know about. Unfortunately, django doesn't have a Copy migration operation,
so lets make one:

```
class CopyFieldsBetweenTables(Operation):

    reversible = False

    def __init__(self, model_from_name, model_to_name, columns):
        self.model_from_name = model_from_name
        self.model_to_name = model_to_name
        self.columns = columns

    def state_forwards(self, app_label, state):
        pass

    def database_forwards(self, app_label, schema_editor, from_state, to_state):
        columns = ", ".join(self.columns)
        base_query = """
            INSERT INTO %s_%s
            (%s)
            SELECT %s
            FROM %s_%s;
        """ % tuple(
            [app_label, self.model_to_name, columns, columns, app_label, self.model_from_name]
        )
        schema_editor.execute(base_query)

    def describe(self):
        return "Copies between two tables for %s" % self.name
```

This is a pretty hacky piece of code, that accepts a table to copy from and to, with the columns to copy. I've written this
to accept multiple columns as I had to reclocate a few to the parent class (you might need to as well).

So instead of deleting the registration, lets change it to this:

```
    CopyFieldsBetweenTables(
        model_from_name='plane',
        model_to_name='aircraft',
        columns=['registration' ],
    ),
```

Groovy! Now we can do this in our code:
```
Plane.objects.count()
> 100
```
Part 1 is done! We've successfully changed our model to use multi-table inheritance! The bad news is that  pesky ManyToManyField wasn't
touched. The problem with that is 
behind the scenes in state `0001_initial` django made us a `planes` table to hold our planes and a `plane_users` table with a 
foreign key to the `planes` table to hold the many-to-many that looks like this:

```
select * from table_plane;
id | registration
---|-------------
 1 | WTF-0001
 2 | TLA-0002

select * from table_plane_pilots;
id | plane_id | user_id
---|------_---|----------
 1 |        1 | 1
 2 |        2 | 1
```

Great, except that when we try to in state `0002_drones_ahoy` we have this:

```
select * from table_aircraft;
id | registration
---|-------------
 1 | WTF-0001
 2 | TLA-0002

select * from table_plane;
aircraft_ptr_id 
----------------
              1 
              2 

select * from table_plane_pilots;
id | plane_id | user_id
---|------_---|----------
 1 |        1 | 1
 2 |        2 | 1
```

Oh crap! Django has successfully migrated `planes` so that the primary key for `planes` is a foreign key back to our aircraft table
but the reference for a `plane_id` still! If we look under the scenes and check the schema we see this:

```
sqlite> .schema table_plane_pilots
CREATE TABLE "table_plane_pilots" (
    "id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
    "plane_id" integer NOT NULL REFERENCES "table_plane" ("id"),
    "user_id" integer NOT NULL REFERENCES "auth_user" ("id"), UNIQUE ("plane_id", "user_id"));

```

Well, this is unfortunate, the reference on `plane_pilots` refers to a column that doesn't exist!

We need to do some more untangling and do to that we need to
[`SeparateDatabaseAndState`](https://docs.djangoproject.com/en/1.10/ref/migration-operations/#separatedatabaseandstate).
You see, the state of our app is now fine - but the database is still busted. So now our migrations needs to look like this:

```
class Migration(migrations.Migration):

    state_operations = [
      # we've renamed what was "operations" above to "state operations"
      # so this is all our original operations, as these are fine
    ]

    database_operations = state_operations

    operations = [
        migrations.SeparateDatabaseAndState(
            database_operations=database_operations,
            state_operations=state_operations)
    ]
```

But we need to do extra stuff to our database operations to make sure everything is setup correct. By separating the database 
and state we can make alterations to the database, with impacting our app
*(I'll level with you, I'm not 100% sure what this does, but it works)*.
The key here is **we can't change the many to many columns**, so we are going to copy the many-to-many, delete it and recrate it.

Since the next bit means adding lots of operations, the next section is commented inline:

```
    database_operations = state_operations + [
        
        # !!! This is a fake model to capture our many to many
        # We use Integer fields so we don't have to deal with more referential wierdness
        
        migrations.CreateModel(
            name='planes_pilots_temp',
            fields=[
                ('plane_id', models.IntegerField()),
                ('user_id', models.IntegerField()),
            ]
        ),
        
        # !!! Copy from the actual M2M to our fake M2M field

        CopyFieldsBetweenTables(
            model_from_name='planes_pilots',
            model_to_name='planes_pilots_temp',
            columns=['plane_id', 'user_id'],
        ),

        # !!! Remove the old many to mnay relationship
        migrations.RemoveField(
            model_name='plane',
            name='pilots',
        ),

        # !!! .... and now add the many-to-many it back
        migrations.AddField(
            model_name='plane',
            name='pilots',
            field=models.ManyToManyField(to=settings.AUTH_USER_MODEL, blank=True),
            preserve_default=True
        ),

        # !!! And we can copy from the temp back in safely!
        CopyFieldsBetweenTables(
            model_from_name='planes_pilots_temp',
            model_to_name='planes_pilots',
            columns=['plane_id', 'user_id'],
        ),

        # !!! Lastly delete the temp field
        migrations.DeleteModel('planes_pilots_temp'),
```

There, Easy!!! Except there is one more problem hiding behind the scenes, if there are *any* Foreign keys, like our parking bay,
they still have references to the old column. Fortunately, in our database_operations we need to add:

```
        # Fix status and review request fields
        migrations.AlterField(
            model_name='parking_bay',
            name='plane',
            field=models.ForeignKey(to='my_app.Plane'),
            preserve_default=True,
        ),
```

Congratulations, if you've made it this far, you've been able to change the inheritance of your model,
fixed all of your relationships, and maintained most of your sanity!
