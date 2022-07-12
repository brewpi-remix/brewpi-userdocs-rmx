Running Multiple Chambers on the Same RaspberryPi
=================================================
You may wish to run more than one chamber on a single Raspberry Pi.  As of release 0.5.1 this is supported with the normal install tools.

You will need an Arduino per chamber, configured appropriately.

Clean Install Required
----------------------

Installing a multi-chamber system is only possible on the initial install.  If you have a current single-chamber setup you must remove it and reinstall from the beginning.  If you need to uninstall you can either start over with a clean SD card and fresh install of Raspbian (preferred) or try the uninstaller:

.. code-block:: console

    curl -L uninstall.brewpiremix.com | sudo bash

Follow the instructions on the screen.

Multi-Chamber Installation
--------------------------
Starting with a clean system, run the standard installer:

.. code-block:: console

    curl -L install.brewpiremix.com | sudo bash

Now just follow the instructions on the screen.  The important choice comes during this part of the install:

.. code-block:: console

    If you would like to use BrewPi in multi-chamber mode, or simply not use the
    defaults for scripts and web pages, you may choose a name for sub directory and
    devices now.  Any character entered that is not [a-z], [0-9], - or _ will be
    converted to an underscore.  Alpha characters will be converted to lowercase.
    Do not enter a full path, enter the name to be appended to the standard path.

    Enter device/directory name or hit enter to accept the defaults.
    [<Enter> = Single chamber only]:

This is where you must enter a directory name to use, for instance "chamber1".  No spaces or special characters may be used.  After this entry you will be asked for a friendly name for your chamber to be displayed in menus and on the web page:

.. code-block:: console

    Now enter a friendly name to be used for the chamber as it will be displayed.
    Capital letters may be used, however any character entered that is not [A-Z],
    [a-z], [0-9], - or _ will be replaced with an underscore. Spaces are allowed.

    [<Enter> = $CHAMBER]: 

You may use spaces and capitalization here such as "Chamber 1" however special characters are not allowed.

Arduino Selection
-----------------
During the install, if there is only one Arduino the script will create a udev rule for that controller.  If more than one is present, a list of Arduino serial numbers connected will be displayed.

Keeping track of serial numbers may be somewhat unwieldy.  To avoid this, plug a single new Arduino in for each install pass.  An Arduino which has previously been configured for a different chamber will be ignored.

Adding Additional Chambers
--------------------------
For each additional chamber desired, simply plug in a new Arduino and re-run the install.sh script in the tools directory:

.. code-block:: console

    sudo ~/brewpi-tools-rmx/install.sh

Multi-Chamber Index
-------------------
A link to a multi-chamber index will be created in the root of the web directory.  The chambers will be in a sub-directory underneath the root.  The multi-chamber index will allow a terse view of each configured chamber's status, and you can view the full chamber web page by clicking the corresponding LCD.

