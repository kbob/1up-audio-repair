# Repair a 1UP's headphone jack.

This is a prototype of the
[1Bitsy-1UP](https://github.com/1Bitsy/1bitsy-1up)'s new audio output
section.  It is being implemented as a daughter card, but if it works,
it will be integrated into a future version of the 1Up


## Objectives

The new audio section will have these features.

 * Stereo headphone out or mono speaker out.

* Automatic switching between speaker and headphone when 'phones are
   plugged in.

* Thumbwheel for volume control.

* The volume wheel will directly control audio gain, but will also be
  readable by software.

* Headphone presence will directly control audio signal routing, but
  will also be readable by software. Software will produce stereo
  signal when the headphones are active and mono signal when the
  speaker is active.

* The amplifier's mute function will be controllable by software.

* The amplifier's shutdown (low power) function will be controllable
* by software.


## The Design

The audio output will be built around the PAM8019 amplifier from
Diodes Incorporated.  Headphone outputs will be routed to a 3.5mm
headphone jack.  Speaker outputs will be routed to a terminal block
for an off-board speaker.

The board will be configurable to take power either from the 1Bitsy's
+3v3 rail or from a separate power connection.


## Considerations

This is speculation based on the PAM8019 datasheet.

The 8019's digital input pins, MUTE and ~SD, are 3V compatible.  When
the 8019 is at 5V, a 3.3V GPIO will control those inputs.

The HP/~SPK input is not 3V compatible when the 8019 is at 5V.  The
HP/~SPK input will be generated directly from the headphone tip
switch.  In 5V operation, the 3V GPIO signal will be generated from a
voltage divider.  In 3V operation, the GPIO signal can be connected
directly to the tip switch.  (The GPIO pin happens to be an analog
input, so we could also leave the voltage divider in and read an
analog value instead of digital.)

The 8019's Volume input needs to have a range of 0 to +5V to give the
maximum attenuation of -60dB.  But the STM32's analog input can't
exceed 3.3v.  So a voltage divider is called for.  The problem is that
the Volume voltage already comes from a 50K potentiometer, which is a
voltage divider.  Adding another will make the volume control
nonlinear.

The 8019 has a circuit to detect low power and fade out the audio when
it happens.  It is supposed to suppress pops on power down.  It will
require experimentation to find the best resistor values for that.

The 8019 has a "non clip power limit" circuit.  The voltage at the PL
pin determines the maximum power the amp will deliver.  I will put in
a header to attach an external potentiometer to test various values of
PL with whatever speakers we decide to use.


## Interface

The board will connect directly to the 1Bitsy at the following
pins.  The pin arrangement will match the 1Bitsy's arrangement
so the boards can be stacked.

* +3V3
* GND
* PA0 for headphone tip sense
* PA1 for volume sense
* PA2 for Mute control
* PA3 for ~Shutdown control
* PA4/DAC1
* PA5/DAC2

A solder jumper will connect the amplifier VDD to the 1Bitsy's 3v3
supply.

There will be headers to attach external potentiometers or resistor
networks to dial in the correct values for the UVP and PL pins.


## Misc.

Here is a Maxim app note describing a headphone sense circuit.  Thanks
to James Hagerman for finding it and to an anonymous Maxim engineer
for writing it.

https://www.maximintegrated.com/en/app-notes/index.mvp/id/4607


## Errata

v0.2 holes are too small for the headphone jack.
