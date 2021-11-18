# Airbag research

## Data formats

### ASM

...

### EDR

..

### Gen 11 GM [Gomez2021escar]

### Crashdata (EEPROM) [Gomez2021escar]

### DTCs [Gomez2021escar]

### Raw dumps [Gomez2021escar]

## Acquisition methods

There are different methdos to acquire data from airbag ECUs. Either physically from the storage systems directly (e.g. embedded forensic methods) or by using tools.

### Tesla EDR tool

You get an .json file containg XYZ.

The PDF report contains different hexadecimal information at the end. We decoded it as follows:

| Identifier / Data blob | Example data | Description |
| ---------- | ---- | ----------- |
| F014 | 313531323837362d30302d42ffffffffffffffff | Restraint Control Module - universal |
| F015 | 3243323030333139363141413131 | UNKOWN |
| F190 | 35594a3345374542304d46383331383830 | VIN |
| FD00 | 3238352e3031352e323139000000 | UNKOWN |
| fd60.bin | Left Front Crash Sensor |
| fd61.bin | Right Front Crash Sensor|
| fd62.bin | Left Side Impact Crash Sensor (B-Pillar) |
| fd63.bin | Right Side Impact Crash Sensor (B-Pillar) |
| fd64.bin | Right Side Impact Crash Sensor (C-Pillar) |
| fd65.bin | Left Side Impact Crash Sensor (C-Pillar) |
| fd66.bin | Right Side Door Pressure Sensor |
| fd67.bin | Left Side Door Pressure Sensor |

### Bosch CDR

## Analysis methods
