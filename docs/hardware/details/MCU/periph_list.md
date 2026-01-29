# STM32G484 — GPIO / Peripherals for Sensorless FOC ESC

## Inputs
- Phase currents **Ia, Ib, Ic** → **3× PGA OPAMP ( → 3× ADC internally)**
- DC bus voltage **Vbus** → **1× PGA OPAMP ( → 1× ADC internally)**
- Board / FET temperature (NTC) → **1× PGA OPAMP ( → 1× ADC internally)**
- Throttle / command input:  → **1× Timer input (DMA)**
    - **DSHOT**
    - **PWM / PPM (alternative)**
- Reset button → **1× GPIO**

## Outputs
- 3-phase inverter drive → **TIM1 or HRTIM: 3 PWM + 3 complementary outputs + deadtime**
- Buzzer → **1× GPIO**
- Status RGB LEDs → **3× GPIO** 

## Bidirectional / Debug / Communication

- **SWD (J-Link)**
    - **SWDIO**: Bidirectional data line (debug + flash) → **PA13**
    - **SWCLK**: Debug clock → **PA14**  
    - **NRST**: Allows full device reset, recovery from bad clock / low-power lockups → **NRST pin**
    - **SWO (ITM trace)**: Real-time printf / event tracing (single-wire trace) → **PB3**  
- **USB FS (CDC / DFU)**
    - **USB_DM**: Differential data line (D−) → **PA11**  
    - **USB_DP**: Differential data line (D+) → **PA12** 
    - **VBUS sense**: Used to detect cable presence → **1x GPIO**

## Grand Total

- **ADC pins**: 5  
- **PWM pins**: 6  
- **Timer input pins**: 1  
- **USB pins**: 2  
- **GPIO pins**: 6  
- **Debug pins**: 4  

➡️ **Total MCU pins used: 24**

The STM32G484CEU6 will provide 48 pins, which should be largely enough.