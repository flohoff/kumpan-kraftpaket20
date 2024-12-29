JTAG
====

OpenOCD config
--------------

Meine OpenOCD config mit einem Busblaster JTAG Interface:

    source [find interface/ftdi/dp_busblaster.cfg]

    set CHIPNAME tm4c123gh6pm
    source [find target/stellaris.cfg]


RTT Data channel
----------------

Meine aktuelle Kraftpaket 2.0 Firmware enthält noch Debug Code für eine JTAG
RTT data exchange.

Um das mit OpenOCD oder gdb zu aktivieren:

    rtt setup 0x20006C00 100 "SEGGER RTT"
    rtt start
    rtt channels
    rtt server start 9090 0

Hier der identifier im RAM:

	(gdb) xxd 0x20006c00 0x70
	20006c00: 5345 4747 4552 2052 5454 0000 0000 0000  SEGGER RTT......
	20006c10: 0300 0000 0300 0000 9ccc 0000 0852 0020  .............R. 
	20006c20: 0004 0000 0d00 0000 0000 0000 0000 0000  ................
	20006c30: 0000 0000 0000 0000 0000 0000 0000 0000  ................
	20006c40: 0000 0000 0000 0000 0000 0000 0000 0000  ................
	20006c50: 0000 0000 0000 0000 0000 0000 0000 0000  ................
	20006c60: 9ccc 0000 f063 0020 1000 0000 0000 0000  .....c. ........

