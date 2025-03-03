# Populating the bus

One-wire devices are individually laser-inscribed with a purportedly unique "ROM code" that serves as a bus address. It's presented on the wire as an eight bit family code, six bytes of address, and eight more bits of CRC.

The family code seems to map to differences in protocol details and to support of distinguishing features. For example, my read of the data sheet for the MAX30207, family code 0x54, suggests the device doesn't start converting analog temperature to a digital output value until the host reads a 16-bit CRC the device sends after receiving the 0x44 CONVERT TEMPERATURE command. Every other device I've looked at begins converting the temperature immediately.

Motivated in part by this seeming oddness, I wanted representatives of as many 1W "families" as reasonably possible, to test drivers for various functions of each. The things are cheap, but I didn't pay enough attention to the packaging specs when ordering about eight of them and ended up with two bare chips so small I lost them while peeling open their tape/reel carriers. They're somewhere near my workbench, likely embedded in the wood flooring by the wheels on my sitting stool.

One of the tiny packages I successfully got soldered to copper whiskers and then encased in a drop of epoxy for strain relief. Three more (less microscopic) I matched up to SM prototype boards I had on hand. I used heavy wires for ground and a no-connect intertie to give these some structure. Two were in through-hole packages, so I could solder them onto the test harness directly.

Adjacent parts are crammed in tight, so I used a conformal coating -ish Liquid Electrical Tape goop on some of the conductive bits to reduce the likelihood of shorts. The same stuff can (barely) be seen here covering the bus weaves I did in the base board.

![Population in progress](images/assembly.jpg)

Here are the devices as populated, by jumper position (left to right with the pins closest to you):

| Position | Device | Family |
| -------- | ------ | ------ |
|  20-21   | DS28EA00 |  42h  |
|  19-22   | TMP1826 | 26h |
|  18-23   | DS1822Z | 22h |
|  17-24   | 
|  16-25   | 
|  15-26   | 

