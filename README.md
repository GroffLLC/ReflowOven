# ReflowOven
Reflow Oven Code for Arduino


The software is designed to drive a SSR with an Arduino microcontroller.
System includes Thermocouple w/ amplifier LCD, Arduino Mini Pro, SSR, Button, and toaster heating elements.

The code works with a state machine.

startUp State:
Display splashscreen on LCD
Thermocouple Active:
Yes->Go to Idle state
No->Go to Error state

idle State:
Read oven temperature
Wait for button to be pressed for start condition
Button press:
Yes->If oven is under start threshold, go to preHeat State else stay in idle
No->Stay in idle state

Advanced:
Add another button to select different profiles, temperatures, and times

preHeat State:
Turn on the SSR
Start Timer
Poll Thermocouple for temperature
Temperature must break preheat temperature within a certain period of time, if not go to error
If temperature is exceeded within time, go to soak State

Advanced:
Use start temperature to set on/off cycle to get a linear slope over time to reach temperature within a time

soakState:
Cycle the SSR on/off for periods of time to raise the temperature slowly over time
If the soak time is exceeded before timeout then go to reflow else go to error

Advanced:
Read the temperature change from on/off durations and adjust to meet temperature

reflow State:
Turn the SSR on until the reflow temperature is exceeded
Turn off for 10 seconds
Tell the user to open the oven

Advanced:
Add a cooling state to open oven for the user
Add a fan to aid in cooling

Error State:
Display the error that occured

