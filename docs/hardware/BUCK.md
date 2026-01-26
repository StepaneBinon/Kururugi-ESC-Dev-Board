# BUCKs converters

We are going to use the LM5160 fammily. 

_Note1_: 

## Technical Brief: Forced PWM (FPWM)

FPWM is a good way to improve the overall behavior of the ESC as we can avoid should be able to avoid 

When FPWM pin is grounded, the low mosfet simulate a diode and is only on when the current is flowing to the output. This allow the use of a method called _pulse skipping_ which improve otherall efficiency of the buck at the cost of the dynamic. 

## Technical Brief: Selection of the Feedback Resitors $R_{FB1} \text{ and } R_{FB2}$

$V_{OUT} = \frac{V_{REF} \times (R_{FB1} + R_{FB2})}{R_{FB1}}$, specified in the datasheet.

Where $V_{REF} = 2V$. We want $V_{OUT} = 10V$ so $\frac{R_{FB2}}{R_{FB1}} = 4$.

## Technical Brief: Selection of the Collector Voltage $V_{cc}$

As the $V_{out}$ voltage is 10V, $V_{cc}$ could be powered using $V_{out}$ to gain efficiency and limit termal losses inside the chip (with the LM5160A chip). It is not implemented as it adds layout complexity for a gain we deemed minimal.

## Technical Brief: Selection of the Soft Start Capactor $C_{ss}$

$C_{ss}$ must be greater than 1nF. We want to soft start in 1µs, 

## Technical Brief: Selection of the Current Limit Timer $C_{BST}$

This capacitor is used to recharge

## Technical Brief: Selection of the On Time $T_{on}$

The on time must be greater than 150ns. We can compute T_on as follow.

$T_{\text{ON}} = \frac{R_{\text{ON}} \cdot 1 \times 10^{-10}}{V_{\text{IN}}} \;\text{s}$

And, to set a specific frequency, we cqn compute R_on using:

$R_{\text{ON}} = \frac{V_{\text{OUT}}}{f_{\text{SW}} \cdot 1 \times 10^{-10}} \;\Omega$

## Technical Brief: Selection of the Current Limit Timer $T_{off(CL)}$

This compute the delay if too much current is draw from the IC output (2.5A)

$T_{\text{OFF(CL)}} =
\frac{5\,V_{\text{IN}}}{24\,V_{\text{FB}} + 12}\;\mu\text{s}$