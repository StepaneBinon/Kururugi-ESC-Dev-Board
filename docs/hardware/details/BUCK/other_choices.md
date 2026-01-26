# Other choices

Following are listed some other engineering choices for the buck converter layout.

## Technical Brief: Output capacitor $C_{out}$

We have $\Delta I_{L,\max} = 397mA$ and we want 10mV of variation maximal. Hence, $C_{OUT} = \frac{\Delta I_{L,\max}}{8 \times f_{SW} \times \Delta V_{O,\text{ripple}}} = 5.5\mu F$. We will take $C_{OUT} = 1\times10 = 20\mu F$. We chosed to use 2 capacitance to reduce ESR in X7R with 2012m format with a voltage range of 25V to limit the impact of DC biais (6 to 8µF expected).

## Technical Brief: Selection the series ripple resistor $R_{ESR}$

Resr is not usefull as we deemed the ESC+MLCC ESR+intern path to already generate 25mV ripple. We will still add a $0\Omega$ capacitor in case the current ripple is not enough.

## Technical Brief: Forced PWM (FPWM)

If FPWM is put to low, then the efficiency is increased. The low side mostfet behave as a diode and some commutation steps can be skip if low cuurent is required. However, this create some noise and less predictable behavior overall as steps can be skipped. Thus we will force CCM by putting FPWM to high.

## Technical Brief: Selection of the Collector Voltage $V_{CC}$

As the $V_{out}$ voltage is 10V, $V_{cc}$ could be powered using $V_{out}$ to gain efficiency and limit termal losses inside the chip (with the LM5160A chip). It is not implemented as it adds layout complexity for a gain we deemed minimal.

## Technical Brief: Selection of the Feedback Resitors

$V_{OUT} = \frac{V_{REF} \times (R_{FB1} + R_{FB2})}{R_{FB1}}$, specified in the datasheet.

Where $V_{REF} = 2V$. We want $V_{OUT} = 10V$ so $\frac{R_{FB2}}{R_{FB1}} = 4$. We should try to keep the sum (lost power), in the $10k\Omega \text{ to } 100k\Omega$ order.

## Technical Brief: Selection of the Current Limit Timer $C_{VCC}$

It is recommended to have $C_{VCC} = 1\mu F$, good quality X7R.

## Technical Brief: Selection of the Current Limit Timer $C_{BST}$

Soft start is important to limit current flow at ESC start as all capactior will require to be chatge simultaneously. If well control, it could even be used to reduce the resistance of the boostrap capacitor of the gate driver so we can charge it faster during normal operation.

It is recommended to have $C_{BST} = 10nF$, with a good quality X7R. It is fed by $C_{VCC}$ during off times.

## Technical Brief: Selection of the Current Limit Timer $T_{off(CL)}$

This compute the delay if too much current is draw from the IC output (2.5A)

$T_{\text{OFF(CL)}} =
\frac{5\,V_{\text{IN}}}{24\,V_{\text{FB}} + 12}\;\mu\text{s}$