# Technical Brief: Switching Frequency - $R_{on}$

### Check minimal off time

First, we need to ensure that the buck can work for the minimum V_in of a 4S fully empty LIPO which is 4x3=12V, t_off typical is 170ns.

$F_{SW, \max(@V_{IN, \min})} = \frac{V_{IN,\min} - V_{OUT}}{V_{IN,\min} \cdot T_{OFF,\min}}$

1. For $V_{IN, \min} = 10.5V, F_{SW} = 280kHz$
2. For $V_{IN, \min} = 11.0V, F_{SW} = 535kHz$
3. For $V_{IN, \min} = 11.5V, F_{SW} = 768kHz$
4. For $V_{IN, \min} = 12.0V, F_{SW} = 981kHz$

In the end, for VersionV1.0, we deemed that battery will never continuously drop under 12V. The full range of frequency of the LM5160 cannot be used and we must ensure F_sw<981kHz. 

_Note1_: Raising the UVLO could protect from <12V on battery rail.

### Check minimal on time

Then, we have to check that the minimum on time (150ns typical) is low enough to ensure we can convert from the maximal tension. Let's take a fully charge 6S transient => 60V.

$F_{SW,\max(@V_{IN,\max})} = \frac{V_{OUT}}{V_{IN,\max} \cdot T_{ON,\min}} = 1.1MHz$ 

Thus, the full range frequency of the LM5160 can be used with a confortable margin as 60V whas considered in input.

### Conclusion

We will aim for F_sw = 900kHz. This is 900/128=7 times greater than the 128kHz max frequency of our PWM and well withing the 5-10x law of sampling rate, so there should be no issues.

$R_{\text{ON}} = \frac{V_{\text{OUT}}}{F_{\text{SW}} \times 10^{-10}} = 111k\Omega$, we will use $110k\Omega$ as we design with 1% resistors for VersionV1.0

$T_{\text{ON}, \text{typ}} = \frac{R_{\text{ON}} \times 10^{-10}}{V_{\text{IN}}} = 458ns$