# Micro-Controller Unit

For the Microcontroller Unit, the STM32G484 will be used. It was chosen to use an STM MCU because we wanted to learn how to use them. 

The G4 familly was specifically designed with motor control in mind an is a new adition to the STM32 catalog. The F4 is an other option we looked at, it is more general purpose. A key difference is that the G4 as stronger analogs (faster ADCs (4Msps vs 2Msps), more flexible triggering, often HRTIM, comparators, op-amps). F4 is less oriented toward power electronics.

To ensure we had some headroom for the development board we are going to use the STM32G484, one of the high tier of the familly. An other feature we looked for was the triple ADC, to reduce reading time, and the presence of an HRTIM, which are provided by the 484. An other nice to have for us is the precense of a:

- CORDIC which allows computation of sin, cos, tan, atan2, vector magnitude and polar to cartesian conversion in hardware.
- FMAC which allows FIR/IIR filtering, convolution and dot products in harware.

All these give us a lot of headroom to build the fastest ESC possible.