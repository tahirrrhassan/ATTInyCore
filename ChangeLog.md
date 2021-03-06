### This document lists significant changes and bugfixes, including those not in yet in a release.
1.4.0
* Included Servo library now works with PLL as Timer1 clock source (trivial fix - I clearly never looked into it when I merged in the 8-bit servo code!). Now it also lets you use Servo if you have external crystal running at unsupported speed if you use the PLL for Timer1...
* Major improvements to part-specific documentation pages.
* Remove the HAVE_BOOTLOADER mechanism, which existed to clean up timer registers that a bootloader may have left configured. Neither Optiboot not Micronucleus do this, so HAVE_BOOTLOADER had no function. Is now commented out in the pins_arduino's where it existed, as is the code it enabled. Saves a small amount of flash, and makes init() in wiring.c far easier to follow once the do-nothing code isn't visible.
* Correct a number of typos in boards.txt
* Fix several missing optiboot bootloaders
* Add support for setting CLKPR so bootloaders off internal at speeds other than 8 and 1 MHz can work at less agonizing baud rates.
* Fix inverted LED blinking on all parts
* Fix LED blinking on x61 family (#264)
* Add support for VUSB uploads to Digispark (t85, t167), Micronucleus/California STEAM (t84a)  Wattuino (841). Requires board manager installation, or another compatible board, in order tp pick up the support files.
* Add support for the DigiSpark Pro pin mapping for the ATtiny87/167 with other bootloader options.
* Add support for 16 MHz with *INTERNAL* oscillator on ATtiny841, 441. Support is still experimental; there are a few caveats - see [ATtiny441, 841](avr/extras/ATtiny_x41.md)
* Tested voltage dependence of internal oscillator, allowing significant simplification of the bootloader files for the ATtiny841/441,828,1643.
* Support PIN_Pxn notation.
* Document a few really odd GPIO features on ATtiny841, 441, 828.
* Document minimum baud rate of builtin software serial "Serial" for parts without hardware serial.
* Remove TUNED_OSCCAL_VALUE defines from pins_arduino.h for variants; this was set to OSCCAL in those files (despite the fact that we tested for whether it was defined before trying to use it!), leading to compiled binaries copying OSCCAL to a register and then writing it back. (thanks @ArminJo)
* Fix bug when switching between I2C master and slave modes on USI devices (thanks @martin-schmied1)
* Fix pulseIn(), both pulse length, and timeout (the latter is broken in official avr core too) (#384)
* Add pulseInLong()
* (untested) Don't generate .lst unless told to 'export compiled binary' (#379 - though note that that issue also appears to involve a problem with their compiler, or maybe just an extremely perverse username that's breaking things)

1.3.3
* Add support for external CLOCK on 48/88/828. Document how to use external clock on other parts via manual AVRdude step (#355).
* Fix bug with using 32K ULP as clock source on 828.
* A bit of boards.txt cleanup.
* Serial hogged an unnecessary amount of ram on the 841/441/1634. Pulled in the latest version of HardwareSerial from the official AVR core; this sorts out that issue.
* Add printf support to printable class.
* Add CLOCK_SOURCE define to identify clock source (#358)
* Add support for 4MHz internal on all boards (#358)
* Add support for 16.5MHz on x5 and x61 (#349)
* Documentation improvements (#373, #375)
* Burn Bootloader now executes as a single command; this should fix issues with some programmers. (#372)

Prior to 1.3.3, a proper changelog was not kept. See the releases for information about changes introduced during that timeframe.
