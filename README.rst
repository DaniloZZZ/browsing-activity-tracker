Browsing Activity Tracker
=========================

This extension provides a flexible way to log your browsing activity. In
particular, it allows you to track how much time you spend on websites. The
approach is minimalistic and give you direct access to the raw browsing data
that you can then analyze and aggregate to your taste.

In contrast, other extensions with the same purpose often require that you
create an account on their website and store your browsing data. Furthermore,
they only give you access to an automatically generated report with very little
control over how it is produced.

Installation
++++++++++++

The extension is available both as a Firefox add-on and as a Chrome extension.

How does it work?
+++++++++++++++++

The extension notifies a callback URL by sending an HTTP POST request whenever
one the following events occur:

* the browser window is activated (gains focus)
* a tab is activated
* a webpage is loaded
* the browser window is deactivated (loses focus)

The content of the POST request is a JSON object containing the following keys:

=========  ===========
Key Name   Description
=========  ===========
``title``  Title of the webpage (typically the content of the ``<title>`` tag)
``url``    URL of the webpage
``time``   Time at which the event occured. Number of milliseconds elapsed since 1 January 1970 00:00:00 UTC
``key``    A key identifying the browser sending the request
=========  ===========

For window activation events, all the keys except for the ``time`` key are set
to ``null``.

Example of request content:

.. code:: json

    {"url":"http://getbootstrap.com/css/",
     "time":1405240158749,
     "title":"CSS · Bootstrap",
     "key":"firefox"}


Also note that the window activation and deactivation events are triggered by
your window manager and vary depending on your operating system and window
manager. For example, in window managers based on X11, a deactivation event is
always triggered before an activation event.

Configuration
+++++++++++++

The browser key and the callback URL can be customized in the extension
preferences. The key is useful in settings where you are logging events from
several browsers at the same time as well as to provide some (very limited)
authentication.