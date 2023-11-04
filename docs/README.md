
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

I've labelled the keys ROW_COLUMN with rows (bottom to top) 0 to 5, and columns (left to right) A to U.

![Membrane Top](imgs/mem_top.jpg "Membrane Top")

Traces in the top membrane leave the membrane at around the `5Q` key area, to connect to the PCB. These traces leave in 2 "bunches", the left bundle contains 12 tracks, the right 7 tracks. All in 19 tracks, these are the "_columns_" in the keyboard matrix.

![Membrane Bottom](imgs/mem_bot.jpg "Membrane Bottom")

Traces in the bottom membrane also leave the membrane at around the `5Q` key area, to connect to the PCB. These traces leave in 2 "bunches", the left bundle contains 3 tracks, the right 7 tracks. All in 10 tracks, these are the "_rows_" in the keyboard matrix.

Hence, the size of the keyboard matrix is 10 x 19, requiring 29 connections to the PCB, via 3 x 10pin Kyocera 6232 connectors.
