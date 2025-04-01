# Funciones y Objetos en C++

## ¿Qué sucede después de llamar a la función `cambiarNombre`?

Después de ejecutar la función `cambiarNombre`, se muestra el mensaje:

#### Destructor: Punto cambiado(70, 80) destruido.


### Explicación:

El objeto `original` mantiene su nombre sin cambios. Esto ocurre porque la función `cambiarNombre` recibe su argumento **por valor**, lo que significa que dentro de la función se crea una **copia temporal** del objeto `original`, denominada `p`.  
- La modificación del atributo `name` solo afecta a la copia `p`, no al objeto `original` en `main`.
- Al finalizar la función, la copia `p` es destruida, lo que activa el destructor y genera el mensaje.  
- Sin embargo, `original` sigue existiendo sin alteraciones.

---

## Ubicación en memoria de `original` y `p`  
¿Son el mismo objeto?  

### `original`
- Se encuentra en el **stack** de `main()`, ya que es una variable local de esta función.
- Sus atributos (`name`, `x`, `y`) también están almacenados en el **stack**.

### `p` en `cambiarNombre`
- `p` es una **copia** del objeto `original`.
- Sus atributos (`name`, `x`, `y`) son **independientes** de los de `original`.
- Cuando la función `cambiarNombre` finaliza, `p` se elimina del **stack**, ejecutando su destructor.

Por lo tanto, `original` y `p` **no son el mismo objeto**. Aunque al inicio tienen valores idénticos, son entidades separadas en la memoria.

---

## Modificación de `cambiarNombre` para usar referencias  

Si `cambiarNombre` se modifica para recibir el argumento **por referencia**, entonces ahora sí puede modificar `original` directamente.

---

## Cambio en `main` y en `cambiarNombre`  

Al utilizar referencias:
- `p` ya no es una copia, sino que **almacena la dirección de memoria de `original`**.
- Cualquier modificación en `p->name` afectará directamente a `original`, ya que `p` apunta al mismo objeto en `main()`.

