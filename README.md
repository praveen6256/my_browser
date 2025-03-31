# MY_Browser

This is a simple custom web browser built using Python. It allows users to enter a URL and navigate websites with basic browsing functionalities like back, forward, home, and reload.

## Features
- Open and navigate web pages
- Back, Forward, Home, and Reload buttons
- URL/Search bar for navigating websites
- Developed using Python and PyQt5

## Requirements
Ensure you have Python installed on your system. You also need the following dependencies:

```sh
pip install PyQt5 PyQtWebEngine
```

## Installation
1. Clone this repository or create a new project in PyCharm.
2. Install the required dependencies using the command above.
3. Copy the following Python script into your project:

```python
import sys
from PyQt5.QtCore import *
from PyQt5.QtWidgets import *
from PyQt5.QtWebEngineWidgets import *


class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.browser = QWebEngineView()
        self.browser.setUrl(QUrl('http://google.com'))
        self.setCentralWidget(self.browser)
        self.showMaximized()

        # navbar
        navbar = QToolBar()
        self.addToolBar(navbar)

        back_btn = QAction('Back', self)
        back_btn.triggered.connect(self.browser.back)
        navbar.addAction(back_btn)

        forward_btn = QAction('Forward', self)
        forward_btn.triggered.connect(self.browser.forward)
        navbar.addAction(forward_btn)

        reload_btn = QAction('Reload', self)
        reload_btn.triggered.connect(self.browser.reload)
        navbar.addAction(reload_btn)

        home_btn = QAction('Home', self)
        home_btn.triggered.connect(self.navigate_home)
        navbar.addAction(home_btn)

        self.url_bar = QLineEdit()
        self.url_bar.returnPressed.connect(self.navigate_to_url)
        navbar.addWidget(self.url_bar)

        self.browser.urlChanged.connect(self.update_url)

    def navigate_home(self):
        self.browser.setUrl(QUrl('http://programming-hero.com'))

    def navigate_to_url(self):
        url = self.url_bar.text()
        self.browser.setUrl(QUrl(url))

    def update_url(self, q):
        self.url_bar.setText(q.toString())


app = QApplication(sys.argv)
QApplication.setApplicationName('My Cool Browser')
window = MainWindow()
app.exec_()
```

## Usage
- Run the script in PyCharm or using the command line:

  ```sh
  python custom_browser.py
  ```
- Enter a website URL in the URL bar.
- Use the Back, Forward, Home, and Reload buttons to navigate.

## License
This project is open-source and free to use. Modify it as needed!

