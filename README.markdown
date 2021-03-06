clipcli
=======

Lightweight Python command-line interface to the GTK clipboard.

Dependencies
------------

- Python 2.6 or (hopefully) 2.7.

    I've only tested this thing with Python 2.6.  It might work with earlier versions too, though I didn't think about that when writing it.  I have not yet consciously accepted the existence of Python 3.
    
    It's pretty dead simple so the chances that it will work with other versions are pretty good.

- `argparse`:
  Included with Python 2.7; otherwise installable via

        $ easy_install argparse

- [`pygtk`](http://pypi.python.org/pypi/PyGTK/2.12.1):
  Generally installable via system package managers: for instance, debian-likes have the package `python-gtk2`.

    Otherwise this will do:

        $ easy_install pygtk



Usage
-----

    clipcli [-h] [-d] [-f FILE] [-l] [TARGET]

    positional arguments:
      TARGET                display the contents of this target

    optional arguments:
      -h, --help            show this help message and exit
      -d, --debug           enable debug tracing
      -f FILE, --file FILE  the file to which output will be directed
      -l, --list            list available targets

Examples
--------

These examples were created
after copying from within the Chrome browser the words "The argparse module"
that appear at the beginning of the
[argparse documentation](http://docs.python.org/library/argparse.html).

The bash-python `crapwrap` function is used just to make this page presentable.
Any suggestions of ways to provide more intelligent wrapping of tidied html are quite welcome.

    $ clipcli -l
    TIMESTAMP
    TARGETS
    MULTIPLE
    COMPOUND_TEXT
    STRING
    TEXT
    UTF8_STRING
    text/html
    text/plain

    $ clipcli text/plain
    The argparse module

    $ function crapwrap { python -c '
        from fileinput import input
        from itertools import chain
        from textwrap import TextWrapper
        wrap = TextWrapper(subsequent_indent="......").wrap
        lines = chain.from_iterable(wrap(l) for l in input())
        from sys import stdout
        stdout.writelines(l + "\n" for l in lines)
      ' "$@"; }

    $ clipcli text/html | tidy -c -q -i 2>/dev/null | crapwrap
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
    <html>
    <head>
      <meta name="generator" content=
      "HTML Tidy for Linux (vers 25 March 2009), see www.w3.org">
      <meta http-equiv="content-type" content=
      "text/html; charset=us-ascii">
      <title></title>
      <style type="text/css">
    span.c2 {-webkit-border-horizontal-spacing: 0px; -webkit-border-
    ......vertical-spacing: 0px; -webkit-text-decorations-in-effect: none;
    ......-webkit-text-size-adjust: auto; -webkit-text-stroke-width: 0px;
    ......border-collapse: separate; color: rgb(0, 0, 0); font-family:
    ......'Liberation Serif'; font-size: medium; font-style: normal; font-
    ......variant: normal; font-weight: normal; letter-spacing: normal;
    ......line-height: normal; orphans: 2; text-align: auto; text-indent:
    ......0px; text-transform: none; white-space: normal; widows: 2; word-
    ......spacing: 0px}
      tt.c1 {background-color: transparent; padding-top: 0px; padding-
    ......right: 1px; padding-bottom: 0px; padding-left: 1px; font-size:
    ......0.95em; font-weight: bold;}
      </style>
    </head>
    <body>
      <span class=
      "Apple-style-span Apple-style-span c2">The<span class="Apple-
    ......converted-space">&Acirc;&nbsp;</span><tt class="xref docutils
    ......literal c1"><span class="pre">argparse</span></tt><span class
    ......="Apple-converted-space">&Acirc;&nbsp;</span>module</span>
    </body>
    </html>

