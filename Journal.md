# Journal

## 8/5/26

- Found the ESP-32 MCU i want to use ([ESPRESSIF ESP32-S3-WROOM-1-N8](https://www.lcsc.com/product-detail/C2913198.html?s_z=n_q_esp32-S3%2520wroom&spm=wm.fly.bg.0.xh&lcsc_vid=RAALBlxfRVNXA1xQFAVeUlQHEgMNX1dfRlReAwIAQVExVlNRT1NbUlNfRVVaUTsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D))
- [Found 18650 battery mount tray](https://www.lcsc.com/product-detail/C2988620.html?s_z=n_q_18650%2520battery%2520holder&spm=wm.fly.bg.0.cbh&lcsc_vid=RAALBlxfRVNXA1xQFAVeUlQHEgMNX1dfRlReAwIAQVExVlNRT1NbUFRWQVVeVjsOAxUeFF5JWBYZEEoKFBINSQcJGk4%3D)
- Got the [USB-C Port](https://www.lcsc.com/product-detail/C2689970.html?s_z=n_q_C2689970&globalKeyword=C2689970)
- Got the [PD sink from a previous project](https://www.lcsc.com/product-detail/C22373734.html?s_z=n_q_C22373734&globalKeyword=C22373734)
- Find the Battery charger ic i want to use ([the TP4056](https://www.lcsc.com/product-detail/C16581.html?s_z=n_q_TP4056&spm=wm.fly.bg.0.xh&lcsc_vid=RAALBlxfRVNXA1xQFAVeUlQHEgMNX1dfRlReAwIAQVExVlNRT1NYV1VXQFRZVDsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktXR1FaSQwSGg0%3D))
  - Spent a while setting the battery charging circut up

- Started the Layout and routing on the PCB

<https://lapse.hackclub.com/timelapse/oYXOqTZ7uB9a>

## 9/5/26

- did a bit more routing and declared some parts

## 27/5/26

- found the BMS ic i want to use [on LCSC](https://www.lcsc.com/product-detail/C351410.html)
- also found a better data sheet from [Digikey](https://www.digikey.co.uk/en/products/detail/shenzhen-slkormicro-semicon-co-ltd/DW01A/28143000) because the one on LCSC was a bit too vague
- finished the 3.7v battery system schematic
- re-routed the entire board so far, as it is routed very bad

## 28/5/26

- made 2 pages in the schematic for the power systems and for the MCU and 4.5v switching for the output to the string lights

## 6/6/26

Fun date

- Found the screw terminal i want to use to connect the 4.5v output to the string light leads
- looked into the 3.7v to 4.5v converter i want to use

## 01/07/26

- finished the 4.5v boost circut

## 02/07/26

- re-did the 4.5v boost circut but remembered to save it this time lol
- added test-points for the +4.5v and +3.3v rails so that i can test that the converters are working correctly
- added a test point for the VUSB net so that i can check that the correct voltage (5v) is being negotiated by the usb-c sink
- added a power switch to the output from the BMS
- added reset button
- applied parts to some of the passives i had placed over time

## 03/07/26

- added smoothing caps to the usb data lines
- connected the enable pin of the TPS61254YFFR(4.5v boost ic) to GPIO-1 on the esp32 so that i can control it from EspHome by driving the pin high
- put no-connect flags on all the unused pins
- started to layout the PCB for the (hopefully final time) whilst doing so, checking over the schematic for every part

## 04/07/26

- finished layout of the PCB
- added a little silkscreen message :)
- changed the size of the vias on the ground pin of the esp32-s3 as they were too small for JLCPCB
- made sure that the ground plane was not under the antenna of the esp32 so that the performance of wifi is less affected
- checked ordering through JLCPCB to make sure that they can make it all
- found that PCBA is super expensive, looking at soldering the parts myself
- finding replacements for some parts because they are out of stock

## 05/07/26

all of the changes i am making today are as a result of asking for someone to look over my schematic on ([#electronics](https://hackclub.slack.com/archives/C056AMWSFKJ/p1783166697054009)) in Slack and getting feedback :)
today i am going to:

- [X] Remove the PD sink and replace it with 2 5.k resistors to reduce cost. As i am getting 5v from the usb-c supply, i don't need to use a sink because it does not require proper PD negotiation, and it can request 5v from any usb-c source by just putting a 5.1k resistor to ground on each cc pin
  - removed the sink and placed the resistors
- [X] replace the esp32-s3 with and esp32-c3 to reduce cost, as the s3 is more powerful than i need for this application
  - change up the boot button so that it holds GPIO9 high when not pressed
  - connect up all the other parts
- [X] use the PWM pins on the c3 to allow for dimming for the lights
  - found a MOSFET to take the 3.3v PWM output from the esp32 and turn it into a 4.5v PWM output for the load
  - set up the MOSFET to transform the PWM signal from the ESP32 to a 4.5v PWM output for the lights
- finished the layout of the PCB
- removed the 0 ohm resistors as they are unnecessary for the length of my usb data lines
- 4 m3 mounting holes

## 06/07/26

- changed my 3.3v source, the one i was using, LCSC dont have carry anymore
  - im now going to be using the TI TPS63001DRCR
- found the inductor i want to be using, i got it from the recommended parts list from TI.
  - placed all the resistors and caps needed
  - finished the layout for the 3.3v source
- checked ordering at JLCPCB to make sure there arent any problems
  - replace R2 and R6 as the ones i had selected are now out of stock at LCSC
- whilst i was checking the JLCPCB ordering, i found that the 4.5v boost ic i was using is not compatible with the economic PCBA with JLCPCB, and can only be done with the standard PCBA, which costs around $145. due to the package size i cannot solder it myself, so i must find an alternative ic
  - found the ME2188A45, it is a working alternative for the TPS61254YFFR
  - placed and assembled it on the schematic
  - finished the layout on the PCB, and beefed up some of the traces that will be taking high current
  
## 08/07/26

- started modeling the base of the enclosure
  - created the basic outside shape
  - added the bases for the threaded inserts to hold in the PCB

## 09/07/26

- added vents to one side of the base of the enclosure
- added vents to the opposite side to the usb-c port
- sliced the base of the enclosure to get a better feel for how it will print, i think i need to make the walls between the vents a bit bigger, it looks like it will be a bit too fragile
  - made the gaps between each of the vents bigger
- finished up the base (for now)
  - except i still need to find some threaded inserts for the bolts from the PCB to go into, and need to figure out how i am going to attach the top and bottom pieces of the enclosure together
- printed the base as it is now so that i can make sure that the bottom and top fit together properly
- the base finished printing, i think that the vents are still too a bit weak, i need to make the gaps between the holes bigger.

## 10/07/26

- [X] i need to make the caps on the usb data lines bigger, as they are too small to solder by hand rn
- [X] i need to make the mounting holes in the PCB bigger as they are a bit too small for the M3 bolts

- I made the non-18650/JST version of the board
  - i plan on using [this battery](https://thepihut.com/products/2000mah-3-7v-lipo-battery) for my version of the enclosure
  - i am going to use [this JST connector](https://www.lcsc.com/product-detail/C131337.html?spm=wm.fly.bg.4.xh&lcsc_vid=QlgMAlMDFARbA1IFRQNZBFZRFlULVQJREQQMBlRVFQQxVlNeRFZeU11SR1JbVzsOAxUeFF5JWBYZEEoKFBINSQcJGk4eFQsCAgIaSgADAwAHC0slRlRWV1VUWQkaCgg%3D)
  - did the layout for the JST board, and made it more compact than the 18650, as is the benefit of the non-18650 board
  - added a cutout to the board, next to the battery connector, to allow the wires to pass to the bottom of the board.
- started puting all the files into the Github repo

## 13/07/26

- [X] i need to make the vents on the base of the enclosure smaller, they feel a bit too weak
- [X] i need to make the holes for the heated inserts bigger in the base of the 18650 board as i haven't made them the right size for the insert, i have just made them the size of the bolt
  - made the holes in the base 4.2 mm, as my threaded inserts have an outer diameter of 4.8mm. I got the sizing and offsets from [this](https://www.cnckitchen.com/blog/tipps-amp-tricks-fr-gewindeeinstze-im-3d-druck-3awey) article
  - since i made the holes bigger, i also had to make the outer diameter of the parts that hold the inserts bigger
  - i have started a print of the base of the enclosure, so that i can feel how effective my changes have been

- found the size of heat-set insert and machine screws i want to use, i am using M3x8 machine screws ([these](https://uk.store.bambulab.com/products/m3-socket-head-cap-machine-screws-shcs-1?id=41622217621564) ones from Bambu lab) and M3 heat-set inserts with an external diameter of 4.8mm and a height of 3.8mm, as those are suitable and i have them on hand
- finishing up the enclosure for the 18650 version
  - added a hole in the side of the base so that i can have an m3 machine screw go into the side of one of the support pillars on the top of the enclosure, to attach the top to the bottom of the enclosure
  - sketch 5 is fucked, i cant select any of the profiles to extrude them, im just going to fully remake the sketch at this point
  - fixed sketch 5
  - printing out both of the parts of the enclosure to check the fit
    - i think that the top of the enclosure can be made a bit thinner overall, as it is very bulky
    - the holes for the threaded inserts are a bit small so i am going to make them bigger
    - the hole for the screw that holds in the top of the enclosure is a bit too shallow, so i will make it deeper
  - printing out another copy
    - [] i need to move one of the ribs on the underside of the top of the enclosure away from the hole
    - [] remove the chamfer on the pin with the screw, as it interferes with it being able to fit properly
    - [] add more ribs to the underside of the top of the enclosure as it still a bit too flexible
    - [] make the pin with the screw on it a bit shorter, as it is too long
    - [] add a fillet's to the top of the enclosure

- started working on the base of the JST Version enclosure
  - the board is not that big, so the battery that i was planning on using is too big to fit underneath it, and the JST version is supposed to be the small one, so i am going to switch to [this one](https://thepihut.com/products/500mah-3-7v-lipo-battery)
  - since i have changed the battery, i can make the standoffs on for the board shorter, from 8mm to 5mm
  - the walls need to be reasonably thick because of the space necessary for the screws to fit in, so i am minimizing the wall thickness by not having the wall thickness be even everywhere
  - i am carving a kind of alcove into the side of the base of the enclosure, as the battery is in the way of the pins of the screw terminal
  
## 14/07/26

- [X] move the rib on the underside of the top of the enclosure away from the hole
- [X] remove the chamfer on the pin with the screw, as it interferes with it being able to fit properly
- [X] add more ribs to the underside of the top of the enclosure as it is still a bit too flexible
- [X] make the pin with the screw in it shorter, as it is too long
- [X] add a fillet to the top of the enclosure

- i reshaped the hole for the screw on the top of the enclosure, as it is kinda deformed when it was printed so i am going to flatten the top a bit so that it prints better. I also made the hole smaller so that i has more grip
- added the pass-through for the reset button on the 18650 version of the board
  - cut the hole into the top of the enclosure and added the container/rails for the button to go along
  - modeled the stick thing so that the button can be pushed from outside the enclosure and constrained it into the assembly
- printing out the 18650 version so that i can see how it all fits together
  - the hole for the button is way to small
  - the pass-through pin is too tight in its tracks
- Moved the reset button because the place that i had it is too inaccessible
  - i moved it on the PCB
    - re-uploaded all the files to GitHub

- moved the screw terminals on the JST version closer to the edge as the through-hole pins were interfering with the space for the battery
  - re upload all of the files for the JST version on GitHub
  - changed the model in Fusion
- 
