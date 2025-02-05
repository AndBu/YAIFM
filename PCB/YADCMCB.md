# Yet Another DC Motor Control Board (YADCMCB) [v0.9]

This PCB can be used for controlling the motor of Yet Another IKEA Fridans Motorization (YAIFM). The design goal of the PCB was to make assemble quick and easy from readily available PCB modules such as the DRV8833 DC motor controller (or the DC MX1508 motor controller), the Wemos D1 Mini ESP8255 board (or the Wemos S2 Mini ESP32 board).

**The board is currently in testing. Not all functions are tested.**

**THE PINOUT OF THE BOARD IS DIFFERENT FROM THE PINOUT OF THE PROTOBOARD FOR THE YAIFM Project**

A typical motor to control with this board is the [GA12-N20 geared DC/DC motor](https://www.aliexpress.com/item/4001045242610.html).

## Pinout

The board has 8 outputs, of which 2 are hardwired to ground and one is hardwired to the 3.3V supply of the Wemos D1 Mini:
- W: OUT1 of the DRV8833 (or MX1508 if used)
- R: OUT2 of the DRV8833 (or MX1508 if used)
- Y: SCL/D1 of the Wemos D1 Mini
- K: 3.3V
- G: SDA/D2 of the Wemos D1 Mini
- B: GND
- S: MISO/D7 of the Wemos D1 Mini

The first 6 letters in the above table correspond to the wire colors of the [GA12-N20 geared DC/DC motor](https://www.aliexpress.com/item/4001045242610.html) (last check: Feb 2025). Output "S" is a GPIO where e.g. and endstop switch can be connected.

The 3.3V supply of the Wemos D1 Mini cannot source a lot of current (it's an LDO connected to 5V). Don't use it for powering anything more than ICs or low-power LEDs.

## USB-C Decoy + POL Option

The board can fit [this USB-C decoy](https://www.aliexpress.com/item/1005008134795923.html) on the top layer. Together with this [non-isolated DC/DC (POL "Point of Load") converter](https://www.aliexpress.com/item/1005006005553178.html) (**choose the version with an output voltage of 5V when you order!**), the user can operate the Motor at a voltage of 9V (or 12V, but this is out of spec for the DRV8833 and MX1503) when plugged into a compatible USB-C power source.

When the USB-C decoy board and the POL are fitted, the Wemos D1 Mini is powered from the voltage provided by the POL and the motor is powered from the negotiated USB-C input voltage. **JP1 must be open if your are using the USB-C decoy.**

**Do not power the board from the USB-C decoy and the USB-C port on the Wemos D1 Mini at the same time.**

## INA 219 Option

The board allows for fitting INA219 current sensor board, inserted into the supply current path of the motor controller PCB. The current sensor can be used to detect motor stalling or measure output power. The response of the sensor is limited by the input capacitance of the motor controller PCB.

This options is not yet tested or documented. **When no INA219 current sensor board is fitted, JP2 must be closed.**

## Jumpers

The board has two jumpers:

- **JP1** shorts the output of the USB-C decoy (which is wired to the supply of the motor control PCB) with the 5V rail of on the Wemos D1 Mini. **When using a USB-C decoy board, JP1 must remain open.**
- **JP2** shunts the current-sensing path of the INA219. **When no INA219 current sensor board is fitted, JP2 must be closed.**