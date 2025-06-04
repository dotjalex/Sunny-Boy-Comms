# Sunny-Boy-Comms
Simple, cheap, UART/RS232 communication with SB1100, SB1200 and SB1700 PV inverters.
I would expect this to be applicable to any SMA products using the "piggy-back" connector card slot such as the Sunny Island, Windy Boy, Sunny Mini Central, etc.

WARNING! Access to the "piggy-back" slot requires removing the inverter cover, high voltage DC and AC will be present inside with no RCD to save you here, DANGER OF DEATH OR ELECTROCUTION, even after disconnection of solar and mains there are some large capacitors in there which will still be high voltage DC. Equally the logic components are sensitive to ESD or crossed wires to higher voltages, this will be the end of the logic circuits.

Having obtained a Sunny Boy SB1700 effectivly for free I was keen to get some panels on my garage roof and see what it could do, annoyingly with modern panels at 4x425Ws connected the voltage isnt high enough to hit the PV-DC start voltage. I could add another panel but this would then be well over the DC-Ic-Max for this inverter. It would seem a simple change to the settings would be enough to get it working though, but no, no buttons, no internal dip switches, and without a £130 piggy-back card, no external communication. Luckily I found this website: https://mensi.ch/blog/articles/data-interface-of-an-sma-sunnyboy-inverter, this gave me enough information to determine which pins did what and that they were likely TTL/UART level coms.

![IMG_20250604_113430](https://github.com/user-attachments/assets/422449d5-dde8-4a78-8f88-8491f204e9b1)

Here is the slot. 
The 14 pin header at the top is the logic circuit output of the inverter, the 12 pin header at the bottom is the output to the 4 screw terminals. There is also a 6 pin jumper block right of the 12 pin bottom header to add termination resistance if required.
SMA used to sell USBPBS (direct USB connection), 485USPB (RS485 adapter card), 232USPB (RS232 adapter card), BTPB-EXTANT (bluetooth adapter card) and others as well to fit in this slot depending on requirements. They all provide galvanic isolation between the inverter logic and the outside world, great if youve just spent £1k on one of these back when they were new. As mine was free I dont care too much if I blow it up:

![IMG_20250604_210406](https://github.com/user-attachments/assets/ae25ba43-2dee-45db-89d5-3266852c4045)

  Top Header
  
  2  4  6  8 10 12 14
  
  1  3  5  7    9   11  13 

 Pin 3 RX
 
 Pin 5 TX
 
 Pin 9 GND
 
 Pin 10 5V+ dont connect this, I'm including for refernce only.

![IMG_20250604_2104062](https://github.com/user-attachments/assets/694474a2-18f8-47c8-93b4-f2d2f0d462f8)

A cheap TTL/UART-USB will now work. Bearing in mind there is no galvanic isolation I used a laptop on battery only sat on a non conductive surface and I grounded myself when touching any part of the inverter or laptop. AC was turned off with solar connected. I kept the cable connected only long enough to change what I needed, this is not a safe solution to leave connected.

I used 'Sunny Data Control 3.92' to access the parameters. This can be downloaded from SMA's website.
You will need to use a security login to change the parameters, go to 'extras' > 'security level' and a box will pop up. Enter "ID00xx" where xx = todays date + todays month + todays year. For instance today is 04/06/25 = 04 + 06 + 25 = 35 so "ID0035".

The default PVDC-start was 180v, I set this to 150v which is the minimum. As soon as AC was reconnected it started working. Awesome, a nearly free solar setup.

I hope this saves someone the hours of searching I went through to find a dirt cheap resolution to changing the settings on their inverter.
