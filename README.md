# fox

Fox activity tracking badge

Video of first test run https://youtu.be/t2BXkpbrm-A

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
