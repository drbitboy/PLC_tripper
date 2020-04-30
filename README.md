

Concept for detecting any of four stations of a Belt Conveyor Tripper
using four discrete inputs including odd parity and at-station inputs.

               Station #          1         2         3         4

                                                   +----+    +----+
                                  0         0      |  8 |    |  8 |
           INP_TWO_BIT(8)  ------------------------+    +----+    -----

                                         +----+              +----+
                                  0      |  4 |       0      |  4 |
           INP_ONE_BIT(4)  --------------+    +--------------+    +----

                               +----+                        +----+
                               |  2 |       0         0      |  2 |
        INP_PARITY_BIT(2)  ----+    +------------------------+    +----

                               +----+    +----+    +----+    +----+
                               |  1 |    |  1 |    |  1 |    |  1 |
    INP_AT_STATION_BIT(1)  ----+    +----+    +----+    +----+    +----


        Resulting integer         3         5         9        15
        => component bits        2+1       4+1       8+1     8+4+2+1

### Legend

Discrete Inputs:

                      +----+       <===1
                      |  b |
    INP_NAME(B)   ----+    +-----  <===0
         
    Where:
      INP_NAME is the name of the input
      (B) the bit value contributed to the integer when this bit is 1
      <===1 is the signal level where the PLC senses a 1 for this input
      <===0 is the signal level where the PLC senses a 0 for this input
      b represents the bit value contribution at this station for this
        input when all four bits are combined into an integer

N.B. The width of each input signal must be longer than the
sum of
* 200ms of conveyor movement (to filter spurious signals and/or bounce)
* two scan times (say 10ms) of conveyor movement
* enough distance to stop the cart and maintain the same input values

N.B. Odd parity is either 0 or one to ensure that the number of 1 bits
is odd when counting INP_TWO_BIT, INP_ONE_BIT, and INP_PARITY_BIT, and
excluding INPUT_AT_STATION_BIT.

N.B. There are eight possible values for the three bits (two, one,
parity); four are shown above; the other four values are parity errors,
but will only be detected as such when the at-station bit is 1.
