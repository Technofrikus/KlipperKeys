# Klipper Keys

__For pictures etc see: https://www.printables.com/model/539404-klipper-keys-keyboard-for-3030-and-2020-profiles__

This “keyboard” with 5 keys gets conneted directly to the GPIOs of the RasbperryPi. This way no MCU or anything fancy is needed. The case is tested on a vCore 3.1 400mm with 3030 profiles. Not sure about clearance on other printers. But electrically should also work for Vorons etc.

For me light switching during printing is not super reliable. Not sure why. Everything else works great.

The PCB is OpenSource and all files, including production files, can be found here:

https://github.com/Technofrikus/KlipperKeys

You need:

## BOM:

### Printing
1x Case
1x Baseplate (choose which profile size you need)
1x PCB

### Cable
6-wire cable in your needed length
both ends crimped with Dupont connectors (standard 2.54mm pitch)

### Hardware
1x 6-pin-header
4x M3 threaded insert (5,7mm length or shorter work)
4x M3x10 screw

#### For 2020 profile
2x M3x8/10
2x hammer nut
Can also use bigger screws (not longer), just have to increase the size of the hole a little with a knife.

#### For 3030 profile
2x M5/6x12
2x hammer nut with the same thread size
5x MX-compatible switches and keycaps
Try these printable relegendable keycaps I used with some tips for printing: https://www.thingiverse.com/make:912979
 

### Connecting

The Pins are named on the PCB. Also check the picture for the marked pins. Reference: https://pinout.xyz
Configuration

Then add these settings to your macro-file. I have a user-macro-cfg which I included from printer.cfg to have these things separate. But you can also put it directly in the printer.cfg
These gcodes are custom to my setup (lights) and RatOS (unload_filament). Please change these to your liking and printer setup.
```
[gcode_button button_light]
pin: ~rpi:gpio17
press_gcode: CASE_LIGHTS_TOGGLE

[gcode_button button_load]
pin: ~rpi:gpio9
press_gcode: LOAD_FILAMENT

[gcode_button button_unload]
pin: ~rpi:gpio10
press_gcode: UNLOAD_FILAMENT

[gcode_button button_PLATemp]
pin: ~rpi:gpio22
press_gcode:
 SET_HEATER_TEMPERATURE HEATER=extruder TARGET=200
 SET_HEATER_TEMPERATURE HEATER=heater_bed TARGET=60

[gcode_button button_cooldown]
pin: ~rpi:gpio27
press_gcode:
 TURN_OFF_HEATERS
```
 

If you want to use a Button as an Emergency-Stop, use this code:
```
[gcode_button ESTOP_BUTTON]
pin: ...
press_gcode:  
   {action_emergency_stop("Impending Doom Averted!")}
```
I have not tested this, but ThaoChan provided it and it works for him. Thanks again Thao for your help with the Config! Check it out here: https://www.reddit.com/r/klippers/comments/ssj67j/comment/ju6ld9p/?utm_source=reddit&utm_medium=web2x&context=3 
