# BUCKs converters

We are going to use the LM5160 fammily. 

_Note1_: 

## Technical Brief: Selection of the Bootstrap Diode $D_{boot}$

$V_{OUT} = \frac{V_{REF} \times (R_{FB2} + R_{FB1})}{R_{FB1}}$, specified in the datasheet.

Where $V_{REF} = 2V$. We want $V_{OUT} = 10V$ so $\frac{R_{FB2}}{R_{FB1}} = 4$.





## Technical Brief: Selection of the Collector Voltage $V_{cc}$

As the $V_{out}$ voltage is 10V, $V_{cc}$ could be powered using $V_{out}$ to gain efficiency and limit termal losses inside the chip (with the LM5160A chip). It is not implemented as it adds layout complexity for a gain we deemed minimal.