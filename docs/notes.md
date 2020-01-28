# Odrive Notes
## Timers
**TIM1:**
This timer is connected to M0 with the following connections:
- TIM1_CHN : M0_AL_Pin &nbsp; &nbsp; &nbsp; TIM1_CH : M0_AH_Pin
- TIM2_CHN : M0_BL_Pin &nbsp; &nbsp; &nbsp; TIM2_CH : M0_BH_Pin
- TIM3_CHN : M0_CL_Pin &nbsp; &nbsp; &nbsp; TIM3_CH : M0_CH_Pin

This timer is configured as PWM Mode 2 with Deadtime insertion. Timer runs in master mode with Output trigger during update event. All the the 4 channels are configured with the 4th channel to be configured as non PWM. This has one enabled interrupt, the TIM1_UP_TIM10_IRQn.

**TIM8:**
This timer is configured similarly as that for TIM1, and this timer is connected to M1. This timer has two interrupts, the TIM8_UP_TIM13_IRQn and TIM8_TRG_COM_TIM14_IRQn.

**TIM2:**
This timer manages the Brake Resistor connections and the connections are as follows:
- TIM2_CH3 : AUX_L_Pin
- TIM2_CH4 : AUX_H_Pin

This timer is configured as PWM Mode 2. It runs in Master Mode. In this timer the channel 3 is configured with PWM pulse as 0 and OCPolarity as LOW, and the channel 4 is configured with PWM pulse of TIM_APB1_PERIOD_CLOCKS+1 and OCPolarity as HIGH.

**TIM3:**
The timer is connected to M0 Encoder with the following connections:
- TIM3_CH1 : M0_ENC_A_Pin
- TIM3_CH2 : M0_ENC_B_Pin

This timer is initialised with Encoder Mode (Input Capture Mode). The period of the timer is set as 65536 (Max value). 

**TIM4:**
This timer is configured similarly as that of TIM3, and this timer is connected to M1 Encoder.

**TIM5:**
This timer is connected to GPIO Pins 3 and 4. Configured in master mode with a period of 0xFFFFFFFF (32 Bit Max).
The connections are:
- TIM5_CH3 : GPIO_3_Pin
- TIM5_CH4 : GPIO_4_Pin

Channel 3 and 4 of the timer is configured in Input Capture mode. This is configured with an interuppt as well, the TIM5_IRQn.

**TIM13:**
This is not explicitly configured as a master type, Counter is in Up mode with a period of ```(2 * TIM_1_8_PERIOD_CLOCKS * (TIM_1_8_RCR+1)) * ((float)TIM_APB1_CLOCK_HZ / (float)TIM_1_8_CLOCK_HZ) - 1```. This timer is not connected to any Pins. An interrupt, the TIM8_UP_TIM13_IRQn interrupt is also initialised with the timer.

## ADC
**ADC1:**
This ADC is running in Single-Channel Single Conversion Mode with a resolution of 12 bits and with a prescalar factor of 4.
This ADC is connected to the following pins:
- ADC1_IN10 : M0_IB_Pin
- ADC1_IN11 : M0_IC_Pin
- ADC1_IN12 : M1_IC_Pin
- ADC1_IN13 : M1_IB_Pin
- ADC1_IN15 : M0_TEMP_Pin
- ADC1_IN4 : M1_TEMP_Pin
- ADC1_IN5 : AUX_TEMP_Pin
- ADC1_IN6 : VBUS_S_Pin

This ADC is configured to have a Software Trigger and it has a configured interrupt ADC_IRQn.

Channel 6 (VBUS_S_Pin) is configured as regular channel with rank 1 and with sampling time of 3 Cycles. This same channel is also configured as Injected channel of rank 1 with the same sample time as that of regular channel. The number of conversions is set as 1 (hence Single Mode). This injected channel is triggered by the trigger from TIM1 timer. [The above injection settings only applies to Channel 6]. Also this ADC is configured in DMA Mode at DMA2 Stream0.

The rest of the channels are not configured at all, hence this ADC will be dealing with VBUS_S_Pin only.

**ADC2:**
This ADC is running in Single-Channel Single Conversion Mode with a resolution of 12 bits and with a prescalar factor of 4.
This ADC is connected to the following pins:
- ADC2_IN10 : M0_IB_Pin
- ADC2_IN11 : M0_IC_Pin
- ADC2_IN12 : M1_IC_Pin
- ADC2_IN13 : M1_IB_Pin
- ADC2_IN15 : M0_TEMP_Pin
- ADC2_IN4 : M1_TEMP_Pin
- ADC2_IN5 : AUX_TEMP_Pin
- ADC2_IN6 : VBUS_S_Pin

The ADC2 is configured to be triggered with rising edge of the trigger from TIM8 timer. ADC2 also has a configured interrupt ADC_IRQn.

Channel 13 (M1_IB_Pin) is configured as regular channel with rank 1 and with sampling time of 3 Cycles.

Channel 10 (M0_IB_Pin) is configured as an injected channel with rank 1, with number of injected conversions set to 1 (Single Mode). This channel also has the sampling time of 3 Cycles. This injection channel is triggered by the trigger from the TIM1 timer.

**ADC3:**
This ADC is running in Single-Channel Single Conversion Mode with a resolution of 12 bits and with a prescalar factor of 4.
This ADC is connected to the following pins:
- ADC3_IN10 : M0_IB_Pin
- ADC3_IN11 : M0_IC_Pin
- ADC3_IN12 : M1_IC_Pin
- ADC3_IN13 : M1_IB_Pin

The ADC3 is configured to be triggered with the rising edge of the trigger from TIM8 timer. This also has a configured interrupt ADC_IRQn.

Channel 12 (M1_IC_Pin) is configured as a regular channel with rank 1 and sampling time of 3 Cycles.

Channel 11 (M0_IC_Pin) is configured as an injected channel with rank 1, with number of injected conversions set to 1 (Single Mode). This channel also has the sampling time of 3 Cycles. This injection channel is triggered by the trigger from the TIM1 timer.