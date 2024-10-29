# MPMC Lab ALP's

## [ 1.a ] ALP to add two 8 bit numbers
 CODE | COMMENTS |
| ----- | --- |
| MVI A, 02H | 1st Number Loaded to Accumulator |
| MVI B, 03H | 2nd Number Loaded to B Register |
| ADD B | A <== A+B |
| STA 1050H | Store result in memory location 1050H|
| HLT | End the program|

## [ 1.b ] ALP to add two 8 bit numbers from a _memory location_
 CODE | COMMENTS |
| ----- | --- |
| LXI H, 1000H| Fetch data in memory location 1000H,Move to register H |
| MOV A, M | Move data in H-L pair to Accumultor |
| INX H | Increment register H |
| ADD M | A <== A+M |
| STA 1002H | Store the result in memory location 1002H|
| HLT | End the program|
