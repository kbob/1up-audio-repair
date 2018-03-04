# V0.3

## Schematic Changes

* J1 only has power, not ground. (This will still be a flying jumper to the
  1Bitsy’s VIN pin.)

* PL pin is tied low instead of having a voltage divider and header.

* UVP pin is tied to a voltage divider with resistor values specified and
  no header.

* HP/~SPK now has the MAXIM app note circuit to pull the pin low when
  'phones are disconnected and isolate the pin from the headphone jack.

* Speaker headers changed from screw terminals to 2.54mm headers.

* Board no longer has option to use 1Bitsy's 3v3 power.

## Board Changes

* Smaller form factor.

* Speaker jacks replaced with solder points.

* Lots of test/patch points removed.

* Mounting holes removed.

* Headphone jack holes enlarged.


# V0.2

## Schematic Changes

* add jumpers to voltage dividers on PL and UVP pin for experimentation.

* Make power supply jumper selectable (either +3V3 or external power).

## Board Changes

* Change board format to 2 inch square.  Make room to work instead of making
  it fit the 1Bitsy.

* Add through hole + SMD pads to most passives for easy change-out.

# V0.1

First version.
