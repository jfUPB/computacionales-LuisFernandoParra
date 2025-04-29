#  ¿Qué es una Cola (FIFO)?

Una **cola** es una estructura de datos que funciona como una fila de personas esperando su turno. Su principio es **FIFO**: *First In, First Out*, es decir, el primero en entrar es el primero en salir.

---

##  Analogía sencilla: fila en el cine

Imagina una fila de personas para comprar entradas de cine. El primero que llega será el primero en comprar, y los que llegan después esperan su turno. En programación, funciona igual: los datos que entran primero son los primeros en salir.

---

##  ¿Cómo funciona una cola con nodos?

Una cola se compone de nodos enlazados. Cada nodo contiene:

- Datos (en este caso, posición, color, radio, opacidad)
- Un puntero al siguiente nodo (`next`)

Tiene dos punteros principales:

- `front`: apunta al primer nodo (el que se elimina primero)
- `rear`: apunta al último nodo (donde se agregan los nuevos)

Ejemplo visual de la estructura:

```
front → [Nodo1] → [Nodo2] → [Nodo3] → nullptr
```

---

## 🛠️ Implementación de `enqueue()` y `dequeue()`

### `enqueue(x, y, radius, color, opacity)`

1. Crear un nuevo nodo con los valores dados.
2. Si la cola está vacía, asignar ese nodo a `front` y `rear`.
3. Si no está vacía:
   - Asignar `rear->next = nuevoNodo`
   - Actualizar `rear = nuevoNodo`
4. Incrementar `size`.
5. Si `size > maxSize`, llamar a `dequeue()`.

### `dequeue()`

1. Si la cola está vacía, no hacer nada.
2. Guardar `front` en una variable temporal.
3. Avanzar `front = front->next`.
4. Liberar el nodo antiguo con `delete`.
5. Decrementar `size`.
6. Si `front == nullptr`, también asignar `rear = nullptr`.

---

##  Error común

Un error común es **no actualizar `rear` cuando la cola se vacía**, o **no liberar memoria** al eliminar nodos, lo que puede causar fugas de memoria (*memory leaks*). Siempre usa `delete` para cada nodo eliminado y verifica si debes poner `rear = nullptr`.

---

##  Resumen

- Una cola es una estructura FIFO: el primero en entrar es el primero en salir.
- `enqueue()` agrega nodos al final.
- `dequeue()` elimina nodos desde el frente.
- Siempre gestiona correctamente la memoria.
- Asegúrate de actualizar tanto `front` como `rear` adecuadamente.

---

##  Representación visual simple

Antes de `dequeue()`:
```
front → [A] → [B] → [C] → nullptr
```

Después de `dequeue()`:
```
front → [B] → [C] → nullptr
```
