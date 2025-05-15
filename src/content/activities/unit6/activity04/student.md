# ACTIVIDAD 4

## Propósito del patrón State

El patrón **State** permite que un objeto modifique su comportamiento según su estado interno, sin necesidad de usar múltiples estructuras condicionales como `if` o `switch`.  
Es especialmente útil cuando un objeto puede operar de diferentes maneras dependiendo de su situación actual, y puede cambiar entre esas formas de manera dinámica.  
En este proyecto, las partículas modifican su forma de moverse dependiendo del estado en el que se encuentren: pueden estar en modo normal, de atracción, de repulsión o completamente detenidas.

## Diagrama explicado en palabras simples

Podemos imaginar que la clase `Particle` es como un nodo central (una burbuja) que puede encontrarse en uno de cuatro estados distintos:

- Normal  
- Attract  
- Repel  
- Stop

Cada uno de estos estados es un punto al que la partícula puede transicionar, y el cambio entre ellos se da mediante la pulsación de teclas:

- Presionar `n` → cambia al estado **Normal**  
- Presionar `a` → cambia al estado **Attract**  
- Presionar `r` → cambia al estado **Repel**  
- Presionar `s` → cambia al estado **Stop**

Las teclas funcionan como disparadores, y las transiciones entre estados son como flechas que conectan los diferentes nodos.

## Ventajas del patrón State frente a estructuras if/switch

Al utilizar el patrón State, el código se vuelve más claro y estructurado.  
En lugar de llenar el método `update()` con condicionales que verifiquen cuál es el estado actual, cada estado tiene su propia clase y se encarga de definir su propio comportamiento.  
Esto mejora la cohesión del código, ya que cada parte cumple una función específica.  
Además, si en algún momento se necesita añadir un nuevo estado (por ejemplo, uno llamado `Explode`), se puede hacer creando una nueva clase sin modificar el código existente de `Particle`.  
Esto respeta el **Principio Abierto/Cerrado**, que dice que el software debe ser extensible sin necesidad de cambiar lo que ya funciona.

## Rol de los métodos `onEnter` y `onExit`

Los métodos `onEnter` y `onExit` se ejecutan cuando un objeto entra o sale de un estado, respectivamente.  
Sirven para configurar o limpiar condiciones específicas.  
Por ejemplo, en `AttractState::onEnter()` se podría mostrar una animación o guardar la posición actual del mouse.  
En `StopState::onExit()` se podría restablecer la velocidad de la partícula para que retome su movimiento.  
Aunque en este caso particular no se usan demasiado, son herramientas útiles cuando se necesita realizar efectos visuales o reiniciar valores al cambiar de estado.
