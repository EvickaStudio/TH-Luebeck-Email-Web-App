import os
import urllib.request
from PyQt5.QtCore import QUrl
from PyQt5.QtWidgets import QApplication
from PyQt5.QtGui import QIcon
from PyQt5.QtWebEngineWidgets import QWebEngineView, QWebEnginePage, QWebEngineProfile


class ThMail:
    """
    A class to represent the ThMail webmail application.

    ...

    Attributes
    ----------
    app : QApplication
        an instance of QApplication
    view : QWebEngineView
        an instance of QWebEngineView
    profile : QWebEngineProfile
        an instance of QWebEngineProfile
    page : QWebEnginePage
        an instance of QWebEnginePage

    Methods
    -------
    load_webmail():
        loads the ThMail webmail application
    save_session():
        saves the session by clearing visited links, http cache and cookies
    """

    def __init__(self):
        """
        Constructs all the necessary attributes for the ThMail object.
        """
        self.app = QApplication([])
        self.view = QWebEngineView()
        self.profile = QWebEngineProfile.defaultProfile()
        self.profile.setPersistentCookiesPolicy(
            QWebEngineProfile.ForcePersistentCookies
        )
        self.page = QWebEnginePage(self.profile, self.view)
        self.view.setPage(self.page)
        self.view.setGeometry(100, 100, 1300, 800)  # set the geometry to 800x600

    def check_favicon(self):
        """
        Checks if the favicon.ico file exists in the current directory, if not downloads it from the web.
        """
        if not os.path.exists("favicon.ico"):
            urllib.request.urlretrieve(
                "https://qis.th-luebeck.de/favicon.ico", "favicon.ico"
            )

    def load_webmail(self):
        """
        Loads the ThMail webmail application.
        """
        self.check_favicon()
        self.app.setWindowIcon(QIcon("favicon.ico"))
        self.view.load(QUrl("https://webmail.th-luebeck.de/"))
        self.view.show()

    def save_session(self):
        """
        Saves the session by clearing visited links, http cache and cookies.
        """
        self.profile.clearAllVisitedLinks()
        self.profile.clearHttpCache()
        self.profile.clearAllCookies()

    def run(self):
        """
        Runs the application and connects the save_session method to the aboutToQuit signal.
        """
        self.app.aboutToQuit.connect(self.save_session)
        self.app.exec_()


if __name__ == "__main__":
    thmail = ThMail()
    thmail.load_webmail()
    thmail.run()
