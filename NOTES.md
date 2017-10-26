# Notes

## 2017-10-26 which amp?

During IRC discussion, @esden, @scanlime, @jboone and myself (@kbob)
decided some things.

 * I²S is the right answer.  @jboone especially likes the AK4951.
   But the 1Bitsy does not have I²S pins available, and enabling it
   requires major rework.

 * The desired audio configuration is stereo headphones or mono
   speaker.  There is no desire to use them simultaneously.

 * The digital potentiometer is not needed.  Software volume control
   should be just fine.

Then we discussed a bunch of amplifier chips.  We did not reach a
decision.

 * TPA6135A2 (current chip) for headphones + TPA2012D2 for speaker

   Pros of TPA2012D2:
    + outputs are direct coupled

   Cons:
    - is stereo; we only need mono.

 * TPA0213 for both.  This actually meets our needs pretty well.
   It has three input channels, uses headphone presence detect
   to switch the speakers on and off.

   Cons:
    - power limited: 0.6W into 4Ω w/ 3V power.
    - outputs are capacitively coupled.

 * TPA601A4 for both.  @scanlime found this chip.  It is a stereo
   headphone/speaker amp with independent volume adjustments.

   Pros:
    + has a nice auto-fade function when switching between headphones
      and speakers.

   Cons:
    - speakers are stereo.
    - minimum recommended power voltage is 4V.
    - outputs are capacitively coupled.

 * PAM8019 for both.  Another @scanlime find.

   Pros:
    + Class AB for headphones, class D for speakers.
    + about 50¢ in quantity 100.

   Cons:
    - speakers are stereo.
    - headphone outputs are capacitively coupled.  (Speakers are direct.)

 * WM9094 for both.  Also @scanlime's.

   Pros:
    + tiny BGA package.

   Cons:
    - not readily available.
    - tiny BGA package.

 * @jboone mentioned that the Paper Jamz Pro used an amp from Nuvoton.
   No specific part was recommended.

Based on all this, I am leaning toward the PAM8019.  The TPA6135A2 +
TPA2012D2 are also okay.


