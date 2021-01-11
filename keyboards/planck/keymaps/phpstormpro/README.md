# PhpStormPro

![Planck keyboard](https://raw.githubusercontent.com/BeckTimothy/MyPlanckFirmware/master/img/planck.jpg)
---
If you'd like to get started developing your own keyboard firmware check out the [QMK documentation](https://docs.qmk.fm/#/newbs_getting_started).

__Keymap Maintainer:__ [Timothy Beck](https://github.com/BeckTimothy)     
__Hardware Supported:__ Planck PCB w/ STM32F303CB cortex-M4  128Kb       
    _(this was designed for planck rev6 but should work with any planck with enough flash mem.. all of them?)_    
__Firmware Size:__ 58,764 bytes of 128,000 bytes available     
__Hardware Availability:__ [OLKB.com](https://olkb.com), [Massdrop](https://www.massdrop.com/buy/planck-mechanical-keyboard?mode=guest_open), [Ergodox (Planck EZ)](https://ergodox-ez.com/pages/planck)

---


This keymap firmware is developed by [Timothy Beck,](https://github.com/BeckTimothy) for the Plank 40% keyboard, for on-the-go Web development within the PhpStorm IDE. I prefer to have my symbols on my home row and I use curly braces more than square brackets so I'm swapping their shifted state as well as adding useful niche macros for templating projects. I've also swapped the debounce mode to per-key to allow less chance of a kind of 'blocking' under rare circumstances when two keys are pressed within 5ms of each other and increased the polling rate to 1000 tps instead of the default 125 preventing another type of rare 'blocking' when keys are pressed within 8ms of each other, blech.

To flash my firmware onto your device you can:
- make sure your qmk_firmware directory is up to date, 
- make sure to read the QMK CLI docs,
- then run `qmk compile -kb planck/rev6 -km phpstormpro`

To preview my firmware layout use the provided json on the [qmk configurator](https://config.qmk.fm/#/planck/rev6/LAYOUT_planck_grid), or view the [keymap.c here,](//keymap.c) or look at the images below.

## Layer 0 
is a standard QWERTY layout. The Raise and Lower keys shift layers to layer 4 and 3, respectively.

![Planck keyboard layer 0](https://raw.githubusercontent.com/BeckTimothy/MyPlanckFirmware/master/img/planckLayer0.PNG)

## Layers 1 and 2 
are Colemak and Dvorak, alternative layouts to QWERTY. You can swap your default layer between layers 0, 1, and 2 on layer 6.

## Layer 3
contains F-keys in the lower left and a num pad on the right, I'm working on adding PHP Class and API boilerplating scripts to the top row.

![Planck keyboard layer 3](https://raw.githubusercontent.com/BeckTimothy/MyPlanckFirmware/master/img/planckLayer3.PNG)

## Layer 4
contains a num row with shiftable symbols along the top row. Home row contains my most used symbols for development, and a reverse shifted curly/square bracket key as I use curly far more often than square brackets.

![Planck keyboard layer 4](https://raw.githubusercontent.com/BeckTimothy/MyPlanckFirmware/master/img/planckLayer4.PNG)

Example of reverse shifted curly/square brace macro:
```$xslt 
case RV_LBRC:
    	  if (record->event.pressed) {
    	    if (get_mods() & MOD_MASK_SHIFT) { // act as left square bracket if shift is pressed
    	        del_mods(MOD_MASK_SHIFT);
    	        register_code(KC_LBRACKET);
    	        unregister_code(KC_LBRACKET);
    	        register_code(KC_LSFT); //This works because all shift keys on Planck are programmed to be left shift
             } else { // otherwise act as left curly brace
               register_code16(KC_LEFT_CURLY_BRACE);
               unregister_code16(KC_LEFT_CURLY_BRACE);
             }
         }
         return false;
         break;
```

## Layer 5
is Plover layout, a layout for stenographers. I have no intention of using this or changing it as I haven't needed it yet.

## Layer 6
contains qmk specific scripts that modify hardware features. This is for the most part unchanged from the rev6 firmware with the exception of the added F-keys along the border of the keymap, this aren't mod friendly, mod friendly F-keys van be found in layer 3.

![Planck keyboard layer 6](https://raw.githubusercontent.com/BeckTimothy/MyPlanckFirmware/master/img/planckLayer6.PNG)


