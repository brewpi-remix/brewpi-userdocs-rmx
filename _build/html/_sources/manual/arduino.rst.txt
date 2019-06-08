Programming your Arduino
========================

Programming via Command Line
-------------------------------------
Currently the web-based firmware update method is not very dependable.  I sincerely recommend using ``updateFirmware.py``, which is located in your BrewPi Utility directory.  This method has the advantage of providing a menu to download the correct firmware package.  When you install BrewPi Remix you will be presented with the opportunity to flash your Arduino.  There are cases where you may want to re-flash, or change your currently connected Arduino.

Run it with:

.. code-block:: console

    sudo /home/brewpi/utils/updateFirmware.py

The script will pick the serial port currently configured for BrewPi.  With a single chamber install, this defaults to 'auto' and will choose the first Arduino it finds if there are multiple controllers plugged in.  In multi-chamber mode, the script will flash the Arduino corresponding to the local installation's configuration file.

The script will guide you through the process, presenting you with a choice of firmware versions which are available and appropriate for your shield type.  Generally you will want to choose the latest version.

Finally, the script will offer to back up and restore your settings and configured devices if it was previously configured.  CHoose according to your preferences.

When complete, the script will attempt to restore the state of your system; if it was running before you started it will attempt to restart BrewPi.

Selecting a Shield
^^^^^^^^^^^^^^^^^^
If your Arduino has never been flashed before, you will first be prompted with the opportunity to select a shield type. The available types are:

 - **RevA**: One of the original BrewPi Arduino shields. Very few of these are in the wild, and it is only supported through firmware version 0.2.10.
 - **RevC**: The successor to RevA (no idea what happened to RevB), this is the most common type. It includes support for a parallel LCD screen display and a rotary encoder which can be used to make manual adjustments.  Nearly all shields right now are RevC.  *Even if you do not use a shield* you should select the RevC for most purposes.
 - **I2C**: The newest shield variant which supports an I2C/TWI LCD display.  Technically speaking this firmware version does not need a shield in order to allow complete functionality, unlike the parallel LCD versions which require some additional circuitry.  If you are not going to use a shield at all however you want to use an I2C LCD you should choose this shield type.  Be aware that this firmware shield version moves the OneWire sensor to A0 from A4.

For the most part, the shield type designation for the firmware is really about the capabilities of the firmware more than if you have a shield plugged in or not.  Nearly all guides will default to the RevC pinouts.

If you have an Arduino that is currently flashed with one shield type and you wish to change, you can use the `-h` or `--shield` argument like so:

.. code-block:: console

    sudo /home/brewpi/utils/updateFirmware.py --shield

Beta Versions
^^^^^^^^^^^^^^^^^^
If you would like to be presented with possible beta versions of firmware as a choice, use the `-b` or `--beta` argument like so:

.. code-block:: console

    sudo /home/brewpi/utils/updateFirmware.py --beta

Programming via Web Interface
-------------------------------------

.. note:: The web-based firmware flashing is not dependable in the current version and lacks some of the functionality of the command-line tool.  It is recommended to avoid the web-based interface for flashing right now.  For the most part the following documentation has not been updated from the original BrewPi Legacy branch and may no longer be correct.

Uploading a new hex file to your Arduino can be done straight from the BrewPi web interface.
The serial port is read from the config file (``/home/brewpi/settings/config.cfg``), so make sure the settings are correct.
If this file does not contain port settings, BrewPi uses the defaults from (``/home/brewpi/settings/defaults.cfg``)
BrewPi defaults to ttyACM0 and when it cannot find it, it tries ttyACM1.
If your serial port is one of these, you don't have to do anything.

The default should normally work (``/dev/ttyACM0``), but if your script fails to start because the serial port is not found, run this to see the candidates:

.. code-block:: console

    ls /dev/ttyA*

It is definitely not ``ttyAMA0``, that is the internal serial port.
Official Arduinos normally appear as ttyACM0 or if that is already taken, ttyACM1.
Arduino clones sometimes appear as ttyUSB0 or similar. If that is the case, add these lines to  (``/home/brewpi/settings/config.cfg``):

.. code-block:: console

    port = /dev/ttyUSB0
    altport = /dev/ttyUSB1


Uploading a new HEX file to your Arduino
----------------------------------------
To program your Arduino from the web interface, take the following steps:

#.  Log on to your BrewPi web interface by entering the Raspberry Pi's IP address into a web browser.
    The IP is displayed when the installer finishes, or by typing ``ifconfig`` at the shell (look for inet addr).
    If the page says 'script not running' you should start the BrewPi script first.
    This is automatically done by the CRON job within one minute if you click the 'start script' button.
    If you have not set up CRON jet, you can manually start the script with:

    .. code-block:: console

        sudo -u brewpi python /home/brewpi/brewpi.py

#.  Open the maintenance panel and go to the `Reprogram Arduino` tab.

#.  Download the HEX file appropriate for your setup from https://github.com/lbussy/brewpi-firmware-rmx/releases.
    You can also compile your own hex file with Atmel Studio.
    Make sure you have the right file for your Arduino type (UNO or Leonardo) and the right shield (Rev A or Rev C).
    Only the first 100 BrewPi shields were rev A. If you bought one recently, you have Rev C.

#.  The program script can automatically restore your settings and devices after upgrading.
    If you are uploading to a virgin Arduino, just answer NO to both.

#.  Next, just click the program button. If your script was started by CRON, the output will appear in the black box.

#.  The BrewPi script will automatically restart after programming and report which version of BrewPi it has found on the Arduino.


Troubleshooting
---------------
* If you're prompted with an error: "cannot move uploaded file" rerun the fix permissions script in ``sudo /home/brewpi/doPerms.sh``.
* If saving devices in the device manager does not work, your EEPROM was probably not reset properly. Try reprogramming without settings and devices restore.
* Check whether it is not a hardware problem by programming your Arduino using the Arduino IDE. Just open the `blink` example and click `upload`.
