# Pedestrian_Touchless_Button

Explanation

The pedestrian waves at the sensor, which detects the input. The sensor sends a signal to the microcontroller. The microcontroller here displays ‘WAIT’ on the screen.
The microcontroller sends a request of demand to the main controller. The main controller calculates the amount of time the pedestrian has to wait for safe crossing. 
After said time, when the main controller is about to complete its stages, it sends a signal to the microcontroller.
The microcontroller, which powers the motor and the buzzer, now displays ‘WALK’ on the screen. The tactile motor starts to rotate at a desirable speed, and the buzzer starts beeping.
The buzzer starts with a low frequency, but gradually as time goes on, its frequency increases indicating that there is little time left for crossing the street.
As the time for crossing ends, the microcontroller stops giving power to the motor and the buzzer.


Anti-Fault System
	
The motor’s voltage and current are monitored on the display through the INA219 IC, via I2C communication with the STM32, to make sure the motor is not drawing high current.
The microcontroller will send a request to the main controller after a buffer period of 2-3 seconds after receiving an input from the IR sensor. If another request arrives within that window of time, then the first request gets cancelled and the second one is considered, but again if a third request or continuous request arrives, then the STM will cancel all the requests, thinking something went wrong with the input or someone is tampering with the input button. 
The STM32 will be coded in such a way that, If the input from the IR sensor is high for more than a certain period of time, for example 2.5 seconds, the request will be cancelled.
The functioning of the display(WALK or STOP) is verified as whenever the STM receives a high input from the main controller, it changes from “STOP” to “WALK”.


the main.c (STM32CUBEIDE) file does the following:-
PC13 and PC15: GPIO_Output
PA8: TIM1_CH1
PA15: TIM2_CH2
PA1: ADC1_IN1
