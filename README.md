# Mouse-Jiggler-PCB-Demo
This is a PCB designed in KiCAD as a demo for Seattle Makers.

It's based on [Arduino based Mouse Jiggler](https://github.com/MAKERSUN99/MAUS) 
published on GitHub. MAKERSUN99 published the schematic and the PCB as
a PDF so the circut and basic layout is clear, but not the original KiCAD
files.

It is a good demo because it can be incrementally designed. At its core,
it is a USB A male connector and an ATTINY85. The ATTINY can do raw GPIO
manipulation to handle USB connectivity and so it can emulate a mouse.

But USB devices should have ESD protection and so you can add that as a
pair of zener diodes and a capacitor.

Similarly, the ATTINY is supposed to have a capacitor close to VCC to condition
power for it.

Once that is done, you still ought to have a way to program the ATTINY so, you
can add a 1x5 pin header to connect to VCC, GND, PB2, PB3,and PB4.

After that, it's nice to have a LED and an associated resistor to show
activity.

Finally, you can add a WS2812B/NeoPixel for more interesting light effects.

## Steps to build it in KiCAD
Components:

|Part Description|Manufacturer Part Number|LCSC Part Number|
|-|-|-:|
|100nF Capacitor|CL21B104KBCNNNC|[C1711](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_Samsung-Electro-Mechanics-CL21B104KBCNNNC_C1711.pdf)|
|100uF Capacitor|CL31A107MQHNNNE|[C15008](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_Samsung-Electro-Mechanics-CL31A107MQHNNNE_C15008.pdf)|
|Zener Diode|MM1Z5226B|[C118713](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_ST-Semtech-MM1Z5226B_C118713.pdf)|
|LED|XL-2012VRC|[C7371913](https://www.lcsc.com/datasheet/lcsc_datasheet_2402181500_XINGLIGHT-XL-2012VRC_C7371913.pdf)|
|1x5 male header|DS1021-1x5SF11-B|[C7430361](https://www.lcsc.com/datasheet/lcsc_datasheet_2312201431_CONNFLY-Elec-DS1021-1x5SF11-B_C7430361.pdf)|
|NeoPixel|WS2812B-B/T|[C2761795](https://www.lcsc.com/datasheet/lcsc_datasheet_2106062036_Worldsemi-WS2812B-B-T_C2761795.pdf)|
|68 Ohm Resistor|FRC0805J680 TS|[C2907341](https://www.lcsc.com/datasheet/lcsc_datasheet_2308241947_FOJAN-FRC0805J680-TS_C2907341.pdf)|
|1.5k Ohm Resistor|FRC0805J152 TS|[C2907290](https://www.lcsc.com/datasheet/lcsc_datasheet_2308241947_FOJAN-FRC0805J152-TS_C2907290.pdf)|
|220 Ohm Resistor|FRC0805J221 TS|[C2933537](https://www.lcsc.com/datasheet/lcsc_datasheet_2308241113_FOJAN-FRC0805J221-TS_C2933537.pdf)|
|10k Ohm Resistor|FRC0805J103TS|[C2930231](https://www.lcsc.com/datasheet/lcsc_datasheet_2308241947_FOJAN-FRC0805J103TS_C2930231.pdf)|
|ATTiny85 MPU|ATTINY85-20SU|[C89852](https://www.lcsc.com/datasheet/lcsc_datasheet_2011170235_Microchip-Tech-ATTINY85-20SU_C89852.pdf)|
|Male USB A Connector|KH-USB180-AM-4P|[C2828094](https://www.lcsc.com/datasheet/lcsc_datasheet_2105241835_Shenzhen-Kinghelm-Elec-KH-USB180-AM-4P_C2828094.pdf)|

KiCAD has the footprints and symbols for most of the above, but you need
to get the footprints from LCSC for three. To do that run this PowerShell:

``` powershell
cd $env:TEMP
python -m venv easyeda2kicad\.venv
. .\easyeda2kicad\.venv\Scripts\Activate.ps1
easyeda2kicad.exe --full --lcsc_id=C2761795
easyeda2kicad.exe --full --lcsc_id=C89852
easyeda2kicad.exe --full --lcsc_id=C2828094
```
