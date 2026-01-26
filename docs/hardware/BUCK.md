# BUCKs converters

We are going to use the LM5160 fammily. This are justification of the engineering decisions based on the `resources\datasheets\BUCK CONVERTER\TI - LM5160X.pdf` datasheet.

## Technical Brief: Forced PWM (FPWM)

If FPWM is put to low, then the efficiency is increased. The low side mostfet behave as a diode and some commutation steps can be skip if low cuurent is required. However, this create some noise and less predictable behavior overall as steps can be skipped. Thus we will force CCM by putting FPWM to high.

## Technical Brief: Generation of ripple

This design does not rely on a clock (COT - Constant-On Time), instead it wait for the output voltage to drop under a given Vref during buck off time, then fire for a given amout of time (T_on). This allows the tension output to be contant and not dependant of Vin. However, this as 2 major drawbacks:

1. A reference voltage V_ref must be defined so the comparators can work. This is done internally in the IC.
2. The ripple magnitude must be an order of magnitude more important than the one of the noise so they can be distinguished: highly filtered systems (low ESR/MLCC heavy) may not be generate enough ripple.

_Note1_: Point 2 must be looked at on the final system, as we may have issue with ripple amplitude

## Technical Brief: Selection of the Feedback Resitors $R_{FB1} \text{ and } R_{FB2}$

$V_{OUT} = \frac{V_{REF} \times (R_{FB1} + R_{FB2})}{R_{FB1}}$, specified in the datasheet.

Where $V_{REF} = 2V$. We want $V_{OUT} = 10V$ so $\frac{R_{FB2}}{R_{FB1}} = 4$. We should try to keep the sum (lost power), in the $10k\Omega \text{ to } 100k\Omega$ order.

## Technical Brief: Selection of the Collector Voltage $V_{CC}$

As the $V_{out}$ voltage is 10V, $V_{cc}$ could be powered using $V_{out}$ to gain efficiency and limit termal losses inside the chip (with the LM5160A chip). It is not implemented as it adds layout complexity for a gain we deemed minimal.

## Technical Brief: Selection of the Soft Start Capactor $C_{SS}$

$C_{ss}$ must be greater than 1nF. For VersionV1.0, having a long soft start seems very relevant to avoid bug. In general, having a long start for ESC does not have an major impact.

## Technical Brief: Selection of the Current Limit Timer $C_{VCC}$

It is recommended to have $C_{VCC} = 1\mu F$, good quality X7R.

## Technical Brief: Selection of the Current Limit Timer $C_{BST}$

Soft start is important to limit current flow at ESC start as all capactior will require to be chatge simultaneously. If well control, it could even be used to reduce the resistance of the boostrap capacitor of the gate driver so we can charge it faster during normal operation.

It is recommended to have $C_{BST} = 10nF$, with a good quality X7R. It is fed by $C_{VCC}$ during off times.

## Technical Brief: Switching Frequency - $R_{on}$

### Check minimal off time

First, we need to ensure that the buck can work for the minimum V_in of a 4S fully empty LIPO which is 4x3=12V, t_off typical is 170ns.

$F_{SW, \max(@V_{IN, \min})} = \frac{V_{IN,\min} - V_{OUT}}{V_{IN,\min} \cdot T_{OFF,\min}}$

1. For $V_{IN, \min}$ = 10.5V, F_{SW = 280kHz}$
2. For $V_{IN, \min}$ = 11.0V, F_{SW = 535kHz}$
3. For $V_{IN, \min}$ = 11.5V, F_{SW = 768kHz}$
4. For $V_{IN, \min}$ = 12.0V, F_{SW = 981kHz}$

In the end, for VersionV1.0, we deemed that battery will never continuously drop under 12V. The full range of frequency of the LM5160 cannot be used and we must ensure F_sw<981kHz.

### Check minimal on time

Then, we have to check that the minimum on time (150ns typical) is low enough to ensure we can convert from the maximal tension. Let's take a fully charge 6S spike, so 40V (which should never happen as it will be filtered out).

$F_{SW,\max(@V_{IN,\max})} = \frac{V_{OUT}}{V_{IN,\max} \cdot T_{ON,\min}} = 1.1MHz$ 

Thus, the full range frequency of the LM5160 can be used.

### Conclusion

We will aim for F_sw = 900kHz. This is 900/128=7 times greater than the 128kHz max frequency of our PWM and well withing the 5-10x law of sampling rate, so there should be no issues.

$R_{\text{ON}} = \frac{V_{\text{OUT}}}{F_{\text{SW}} \times 10^{-10}} = 111k\Omega$, we will use 110kHz as we design with 1% resistors for VersionV1.0

$T_{\text{ON}, \text{typ}} = \frac{R_{\text{ON}} \times 10^{-10}}{V_{\text{IN}}} = 458ns$

## Technical Brief: Selection of the Current Limit Timer $T_{off(CL)}$

This compute the delay if too much current is draw from the IC output (2.5A)

$T_{\text{OFF(CL)}} =
\frac{5\,V_{\text{IN}}}{24\,V_{\text{FB}} + 12}\;\mu\text{s}$