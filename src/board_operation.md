# Operation

The four rightmost pins on the header carry Vcc, GND, the 1W bus and
(optionally) a control line for 1W's strong pullup FET, more on this later. The
remaining 36 pins jumper individual devices to the 1Wire bus - each back-row pin
connects to its nearest column of interconnected through-hole points, and the
front-row pins all connect to the 1W bus connection pin. If I were building a
board from scratch I'd consider using a multiplex gate IC in place of the
jumpers, so automated tests could autonomously combine or isolate individual bus
nodes.

Here's the header diagrammed, looking at the box with the pins closest to you:

```
   20 19 18 17 16 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1
    o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o

    o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o  o
   21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40
```

| Pin | Assignment |
|-----|------------|
|   1 | VCC |
|   2 | Strong pull-up control |
|  39 | 1Wire bus |
| 40  | GND |

The remaining 36 pins are paired, 20-21, 19-22, 18-23 and so on, isolating a
corresponding column of through-hole points unless jumped (as shown for 18-23 in
the introduction picture). The columns connected are those with holes closest to the far edge
of the board in the picture, without connections.

The hard-soldered jumper wires serve to distribute alternating VCC and GND
through the remaining columns - so every three columns is a complete set of VCC,
1W and GND and devices can be packed in quite tightly. They're uninsulated
conductors, to be painted over with "liquid electrical tape" to protect things
from accidentally shorting if they get bumped out of place.


