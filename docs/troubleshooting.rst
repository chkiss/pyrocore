Trouble-Shooting Guide
======================

Reporting Problems
------------------

If you have any trouble during *pyrocore* installation and
configuration, or using any of the commands, join the `pyroscope-users`_
mailing list or the inofficial ``##rtorrent`` channel on
``irc.freenode.net``. IRC will generally provide a faster resolution.

If you are sure there is a bug, then `open an issue`_ on *GitHub*.
Make sure that nobody else reported the same problem before you,
there is a `search box`_ you can use (after the **Filter** button).
Please note that the *GitHub* issue tracker is not a support platform,
use e-mail or IRC for that.

.. note::

    Please describe your problem clearly, and provide any pertinent
    information.
    What are the version numbers of software and OS?
    What did you do?
    What was the unexpected result?
    If things worked and ‘suddenly’ broke, what did you change?

    On IRC, don't ask if somebody is there, just describe your problem.
    Eventually, someone will notice you – IRC is a global medium, and
    people *do* live in different time zones than you.

    Put up any logs on `0bin <http://0bin.net/>`_ or any other pastebin
    service, and make sure you removed any personal information you
    don't want to be publically known. Copy the pastebin link into IRC
    or into your message.

The following helps with querying your system environment, e.g. the
version of Python and your OS.

.. _`pyroscope-users`: http://groups.google.com/group/pyroscope-users
.. _`open an issue`: https://github.com/pyroscope/pyrocore/issues
.. _`search box`: https://help.github.com/articles/searching-issues/


Providing Diagnostic Information
--------------------------------

Python Diagnostics
^^^^^^^^^^^^^^^^^^

Execute the following command to be able to provide some information on
your Python installation:

.. code-block:: shell

    deactivate 2>/dev/null; /usr/bin/virtualenv --version; python <<'.'
    import sys, os, time, pprint
    pprint.pprint(dict(
        version=sys.version,
        prefix=sys.prefix,
        os_uc_names=os.path.supports_unicode_filenames,
        enc_def=sys.getdefaultencoding(),
        maxuchr=sys.maxunicode,
        enc_fs=sys.getfilesystemencoding(),
        tz=time.tzname,
        lang=os.getenv("LANG"),
        term=os.getenv("TERM"),
        sh=os.getenv("SHELL"),
    ))
    .

If ``enc_fs`` is **not** ``UTF-8``, then call
``dpkg-reconfigure locales`` (on Debian type systems) and choose a
proper locale (you might also need ``locale-gen en_US.UTF-8``), and make
sure ``LANG`` is set to ``en_US.UTF-8`` (or another locale with UTF-8
encoding).


OS Diagnostics
^^^^^^^^^^^^^^

Similarly, execute this in a shell prompt:

.. code-block:: shell

    uname -a; echo $(lsb_release -as 2>/dev/null); grep name /proc/cpuinfo | uniq -c; \
    free -m | head -n2; uptime; \
    strings $(which rtorrent) | grep "client version"; \
    ldd $(which rtorrent) | egrep "lib(torrent|curses|curl|xmlrpc.so|cares|ssl|crypto)"; \
    ps auxw | egrep "USER|/rtorrent" | grep -v grep


Common Problems & Solutions
---------------------------

**TODO** Provide feedback on what you ran into in the past. Or make a PR with additions.