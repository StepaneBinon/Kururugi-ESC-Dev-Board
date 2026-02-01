# Other choices

Following are listed some other engineering choices for the buck converter layout.

## Technical Brief: Output capacitor $C_{out}$

We have $\Delta I_{L,\max} = 397mA$ and we want 10mV of variation maximal. Hence, $C_{OUT} = \frac{\Delta I_{L,\max}}{8 \times f_{SW} \times \Delta V_{O,\text{ripple}}} = 5.5\mu F$. We will take $C_{OUT} = 1\times10 = 20\mu F$. We chosed to use 2 capacitance to reduce ESR in X7R with 2012m format with a voltage range of 25V to limit the impact of DC biais (6 to 8µF expected).

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

## Technical Brief: Selection of the Soft Start Capactor $C_{SS}$

$C_{ss}$ must be greater than 1nF. For VersionV1.0, having a long soft start seems very relevant to avoid bug. In general, having a long start for ESC does not have an major impact.

$C_{SS} = \frac{I_{SS} \times T_{\text{startup}}}{V_{SS}}$

With $V_{SS} = 2V$, $I_{SS} = 10\mu A$ and $C_{SS}=1\mu F$, we have $T_{\text{startup}} = 200ms$.

## Technical Brief: Under voltage lockout - RUV1/RUV2

We want $V_{IN,\text{rise}}=18V$ and $\Delta V_{IN}=2.5V$ . We have $I_{HYS}=10mA$. 

Hence, $R_{UV2} = \frac{\Delta V_{IN}}{I_{HYS}} = 125\,\text{k}\Omega$.

And because $V_{IN,\text{rise}} = V_{UVLO}\left(1 + \frac{R_{UV2}}{R_{UV1}}\right)$, we have $R_{UV2} = 9.25\,\text{k}\Omega$.

We will take $R_{UV1}=9.31\text{k}\Omega and $R_{UV2}=124\text{k}\Omega$