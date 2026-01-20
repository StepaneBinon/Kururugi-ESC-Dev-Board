# Gate Driver

## Technical Brief: Selection of the Bootstrap Capacitor $C_{boot}$

An usual value in the drone context is to take Cg=1µf. Lets check it is ok with my configuration. We can use the datasheet of the INFINEON 2EDL8X2X.

a) $\Delta V_{Cboot\_max} = V_{dd} - V_F - V_{HBR} - V_{HBH}$ = 2.48V

as maximum are $V_{dd} = 10V$, $V_F = 1.25V$, $V_{HBR} = 6.0V$ and $V_{HBH} = 0.27V$

b) $Q_T = Q_g + \frac{I_{HB}+I_{HBS}}{F_{SW}} = 217.5nC$

as maximum are $Q_g = 120nC$, $I_{HB} = 0.7mA$, $I_{HBS} = 1.25mA$ and $F_{SW\_min} = 20kHz$, for 100% duty cycle

Both $I_{HB}$ and $I_{HBS}$ are quite high, this is a price to pays for fast propagation time and gate opening/closing.

c) $C_{boot\_min} \geq \frac{Q_T}{V_{Cboot\_max}} = 87.7nF$

d) To avoid DC voltage biais present on MLCC capacitor, aging, we are going for a 50V rated capacitor for 1µF on a 1608m package size, which should provide enough margin

0402,~60% to 70% loss,300nF – 400nF,Safe (4x margin) <br>
**0603,~20% to 30% loss,700nF – 800nF,Very Safe (8x margin)** <br>
0805,~10% to 15% loss,850nF – 900nF,Ideal

The bigger issue with oversized capacitor are the following
 - important current at first charge, can burn the internal diode
 - slow to charge the last bit -> may be an issue for the last few mV
 - Common rule is to have Cvdd x10 to x20 larger
 - Self Resonning Freq is higher, it might not have the punch needed for high PWM

We should start to see depletion, taking $C_{boot} = 700nF$, problem appears around $F_{SW} = \frac{I_{HB}+I_{HBS}}{(C_{boot}*V_{Cboot\_max})-Q_g} = 1207kHz$

## Technical Brief: Selection of the Bootstrap Diode $D_{boot}$

We estimate the resitance of each diode to be $R_{BSD}=21.5\Omega$, thus $I_{DD,peak} = \frac{10}{R_{BSD}}=465mA$, from empty to full. This is an RC system, that will be charged in $t_{charge} = 5*\tau = 5*RC = 86\mu s$. If we take $C = 87.7nF$, then $t_{charge} = 1.8\mu s$. Some value analysis

- At 128kHz and 99% duty cycle $0.8\mu s$ are available to charge the system (ultimate goal). 
- At 96kHz and 99% duty cycle, $1.0\mu s$ are available to charge the system. 
- At 64kHz and 99% duty cycle, $1.6\mu s$ are available to charge the system.
- At 48kHz and 99% duty cycle, $2.1\mu s$ are available to charge the system.
- At 24kHz and 99% duty cycle, $4.2\mu s$ are available to charge the system.

So $t_{charge} = 1.8\mu s$, seems far to limited as no margin is even taken. A external diode seems to be needed.




-----
Draft:

The termal dissipation is then of $P = R_{BSD}*I_{DD,mean}^2 = 1.157W$. 
$F_{SW,max} = 128kHz$, $Q_{T,max} = Q_g + Q_{boot} = 920nC$ and $I_{DDO}=3.2mA$
$I_{DD,mean} \approx I_{DDO} + Q_T*F_{SW,max} = 120.96mA$, 

----

## Technical Brief: Selection of the Bootstrap Diode $D_{boot}$

## Technical Brief: Selection of the Bypass Capacitor $C_{V_{dd}}$

Common rules is to have $C_{Vdd} \geq 10 \sim 20 * C_{boot}$. Hence, for safety, we will take 
