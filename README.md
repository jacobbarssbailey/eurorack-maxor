# MaxOr

There are a number of commercial eurorack-format synthesizer modules available that will work as a logical OR function. While they do a fine job combining multiple gate/trigger signals, typically they work by passing each input through a diode, resulting in the output being the maximum input level minus the the voltage drop across the diodes. Fine for gates and triggers, not so fine for combining control voltages.

This module takes a similar approach to these passive modules, but exchanges the passive diodes for "ideal" diodes (i.e. an opamp and two diodes that conspire to behave like normal diodes, only with a magical 0V voltage drop). The result is a module that precisely combines multiple CVs, and outputs the maximum value from the set.

### Why would you want this?

@TODO

## Behavior

Each channel accepts three inputs, and the maximum (positive) voltage among them becomes the output. Some examples of what you should expect:

| Input A | Input B | Input C | Output |
| ------- | ------- | ------- | ------ |
|      0V |      0V |      1V |     1V |
|      1V |      3V |      2V |     3V |
|      5V |      0V |      5V |     5V |
|      5V |      8V |      5V |     8V |
|     -8V |     -3V |     -2V |     0V |

Note that this module does nothing for negative voltages; they are treated as if they were 0V. For this reason alone, I don't recommend using this module for audio signals.

I used TL074 opamps here, with fine results. You could probably get a wider range of acceptable voltages with a rail-to-rail opamp, but if you're seeing a lot of 11.5V signals floating around your synthesizer, you may have other issues to work around, no?


## Construction

This module was originally constructed to be milled from a single singled PCB. As such, I've favored hand-solderable surface mount components, to limit the amount of through-hole drilling.

Jacks are Erthenvar horizontal jacks.

Total module depth is about 1.7" (~44mm).