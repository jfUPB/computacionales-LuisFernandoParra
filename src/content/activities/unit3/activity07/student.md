# Actividad 7

## Diferencia entre un constructor y un destructor en C++

- **Constructor**: Se ejecuta automáticamente al crear un objeto y su propósito es inicializar sus atributos.
- **Destructor**: Se ejecuta automáticamente cuando un objeto sale de su ámbito o se libera memoria, permitiendo la limpieza de recursos.

## Diferencia entre un objeto y una clase en C++

- **Clase**: Es un modelo o plantilla que define atributos y métodos.
- **Objeto**: Es una instancia concreta de una clase que ocupa espacio en memoria.

## Diferencia entre el objeto `Punto` en C++ y C#

- En **C++**, `Punto p(10, 20);` crea el objeto en el *stack* y su destructor se ejecuta automáticamente al salir del ámbito.
- En **C#**, `Punto p = new Punto(10, 20);` crea el objeto en el *heap*, y la memoria es gestionada por el *Garbage Collector*.

## ¿Qué es `p` en C++ y en C#?

- En **C++**, `p` es un objeto real almacenado en el *stack*.
- En **C#**, `p` es una referencia a un objeto ubicado en el *heap*.

## Ubicación de `p` en la memoria en C++ y C#

- **C++**: `p` se almacena en el *stack*.
- **C#**: `p` es una referencia en el *stack*, pero el objeto real está en el *heap*.

## Observaciones con el depurador sobre `p`

- En **C++**, `p` tiene una dirección fija en el *stack* y sus atributos `x` e `y` se almacenan de forma contigua en la memoria.
- En **C#**, `p` es una referencia a un objeto en el *heap*, por lo que la dirección que almacena `p` no corresponde directamente a la del objeto real.

## ¿Qué es un objeto en C++ y en C# según lo observado?

- En **C++**, un objeto es una instancia directa de una clase, que puede almacenarse en el *stack* o en el *heap* según cómo se declare.
- En **C#**, un objeto siempre se encuentra en el *heap* y solo se accede a él mediante referencias.
