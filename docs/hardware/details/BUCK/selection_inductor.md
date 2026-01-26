# Technical Brief: Selection of the induction - L

We estemeed the max current to be 590mA according the following value:
1. The MCU (STM32G484): 300mA
2. The 3xGD (2EDL8X2X): 3x30 = 90mA
3. Other (diodes, LDO efficiency): 200mA

Taking some margin, we will size the buck for $I_{O,max}=1.0A$. The highest operating point for such a load, considering sag, is set at 28V and that a maximal of 40% ripple is wanted at high current.

$L_{\min} = \frac{V_O \times \left( V_{IN,\max} - V_O \right)}{V_{IN,\max} \times F_{SW}\times  I_{O,\max}\times  0.4} = 18\mu H$

So the peak to peak curent is $\Delta I_L = \frac{V_O \left( V_{IN} - V_O \right)}{V_{IN} \, f_{SW} \, L} = 397mA$. And the max current is 1+0.397/2=1.198A which is less than the high side mostfet current limit.

The selected inductor must have a saturation above 2.875A, to be able to take overload and short circuit conditions.