### ¿Cuál es la función de cada tipo de instrucción?
- A-instruction:Se usa para cargar un valor en el registro A, puede representar una dirección de memoria o un valor numérico constante
- C-instruction:Realiza operaciones aritméticas o lógicas con los registros A, D y M, almacena resultados en registros o memoria y puede controlar el flujo del programa con saltos condicionales o incondicionales
- ## ¿Cómo se representa cada tipo de instrucción en binario?
-  A-instruction:
  - Se representa con un bit inicial en 0, seguido de 15 bits que representan un número
    ```
    0 v v v v v v v v v v v v v v v
    ```
- C-instruction:
- Se representa con un bit inicial en 1, seguido de campos que indican la operación a realizar, el destino del resultado y el tipo de salto
 ```
  1 1 1 a c1 c2 c3 c4 c5 c6 d1 d2 d3 j1 j2 j3
```
### Proporciona al menos 3 ejemplos de cada tipo de instrucción, explicando qué hace cada una
#### Ejemplos de A-instructions:
```
@10 // carga el valor de registro en A
0000000000001010 // Valor en Binario
```
```
@LOOP // Carga la dirección de memoria de la etiqueta LOOP en A
```
- El valor en binario dependerá de la dirección asignada a LOOP por el ensamblador
- Sirve para referenciar una parte del código con un salto (JMP)
```
@24576 // Carga la dirección de la memoria del teclado en A (KBD)
0110000000000000 // Valor en Binario
```
- Se usa para leer la entrada del teclado en Hack

#### Ejemplos  de C-instructions:
```
D=A // Guarda el valor del registro A en el registro D.
1110110000010000 // Valor en Binario
```
- Copia el contenido de A en D
```
D=D-A// Resta el valor de A al valor de D y guarda el resultado en D
1110010011010000// Valor en Binario
```
```
0;JMP  // Salta incondicionalmente a la dirección almacenada en A.
1110101010000111 // Valor en Binario
```
- Se usa para implementar bucles
