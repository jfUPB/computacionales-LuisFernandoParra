### ¿Qué es el direccionamiento directo? 
El direccionamiento directo es un método en el cual una instrucción hace referencia a una dirección de memoria específica
### ¿Cómo se usa en el lenguaje ensamblador Hack?
En el lenguaje ensamblador Hack el direccionamiento directo se usa mediante la instrucción @algo, donde algo es un número que representa una dirección de memoria.
### ¿Qué significa M=D en lenguaje ensamblador Hack? ¿Y D=M?
M=D significa que guarde en memoria el valot de D, mientras que D=M significa que D tome el valor que previamente este guardado en memoria
### Explica con tus palabras el concepto de “puntero” en el contexto de la memoria y proporciona un ejemplo sencillo en lenguaje ensamblador Hack
Un puntero es una variable que almacena una dirección de memoria en lugar de un valor directo. Es decir, en lugar de contener un dato, el puntero indica dónde se encuentra ese dato en la memoria.
### Ejemplo:
```
@200   
D=A     // D = 200
@60     
M=D     // M[60] = 200  (La dirección 60 ahora es un puntero a 200)
@60     
D=M     // D = M[60] (Carga la dirección 200 en D)
A=D     // A = 200 (Ahora A apunta a la dirección 200)
M=42    // M[200] = 42 (Guardamos el valor 42 en la dirección 200)
@200    
D=M     // Cargamos el valor de la dirección 200 en D (debería ser 42)
```

