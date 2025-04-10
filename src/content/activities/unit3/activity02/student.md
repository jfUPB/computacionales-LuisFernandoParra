``` cpp
 
#include <iostream>
using namespace std;


// Intercambio por valor (no afecta a los valores originales)
void swapPorValor(int a, int b) {
    int z = a;
    a = b;
    b = z;
}

// Intercambio por referencia (afecta a los valores originales)
void swapPorReferencia(int& a, int& b) {
    int z = a;
    a = b;
    b = z;
}

// Intercambio por puntero (afecta a los valores originales)
void swapPorPuntero(int* a, int* b) {
    int z = *a;
    *a = *b;
    *b = z;
}

int main() {
    int x = 5, y = 10;

    cout << "Valores originales: x = " << x << ", y = " << y << "\n";

    // Prueba de swapPorValor
    swapPorValor(x, y);
    cout << "Después de swapPorValor: x = " << x << ", y = " << y << " (sin cambios)\n";

    x = 5, y = 10;

    // Prueba de swapPorReferencia
    swapPorReferencia(x, y);
    cout << "Después de swapPorReferencia: x = " << x << ", y = " << y << "\n";

    x = 5, y = 10;

    // Prueba de swapPorPuntero
    swapPorPuntero(&x, &y);
    cout << "Después de swapPorPuntero: x = " << x << ", y = " << y << "\n";

    return 0;
}
```


1. 
La función swapPorValor(int a, int b) no intercambia los valores de x e y en main() porque trabaja con copias de los valores originales. Cuando la función se llama, a y b reciben copias de los valores de x e y, por lo que cualquier cambio que se haga dentro de la función solo afecta a esas copias y no a las variables originales en main(). Al finalizar la función, las copias se destruyen y x e y permanecen sin cambios.

2. 
- *Por referencia:* En swapPorReferencia(int& a, int& b), los parámetros a y b son referencias a x e y. Esto significa que a y b no son copias, sino alias de las variables originales. Cualquier modificación en a y b afecta directamente a x e y en main(), por lo que el intercambio se mantiene después de la ejecución de la función.

- *Por puntero:* En swapPorPuntero(int* a, int* b), los parámetros son punteros a x e y. Al recibir las direcciones de memoria de x e y, la función puede acceder y modificar sus valores a través de *a y *b. Como el cambio se realiza en la memoria donde están almacenadas x e y, los valores originales se intercambian correctamente.
- 3
  
## Ventajas de usar referencias
- **Sintaxis simplificada:**  
  Al usar referencias se evita la necesidad de desreferenciación explícita (no se requiere el operador `*`), lo que resulta en un código más limpio y fácil de leer.
- **Seguridad:**  
  Las referencias deben estar ligadas a una variable existente y no pueden ser nulas, lo que reduce la posibilidad de errores asociados a punteros nulos.
- **Claridad semántica:**  
  Usar referencias indica claramente que se opera sobre la variable original, facilitando la comprensión del código.

## Ventajas de usar punteros
- **Flexibilidad:**  
  Los punteros permiten ser reasignados para apuntar a diferentes ubicaciones en memoria, lo cual es útil en escenarios donde se requiere manipular estructuras dinámicas.
- **Posibilidad de manejo de nulos:**  
  Al poder ser nulos, los punteros permiten representar la ausencia de una dirección válida, lo que puede ser necesario para el control de flujo o manejo de errores.

## Consideraciones
- **Referencias:**
  - Una vez vinculada, una referencia no puede cambiar para referirse a otra variable.
  - No permiten representar un “estado nulo” (no pueden ser `null`), lo que limita su uso en escenarios que requieren esta posibilidad.
  
- **Punteros:**
  - Requieren una gestión más cuidadosa, ya que se debe asegurar que no se desreferencien punteros nulos o inválidos, lo cual podría causar errores en tiempo de ejecución.
  - La necesidad de desreferenciación explícita puede aumentar la complejidad del código y la posibilidad de cometer errores si no se usa adecuadamente.

