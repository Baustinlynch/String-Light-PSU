# String-light-controller

an esp-home controller for 4.5V string-lights with PWM dimming and a battery with USB-C recharging.

## Operation

The board features an ESP32-C3 to interface with the PWM pin at GPIO4, which is then transformed through the mosfet (Q2) into a 4.5v PWM signal.
The PWM output can be used to change the brightness of the lights, and can be easily controled through esp-home to turn any 4.5v string lights into smart-lights with homeassistant!
String lights that use 3 AA or AAA batteries operate at 4.5v and are compatible with this board.

## Assembly

All PCB parts can be assembled by JLCPCB PCBA, but I have also selected parts that are relatively easy to solder by hand using a hotplate and soldering iron.

### 18650 version

#### Parts

- One fully assembled board
- One 18650 battery
- 3D printed case parts
  - These should be fine printed in PLA, but a higher-temperature filament may be better as some switching regulators can produce more heat that PLA may not handle.
- 4 M3 threaded inserts (full dimensions will be picked later; I haven't finished modeling it yet)
- 3 M3 bolts (full dimensions will be picked later; I haven't finished modeling it yet)

#### Assembling 
(case is not fully designed so this is tbd)