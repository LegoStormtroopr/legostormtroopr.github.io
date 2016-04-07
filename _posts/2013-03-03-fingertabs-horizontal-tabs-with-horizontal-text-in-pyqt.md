---
id: 2802
title: '&#8220;FingerTabs&#8221; &#8211; Horizontal Tabs with Horizontal Text in PyQt'
date: 2013-03-03T10:17:40+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=2802
permalink: /2013/03/fingertabs-horizontal-tabs-with-horizontal-text-in-pyqt/
categories:
  - Programming
  - Python
tags:
  - desktop development
  - FingerTabs
  - programming
  - PyQt
---
On advice from someone far more experienced in user interface, I was given some feedback on Canard (a questionnaire specification editor) and was pointed in the direction of FingerTabs. Although, its not a widely used term ([unless you are an archer](http://en.wikipedia.org/wiki/Finger_tab)) I couldn&#8217;t find anything other term for what are height-wise stacked (in PyQt this west or east positioned tabs) tabs with horizontal labels. FingerTabs are call so, because they look like a bunch of long little fingers, although this visual metaphor breaks down if you have more than 5 tabs, or a Lovecraftian imagination. For example:

<div style="width: 294px" class="wp-caption alignnone">
  <img class=" " alt="Normal (or top aligned) tabs." src="http://i47.tinypic.com/33ndiq0.png" width="284" height="185" />
  
  <p class="wp-caption-text">
    Normal (or top aligned) tabs.
  </p>
</div>

<div style="width: 294px" class="wp-caption alignnone">
  <img class=" " alt="Left (or west) aligned tabs with PyQt Default text orientation." src="http://i45.tinypic.com/sxm2de.png" width="284" height="185" />
  
  <p class="wp-caption-text">
    Left (or west) aligned tabs with PyQt Default text orientation.
  </p>
</div>

<div style="width: 292px" class="wp-caption alignnone">
  <img class=" " alt="Left aligned tabs with normal (or horizontal) oriented text." src="http://i47.tinypic.com/ohpt06.png" width="282" height="182" />
  
  <p class="wp-caption-text">
    Left aligned tabs with normal (or horizontal) oriented text.
  </p>
</div>

If you want to go down the path of stacked tabs, the last way is probably the best to go for as it is much easier to read, and you can fit more tabs in the space vertical space, with little loss of horizontal space, as the examples above illustrate. Interestingly enough getting the last one, is quite easy, although not well publicised.

Changing from the top to the bottom is just a matter of extending the QTabBar of the QTabWidget and overriding the default paintEvent and sizeHint. This allows you to override the original text orientation, and insert it in a more readbale fashion. The difficult bit was determining how to reuse the default tab sytling (line 10 and 17 in FingerTabs.py below).

<noscript>
  <pre><code class="language-python python">from PyQt4 import QtGui, QtCore
from FingerTabs import FingerTabWidget

import sys

app = QtGui.QApplication(sys.argv)
tabs = QtGui.QTabWidget()
tabs.setTabBar(FingerTabBarWidget(width=100,height=25))
digits = ['Thumb','Pointer','Rude','Ring','Pinky']
for i,d in enumerate(digits):
    widget =  QtGui.QLabel("Area #%s &lt;br&gt; %s Finger"% (i,d))
    tabs.addTab(widget, d)
tabs.setTabPosition(QtGui.QTabWidget.West)
tabs.show()
sys.exit(app.exec_())
</code></pre>
  
  <pre><code class="language-python python"># Updated so a PyQT4 Designer TabWidget can be promoted to a FingerTabWidget

from PyQt4 import QtGui, QtCore
 
class FingerTabBarWidget(QtGui.QTabBar):
    def __init__(self, parent=None, *args, **kwargs):
        self.tabSize = QtCore.QSize(kwargs.pop('width',100), kwargs.pop('height',25))
        QtGui.QTabBar.__init__(self, parent, *args, **kwargs)
                 
    def paintEvent(self, event):
        painter = QtGui.QStylePainter(self)
        option = QtGui.QStyleOptionTab()
 
        for index in range(self.count()):
            self.initStyleOption(option, index)
            tabRect = self.tabRect(index)
            tabRect.moveLeft(10)
            painter.drawControl(QtGui.QStyle.CE_TabBarTabShape, option)
            painter.drawText(tabRect, QtCore.Qt.AlignVCenter |\
                             QtCore.Qt.TextDontClip, \
                             self.tabText(index));
        painter.end()
    def tabSizeHint(self,index):
        return self.tabSize

# Shamelessly stolen from this thread:
#   http://www.riverbankcomputing.com/pipermail/pyqt/2005-December/011724.html
class FingerTabWidget(QtGui.QTabWidget):
    """A QTabWidget equivalent which uses our FingerTabBarWidget"""
    def __init__(self, parent, *args):
        QtGui.QTabWidget.__init__(self, parent, *args)
        self.setTabBar(FingerTabBarWidget(self))
</code></pre>
  
  <pre><code class="language-text text">This [trivial fingertab gist](https://gist.github.com/LegoStormtroopr/5075267) is released as Public Domain, but boy would it beswell if you could credit me, or tweet me [@LegoStormtoopr](http://www.twitter.com/legostormtroopr) to say thanks!</code></pre>
</noscript>

For what its worth, those 38 lines of code took about 4 hours to write for a staggering 1 line of code every 6 minutes (and 20 seconds).

Thanks go to the two threads from StackOverflow, where the first answer got me close enough to implement the above:

  * <http://stackoverflow.com/questions/3607709/how-to-change-text-alignment-in-qtabwidget>
  * <http://stackoverflow.com/questions/12901095/change-background-color-of-tabs-in-pyqt4>