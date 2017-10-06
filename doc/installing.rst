=============================================
Installing the Desktop Synchronization Client
=============================================

You can download the  latest version of the ownCloud Desktop Synchronization
Client from the `ownCloud download page
<https://owncloud.org/install/#desktop>`_.
There are clients for Linux, Mac OS X, and Microsoft Windows.

Installation on Mac OS X and Windows is the same as for any software
application: download the program and then double-click it to launch the
installation, and then follow the installation wizard. After it is installed and
configured the sync client will automatically keep itself updated; see
:doc:`autoupdate` for more information.

Linux users must follow the instructions on the download page to add the
appropriate repository for their Linux distribution, install the signing key,
and then use their package managers to install the desktop sync client. Linux
users will also update their sync clients via package manager, and the client
will display a notification when an update is available.

Linux users must also have a password manager enabled, such as GNOME Keyring or
KWallet, so that the sync client can login automatically.

You will also find links to source code archives and older versions on the
download page.

Customizing the Windows installation
----------------------------------

If you just want to install ownCloud Desktop Synchronization Client on your local
system, you can simply launch the .msi file and configure it in the wizard
that pops up.

Features
^^^^^^^^

The MSI installer provides several features that can be installed or removed
individually, which you can also control via command-line, if you are automating
the installation::

   msiexec /passive /i ownCloud-x.y.z.msi

will install the ownCloud Desktop Synchronization Client into the default location
with the default features enabled. If you want to disable e.g. desktop shortcut
icons you can simply change the above command to::

   msiexec /passive /i ownCloud-x.y.z.msi REMOVE=DesktopShortcut

See the following table for a list of available features:

+--------------------+--------------------+----------------------------------+---------------------------+
| Feature            | Enabled by default | Description                      |Property to disable        |
+====================+====================+==================================+---------------------------+
| Client             | Yes, required      | The actual client                |                           |
+--------------------+--------------------+----------------------------------+---------------------------+
| DesktopShortcut    | Yes                | Adds a shortcut to the desktop   |`NO_DESKTOP_SHORTCUT`      |
+--------------------+--------------------+----------------------------------+---------------------------+
| StartMenuShortcuts | Yes                | Adds shortcuts to the start menu |`NO_START_MENU_SHORTCUTS`  |
+--------------------+--------------------+----------------------------------+---------------------------+
| ShellExtensions    | Yes                | Adds Explorer integration        |`NO_SHELL_EXTENSIONS`      |
+--------------------+--------------------+----------------------------------+---------------------------+

*** Installation ***

You can also choose to only install the client itself by using the following command::

  msiexec /passive /i ownCloud-x.y.z.msi ADDDEFAULT=Client

If you for instance want to install everything but the `DesktopShortcut` and the `ShellExtensions` feature, you have two possibilities:

1. You explicitly name all the features you actually want to install (whitelist) where `Client` is always installed anyway::
  msiexec /passive /i ownCloud-x.y.z.msi ADDDEFAULT=StartMenuShortcuts

2. You pass the `NO_DESKTOP_SHORTCUT` and `NO_SHELL_EXTENSIONS` properties::
  msiexec /passive /i ownCloud-x.y.z.msi NO_DESKTOP_SHORTCUT="1" NO_SHELL_EXTENSIONS="1"

*NOTE*: THe ownCloud MSI remembers these properties, so you don't need to specify them on upgrades.
*NOTE*: You cannot use these to change the installed features, if you want to do that, see the next section.

*** Changing installed features ***

You can change the installed features later by using `REMOVE` and `ADDDEFAULT` properties.
If you want to add the the desktop shortcut later::
  msiexec /passive /i ownCloud-x.y.z.msi ADDDEFAULT="DesktopShortcut"

If you want to remove it, simply do::
  msiexec /passive /i ownCloud-x.y.z.msi REMOVE="DesktopShortcut"

*NOTE*: Windows keeps track of the installed features and using `REMOVE` or `ADDDEFAULT` will only affect the mentioned features.

Compare `REMOVE <https://msdn.microsoft.com/en-us/library/windows/desktop/aa371194(v=vs.85).aspx>`_
and `ADDDEFAULT <https://msdn.microsoft.com/en-us/library/windows/desktop/aa367518(v=vs.85).aspx>`_
on the Windows Installer Guide.

*NOTE*: You cannot specify `REMOVE` on initial installation as it will disable all features.

Installation folder
^^^^^^^^^^^^^^^^^^^

You can adjust the installation folder by specifying the `INSTALLDIR`
property like this::

  msiexec /passive /i ownCloud-x.y.z.msi INSTALLDIR="C:\Program Files (x86)\Non Standard ownCloud Client Folder"

Be careful when using PowerShell instead of `cmd.exe`, it can be tricky to get
the whitespace escaping right there. Specifying the `INSTALLDIR` like this
only works on first installation, you cannot simply reinvoke the .msi with a
different path. If you still need to change it, uninstall it first and reinstall
it with the new path.

Disabling automatic updates
^^^^^^^^^^^^^^^^^^^^^^^^^^^
To disable automatic updates, you can pass the `SKIPAUTOUPDATE` property.::

    msiexec /passive /i ownCloud-x.y.z.msi SKIPAUTOUPDATE="1"


Launch after installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^

To launch the client automatically after installation, you can pass the `LAUNCH` property.::

    msiexec /i ownCloud-x.y.z.msi LAUNCH="1"

This option also removes the checkbox to let users decide if they want to launch the client
for non passive/quiet mode.

`ǸOTE:` This option does not have any effect without GUI.

Installation Wizard
-------------------

The installation wizard takes you step-by-step through configuration options and
account setup. First you need to enter the URL of your ownCloud server.

.. image:: images/client-1.png
   :alt: form for entering ownCloud server URL

Enter your ownCloud login on the next screen.

.. image:: images/client-2.png
   :alt: form for entering your ownCloud login

On the Local Folder Option screen you may sync
all of your files on the ownCloud server, or select individual folders. The
default local sync folder is ``ownCloud``, in your home directory. You may
change this as well.

.. image:: images/client-3.png
   :alt: Select which remote folders to sync, and which local folder to store
    them in.

When you have completed selecting your sync folders, click the Connect button
at the bottom right. The client will attempt to connect to your ownCloud
server, and when it is successful you'll see two buttons: one to connect to
your ownCloud Web GUI, and one to open your local folder. It will also start
synchronizing your files.

.. image:: images/client-4.png
   :alt: A successful server connection, showing a button to connect to your
    Web GUI, and one to open your local ownCloud folder

Click the Finish button, and you're all done.
