# Technical Brief: Ripple generation

This design does not rely on a clock (COT - Constant-On Time), instead it wait for the output voltage to drop under a given Vref during buck off time, then fire for a given amout of time (T_on). This allows the tension output to be contant and not dependant of Vin. However, this as 2 major drawbacks:

1. A reference voltage V_ref must be defined so the comparators can work. This is done internally in the IC.
2. The ripple magnitude must be an order of magnitude more important than the one of the noise so they can be distinguished: highly filtered systems (low ESR/MLCC heavy) may not be generate enough ripple.

We estimeed that design one would be sufficient in our case.

![alt text](ripple_desings.png)

_Note1_: Point 2 must be looked at on the final system, as we may have issue with ripple amplitude.

## Technical Brief: Selection the series ripple resistor $R_{ESR}/R_3$

Resr is not usefull as we deemed the ESC+MLCC ESR+intern path to already generate 25mV ripple. We will still add a $0\Omega$ capacitor in case the current ripple is not enough.