```
@16384
D=A
@16
M=D
@24576
D=M
@112
D=D-A
@32
D;JGE
@24576
D=M
@66
D=D-A
@18
D;JGE
@4
0;JMP
@16
D=M
@16384
D=D-A
@4
D;JLE
@16
AM=M-1
M=0
@4
0;JMP
@16
D=M
@24576
D=D-A
@4
D;JGE
@16
A=M
M=-1
@16
M=M+1
@4
0;JMP

```
