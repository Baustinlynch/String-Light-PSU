# String-light-controller

an esp-home controller for 4.5V string-lights with PWM dimming and a battery with USB-C recharging.

## Operation

The board features an ESP32-C3 to interface with the PWM pin at GPIO4, which is then transformed through the mosfet (Q2) into a 4.5v PWM signal.
The PWM output can be used to change the brightness of the lights, and can be easily controled through esp-home to turn any 4.5v string lights into smart-lights with homeassistant!
String lights that use 3 AA or AAA batteries operate at 4.5v and are compatible with this board.

## Assembly

[[Assembly]]
