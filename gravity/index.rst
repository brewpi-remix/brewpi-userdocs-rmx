Specific Gravity Tracking
========================================

BrewPi Remix will incorporate readings from a gravity device, currently the `Tilt <https://tilthydrometer.com/products/copy-of-tilt-floating-wireless-hydrometer-and-thermometer-for-brewing>`_, `Tilt Pro <https://tilthydrometer.com/products/tilt-pro-wireless-hydrometer-and-thermometer>`_ or `iSpindel <https://www.ispindel.de/>`_.  The Tilt uses Bluetooth Low Energy (BLE) and the iSpindel uses WiFi.  Because of this difference, they will connect to BPR in different ways.  You may have one or the other attached to a chanber, and only a single device.

Between teh two, I find the Tilt and Tilt Pro to be the most hassle-free choice, but they do come at a premium price.  For me it's worth it, but you will have to make up your own mind.

Tilt
-----------

To configure the Tilt or Tilt Pro, you may choose the color during the install.  Doing so puts a configuration line in the `config.cfg` designating this color such as:

.. code-block:: console

    tiltColor = Yellow

You may also choose to clamp the readings to prevent wide swings which can be created by moving or shaking the fermentor:

.. code-block:: console

    clampSGUpper = 1.175
    clampSGLower = 0.970

If you failed to add the Tilt on the original install, or if you wish to change the color, edit the file and restart the script.

iSpindel
-----------

To add iSpindel, you must have the iSpindel configuration set in your config.cfg in the format:

.. code-block:: console

    tiltColor = iSpindel-Yellow

The name or color used is configured within the iSpindel configuration portal. Point your iSpindel to the brewpi-api.php file as its "HTTP" service type on port 80. More information may be found in the `iSpindel documentation <https://www.ispindel.de/docs/README_en.html#portal>`_.

If you are using a multi-chamber configuration, point the iSpindel at the brewpi-api.php in the directory corresponding to the chamber you wish to serve. 

As with the Tilt, you may choose to clamp the readings to prevent wide swings which can be created by moving or shaking the fermentor:

.. code-block:: console

    clampSGUpper = 1.175
    clampSGLower = 0.970

If you failed to add the iSpindel on the original install, or if you wish to change the name, edit the file and restart the script.
