# STM32G484 – Peripheral Overview (concise)

## Core & System
- **Cortex-M4F CPU (170 MHz)**  
  MCU core with FPU and DSP instructions for real-time control.
- **NVIC / SysTick**  
  Interrupt controller and system timer.
- **CRC**  
  Hardware CRC calculation.
- **DBG / SWD**  
  Debug and trace interface.

## Memories
- **Flash memory**  
  On-chip program storage.
- **SRAM**  
  Data and stack memory.
- **ART accelerator**  
  Zero-wait-state Flash access at high clock.

## Analog peripherals
- **ADC (3× 12-bit, up to 4 Msps each)**  
  Fast, hardware-triggerable ADCs with oversampling and injected channels.
- **DAC (2× 12-bit, 4 channels total)**  
  Waveform generation, references, thresholds.
- **Comparators (6×)**  
  Fast analog comparators with internal routing to timers/ADC (faults, ZC).
- **Operational amplifiers (4×)**  
  Configurable PGA or follower for current sensing and signal conditioning.
- **Internal voltage reference (VREFBUF)**  
  Stable reference for ADC/DAC/comparators.
- **Temperature sensor / Vbat monitor**  
  Internal monitoring sources.

## Advanced math accelerators
- **CORDIC**  
  Hardware sin/cos, atan2, magnitude, vector rotation.
- **FMAC**  
  Hardware FIR/IIR filters, dot products, convolution.

## Timers
- **HRTIM**  
  High-resolution timer (~184 ps) for SMPS, advanced PWM, dead-time, faults.
- **Advanced timers (TIM1, TIM8)**  
  Complementary PWM, dead-time, break inputs (motor control).
- **General-purpose timers (TIM2–TIM7, etc.)**  
  Time bases, input capture, output compare.
- **Low-power timers (LPTIM)**  
  Low-energy timing and pulse counting.
- **RTC**  
  Calendar and timekeeping.

## Communication interfaces
- **USART / UART (multiple)**  
  Serial communication.
- **SPI / I²S**  
  High-speed synchronous serial.
- **I²C**  
  Standard and fast-mode serial bus.
- **FDCAN**  
  CAN-FD controller for robust field networks.
- **USB FS (device)**  
  Full-speed USB device interface.
- **IRDA / LIN / SmartCard support**  
  Via USART modes.

## Data movement & glue
- **DMA (with DMAMUX)**  
  High-throughput peripheral↔memory transfers with flexible routing.
- **DMAMUX request generator**  
  Timer/event-driven DMA triggers.
- **Event system (internal routing)**  
  Peripheral-to-peripheral connections without CPU.

## Security & safety
- **Independent watchdog (IWDG)**  
  Hardware fail-safe reset.
- **Window watchdog (WWDG)**  
  Software supervision.
- **Brown-out reset (BOR)**  
  Supply voltage monitoring.
- **Memory protection unit (MPU)**  
  Region-based memory access control.

## Clock & power
- **RCC**  
  Clock generation and distribution.
- **PLL / HSI / HSE / LSI / LSE**  
  Flexible clock sources.
- **Low-power modes (Sleep/Stop/Standby)**  
  Energy management.

## GPIO & external
- **GPIO with EXTI**  
  Digital I/O and external interrupts.
- **AF matrix**  
  Flexible pin multiplexing.