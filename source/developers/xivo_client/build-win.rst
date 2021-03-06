.. index:: single:XiVO Client

*********************************************
Building the XiVO Client on Windows platforms
*********************************************

This page explains how to build an executable of the XiVO Client from its
sources for Windows.


Windows Prerequisites
=====================

Cygwin
------

`Cygwin Web site <http://www.cygwin.com/>`_

Click the "setup" link and execute.

During the installer, check the package:

* Devel > git


Qt SDK
------

You need the development files of the Qt library.

To download the Qt SDK, you might need to create an account on the Nokia website.

`Qt SDK download page <http://www.developer.nokia.com/Develop/Qt/Tools>`_

During the installer:

* choose a Custom installation
* uncheck all components
* check only:

  * Development tools / Desktop Qt / Qt 4.8.1 (Desktop) / Desktop Qt 4.8.1 - MinGW
  * Miscellaneous / MinGW 4.4


NSIS (optional)
---------------

You will only need NSIS installed if you want to create an installer for the
XiVO Client.

`NSIS download page <http://nsis.sourceforge.net/Download>`_

During the installer, choose the full installation.


Get sources
===========

In a **Cygwin shell**::

   git clone git://github.com/xivo-pbx/xivo-client-qt.git
   cd xivo-client-qt


Building
========

Path configuration
------------------

If you did not change the default path for installation of Qt and NSIS, you can
skip this step, because the default paths are used.

If you did, you must change the values in
:file:`C:\\Cygwin\\home\\user\\xivo-client-qt\\build-deps` to match the paths of
your installed programs. You must use an editor capable of understanding Unix
end of lines, such as `Notepad++ <http://notepad-plus-plus.org>`_.

Replace ``C:\`` with ``/cygdrive/c`` and backslashes (``\``) with slashes
(``/``). You must respect the case of the directory names. Paths containing
spaces must be enclosed in double quotes (``"``).

For example, if you installed NSIS in :file:`C:\\Program Files (x86)\\nsis`, you
should write::

   WIN_NSIS_PATH="/cygdrive/c/Program files (x86)/nsis"


Build
-----

In a **Cygwin shell**::

   source build-deps
   export PATH=$WIN_QT_PATH/bin:$WIN_MINGW_PATH/bin:$PATH

   qmake
   mingw32-make

Binaries are available in the ``bin`` directory.

The version of the executable is taken from the ``git describe`` command.


Launch
======

You can launch the built executable with::

   bin/xivoclient


Package
=======

To create the installer::

   mingw32-make pack

This will result in a ``.exe`` file in the current directory.


Build options
=============

To add a console::

   qmake CONFIG+=console

To generate debug symbols::

   mingw32-make DEBUG=yes


Clean
-----

::

   mingw32-make distclean
