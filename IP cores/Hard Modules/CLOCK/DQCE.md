Dynamic Quadrant Clock Enable
=============================

**DQCE** allows internal logic to dynamically enable or disable a clock. When a
clock network is disabled, all the logic fed by that clock does not toggle,
hence reducing power consumption.

A simplified illustration of the DQCE internal logic is shown below:

```
         +-----------------------------+
         |                             |
         |     +--------+              |
         |     |        |              |
   CE -->+-----+ D      |              |
         |     |        |              |
         |     |      Q +--+           |
         |     |        |  |           |
         |  +--+>Clk    |  |           |
         |  |  |        |  |  +-----+  |
         |  |  +--------+  +--+     |  |
         |  |                 | AND +--+--> Clkout
Clkin -->+--+-----------------+     |  |
         |                    +-----+  |
         |                             |
         +-----------------------------+
```

Ports
-----

- **CE**: Clock enable input, active high.
- **Clkin**: Clock input.
- **Clkout**: Clock output.

Usage
-----

To enable clock output from the DQCE module, set the CE input to high;
otherwise set it to low.

It takes effect when clock input meets **falling edges**.

Limitations
-----------

For LittleBee®(小蜜蜂®) (1K, 2K, 4K) family FPGAs, there are 6 global clocks with
DQCE (GCLK0~GCLK5) per each of the two quadrants, hence the total number of DQCE
is 12.

For LittleBee®(小蜜蜂®) (9K) and Arora(晨熙®) family FPGAs, there are 6 global
clocks with DQCE (GCLK0~GCLK5) per each of the four quadrants, hence the total
number of DQCE is 24.

Some other IP cores may consume DQCEs. Please refer to the IP core's
documentation, and check the *Place & Route Report*.

Additional Information
----------------------

It was mentioned, in [1], that DQCE can be configured to be disabled and primary
clock (PCLK) network will be always enabled. It seems we could not find any
texts about this in any documents. 

However, Dynamic Clock Control (DCCA) of Lattice FPGA is something similar to
DQCE. Maybe we can have a glance at Lattice documentation TN1263.

Reference
---------

[1] [UG286](http://cdn.gowinsemi.com.cn/UG286.pdf), 
    [E](http://cdn.gowinsemi.com.cn/UG286E.pdf).

[2] [DS976](http://cdn.gowinsemi.com.cn/DS976.pdf),
    [E](http://cdn.gowinsemi.com.cn/DS976E.pdf), illustration of DQCE concept.
