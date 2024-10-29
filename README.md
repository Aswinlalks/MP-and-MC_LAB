# MPMC Lab ALP's

## [ 1.a ] ALP to add two 8 bit numbers
| CODE       | COMMENTS                                     |
|------------|----------------------------------------------|
| `MVI A, 02H` | 1st Number Loaded to Accumulator           |
| `MVI B, 03H` | 2nd Number Loaded to B Register            |
| `ADD B`    | A <== A+B                                   |
| `STA 1050H` | Store result in memory location 1050H       |
| `HLT`      | End the program                              |

## [ 1.b ] ALP to add two 8 bit numbers from a _memory location_
| CODE       | COMMENTS                                              |
|------------|-------------------------------------------------------|
| `LXI H, 1000H` | Fetch data in memory location 1000H, Move to H    |
| `MOV A, M` | Move data in H-L pair to Accumulator                  |
| `INX H`    | Increment register H                                  |
| `ADD M`    | A <== A+M                                             |
| `STA 1002H` | Store the result in memory location 1002H            |
| `HLT`      | End the program                                       |

## [ 1.c ] ALP to add two 16-bit numbers from consecutive memory locations and store result
![Relative](IMAGES/MPMC.png)
| CODE           | COMMENTS                                                  |
|----------------|-----------------------------------------------------------|
| `LXI H, C050H` | Load memory location C050H into H-L pair                  |
| `MOV A, M`     | Move data from H-L pair memory to Accumulator             |
| `INX H`        | Increment H-L to point to the next memory location        |
| `MVI B, 00H`   | Initialize B register to 00H for handling carry           |
| `ADD M`        | Add the content of memory (C051H) to Accumulator          |
| `JNC LOOP`     | Jump to LOOP if no carry is generated                     |
| `INR B`        | Increment B register if carry is generated                |
| `LOOP STA C050H` | Store the lower byte result at memory location C050H    |
| `MOV B, A`     | Move Accumulator value to B register                      |
| `STA C050H`    | Store the final result in memory location C050H           |
| `HLT`          | End the program                                           |

## [2.a] Subtraction of 8-bit Numbers


| Memory Location | Label | Mnemonics | Comments                       |
|-----------------|-------|-----------|--------------------------------|
| 4100            |       | LXI H, 4501H | Load address 4501H into HL |
| 4103            |       | LDA 4500H | Load data from 4500H into A   |
| 4106            |       | MVI C, 00H  | Move 00 into register C      |
| 4108            |       | SUB M       | Subtract memory content from A |
| 4109            |       | JNC LOOP    | Jump if no carry to LOOP     |
| 410C            |       | INR C       | Increment C                  |
| 410D            |       | CMA         | Complement Accumulator       |
| 410E            |       | INR A       | Increment A                  |
| 410F            | LOOP  | STA 4502H   | Store result in 4502H        |
| 4112            |       | MOV A, C    | Move C to Accumulator        |
| 4113            |       | STA 4503H   | Store result in 4503H        |
| 4116            |       | HLT         | End the program              |

## Multiplication of 8-Bit Numbers


| Memory Location | Label  | Mnemonics   | Comments                             |
|-----------------|--------|-------------|--------------------------------------|
| 4100            |        | LXI H, 4500H | Load address 4500H into HL          |
| 4103            |        | MOV B, M    | Move data from memory (4500H) to B  |
| 4104            |        | MVI A, 00H  | Initialize Accumulator A to 00      |
| 4106            |        | MVI C, 00H  | Initialize register C to 00         |
| 4108            |        | INX H       | Increment HL to point to next byte  |
| 4109            |        | MOV D, M    | Move data from next byte (4501H) to D |
| 410A            | LOOP   | ADD D       | Add D to Accumulator                |
| 410B            |        | JNC AHEAD   | Jump to AHEAD if no carry           |
| 410E            |        | INR C       | Increment C if there was a carry    |
| 410F            | AHEAD  | DCR B       | Decrement B                         |
| 4110            |        | JNC LOOP    | Jump to LOOP if no carry            |
| 4113            |        | INX H       | Increment HL to store result        |
| 4114            |        | MOV M, A    | Store lower byte result at [HL]     |
| 4115            |        | INX H       | Increment HL to store next byte     |
| 4116            |        | MOV M, C    | Store upper byte result at [HL]     |
| 4117            |        | HLT         | End the program                     |

## Division of Two 8-Bit Numbers


| Memory Location | Label  | Mnemonics   | Comments                             |
|-----------------|--------|-------------|--------------------------------------|
| 4100            |        | LXI H, 4500H | Load address 4500H into HL          |
| 4103            |        | MOV A, M    | Move data from memory (4500H) to A  |
| 4104            |        | INX H       | Increment HL to point to the next byte |
| 4105            |        | MOV B, M    | Move data from next byte (4501H) to B |
| 4106            |        | MVI C, 00H  | Initialize register C to 00         |
| 4108            | AGAIN  | CMP B       | Compare A with B                    |
| 4109            |        | JC AHEAD    | Jump to AHEAD if A < B              |
| 410C            |        | SUB B       | Subtract B from A                   |
| 410D            |        | INC C       | Increment C (quotient)              |
| 410E            |        | JMP AGAIN   | Repeat until A < B                  |
| 4111            | AHEAD  | STA 4502H   | Store remainder (A) at 4502H        |
| 4114            |        | MOV A, C    | Move C (quotient) to A              |
| 4115            |        | STA 4503H   | Store quotient at 4503H             |
| 4118            |        | HLT         | End the program                     |
