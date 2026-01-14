# Gate Driver

It was chosen to use the MP1922 GD which provide both 3A source and 4A sink gate drive current and different usefull features as a fault pin, a integrate current sense amplifier, a programmable slew rate, a thermal shutdown and a desaturation protection among other. This driver is particularlly complex but will provide a lot of usefull information when running and gives us some headroom for future improvments.

The relation between QG, t_sw and Igate is the following Igate = Qg/t_sw. Hence, tsw=40ns@3A,120nC. We consider 40ns to be largely enough. In reality, we expect ~150ns and that will have to be checked.