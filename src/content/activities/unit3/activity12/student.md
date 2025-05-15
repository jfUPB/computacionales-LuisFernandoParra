## Explicación del ciclo de vida de un objeto en el stack vs en el heap

### 1. Objeto en el stack (`pBloque`)
- Se declara dentro de un bloque `{}` en `main()`, lo que significa que su ciclo de vida está ligado a ese ámbito.
- Al llegar al final del bloque, `pBloque` es eliminado automáticamente y su destructor es llamado.
- Esto se debe a que el stack maneja automáticamente la memoria, liberando los objetos cuando salen de su ámbito.

### 2. Objeto en el heap (`pDinamico`)
- Se crea usando `new`, lo que significa que persiste en la memoria hasta que se libere manualmente con `delete`.
- Su ciclo de vida no depende del ámbito donde se declaró.
- Si no se llama a `delete pDinamico`, habrá una fuga de memoria.

---

## ¿Compila el segundo código?

No, no compila. El error ocurre en esta línea:

```cpp
pBloque2->imprimir();
```

El problema es que `pBloque2` se declara dentro del bloque `{}`, pero se intenta acceder a él fuera del bloque. Como `pBloque2` fue creado dentro del bloque, su memoria es liberada al salir del mismo.

**Error:** Uso de una variable fuera de su ámbito.

---

## Modificación para declarar `pBloque2` fuera del bloque

```cpp
Punto* pBloque2 = nullptr;
{
    cout << "Inicio del bloque 2" << endl;
    pBloque2 = new Punto(500, 600);
    pBloque2->imprimir();
}
pBloque2->imprimir(); // Ahora sí funciona
delete pBloque2;
```

### ¿Qué ocurre aquí?
- `pBloque2` es declarado antes del bloque, pero inicializado dentro de él.
- Al salir del bloque, `pBloque2` sigue existiendo porque apunta a un objeto en el heap, que no se elimina automáticamente.
- Como `pBloque2` sigue existiendo fuera del bloque, se puede acceder a su método `imprimir()`.
- Se libera correctamente la memoria con `delete pBloque2;`.

---

## ¿Por qué `pBloque` se destruye al salir del bloque y `pBloque2` no?

| Objeto       | Ubicación de la memoria | Se destruye automáticamente |
|-------------|-----------------------|---------------------------|
| `pBloque`   | Stack                  | Sí, al salir del bloque |
| `pBloque2`  | Stack (puntero) + Heap (objeto) | No, el puntero sigue existiendo y el objeto en heap necesita `delete` |

### Explicación
- `pBloque` es un objeto en el stack, y cuando el bloque `{}` finaliza, se libera automáticamente.
- `pBloque2` es un puntero en el stack, pero el objeto real al que apunta está en el heap.
- El objeto en el heap **NO** se destruye automáticamente cuando el bloque finaliza. Se debe liberar manualmente con `delete`.
