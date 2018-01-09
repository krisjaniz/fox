# fox
![Fox profile picture](/fox_profile_pic.png)

Fox activity tracking badge

Video of first test run https://youtu.be/t2BXkpbrm-A

## Description

A fox activity tracker badge. The idea is that on shake the MMA7660FCT accelerometer sends an interrupt waking up the ATTINY85, which then logs the activity and changes the LEDs accordingly. The LEDs are connected to PCA9632DP1 low power LED driver which can keep the LEDs powered even when the ATTINY is sleeping. Ideally, if the ATTINY85 wakes up and there has been no activity for a few hours, it should save the activity statistics for the day to EEPROM and reset the LEDs to a new start state (switched off). Then the next "day" ATTINY can use that data to know how far along you are in your day's activities.
This is a pretty simple and stupid application and MMSA7660FCT is most certainly overkill for it.

## PCB configuration/hardware

The current PCB design has very small "guide" holes where the LED holes should be. This is because reverse mount LEDs come in various sizes and shapes and having really big holes there is annoying if your LEDs are small. You should either adjust the design in EasyEDA (just drop some NPTH holes on top of the existing ones) or use a drill to make the holes of the size you need. Holes should be completed from the front (visible) side of the board but you can start them at the back, for example, the Kingbright LEDs I use are not really round, they have sort of wings on the sides. If you drill half a hole with a bigger size bit in the back and then finish the hole from the front with the right size bit, you can work around this weirdness.

BOM calls for SMT test points/terminals to enable you to attach the badge to clothing after soldering. Look into the possibility of getting a proper pin instead. You will find those pins in sewing/hobby shops, not at electronics suppliers. Here is what a proper pin looks like:
![Proper pin](/fox_pin.png)

If you are making your own fox PCBs, be advised that it would look the best in red soldermask and ENIG. I advise against black or white soldermasks, you won't see the change in colour in various parts of the fox with those. Even green fox works surprisingly well:
[Green and blue foxes](/fox_page.png)

## Soldering

Solder the MMA7660FCT first. The hardest part is to actually position it. You should tack it down with some tape or better yet some tack-it or similar so that it doesn't move when soldering. Then you can solder the pads using a conical tip soldering iron (the smallest you have) and some solder wire (also the thinnest you have, 0.25mm works best). Soldering it is quite easy if you follow the procedure - go in with the iron as parallel to the board as you can so that the tip can heat up the pad on the MMA and the rest can heat up the pad. The pads on the board are really small so not much heat is necessary and solder will flow and make a connection right away.

After that you can solder all the other components in order of size, leaving battery holder for the last (remember to put a little solder on the center pad of the battery first to ensure good contact). Note that some of the pads, especially on the battery, 0R bridges and the emitters on the transistors, are connected to ground pour or unreasonably thick power lines and you would make your life easier if you used a bigger iron tip than you normally would with surface mount components. You can also skip both the capacitors - those are filter capacitors that aren't really needed for normal operation. That way you can access the MMA for some additional soldering if it turns out you haven't managed to solder it down well enough the first time around.

Unmarked pads are 0R bridges.

Also it is recommended that you don't solder any programming headers to the fox but rather use pogo pins or a spring connector to program it. Or desolder the header after you are satisfied with how the fox works. PB5 (pin 1 in Arduino) is connected on this header so you will get extra interrupts when touching it - which can be useful in debugging but also something to keep in mind.

## Programming

Programming the fox should only be done with a 3.3V programmer - the MMA isn't 5V tolerant and is rated only up to 3.6V. In Arduino I use ATTinyCore and TinyWireM, if you want to use a serial monitor, you can also use SoftwareSerial, just note that by default ATTINY85 is running at 1MHz and if you set 9600 as your serial speed, you will have to set 1200 in the serial monitor.

The test code currently shows configuration of both the accelerometer and LED driver, it doesn't currently put to sleep ATTINY or the accelerometer but those things would be nice to do for reasons of battery life. As it is, the ATTINY is the biggest power consumer on the board if you don't count the LEDs (which you can adjust or switch off completely).

## Usage/testing

The button connector on the ear of the fox can also take a resistor and a LED, for that reason one of the pads is left unconnected. By default this is connected to the RESET pin of the ATTINY so if you choose to deploy a LED there, it will glow weakly if the MCU is powered. Alternatively you can use the solder jumper to change the switch/LED to PB4 (pin 4 in Arduino) for visual indication of ATTINY waking up or other things (as seen in the video). Here is what the fox ear with a LED looks like in the previous version before the additional pads were added to make this easier:

![Fox ear with a LED](/fox_ear.png)

## Files

File | Description
---- | -----------
[fox_EasyEDA_source.txt](/fox_EasyEDA_source.txt) | EasyEDA source
[fox2.zip](/fox2.zip) | gerbers
[fox_test_code.txt](/fox_test_code.txt) | a small test program (Arduino) to test all the peripherals.

## BOM

Part | Count | Description
---- | ----- | -----------
ATTINY85V-10SU MCU, 8BIT, ATTINY, 10MHZ, SOIC-8 85423390 | 1 | MCU
BCX70H TRANSISTOR, NPN, SOT-23 85412900 | 4 | Transistors for driving LEDs
KMS231G LFS SWITCH, SPST, 0.05A, 32V, GULLWING, SIDE 85365007 | 1 | Switch
 KPTR-3216SECK LED, ORANGE, 1206, SMD 85414010 | 12 | Reverse-mount LEDs, you can use any other color you like, just note the voltage - the coin cell gives max 3V, the LEDs will die sooner if you choose a higher voltage variant
MMA7660FCT ACCELEROMETER, 3-AXIS, +/-1.5G, 10DFN 85423990 | 1 | Accelerometer, a pain to solder
5016 TEST POINT, SMT 85366990 | 2 | Holders for the pin (to attach Fox to clothing)
S1751-46R TEST TERMINAL, PCB, SMT 85366930 | 2 | Alternative holders for the pin (do not get both this and the previous)
MCWR08X2200FTL RES, THICK FILM, 220R, 1%, 0.125W, 0805 85332100 | 12 | Resistors for LEDs, higher value could be better
GRM219R71C104KA01D CAP, MLCC, X7R, 0.1UF, 16V, 0805 85322400 | 1 | Filter capacitor
GRM21BR61C106KE15K CAP, MLCC, X5R, 10UF, 16V, 0805 85322400 | 1 | Filter capacitor
PCA9632DP1 LED DRIVER, 4BIT, I2C/SMBUS, TSSOP-8 85423990 | 1 | LED driver IC
MC01W08050R RESISTOR, THICK FILM, 0R, 0.1W 85332100 | 7 | 0R resistors for the bridges
10K resistors | 2 | 10K resistors on SCL and SDA lines

![Fox back with arrows](/fox_back.png)
