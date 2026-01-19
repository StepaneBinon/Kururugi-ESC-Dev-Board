# BUCKs converters

The MP1922 gate driver requires 3A (4.5 to 10V) in source gate drive. An ESC will use 2 mosfets simultaneously. As such, the BUCK must be size to produce at least 6A. Note that control of the mosfet driving slew rate might give some headroom.

This BUCK will also be used to power the STM32G484and the gate drive. The last one, however, get its power from Vg directly.





