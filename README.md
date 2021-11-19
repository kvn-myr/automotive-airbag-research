# Airbag research

## Data formats

### ASM

...

### EDR

..

### Gen 11 GM [Gomez2021escar]

No data format, just the name of an airbag control unit from the manufacturer GM.

### Raw dumps / Crashdata (EEPROM) [Gomez2021escar]

Collect raw data from EEPROM directly.

### DTCs [Gomez2021escar]

Is rather related to the engine control module (ECM) than to the airbag ECU.

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

We extracted multiple sqlite3 databases from Bosch's CDR software. Those are used for interpretation of the hexadecimal data.

Currenlty supported vehicles (`SELECT System FROM CommInfo` in one of the databases) are:

- AUDI001
- BENTLEY03
- BENTLEY04
- BMW004
- BMW005
- FRACO
- LAMB03
- TOYOTA004
- VOLVOGEN

Vehicle coverage based on Bosch:

- Acura
- Alfa Romeo
- Audi
- Bentley
- BMW
- Buick
- Cadillac
- Chevrolet
- Chrysler
- Dodge
- Fiat
- Ford
- GMC
- Holden
- Honda
- Hummer
- Infiniti
- Jeep
- Lamborghini
- Lancia
- Lexus
- Lincoln
- Maserati
- Mazda
- Mercedes-Benz
- Mercury
- MINI
- Nissan
- Oldsmobile
- Opel
- Pontiac
- RAM
- Rolls-Royce
- Saturn
- Scion
- smart
- SRT
- Suzuki
- Toyota
- Volkswagen
- Volvo
- and others

One of the databases (`CRD_l2.sqlite3`) contains information about the location of specific events. The tools extracts 21 unique DPIDs. Those are: `{'$7B', '$79', '$76', '$6F', '$6D', '$69', '$78', '$77', '$6A', '$70', '$74', '$7A', '$75', '$6E', '$72', '$6C', '$6B', '$68', '$73', '$71', '$67'}`

For example: `'DPID $6C Bytes 4-5', None, 'DTC number for fault #4'` or `'DPID $75 Byte 1', None, 'SDM Recorded Vehicle Velocity Change for Axis #1 (140 msec)', None, 'MPH'), (88, 0, 0, 0, 'DPID $75 Byte 3', None, 'SDM Recorded Vehicle Velocity Change for Axis #1 (150 msec)'`.

## Analysis methods
