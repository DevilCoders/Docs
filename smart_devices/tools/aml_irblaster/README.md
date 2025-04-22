Description
===========

Utility for converting hex NEC IR command code into format recognized by Amlogic IR Blaster driver
(string with burst/space lengths).

Build
=====

Just do `ya make`

Usage
=====

1. First find NEC IR code. It can be obtained in the following way on Amlogic device with IR receiver (e.g. Saturn):
   
   * Enable debug in Amlogic IR remote driver: `echo 1 > /sys/class/remote/amremote/debug_enable`
   * Point remote control at IR receiver and press needed button
   * Check dmesg for NEC IR code: `grep -E 'framecode=0x[0-9a-f]{8}+'`

2. Use this tool to convert NEC IR code into Amlogic IR Blaster string. For example:

   `aml_irblaster 0xf708fb04`

3. Pass string to Amlogic IR Blaster driver:

   `echo 900s450s56s56s56s56s56s168s56s56s56s56s56s56s56s56s56s56s56s168s56s168s56s56s56s168s56s168s56s168s56s168s56s168s56s56s56s56s56s56s56s168s56s56s56s56s56s56s56s56s56s168s56s168s56s168s56s56s56s168s56s168s56s168s56s168s56s4050s >  /sys/class/meson-irblaster/irblaster1/send`
