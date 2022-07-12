How to Compile the Code from Source
===================================

These notes are just that; notes.  It will be enough for a reasonably technical person to create the environment in which they can fiddle to their heart's content.  If however you are here as a complete neophyte and have dreams of conquering your Arduino; this is not the right project for you.

Elco and others created this project many years back and by Elco's admission he would (and has) do it differently if he had to do it again.  The project team also crammed about as much as possible into the relatively tiny Arduino Uno.  By way of providing scale:  When I added the I2C code, even though it was a compile-time choice (therefore not adding unnecessary code), I ended up searching through the code to find 26 letters in the text strings to remove to make room enough that it would not crash.  It is that tight.

The original project was created in Atmel studio.  That sent more than a few otherwise sane people screaming and looking for the exits.  At the recommendation of another Brewing-related developer, I moved the project to PlatformIO and have not looked back.

You are free to do you - but I can't help you if you diverge from this path.  And that brings up another sensitive point:

Disclaimer and Limitation
^^^^^^^^^^^^^^^^^^^^^^^^^

I will likely not provide support for anyone related to the source code.  It's just too big a mess, too many choices to make, too many ways it can go wrong.  If there's a one-liner question you want to ask in the forums I might be able to help (or someone else might) but there is no way I can retain my sanity if I try to support people going feral in the source code.

Setting up the Development Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I will make heavy use of existing documentation.  There's no sense in me trying to re-write someone else's work.  If you have an issue with a particular step, your best bet is usually seeking help with that tool's vendor or support methods specifically.  If you need more help and see a link, click it and go get help there.

1.  Install `Microsoft's Visual Studio Code`_ (hereafter "VS Code".)
2.  Install `PlatformIO as an extension within VS Code`_.

.. _Microsoft's Visual Studio Code: https://code.visualstudio.com/
.. _PlatformIO as an extension within VS Code: https://platformio.org/install/ide?install=vscode

At this point, you have a very serviceable development environment.  I encourage you to view the various documentation.  A good place to start is PlatformIO's tutorial on building a cross-platform "Blink_" application.

.. _Blink: https://docs.platformio.org/en/latest/ide/vscode.html#quick-start

Clone the Repository
^^^^^^^^^^^^^^^^^^^^

One need not use any Git functionality, however, I will use that functionality here as an example of how to obtain the source code.  You may use your method; of course, you are on your own down those other paths.

Git is available and sometimes built into OS distributions.  For Windows, I recommend downloading the `Git for Windows`_ available directly from the Git website.

.. _Git for Windows: https://git-scm.com/

Once that is installed, open Git Bash and navigate to your intended source code destination.  i.e. If you want it in a subdirectory if C:\\MyCode, open that folder in Windows Explorer, right-click on "MyCode" and select "Git Bash Here" from the context menu.

At this point you can clone any software into its directory with the simple command:

``git clone {url to git repository}``

For BrewPi Remix, the full command is:

``git clone https://github.com/brewpi-remix/brewpi-firmware-rmx.git``

The entire repository will be cloned to a directory named "brewpi-firmware-rmx."

Compile the Source Code
^^^^^^^^^^^^^^^^^^^^^^^

Open VS Code and PlatformIO will load.  Use the File > Open Folder workflow to open the root folder of the repository (i.e. C:\\MyCode\\brewpi-firmware-rmx).

If you have followed along correctly and used the "Blink" example above, you now know how to compile the firmware and upload it to your controller.

Project Configuration
---------------------

The BrewPi firmware's compile-time options are controlled by the ``Config.h`` file.  Most importantly, the choice of the shield is set with the ``BREWPI_STATIC_CONFIG`` item.

I recommend you take some time reviewing this file and the code instances to understand the options available.

Looking through that file you will also see ``VERSION_STRING`` and ``BUILD_NAME``.  These macros, coupled with the shield type set with ``BREWPI_STATIC_CONFIG`` above, are responsible for some of the in-application information.

There are also two Python scripts, ``git_rev.py`` and ``name_firmware.py``.  These scripts set up the compilation environment variables which feed the above macros, as well as define the naming of the firmware file when created.

Other Environments
------------------

PlatformIO will also run within the Atom environment for its IDE, and it is capable of operating as a stand-alone CLI environment within Linux.  I will leave that as an adventure for the reader.
