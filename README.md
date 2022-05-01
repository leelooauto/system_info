# RPI System Info

Originl project by [SliderBOR](https://www.thingiverse.com/sliderbor/designs) on [Thingaverse](https://www.thingiverse.com/thing:3022136)

## system info Features
- OLED info screen with IP address, host, CPU & Memory utilization
- Button for OLED, reboot and shutdown
- LED via GPIO
- Power switch

## system info Functions
- The OLED shows information about IP address, hostname and current utilization when you push the button  
- When button held for longer than ~8 sec. and released the Raspberry Pi will perform a reboot  
- When button held longer than ~12 sec. and released the Raspberry Pi will shutdown  
- The OLED shows information about the current action  

After the Raspberry Pi is shut down, it can be switched off (only the power indicator LED on the board will remain turned on by hardware design). All other electrical components on the board are turned off (SoC, RAM etc.)


### Material needed
- 3D print
- 2x M2.5 screws
- 2x M2.5 nuts
- 128x32 OLED 0,91" SSD1306 blue or white (link below)
- 1x Push button 6mm x 6mm x 7mm with cap (links below)
- 1x 3 mm LED
- 1x 10K resistor
- 1x 330 resistor
- 1x small piece of PCB 2,54mm hole pitch (link below)
- 11x jumper wires (link below)
- 1x Miniature slide switch (link below)
- 1x Pin header male (2 pins) (link below)
- Hot glue

#### Links (examples only)
- OLED:
  - https://www.aliexpress.com/item/1pcs-0-91-inch-OLED-module-0-91-white-OLED-128X32-OLED-LCD-LED-Display-Module/32672229793.html
- Push button:
  - https://www.aliexpress.com/item/100PCS-6X6x7mm-4PIN-dip-TACT-push-button-switch-Micro-key-power-tactile-switches-6x6x7-6-6/32854062885.html
- Push button cap:
  - https://www.aliexpress.com/item/20pcs-lot-Tactile-Button-Caps-Plastic-Cap-Hat-for-6-6mm-Tactile-Push-Button-Switch-Lid/32865759745.html
- PCB:
  - https://www.aliexpress.com/item/Free-shipping-10Pcs-new-Prototype-Paper-Copper-PCB-Universal-Experiment-Matrix-Circuit-Board-5x7cm-Brand/32351499755.html
- Jumper wire:
  - https://www.aliexpress.com/item/40pcs-lot-10cm-40P-2-54mm-dupont-cable-jumper-wire-dupont-line-male-to-female-dupont/32674901253.html
- Miniature slide switch:
  - https://www.aliexpress.com/item/10pcs-Mayitr-Black-SPDT-Switch-Micro-Toggle-Switch-ON-Off-Miniature-Slide-Switches-For-DIY-Small/32848360942.html
- Pin header:
  - https://www.aliexpress.com/item/10PCS-40Pin-1x40P-Male-Breakable-Pin-Header-Strip-2-54mm-Long-Blue-Red-White-Green-Yellow/32863408765.html


## Python Script
1. SSH to Pi
2. Enable i2c and spi using raspi-config:
```
sudo raspi-config
```
  - Interfacing Options
    - SPI
    - I2C

3. Install the adafruit libraries and other software requirements for the OLED script to work (maybe some of them are already installed)
```
sudo apt-get install python3-pip
sudo pip3 install adafruit-circuitpython-ssd1306
sudo apt-get install python3-pil
sudo apt-get install -y python3-smbus
sudo apt-get install -y i2c-tools
sudo pip3 install psutil
```

4. Check if the OLED is properly connected to I2C bus
```
sudo i2cdetect -y 1
```
You should see a device at address ```3c```

5. Clone this repo >> git clone https://github.com/leelooauto/system_info.git
6. cd system_info
7. Make file executable 
```
sudo chmod 755 system_info.py
```

8. Check if script works
```
python3 system_info.py
```

9. Autostart the script at boot  
```
sudo nano /etc/rc.local
```
10. Add the following line above 'exit 0'  
```
sudo python3 /home/pi/system_info/system_info.py &
```
