| **PC** | **Instrucción** | **Binario** | **Decode** | **Execute** |
|------|----------------|----------------|-------------------------|-------------------------|
| 0    | @60           | 0000000000111100 | Carga el valor 60 en A. | A = 60 |
| 1    | D=A          | 1110110000010000 | Guarda el valor de A en D. | D = 60 |
| 2    | @9           | 0000000000001001 | Carga el valor 9 en A. | A = 9 |
| 3    | D=D+A        | 1110000010010000 | Suma D y A, guarda en D. | D = 60 + 9 = 69 |
| 4    | @6           | 0000000000000110 | Carga el valor 6 en A. | A = 6 |
| 5    | M=D          | 1110001100001000 | Guarda D en M[A]. | M[6] = 69 |
| 6    | @0           | 0000000000000000 | Carga el valor 0 en A. | A = 0 |
| 7    | 0;JMP        | 1110101010000111 | Salta a la dirección 0. | PC = 0 (loop infinito) |

