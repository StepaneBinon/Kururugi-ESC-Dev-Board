# Micro-Controller Unit

For the Microcontroller Unit, the STM32G484 will be used. It was chosen to use an STM MCU because we wanted to learn how to use them. We will select the smallest package as this should provide enough pins. We have two choices:

1. STM32G484CE**T**6: which comes in a LQFP48 (7x7mm) package
2. STM32G484CE**U**6: which comes in a UFQFPN48 (7x7mm) package and provide more GPIO pins, an UART port and 1 additionnal ADC channel compare to 1. It is also almost two times cheaper per unit on JLCPCB.

Thus, we will use a STM32G484CEU6 even if the soldering will be more challenging.

## What is the STM32G4 familly ?

The G4 familly was specifically designed with motor control in mind an is a new adition to the STM32 catalog. The F4 is an other option we looked at, it is more general purpose. A key difference is that the G4 as stronger analogs (faster ADCs (4Msps vs 2Msps), more flexible triggering, often HRTIM, comparators, op-amps). F4 is less oriented toward power electronics.

To ensure we had some headroom for the development board we are going to use the STM32G484, one of the high tier of the familly. An other feature we looked for was the triple ADC, to reduce reading time, and the presence of an HRTIM, which are provided by the 484. An other nice to have for us is the precense of a:

- CORDIC which allows computation of sin, cos, tan, atan2, vector magnitude and polar to cartesian conversion in hardware.
- FMAC which allows FIR/IIR filtering, convolution and dot products in harware.

All these give us a lot of headroom to build the fastest ESC possible.

## STM32G484 — GPIO / Peripherals for Sensorless FOC ESC

### Inputs
- Phase currents **Ia, Ib, Ic** → **3× ADC**
- DC bus voltage **Vbus** → **1× ADC**
- Board / FET temperature (NTC) → **1× ADC**
- Throttle / command input:  → **1× Timer input (DMA)**
    - **DSHOT**
    - **PWM / PPM (alternative)**
- Reset button → **1× GPIO**

### Outputs
- 3-phase inverter drive  
    → **TIM1 or HRTIM: 3 PWM + 3 complementary outputs + deadtime**
- Buzzer → **1× GPIO**
- Status RGB LEDs → **3× GPIO** 

### Bidirectional / Debug / Communication

- **SWD (J-Link)**
    - **SWDIO**: Bidirectional data line (debug + flash) → **PA13**
    - **SWCLK**: Debug clock → **PA14**  
    - **NRST**: Allows full device reset, recovery from bad clock / low-power lockups → **NRST pin**
    - **SWO (ITM trace)**: Real-time printf / event tracing (single-wire trace) → **PB3**  
- **USB FS (CDC / DFU)**
    - **USB_DM**: Differential data line (D−) → **PA11**  
    - **USB_DP**: Differential data line (D+) → **PA12** 
    - **VBUS sense**: Used to detect cable presence → **1x GPIO**

### Grand Total

- **ADC pins**: 5  
- **PWM pins**: 6  
- **Timer input pins**: 1  
- **USB pins**: 2  
- **GPIO pins**: 6  
- **Debug pins**: 4  

➡️ **Total MCU pins used: 24**

The STM32G484CEU6 will provide 48 pins, which should be largely enough.