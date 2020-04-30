

Concept for detecting any of four stations of a Belt Conveyor Tripper
using four discrete inputs including odd parity and at-station.

               Station #          1         2         3         4

                                                   +----+    +----+
                                  0         0      |  8 |    |  8 |
           INP_TWO_BIT(8)  ------------------------+    +----+    -----

                                         +----+              +----+
                                  0      |  4 |       0      |  4 |
           INP_ONE_BIT(4)  --------------+    +--------------+    +----

                               +----+                        +----+
                               |  2 |       0         0      |  4 |
        INP_PARITY_BIT(2)  ----+    +------------------------+    +----

                               +----+    +----+    +----+    +----+
                               |  1 |    |  1 |    |  1 |    |  4 |
    INP_AT_STATION_BIT(1)  ----+    +----+    +----+    +----+    +----


        Resulting integer      2+1=3     4+1=5     8+1=9     8+4+2+1=15

N.B. Odd parity is one to insure the number of 1 bits is odd when
counting INP_TWO_BIT, INP_ONE_BIT, and INP_PARITY_BIT, and excluding
INPUT_AT_STATION_BIT.

### Legend

Discrete Inputs:

                1--->        +----+
                             |  B |
    INP_NAME(B) 0--->   -----+    +------
         
    Where:
      INP_NAME is the name of the input; see below for (B)
      0 represents the signal for the PLC to detect a 0
      1 represents the signal for the PLC to detect a 1
      B represents the bit value contribution for this input, when the
        input is a 1 and all four bits are combined into an integer
