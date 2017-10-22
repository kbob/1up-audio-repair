# Repair a 1UP's headphone jack.

This is a one-off (I hope) daughter board I need to repair a
[1-UP](https://github.com/1Bitsy/1bitsy-1up) whose headphone jack
has come off.


## The Incidents

The headphone jack was known to be fragile.  Eventually, mine pulled
off, and it pulled the pads off the board too.

I epoxied it back into place and carefully soldered wires onto it,
but it pulled off again almost immediately.

So now I am designing a board to replace the whole audio output
section.  I will tie it onto the through-hole pads on the 1Bitsy,
and I will figure out a way to solidly affix it to the 1UP chassis.


## The design

The 1-Up v1.0a has its DAC outputs connected, via a digital
potentiometer, to an amplifier, and the amp drives a headphone jack.

The potentiometer is a Microchip MCP4661-103E.  The 1UP uses
a QFN package, but I'll use a TSSOP to make chip placement easier.
The potentiometer has an I2C interface.


The amp is a Texas Instruments TPA6135A2.  It is only available in a
QFN package.

I've chosen the Switchcraft 35RAPC4BHN3 headphone jack.  It has a
clear plastic cover and two sense pins to detect when the plug is
halfway or fully inserted.  There are a couple of spare pins on the
1Bitsy, so firmware can detect when the headphones are present.
(I wanted the 35RAPC**3**BHN3 which has a single sense pin, but
that chip is currently (November 2017) out of stock at Digikey and
Mouser.

Power regulation is done on the 1Bitsy board, so there is no need
for a power regulator on this board.

The 1UP uses 0402 passive components, but I will use 0603 because I am
more comfortable with them and already have an assortment of parts.


## Compatibility

Mechanically, this is nothing like the original 1UP audio circuit.
Ideally, it will be much stornger.

Electrically, it is the same, with two differences.

* The original does not have headphone presence pins.

* The original has A/C coupling between the DAC and the digipot,
  where it does not belong, and does not have A/C coulpling between
  the digipot and the amp, where it is needed.

Optionally, I could install a 50K digipot, as the 1Bitsy's DACs are
only rated to drive loads above 15K.

## Interface

The board will connect directly to the 1Bitsy at the following
pins.  I will use through hole headers on 0.1" spacing.

* +3V3
* GND
* PA4/DAC1
* PA5/DAC2
* PB8/I2C1 SDA
* PB9/I2C1 SCL
* PA0 for headphone tip sense
* PA1 for headphone ring sense

There will be solder jumpers to:

* select 0dB or +6dB gain on the amp.
