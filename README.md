# MaxOr

There are a number of commercial eurorack-format synthesizer modules available that will work as a logical OR function. While they do a fine job combining multiple gate/trigger signals, typically they work by passing each input through a diode, resulting in the output being the maximum input level minus the the voltage drop across the diodes. Fine for gates and triggers, not so fine for combining control voltages.

This module takes a similar approach to these passive modules, but exchanges the passive diodes for "ideal" diodes (i.e. an opamp and two diodes that conspire to behave like normal diodes, only with a magical 0V voltage drop). The result is a module that precisely combines multiple CVs, and outputs the maximum value from the set.

### Why would you want this?

* Combine several envelopes in a new way
* Combine gate / trigger signals without losing 1V-2V in the process
* Use a constant voltage source to set a lower bound on another CV
* Something else!

## Behavior

Each channel accepts three inputs, and the maximum (positive) voltage among them becomes the output. Some examples of what you should expect:

| Input A | Input B | Input C | Output |
| ------- | ------- | ------- | ------ |
|      0V |      0V |      1V |     1V |
|      1V |      3V |      2V |     3V |
|      5V |      0V |      5V |     5V |
|      5V |      8V |      5V |     8V |
|     -5V |     -8V |      0V |     0V |
|     -8V |     -3V |     -2V |     0V |

Note that this module does nothing for negative voltages; they are treated as if they were 0V. For this reason alone, I don't recommend using this module for audio signals.


## Construction

This module is designed to be milled from a single singled PCB, on an Othermill, though it should also be relatively easy to etch by hand. As such, I've favored hand-solderable surface mount components, to limit the amount of through-hole drilling, and kept all trace gaps to no less than 1/64". The board design could probably be better optimized, before being sent to a commercial board manufacturer, but for home milling, it works quite well.

Jacks are Erthenvar horizontal jacks. At time of writing, they come in packs of 50, and have nice heavy solder tabs.

Pads for protection diodes are included, but to use these, you'll need to cut /remove the traces across them. I included them and then didn't bother with them, in favor of a keyed power connector.

There are no extra power smoothing capacitors on this module, just some 100nF decoupling capacitors around the op amps. If your power distribution board doesn't already contain a few 100µF capacitors nearby, you might find this module oscillating.

Total module depth is about 1.7" (~44mm).
