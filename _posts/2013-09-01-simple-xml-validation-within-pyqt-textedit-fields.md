---
id: 4059
title: Simple XML validation within PyQt TextEdit fields
date: 2013-09-01T03:49:57+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=4059
permalink: /2013/09/simple-xml-validation-within-pyqt-textedit-fields/
categories:
  - Drivel
  - Programming
tags:
  - PyQt
  - "why-isn't-it-built-in"
  - XML
---
As part of [Canard](https://github.com/LegoStormtroopr/canard "GitHub Canard site"), there is need for a very simple XML editor while the rich-text capabilities are finalised. So for the upcoming release, rather than work with a complex GUI, I&#8217;ve taken the easy option and will just allow the user to edit the very cut back rich text XML itself.

The complication with this is that a survey designer could write some invalid XML, which would be inserted into the rest of the document and break the entire file. The solution is to provide as-you-type validation of the XML to check that is valid. Fortunately, this is not as difficult as might be imagined, thanks to how easy to put together PyQt and Python are in general

Below is a screen shot of this little editor in action, with a very short code snippet that demonstrates how to do as-you-type XML validation inside of a PyQt application.

<div style="width: 618px" class="wp-caption alignnone">
  <img alt="Simple PyQT XML Editor in action" src="http://i.imgur.com/uh4Ium4.png" width="608" height="209" />
  
  <p class="wp-caption-text">
    Simple PyQT XML Editor in action
  </p>
</div>[<span style="color: #333333;">

<noscript>
  <pre><code class="language-python python">import sys
from lxml import etree
from PyQt4 import QtCore, QtGui

class editor(QtGui.QMainWindow):
    def __init__(self):
        super(editor, self).__init__()
        self.text = QtGui.QTextEdit()
        self.setCentralWidget(self.text)
        self.text.textChanged.connect(self.validate)
        
        self.statusBar()
        self.setWindowTitle('Simple XML editor')
        self.show() 
    def validate(self):
        try:
            root = etree.fromstring(str(self.text.toPlainText()))
            self.statusBar().showMessage("Valid XML")
        except etree.XMLSyntaxError, e:
            msg = e.error_log.last_error.message
            line=e.error_log.last_error.line
            col=e.error_log.last_error.column
            self.statusBar().showMessage("Invalid XML: Line %s, Col %s: %s"%(line,col,msg))
        except:
            self.statusBar().showMessage("Invalid XML: Unknown error")
        
def main():
    app = QtGui.QApplication(sys.argv)
    w = editor()
    sys.exit(app.exec_())
 
if __name__ == "__main__":
    main()
</code></pre>
</noscript></span>](https://gist.github.com/6402059)