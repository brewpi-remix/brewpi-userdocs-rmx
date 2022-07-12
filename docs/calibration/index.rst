Calibrating your Probes
========================

The DS18B20 probes are factory calibrated and are ±0.5°C accurate. If they are within factory specifications, the maximum difference between two sensors can be 1°C (1.8°F.)  If you are within this range, no calibration is necessary.  The temperatures should be consistent, not exact.

If you are convinced you need to calibrate your sensors, you will need to use direct serial commands.

Calibration Steps:
--------------------

- Connect the sensor to calibrate
- Use ``h{v:1}`` to list the hardware with values and verify the Arduino can see the sensor. (It's easiest if just one temp sensor is connected.)
- Place the sensor and another calibrated thermometer in a large glass of water. Leave for 1 minute to settle.
- Take three readings from each sensor at 30s intervals.
- Average the three readings from each sensor
- The calibration adjustment value is the average value of the calibrated thermometer minus the sensor's average value. 

**Note:**

- The ``h{v:1}`` command always prints uncalibrated, raw values from the sensor.
- The ``d{v:1}`` command always prints values from the sensor that include calibration adjustment. 

Setting Calibration Adjustment
---------------------------------

The ``U`` command has the ``j`` parameter for setting the calibration adjustment on temp sensors ``{h:2}``. Valid values are in the range +/- 7.9°C. (You will always calibrate in degrees C.)

For example, after defining a temp sensor at index 3, you could set its calibration adjustment value like this:

``U{i:3,j:-0.3}``

That command will subtract 0.3°C from the sensors readings if the sensor reads higher than a calibrated thermometer.

Alternative method - relative calibration
-------------------------------------------

Using all available sensors, place them all in a large body of water. From all sensor readings, determine the most likely temperature. Then calibrate all sensors to display this temperature.

While it may not be perfectly accurate, it will be close enough; it will be consistent, so all sensors report the same value given the same temperature.

Accuracy
----------

Calibration adjustment values are stored to the nearest 1/16th of a degree to match the precision of the DS18B20s.
