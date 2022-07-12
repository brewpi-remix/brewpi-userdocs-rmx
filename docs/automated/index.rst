Automated Installation of BrewPi
================================
Part of the "remix" in the BrewPi Remix project was to create all new scripts and methods to install and update BrewPi. These scripts are part of the `brewpi-tools-rmx repository on GitHub <https://github.com/lbussy/brewpi-tools-rmx>`_.
The install script will install all dependencies, set up users and permissions, download the latest code base and setup a few system daemons to keep things running well.

Behind the scenes there are actually four GitHub repositories required to run BrewPi.  None of that will be visible to most users.  Most people will only need to follow the instructions they are presented to get a perfectly running system.

Running the Install Script
--------------------------------------
The initial install is handled by a bootstrap script, which will execute, provide for dependencies, and call the rest of the scripts needed.  Behind the scenes; GitHub repositories will be cloned to your RPi, apt packages will be downloaded and installed, and configuration items created.

If you are security conscious, naturally inquisitive, or would just like to know what's going on, have a look at this :doc:`note about security <./security>`.

Use the following command to begin the installation, no other preparation or commands are necessary.  The script is automatically downloaded for you:

.. code-block:: console

    curl -L install.brewpiremix.com | sudo bash

Now just follow the instructions on the screen.

After the Install
------------------------------
If the installation was successful, your last step will be to :doc:`to set up your devices in the device manager <../devices/index>`.
