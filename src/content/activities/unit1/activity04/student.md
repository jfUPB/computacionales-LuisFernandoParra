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
- e representa con un bit inicial en 1, seguido de campos que indican la operación a realizar, el destino del resultado y el tipo de salto
 ```
  1 1 1 a c1 c2 c3 c4 c5 c6 d1 d2 d3 j1 j2 j3
```
### Proporciona al menos 3 ejemplos de cada tipo de instrucción, explicando qué hace cada una
#### Ejemplos de A-instructions:

