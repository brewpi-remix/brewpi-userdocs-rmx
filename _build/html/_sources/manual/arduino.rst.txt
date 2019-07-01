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

.. note:: The web-based firmware flashing is not dependable in the current version and lacks some of the functionality of the command-line tool.  It is recommended to avoid the web-based interface for flashing right now.  This documentation will be updated when the web update functionality is restored.

Troubleshooting
---------------
* If saving devices in the device manager does not work, your EEPROM was probably not reset properly. Try reprogramming without settings and devices restore.
* Check whether it is not a hardware problem by programming your Arduino using the Arduino IDE. Just open the `blink` example and click `upload`.
