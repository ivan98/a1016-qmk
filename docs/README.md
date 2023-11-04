
# Apple Wireless Keyboard A1016

Apple Wireless Keyboard A1016 is the Bluetooth wireless variant of the [Apple Keyboard A1048](https://deskthority.net/wiki/Apple_A1048) from 2003 to 2007.

![A1016 ISO](imgs/a1016_iso.jpg "A1016 ISO")

## PCB

The single PCB contains BCM2040 ([Product Brief](https://pdf.dzsc.com/88888/200673161938941.pdf)) controller and a SST39LF020 2Mbit flash.

![PCB Top](imgs/pcb_0.jpg "PCB Top")

On the left of the PCB, there are 2 x black and 1 x brown connectors to the keyboard membrane / matrix.

These 3 connectors are [Kyocera 6232 series](https://ele.kyocera.com/en/product/connector/fpcffc_connectors/6232/), 10 positions (ie, 10 pins), 1.0mm pitch, non-ZIF, SMT mounted, FPC (flexible printed circuits) / FFC (flexible flat cable).

The difference between black & brown is: black has top contacts, whereas brown has bottom contacts. The meaning of top/bottom is relative to the PCB: top means away from the PCB, bottom means nearest to the PCB.

![PCB Bottom](imgs/pcb_1.jpg "PCB Bottom")

## Membranes

There're 2 membranes, top and bottom, separated by a spacer membrane.

I've labelled the keys ROW_COLUMN with rows (bottom to top) 0 to 5, and columns (left to right) A to U.

![Membrane Top](imgs/mem_top.jpg "Membrane Top")

Traces in the top membrane leave the membrane at around the `5Q` key area, to connect to the PCB. These traces leave in 2 "bunches", the left bundle contains 12 tracks, the right 7 tracks. All in 19 tracks, these are the "_columns_" in the keyboard matrix.

![Membrane Bottom](imgs/mem_bot.jpg "Membrane Bottom")

Traces in the bottom membrane also leave the membrane at around the `5Q` key area, to connect to the PCB. These traces leave in 2 "bunches", the left bundle contains 3 tracks, the right 7 tracks. All in 10 tracks, these are the "_rows_" in the keyboard matrix.

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
