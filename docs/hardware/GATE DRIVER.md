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

We estimate the resitance of each diode to be $R_{BSD}=21.5\Omega$, thus $I_{DD,peak} = \frac{10}{R_{BSD}}=465mA$, from empty to full. This is an RC system, that will be charged in $t_{charge} = 4*\tau = 4*RC = 69\mu s$. If we take $C = 87.7nF$, then $t_{charge} = 7.54\mu s$. Some value analysis

- At 128kHz and 99% duty cycle $0.8\mu s$ are available to charge the system (ultimate goal). 
- At 96kHz and 99% duty cycle, $1.0\mu s$ are available to charge the system. 
- At 64kHz and 99% duty cycle, $1.6\mu s$ are available to charge the system.
- At 48kHz and 99% duty cycle, $2.1\mu s$ are available to charge the system.
- At 24kHz and 99% duty cycle, $4.2\mu s$ are available to charge the system.

So $t_{charge} = 1.8\mu s$, seems far to limited as no margin is even taken. A external diode seems to be needed. The external diode must have a very low reverse current, be adaptage to $V_g = V_{batt}+V_{in} = 60 + 10 = 70V$ in wroste case scenario. We chosed to use a ES1B for its current capabilities and its fast $15ns$ recovery time. With those carateristics, an external resistor of $5\Omega$ must be added, bringing the total resistance to $4.1\Omega$ and $t_{charge} = 1.4\mu s$. This resistor will have to be pulse resistant.

_Note1_: This is hardly enough for the 128kHz, but it might be impossible to go at such a speed in the first place. Improvement will come later. 

_Note2_: For the current computation, 10V is considered. For $C = 87.7nF$, $800-87.7nF$ are already charged. Hence the tension will be much much higher, allowing for a lower resistance. We still have to be careful of first charges from 0V to 10V. 

## Technical Brief: Selection of the Bootstrap Diode $R_{gate}$

We can change these capacitance after installation so we will first select one that allows low EMI to ensure reliability. 

It is important to keep $R_{G,off}$ low so it is immune to displacement current generate by the strong $\frac{dv}{dt}$ on swithcing. This can cause self turn on if $R_{G,off}$ is too high as electron can accumulate in the gate. 

We will take $R_{G,on} = 10\Omega$ and $R_{G,off} = 5\Omega => 10\Omega$ as resistances are parallel. We will use the same diode as for the bootstrap capacitor.

_Note1_: These are very EMI safe values.

## Technical Brief: Selection of the Bypass Capacitor $C_{V_{dd}}$

Common rules is to have $C_{Vdd} \geq 10 \sim 20 * C_{boot}$. Hence, for safety, we will take 15µF in a 3216m/3225m package.
