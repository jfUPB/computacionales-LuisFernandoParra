### Lenguaje de Alto Nivel (C)

```c
#include <stdio.h>

// Condicional
void condicional(int x) {
    if (x > 0) {
        printf("El número es positivo\n");
    } else {
        printf("El número no es positivo\n");
    }
}

// Ciclo while
void ciclo_while() {
    int i = 5;
    while (i > 0) {
        printf("%d\n", i);
        i--;
    }
}

// Ciclo for
void ciclo_for() {
    for (int i = 0; i < 5; i++) {
        printf("%d\n", i);
    }
}

// Escritura de variables por punteros
void escribir_por_puntero(int *p) {
    *p = 42;
}

// Lectura de variables por punteros
int leer_por_puntero(int *p) {
    return *p;
}

// Manipulación de un arreglo por punteros
void manipular_arreglo(int *arr, int size) {
    for (int i = 0; i < size; i++) {
        arr[i] *= 2;
    }
}

// Llamado a funciones con parámetros
int suma(int a, int b) {
    return a + b;
}

// Llamado a funciones con retorno de parámetros
int multiplicar(int a, int b) {
    return a * b;
}

int main() {
    int x = -5;
    condicional(x);
    
    ciclo_while();
    
    ciclo_for();
    
    int valor = 10;
    escribir_por_puntero(&valor);
    printf("Valor después de escritura: %d\n", valor);
    
    int leido = leer_por_puntero(&valor);
    printf("Valor leído: %d\n", leido);
    
    int arr[] = {1, 2, 3, 4, 5};
    manipular_arreglo(arr, 5);
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    int resultado_suma = suma(3, 4);
    printf("Suma: %d\n", resultado_suma);
    
    int resultado_multiplicacion = multiplicar(3, 4);
    printf("Multiplicación: %d\n", resultado_multiplicacion);
    
    return 0;
}
```

### Equivalente en Ensamblador para Hack

```asm
// Condicional
@16  
D=M
@100  
D;JGT
@110  
0;JMP
(100)  
@100
0;JMP
(110)  
@110
0;JMP

// Ciclo while
@5
D=A
@20  
M=D
(150)  
@20
D=M
@120  
D;JEQ
@20
M=M-1
@150
0;JMP
(120)

// Ciclo for
@0
D=A
@30 
M=D
(140)  
@30
D=M
@5
D=D-A
@130 
D;JGE
@30
M=M+1
@140
0;JMP
(130)

// Escritura por puntero
@200  
D=A
@210  
M=D
@42
D=A
@210
A=M
M=D

// Lectura por puntero
@210
A=M
D=M
@220  
M=D

// Manipulación de un arreglo por punteros
@300  
D=A
@310  
M=D
@0
D=A
@320  
M=D
(160)  
@320
D=M
@5
D=D-A
@330  
D;JGE
@310
A=M
D=M
D=D+D
@310
A=M
M=D
@310
M=M+1
@320
M=M+1
@160
0;JMP
(330)

// Llamado a funciones con parámetros y retorno
@400  
D=M
@410 
D=D+M
@420  
M=D

// Multiplicación usando sumas repetitivas
@400
D=M  
@430  
M=0  
@410
M=M-1  
(440)  
@410
D=M  
@450  
D;JEQ
@400
D=M
@430
M=M+D  
@410
M=M-1  
@440
0;JMP  
(450) 


@500
0;JMP
```
