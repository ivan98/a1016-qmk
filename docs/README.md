
# Apple Wireless Keyboard A1016

Apple Wireless Keyboard A1016 is the Bluetooth wireless variant of the [Apple Keyboard A1048](https://deskthority.net/wiki/Apple_A1048) from 2003 to 2007. Pick 1 up for S$5 in Aug 2023, a little dirty but working.

[![A1016 ISO](imgs/a1016_iso.jpg "A1016 ISO")](imgs/a1016_iso.jpg)

## PCB

The single PCB contains BCM2040 ([Product Brief](https://pdf.dzsc.com/88888/200673161938941.pdf)) controller and a SST39LF020 2Mbit flash.

[![PCB Top](imgs/pcb_0.jpg "PCB Top")](imgs/pcb_0.jpg)

On the left of the PCB, there are 2 x black and 1 x brown connectors to the keyboard membrane / matrix.

These 3 connectors are [Kyocera 6232 series](https://ele.kyocera.com/en/product/connector/fpcffc_connectors/6232/), 10 positions (ie, 10 pins), 1.0mm pitch, non-ZIF, SMT mounted, FPC (flexible printed circuits) / FFC (flexible flat cable).

The difference between black & brown is: black has top contacts, whereas brown has bottom contacts. The meaning of top/bottom is relative to the PCB: top means away from the PCB, bottom means nearest to the PCB.

[![PCB Bottom](imgs/pcb_1.jpg "PCB Bottom")](imgs/pcb_1.jpg)

## Membranes

There're 2 membranes, top and bottom, separated by a spacer membrane.

I've labelled the keys ROW_COLUMN with rows (bottom to top) `0` to `5`, and columns (left to right) `A` to `U`. Key `0A` at the bottom left, to key `5U` at the top right.

[![Membrane Top](imgs/mem_top.jpg "Membrane Top")](imgs/mem_top.jpg)

Traces in the top membrane leave the membrane at around the `5Q` key area, to connect to the PCB. These traces leave in 2 "bunches", the left bundle contains 12 tracks, the right 7 tracks. All in 19 tracks, these are the "_columns_" in the keyboard matrix.

[![Membrane Bottom](imgs/mem_bot.jpg "Membrane Bottom")](imgs/mem_bot.jpg)

The bottom membrane is "flipped", so Key `0A` is at the bottom right, and key `5U` is at the top left.

Traces in this bottom membrane also leave the membrane at around the `5Q` key area, to connect to the PCB. These traces leave in 2 "bunches", the left bundle contains 3 tracks, the right 7 tracks. All in 10 tracks, these are the "_rows_" in the keyboard matrix.

Hence, the size of the keyboard matrix is 10 x 19, requiring 29 connections to the PCB, via 3 x 10pin Kyocera 6232 connectors.

## Mapping

|  |  | A 1 (left) | B 2 | C 3 | D 4 | E 5 | F 6 | G 7 | H 8 | I 9 | J 10 | K 11 | L 12 | M 13 | N 14 | O 15 | P 16 | Q 17 | R 18 | S 19 (right)||
 | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
|Row| 9 (left) | KC_ESCAPE | KC_F1 | KC_F2 | KC_F3 | KC_F4 | KC_F5 | KC_UP | KC_RIGHT_CTRL | KC_RIGHT_SHIFT | KC_F16 | KC_NO | KC_NO | KC_F6 | KC_KP_4 | KC_KP_5 | KC_NO | KC_KP_6 | KC_KP_PLUS | KC_AUDIO_VOL_DOWN |
|Row| 8 | KC_GRAVE | KC_Z | KC_X | KC_C | KC_V | KC_B | KC_N | KC_NO | KC_NO | KC_F13 | KC_NO | KC_LCMD | KC_M | KC_COMMA | KC_DOT | KC_NO | KC_SLASH | KC_SPACE | KC_AUDIO_VOL_UP |
|Row| 7 | KC_F12 | KC_NO | KC_NO | KC_KP_DOT | KC_KP_0 | KC_LEFT | KC_DOWN | KC_NO | KC_NO | KC_END | KC_NO | KC_NO | KC_RIGHT | KC_KP_1 | KC_KP_2 | KC_RCMD | KC_KP_3 | KC_KP_ENTER | KC_AUDIO_MUTE |
|Row| 6 | KC_CAPS_LOCK | KC_A | KC_S | KC_D | KC_F | KC_G | KC_H | KC_NO | KC_NO | KC_DELETE | KC_LEFT_ALT | KC_NO | KC_J | KC_K | KC_L | KC_NO | KC_SEMICOLON | KC_QUOTE | KC_MEDIA_EJECT |
|Row| 5 | KC_ENTER | KC_F7 | KC_F8 | KC_EQUAL | KC_BACKSPACE | KC_NO | KC_HOME | KC_NO | KC_BACKSLASH | KC_F14 | KC_NO | KC_NO | KC_PAGE_UP | KC_NUM_LOCK | KC_KP_EQUAL | KC_NO | KC_KP_SLASH | KC_KP_ASTERISK | KC_NO |
|Row| 4 | KC_F9 | KC_F10 | KC_F11 | KC_RIGHT_BRACKET | KC_NO | KC_NO | KC_NO | KC_NO | KC_NO | KC_F15 | KC_RIGHT_ALT | KC_NO | KC_PAGE_DOWN | KC_KP_7 | KC_KP_8 | KC_NO | KC_KP_9 | KC_KP_MINUS | KC_NO |
|Row| 3 | KC_NO | KC_1 | KC_2 | KC_3 | KC_4 | KC_5 | KC_6 | KC_LEFT_CTRL | KC_NO | KC_NO | KC_NO | KC_NO | KC_7 | KC_8 | KC_9 | KC_NO | KC_0 | KC_MINUS | KC_NO |
|Row| 2 | KC_TAB | KC_Q | KC_W | KC_E | KC_R | KC_T | KC_Y | KC_NO | KC_LEFT_SHIFT | KC_NO | KC_NO | KC_NO | KC_U | KC_I | KC_O | KC_NO | KC_P | KC_LEFT_BRACKET | KC_NO |
|Row| 1 | This track is used for Keycaps LED |
|Row| 0 (right) | This track is used for Keycaps LED |

Given this mapping, 28 GPIO pins is needed on a MCU to control this keyboard. Ground for Keycaps LED can be taken from normal ground and GPIO is not needed.

## MCU

28 GPIO pins (available for use) is a relatively high number for MCUs compatible with QMK. 1 suitable candidate is the [RP2040](https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html).

Given its low cost, I've selected the RP2040 from [WeAct Studio](https://github.com/WeActStudio/WeActStudio.RP2040CoreBoard), Sep 2023.

|WeAct RP2040 Pin|Available for our use|Our use|WeAct RP2040 Function|
|--|--|--|--|
|GP0|Yes|Col 1|
|GP1|Yes|Col 2|
|GP2|Yes|Col 3|
|GP3|Yes|Col 4|
|GP4|Yes|Col 5|
|GP5|Yes|Col 6|
|GP6|Yes|Col 7|
|GP7|Yes|Col 8|
|GP8|Yes|Col 9|
|GP9|Yes|Col 10|
|GP10|Yes|Col 11|
|GP11|Yes|Col 12|
|GP12|Yes|Col 13|
|GP13|Yes|Col 14|
|GP14|Yes|Col 15|
|GP15|Yes|Col 16|
|GP16|Yes|Col 17|
|GP17|Yes|Col 18|
|GP18|Yes|Col 19|
|GP19|Yes|Row 9|
|GP20|Yes|Row 8|
|GP21|Yes|Row 7|
|GP22|Yes|Row 6|
|GP23|No||User Key Button|
|GP24|Yes|Keycaps LED|
|GP25|No||WeAct RP2040 LED|
|GP26|Yes|Row 5|
|GP27|Yes|Row 4|
|GP28|Yes|Row 3|
|GP29|Yes|Row 2|

## QMK

### config.h
```
#define LED_CAPS_LOCK_PIN GP24
#define LED_PIN_ON_STATE 1

#define RP2040_BOOTLOADER_DOUBLE_TAP_RESET
#define RP2040_BOOTLOADER_DOUBLE_TAP_RESET_LED GP25
#define RP2040_BOOTLOADER_DOUBLE_TAP_RESET_TIMEOUT 500U
```

### my_keyboard.h
```
#pragma once
#include "quantum.h"

#define LAYOUT( \
    k0A, k0B, k0C, k0D, k0E, k0F, k0M, k4B, k4C, k5A, k5B, k5C, k2A, k1J,     k4J,  k5J, k0J,     k0S, k1S, k2S, k3S, \
    k6A, k6B, k6C, k6D, k6E, k6F, k6G, k6M, k6N, k6O, k6Q, k6R, k4D, k4E,     k4F,  k4G, k4M,     k4N, k4O, k4Q, k4R, \
    k7A, k7B, k7C, k7D, k7E, k7F, k7G, k7M, k7N, k7O, k7Q, k7R, k5D, k4A,     k3J,  k2J, k5M,     k5N, k5O, k5Q, k5R, \
    k3A, k3B, k3C, k3D, k3E, k3F, k3G, k3M, k3N, k3O, k3Q, k3R, k4I,                              k0N, k0O, k0Q, k0R, \
    k7I, k1A, k1B, k1C, k1D, k1E, k1F, k1G, k1M, k1N, k1O, k1Q, k0I,                k0G,          k2N, k2O, k2Q, k2R, \
    k6H, k3K, k1L,            k1R,                    k2P, k5K, k0H,          k2F,  k2G, k2M,     k2E, k2D \
) { \
	  { k0A,  k0B,    k0C,    k0D,  k0E,    k0F,    k0G,    k0H,    k0I,    k0J,    KC_NO,  KC_NO,  k0M,  k0N,  k0O,  KC_NO,  k0Q,  k0R,  k0S   }, \
	  { k1A,  k1B,    k1C,    k1D,  k1E,    k1F,    k1G,    KC_NO,  KC_NO,  k1J,    KC_NO,  k1L,    k1M,  k1N,  k1O,  KC_NO,  k1Q,  k1R,  k1S   }, \
	  { k2A,  KC_NO,  KC_NO,  k2D,  k2E,    k2F,    k2G,    KC_NO,  KC_NO,  k2J,    KC_NO,  KC_NO,  k2M,  k2N,  k2O,  k2P,    k2Q,  k2R,  k2S   }, \
	  { k3A,  k3B,    k3C,    k3D,  k3E,    k3F,    k3G,    KC_NO,  KC_NO,  k3J,    k3K,    KC_NO,  k3M,  k3N,  k3O,  KC_NO,  k3Q,  k3R,  k3S   }, \
	  { k4A,  k4B,    k4C,    k4D,  k4E,    k4F,    k4G,    KC_NO,  k4I,    k4J,    KC_NO,  KC_NO,  k4M,  k4N,  k4O,  KC_NO,  k4Q,  k4R,  KC_NO }, \
	  { k5A,  k5B,    k5C,    k5D,  KC_NO,  KC_NO,  KC_NO,  KC_NO,  KC_NO,  k5J,    k5K,    KC_NO,  k5M,  k5N,  k5O,  KC_NO,  k5Q,  k5R,  KC_NO }, \
	  { k6A,  k6B,    k6C,    k6D,  k6E,    k6F,    k6G,    k6H,    KC_NO,  KC_NO,  KC_NO,  KC_NO,  k6M,  k6N,  k6O,  KC_NO,  k6Q,  k6R,  KC_NO }, \
	  { k7A,  k7B,    k7C,    k7D,  k7E,    k7F,    k7G,    KC_NO,  k7I,    KC_NO,  KC_NO,  KC_NO,  k7M,  k7N,  k7O,  KC_NO,  k7Q,  k7R,  KC_NO } \
}
```

### info.json
```json
{
    "manufacturer": "ivan98",
    "keyboard_name": "my_keyboard",
    "maintainer": "ivan98",
    "bootloader": "rp2040",
    "processor": "RP2040",
    "features": {
        "bootmagic": true,
        "command": false,
        "console": true,
        "extrakey": false,
        "mousekey": false,
        "nkro": true
    },
    "matrix_pins": {
        "cols": ["GP9", "GP8", "GP7", "GP6", "GP5", "GP4", "GP3", "GP2", "GP1", "GP0",
			"GP11", "GP10", "GP13", "GP12", "GP15", "GP14", "GP17", "GP16", "GP18"],
        "rows": ["GP20", "GP19", "GP22", "GP21", "GP27", "GP26", "GP29", "GP28"]
    },
    "diode_direction": "COL2ROW",
    "usb": {
        "device_version": "1.0.0",
        "pid": "0x0200",
        "vid": "0xFEED"
    },
    "layouts": {
        "LAYOUT": {
            "layout": [
                {"x":0, "y":0, "w":1.5}, {"x":1.5, "y":0}, {"x":2.5, "y":0}, {"x":3.5, "y":0}, {"x":4.5, "y":0}, {"x":5.5, "y":0}, {"x":6.5, "y":0}, {"x":7.5, "y":0}, {"x":8.5, "y":0}, {"x":9.5, "y":0}, {"x":10.5, "y":0}, {"x":11.5, "y":0}, {"x":12.5, "y":0}, {"x":13.5, "y":0, "w":1.5}, {"x":15.25, "y":0}, {"x":16.25, "y":0}, {"x":17.25, "y":0}, {"x":18.5, "y":0}, {"x":19.5, "y":0}, {"x":20.5, "y":0}, {"x":21.5, "y":0},
                {"x":0, "y":1}, {"x":1, "y":1}, {"x":2, "y":1}, {"x":3, "y":1}, {"x":4, "y":1}, {"x":5, "y":1}, {"x":6, "y":1}, {"x":7, "y":1}, {"x":8, "y":1}, {"x":9, "y":1}, {"x":10, "y":1}, {"x":11, "y":1}, {"x":12, "y":1}, {"x":13, "y":1, "w":2}, {"x":15.25, "y":1}, {"x":16.25, "y":1}, {"x":17.25, "y":1}, {"x":18.5, "y":1}, {"x":19.5, "y":1}, {"x":20.5, "y":1}, {"x":21.5, "y":1},
                {"x":0, "y":2, "w":1.5}, {"x":1.5, "y":2}, {"x":2.5, "y":2}, {"x":3.5, "y":2}, {"x":4.5, "y":2}, {"x":5.5, "y":2}, {"x":6.5, "y":2}, {"x":7.5, "y":2}, {"x":8.5, "y":2}, {"x":9.5, "y":2}, {"x":10.5, "y":2}, {"x":11.5, "y":2}, {"x":12.5, "y":2}, {"x":13.75, "y":2, "w":1.25, "h":2}, {"x":15.25, "y":2}, {"x":16.25, "y":2}, {"x":17.25, "y":2}, {"x":18.5, "y":2}, {"x":19.5, "y":2}, {"x":20.5, "y":2}, {"x":21.5, "y":2},
                {"x":0, "y":3, "w":1.75}, {"x":1.75, "y":3}, {"x":2.75, "y":3}, {"x":3.75, "y":3}, {"x":4.75, "y":3}, {"x":5.75, "y":3}, {"x":6.75, "y":3}, {"x":7.75, "y":3}, {"x":8.75, "y":3}, {"x":9.75, "y":3}, {"x":10.75, "y":3}, {"x":11.75, "y":3}, {"x":12.75, "y":3}, {"x":18.5, "y":3}, {"x":19.5, "y":3}, {"x":20.5, "y":3}, {"x":21.5, "y":3},
                {"x":0, "y":4, "w":1.25}, {"x":1.25, "y":4}, {"x":2.25, "y":4}, {"x":3.25, "y":4}, {"x":4.25, "y":4}, {"x":5.25, "y":4}, {"x":6.25, "y":4}, {"x":7.25, "y":4}, {"x":8.25, "y":4}, {"x":9.25, "y":4}, {"x":10.25, "y":4}, {"x":11.25, "y":4}, {"x":12.25, "y":4, "w":2.75}, {"x":16.25, "y":4}, {"x":18.5, "y":4}, {"x":19.5, "y":4}, {"x":20.5, "y":4}, {"x":21.5, "y":4, "h":2},
                {"x":0, "y":5, "w":1.5}, {"x":1.5, "y":5, "w":1.25}, {"x":2.75, "y":5, "w":1.5}, {"x":4.25, "y":5, "w":6.5}, {"x":10.75, "y":5, "w":1.5}, {"x":12.25, "y":5, "w":1.25}, {"x":13.5, "y":5, "w":1.5}, {"x":15.25, "y":5}, {"x":16.25, "y":5}, {"x":17.25, "y":5}, {"x":18.5, "y":5, "w":2}, {"x":20.5, "y":5}
            ]
        }
    }
}
```

### keymaps/default/keymap.c
```
#include QMK_KEYBOARD_H

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    /*
     * ┌─────┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬─────┐ ┌───┬───┬───┐ ┌───┬───┬───┬───┐
     * │Esc  │F1 │F2 │F3 │F4 │F5 │F6 │F7 │F8 │F9 │F10│F11│F12│ F13 │ │PSc│Scr│Pse│ │VDn│VUp│VMu│Eja│
     * ├───┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─────┤ ├───┼───┼───┤ ├───┼───┼───┼───┤
     * │ ` │ 1 │ 2 │ 3 │ 4 │ 5 │ 6 │ 7 │ 8 │ 9 │ 0 │ - │ = │ Backsp│ │Ins│Hom│PgU│ │Clr│ = │ / │ * │
     * ├───┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─────┤ ├───┼───┼───┤ ├───┼───┼───┼───┤
     * │ Tab │ Q │ W │ E │ R │ T │ Y │ U │ I │ O │ P │ [ │ ] │     │ │Del│End│PgD│ │ 7 │ 8 │ 9 │ - │
     * ├─────┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┬──┴┐ Ent│ └───┴───┴───┘ ├───┼───┼───┤───┤
     * │ Caps │ A │ S │ D │ F │ G │ H │ J │ K │ L │ ; │ ' │ \ │    │               │ 4 │ 5 │ 6 │ + │
     * ├────┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴─┬─┴───┴────┤     ┌───┐     ├───┼───┼───┼───┤
     * │Shft│ ` │ Z │ X │ C │ V │ B │ N │ M │ , │ . │ / │    Shift │     │ ↑ │     │ 1 │ 2 │ 3 │   │
     * ├────┴┬──┴─┬─┴───┼───┴───┴───┴───┴───┴───┴─┬─┴───┼────┬─────┤ ┌───┼───┼───┐ ├───┴───┼───┤Ent│
     * │Ctrl │Alt │Cmd  │                         │  Cmd│ Alt│ Ctrl│ │ ← │ ↓ │ → │ │   0   │ . │   │
     * └─────┴────┴─────┴─────────────────────────┴─────┴────┴─────┘ └───┴───┴───┘ └───────┴───┴───┘
     */
    [0] = LAYOUT(
        KC_ESC,  KC_F1,   KC_F2,   KC_F3, KC_F4, KC_F5, KC_F6, KC_F7,  KC_F8, KC_F9,   KC_F10,  KC_F11,  KC_F12,  KC_F13,     KC_F14, KC_F15,  KC_F16,     KC_KB_VOLUME_DOWN,KC_KB_VOLUME_UP,KC_KB_MUTE,KC_MEDIA_EJECT,
        KC_NUBS, KC_1,    KC_2,    KC_3,  KC_4,  KC_5,  KC_6,  KC_7,   KC_8,  KC_9,    KC_0,    KC_MINS, KC_EQL,  KC_BSPC,    KC_INS, KC_HOME, KC_PGUP,    KC_NUM,  KC_PEQL, KC_PSLS, KC_PAST,
        KC_TAB,  KC_Q,    KC_W,    KC_E,  KC_R,  KC_T,  KC_Y,  KC_U,   KC_I,  KC_O,    KC_P,    KC_LBRC, KC_RBRC, KC_ENT,     KC_DEL, KC_END,  KC_PGDN,    KC_P7,   KC_P8,   KC_P9,   KC_PMNS,
        KC_CAPS, KC_A,    KC_S,    KC_D,  KC_F,  KC_G,  KC_H,  KC_J,   KC_K,  KC_L,    KC_SCLN, KC_QUOT, KC_NUHS,                                          KC_P4,   KC_P5,   KC_P6,   KC_PPLS,
        KC_LSFT, KC_GRV,  KC_Z,    KC_X,  KC_C,  KC_V,  KC_B,  KC_N,   KC_M,  KC_COMM, KC_DOT,  KC_SLSH,      KC_RSFT,                 KC_UP,              KC_P1,   KC_P2,   KC_P3,   KC_PENT,
        KC_LCTL, KC_LALT, KC_LCMD,                                 KC_SPC,                    KC_RCMD,  KC_RALT,  KC_RCTL,    KC_LEFT, KC_DOWN, KC_RGHT,        KC_P0,       KC_PDOT
    )
};
```
