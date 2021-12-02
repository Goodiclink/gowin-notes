Phase-Lock Loop
===============

**rPLL** acts as a normal phase lock loop, providing frequency control, phase
control, and duty cycle adjustment, driven by a reference clock. (See
[note 1](#Notes).)

rPLL is a substitute for the original PLL module that is deprecated.

Ports
-----

- **CLKIN**: Reference clock input.
- **CLKFB**: Feedback clock input.
- **CLKOUT**: Output clock.
- **CLKOUTP**: Output clock, after phase and duty cycle adjustment.
- **CLKOUTD**: Output clock, of lower frequency.
- **CLKOUTD3**: Output clock, used where CLKOUT(P)-divided-by-3 is required.
- **LOCK**: Lock status output, active high.
- **RESET**: Asynchronous reset input, active high.
- **RESET_P**: Power down reset input, active high. ALL CLKOUT* pins are pulled
  low if bypass mode not configured.
- **FBDSEL**: Feedback clock divider factor dynamic input. 6-bit input. (See
  [note 2](#Notes).)
- **IDSEL**: Input clock divider factor dynamic input. 6-bit input. (See
  [note 2](#Notes).)
- **ODSEL**: Output clock divider factor dynamic input. 6-bit input. Alowable
  divisor values are 2, 4, 8, 16, 32, 48, 64, 80, 96, 112, 128. (See
  [note 3](#Notes).)
- **DUTYDA**: Duty cycle adjustment dynamic input. 4-bit input. (See
  [note 4](#Notes).)
- **PSDA**: Phase adjustment dynamic input. 4-bit input. (See [note 5](#Notes).)
- **FDLY**: Fine clock delay adjustment dynamic input. 4-bit input. (See
  [note 6](#Notes).)

Parameters
----------

Values of **Bold face** are default values.

|  Parameter       |  Value                     |  Description                                                                   |
|------------------|----------------------------|--------------------------------------------------------------------------------|
| FCLKIN           | "3"~"500"; **"100"**       | Reference clock input frequency.                                               |
| CLKFB_SEL        | **"internal"**, "external" | Feedback clock input selection. (Check rPLL logic for further information.)    |
| IDIV_SEL         | **0**~63                   | Input clock divider factor static input. (See [note 2](#Notes).)               |
| DYN_IDIV_SEL     | "true", **"false"**        | Input clock divider dynamic/static select. "true"for dynamic.                  |
| FBDIV_SEL        | **0**~63                   | Feedback clock divider factor static input. (See [note 2](#Notes).)            |
| DYN_FBDIV_SEL    | "true", **"false"**        | Feedback clock divider dynamic/static select."true" for dynamic.               |
| ODIV_SEL         | 2, 4, **8**, 16, 32, 48, 64, 80, 96, 112, 128 | Output clock divider factorstatic input.                    |
| DYN_ODIV_SEL     | "true", **"false"**        | Output clock divider dynamic/static select. "true"for dynamic.                 |
| DYN_SDIV_SEL     | **2**~128 (even numbers)   | CLKOUTD clock divider static input.                                            |
| DUTYDA_SEL       | **"0000"**~"1110"          | Duty cycle static adjustment input. (See [note 4](#Notes).)                    |
| PSDA_SEL         | **"0000"**~"1111"          | Phase static adjustment input. (See [note 5](#Notes).)                         |
| DYN_DA_EN        | "true", **"false"**        | Duty and phase dynamic/static select. "true" fordynamic.                       |
| CLKOUT_FT_DIR    | **1'b1**                   | Output clock (CLKOUT) frequency tuning direction. (Decreaseonly)               |
| CLKOUT_DLY_STEP  | **0**, 1, 2, 4             | Output clock (CLKOUT) delay factor = CLKOUT_DLY_STEP *delay. (delay = 50 ps)   |
| CLKOUTP_FT_DIR   | **1'b1**                   | Output clock (CLKOUTP) frequency tuning direction. (Decreaseonly)              |
| CLKOUTP_DLY_STEP | **0**, 1, 2                | Output clock (CLKOUTP) delay factor = CLKOUTP_DLY_STEP *delay. (delay = 50 ps) |
| CLKOUTD_SRC      | **"CLKOUT"**, "CLKOUTP"    | Output clock (CLKOUTD) source select.                                          |
| CLKOUTD3_SRC     | **"CLKOUT"**, "CLKOUTP"    | Output clock (CLKOUTD3) source select.                                         |
| CLKOUT_BYPASS    | "true", **"false"**        | Output clock (CLKOUT) bypass mode select.                                      |
| CLKOUTP_BYPASS   | "true", **"false"**        | Output clock (CLKOUTP) bypass mode select.                                     |
| CLKOUTD_BYPASS   | "true", **"false"**        | Output clock (CLKOUTD) bypass mode select.                                     |
| DEVICE           | "GW1N-1", "GW1NR-1", "GW1N-1S", "GW1NZ-1", "GW1NS-2", "GW1NS-2C", "GW1NSR-2", "GW1NSR-2C", "GW1NSE-2C", **"GW1N-4"**, "GW1N-4B", "GW1NR-4", "GW1NR-4B", "GW1NRF-4B", "GW1N-9", "GW1N-9C", "GW1NR-9", "GW1NR-9C", "GW2A-18", "GW2AR-18", "GW2A-55", "GW2A-55C", "GW2AN-55C"  | Device select. |


IP Core Customization Dialog
----------------------------

The dialog allows user to customize all parameters of IP core. Detailed
explanation of each parameter can be found in the table above.

### General Group Box

Select "General Mode" or "Advanced Mode" to enable the different options.
Simply use "General Mode" to easily configure the output frequency and phase
adjustment.

"PLL Phase And Duty Cycle Adjustment" only affects "CLKOUTP".

Check "PLL Reset" and/or "PLL Power Down Reset" to enable one or both of these
input ports.

Check "Enable LOCK" at the bottom of the dialog to enable the LOCK output.

### General Mode

In general mode, all divide factor settings are automatically calculated based
on your input clock frequency and expected output clock frequency. Set these two
value and click "Calculate" to generate settings. If CLKOUTD is enabled,
remember to set its expected frequency then calculate again.

A warning dialog will pop up if the calculated settings are not satisfied the
frequency and the tolerance requirement. Adjust these settings then calculate
again.

### Advanced Mode

Advanced mode allows you to manually set the divide factor settings. You can
choose "Dynamic" or "Static" divide factor of each divider. Click "Calculate"
and get the actual output frequency of CLKOUT and CLKOUTD (if enabled).

A warning dialog will pop up if some of the settings are illegal. Set the values
to the recommended ones then calculate again.

Internal Logic
--------------

An illustration of the PLL logic can be found in [2].

Notes
-----

1. GoWin has never explained the meaning of "r" in "rPLL".
2. The actural divisor value is 64-*xxx*SEL. 
3. The raw input values to divisor values are shown below:

   | Raw       | Divisor |
   |-----------|---------|
   | 6'b111111 | 2       |
   | 6'b111110 | 4       |
   | 6'b111100 | 8       |
   | 6'b111000 | 16      |
   | 6'b110000 | 32      |
   | 6'b101000 | 48      |
   | 6'b100000 | 64      |
   | 6'b011000 | 80      |
   | 6'b010000 | 96      |
   | 6'b001000 | 112     |
   | 6'b000000 | 128     |

4. The raw input values to duty cycle adjustment values are shown below:

   | Raw       | Duty Cycle (/16) |
   |-----------|------------------|
   | 4'b0010   | 2                |
   | 4'b0011   | 3                |
   | 4'b0100   | 4                |
   | 4'b0101   | 5                |
   | 4'b0110   | 6                |
   | 4'b0111   | 7                |
   | 4'b1000   | 8                |
   | 4'b1001   | 9                |
   | 4'b1010   | 10               |
   | 4'b1011   | 11               |
   | 4'b1100   | 12               |
   | 4'b1101   | 13               |
   | 4'b1110   | 14               |

   It must be pointed out that the actual duty cycle is also related to the
   phase adjustment value. The calculation is shown below:

   Duty cycle = ( (DUTYDA > PSDA ? 0 : 16) + DUTYDA - PSDA ) / 16 

5. The raw input values to phase adjustment values are shown below:

   | Raw     | Phase  |
   |---------|--------|
   | 4'b0000 | 0°     |
   | 4'b0001 | 22.5°  |
   | 4'b0010 | 45°    |
   | 4'b0011 | 67.5°  |
   | 4'b0100 | 90°    |
   | 4'b0101 | 112.5° |
   | 4'b0110 | 135°   |
   | 4'b0111 | 157.5° |
   | 4'b1000 | 180°   |
   | 4'b1001 | 202.5° |
   | 4'b1010 | 225°   |
   | 4'b1011 | 247.5° |
   | 4'b1100 | 270°   |
   | 4'b1101 | 292.5° |
   | 4'b1110 | 315°   |
   | 4'b1111 | 337.5° |

6. Fine delay value is the number of delay steps while each step delays
    0.125 ns. The raw input values to fine delay adjustment values are shown
    below:

   | Raw (GW1n-1/GW1N-1S) | Raw (other devices) | Fine delay steps |
   |----------------------|---------------------|------------------|
   | 4'b0000              | 4'b1111             | 0                |
   | 4'b0001              | 4'b1110             | 1                |
   | 4'b0010              | 4'b1101             | 2                |
   | 4'b0100              | 4'b1011             | 4                |
   | 4'b1000              | 4'b0111             | 8                |

References
----------

[1] [UG286](http://cdn.gowinsemi.com.cn/UG286.pdf), 
    [E](http://cdn.gowinsemi.com.cn/UG286E.pdf).

[2] [DS976](http://cdn.gowinsemi.com.cn/DS976.pdf),
    [E](http://cdn.gowinsemi.com.cn/DS976E.pdf), illustration of rPLL structure.
