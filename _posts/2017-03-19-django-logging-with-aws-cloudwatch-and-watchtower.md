---
title: Configuring Django logging with Amazon CloudWatch using Watchtower
author: Samuel Spencer
layout: post
categories:
  - django
  - aws
---

You're running your Django app in the cloud, and you want to be able to track your logs with AWS CloudWatch? Easy!

  * Step 1: Install [Python WatchTower](https://watchtower.readthedocs.io/en/latest/) - `pip install watchtower`

  * Step 2: Set up your AWS credentials with the `awscli` - fun fact this also [works with Temporary Credentials on EC2](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html)

  * Step 3: Change up your `LOGGING` settings in your Django settings - make sure at least one handler has `'class': 'watchtower.CloudWatchLogHandler',`

      ```
      LOGGING = {
          'version': 1,
          'handlers': {
              'watchtower':  {
                  'level': 'DEBUG',  # Or some more appropriate level
                  'class': 'watchtower.CloudWatchLogHandler',
              },
          },
          'loggers': {
              'django': {
                  'handlers': ['watchtower'],
                  'level': 'DEBUG',  # Or some more appropriate level
                  'propagate': True,
              },
          }
      }
      ```

  * Step 4: Make sure you have the following permissions setup for the AWS IAM user:

      ```
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": [
                "arn:aws:logs:<YOUR_REGION>:<YOUR_INSTANCE>:log-group:watchtower:log-stream:*"
            ]
        }
      ```
  
  If you don't know what `<YOUR_REGION>` or `<YOUR_INSTANCE>` should be, monitor your console and it will become *painfully* obvious.

Congrats! Now, restart your server and go checkout your CloudWatch and watch your logs come in!

![image](https://cloud.githubusercontent.com/assets/2173174/24124783/7757445a-0e19-11e7-9dba-00df3384ae67.png)
