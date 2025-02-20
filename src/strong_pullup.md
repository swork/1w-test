# Strong pull-up

1Wire is an open-drain bus: nodes and the master keep their single bus I/O pin
in a high-impedance state when idle or reading the line, and short it to ground
to effect signalling. A pull-up resistor keeps the line voltage high when no
device is driving it low.

And yes, a ground return line is required; so calling
it "one wire" brings to mind [a recent NYT crossword
puzzle](https://www.nytimes.com/2025/02/19/crosswords/daily-puzzle-2025-02-20.html).

## Parasite power

Some non-master devices can be "parasite powered", where the signal line's high-state
voltage supplies enough power to an embedded capacitor to keep the device
functioning during bus low-state moments. This at least keeps the system from
being off by two, as many installations are, carrying a third power wire around
the bus along with the signal and ground wires.

But sadly those capacitors aren't reasonably made big enough to carry such
devices through more power-intensive operations, like updating an internal
configuration EEPROM, processing a temperature reading (temperature sensors make
up the bulk of 1W's market niche), and so on, while charged through a pull-up
resistor sized to keep from blowing the power-dissipation abilities of each
node's signal drain circuit. For these operations the 1W spec calls for the bus
to remain idle (high voltage) for a period of time during which Yet Another
Signal at the master[^note]  switches a power FET onto the signal line to
drive it high with authority, while the device or devices needing power draw it.

Pin 39 of my test box gates a tiny FET between Vcc and the 1W bus, accomplishing
this task if configured. As shown this FET isn't wired or populated yet. I
suppose I'll need a little resistor to pull this pin to ground if it's left
floating, as I expect it will be when testing software that doesn't implement
the strong pullup function.

[^note]: So now we're what, a four-wire bus? No, this strong-pullup signal
doesn't go around the bus like the other two or three wires do, it simply
arranges that a transistor actively bonds the signal wire to Vcc for a moment,
rather than just pulled to the Vcc voltage through a passive resistor. Without
this bonding, devices drawing significant current will pull the signal wire
voltage low - maybe too low for the device to continue to operate, and maybe low
enough to make some other device on the bus think it's being signaled by a
falling edge.

