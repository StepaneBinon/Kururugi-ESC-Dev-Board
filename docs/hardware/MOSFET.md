# MOSFET

Two options where analysed. The Onsemi NVMFS5C604NL and the STM STL180N6F7. 

The NVMFS5C604NL mostfets provide a very low RDS_on (1.2mOhm@10V, 1.7mOhm@5V). Without proper cooling, they are rated for 28A@100°C to 40A@25°C. And are rated for a maximum of 203A@100°C to 287A@25°C.

A 6S battery is 4.2x6=25.2V, providing a security margin of 2.3. This may be too low on highly dynamical manouvers and must be checked.

These drastic performances come at a price, QG is 52nC@4.5V and a whopping 120nC@10V. The required gate drivers will have to be thick. 

On the other hand, the STM MOSFET as a greater RDSON at 2.4mOhm but is much faster to switch and as an overall better switching response. Hence, as we design the mosfet for a drone which will never, due to sensorless BEMF measure, reach a duty cycle 100%, or very rarely, we prefer to use the STM MOSFET for the first version. Having the same package, both can be exchanged later.