Basic Configuration of your Raspberry Pi
========================================
This step-by-step guide will help you to set everything up on your Raspberry Pi and Arduino.  Current technology is assumed throughout.  Testing is done during development on the most recent platform available.  At the time of the last update to this section, that was a Raspberry Pi 4, with the latest version of Bullseye installed.  No intentional differences exist between this platform and others, especially older configurations, but changes exist.  If you have issues, you should always upgrade to the Raspberry Pi website's latest Raspberry Pi OS version.  If you deviate from that, you should know enough to help translate these instructions for your own use.

Please also note that while BrewPi Remix will probably work with other \*nix flavors (almost assuredly Raspbian Desktop on a PC, likely Debian, and probably Ubuntu;) these are not tested.  You will undoubtedly have issues I've simply not tested for and am not sure I want to worry about.  Raspbian on the Raspberry Pi is the only officially supported OS.

Installing Raspbian on your Raspberry Pi - Easy Mode
----------------------------------------------------
The easiest cross-platform way to install Linux on your Raspberry Pi is using the NOOBS installer.  There is no amount of documentation I could add here which would be better than that which already exists, so please visit the `Setting up your Raspberry Pi <https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up>`_ page at `RaspberryPi.org <https://www.raspberrypi.org>`_.

Going Headless - No Monitor, Mouse or Keyboard Needed
-----------------------------------------------------
Many folks running BrewPi Remix intend to embed the physical computer in their project and view the interface remotely on a web browser from another computer.  This is a great way to create a nice clean setup, and it's pretty easy to do.

Full instructions are included in the article `Headless Raspberry Pi <https://www.brewpiremix.com/headless-raspberry-pi/>`_ on the BrewPi Remix website.

Using your System
-----------------
From this point you will either execute the BrewPi Remix installer via the Terminal window within the Raspbian Desktop (a black icon with a '``>_``' in it), or via SSH if you are headless.  Nearly all testing is done via SSH which should be the simplest of all scenarios.

SSH is disabled by default on the contemporary Raspbian distros.  This is done because the Raspbian OS is shipped with a well-known password ('raspberry') and leaving it open via SSH is what we call A Bad Idea™.  You will be presented with an opportunity to change the default password if it is set during the BrewPi installation process.  SSH will be enabled if you follow the Headless article referenced above.  If not, you can enable it with two simple commands:

.. code-block:: console

    sudo systemctl enable ssh
    sudo systemctl start ssh

Your RPi's Name
---------------
In the past, it was very common to instruct people to give their Pi a static IP address so they could access it via their local network.  This is still possible, but a rather dated way to approach it.  You can still do this by editing the Interfaces configuration, but a better way is to simply use the name.  There is a function called "mDNS" embedded in computer systems which allows this to happen.

Note that Microsoft appears to be lagging a bit in their mDNS support.  There is a way to enable it for classic programs in Windows 10, but it's not very straightforward.  By far the easiest way to do it is to install Bonjour from Apple.  Apple uses it to detect printers and such on the network so it's proper name is "Bonjour Print Services for Windows."  You can `download it here <https://support.apple.com/kb/DL999?viewlocale=en_US&locale=en_US>`_, it's free, and a very lightweight install.

The stock Raspberry Pi starts out life named 'raspberrypi'.  You would access it over the network using the special domain suffix '.local' so in your SSH software or your web browser you would the name 'raspberrypi.local'.

If you insist on having a static IP address, the configuration has moved to the file /etc/dhcpcd.conf.  To create the static configuration, run:

.. code-block:: console

    sudo nano /etc/dhcpcd.conf

In this file, look for a block that has something like this:

.. code-block:: apacheconf

    # Example static IP configuration:
    #interface eth0
    #static ip_address=192.168.0.10/24
    #static ip6_address=fd51:42f8:caae:d92e::ff/64
    #static routers=192.168.0.1
    #static domain_name_servers=192.168.0.1 8.8.8.8 fd51:42f8:caae:d92e::1

At the very least you will have to uncomment the ``interface``, ``static ip_address`` and ``static routers`` lines by removing the '#' sign.  A minimal configuration may look like this:

.. code-block:: apacheconf

    # Example static IP configuration:
    interface eth0
    static ip_address=192.168.0.10/24
    #static ip6_address=fd51:42f8:caae:d92e::ff/64
    static routers=192.168.0.1
    #static domain_name_servers=192.168.0.1 8.8.8.8 fd51:42f8:caae:d92e::1

Finally, you will need to restart your network interfaces for these changes to occur:

.. code-block:: console

    sudo service networking restart

Because this is much less straightforward than it used to be, and assumes knowledge of what's called CIDR notation and other networking skills, I sincerely recommend NOT using a static address unless you really need it and/or know what you are doing.  I'll answer questions as I can on the forum about this, but just keep in mind I've given you the very sincere recommendation NOT to do it. 

Updating programs
-----------------
Keep your Pi's programs up to date with these commands:

.. code-block:: console

    sudo apt-get update && sudo apt-get upgrade -y

Cleaning Local Repositories
---------------------------
Occasionally you may want to clean out old or unused repository files which take up space on your SD card.  To do so, use the following commands:

.. code-block:: console

    sudo apt-get clean && sudo apt-get autoclean

Updating firmware
-----------------
Make sure you also have the latest firmware version, and stay up to date using the rpi-update tool.  Firmware updates will often fix instability issues, so make sure you keep this up to date.  To run, execute the following command (it will reboot after completion):

.. code-block:: console

    sudo PRUNE_MODULES=1 RPI_REBOOT=1 rpi-update

Work Complete
-----------------
If you have followed along, you now have a perfectly functioning, up to date, Raspberry Pi on your network, capable of running BrewPi Remix.  Congratulations, this was probably the toughest part!
