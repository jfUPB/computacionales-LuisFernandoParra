

## 1. ¿Qué aprendí en esta unidad?

En esta unidad aprendí a trabajar con **programación orientada a objetos en C++**, y logré comprender varios conceptos fundamentales a través de la práctica directa. Por ejemplo, al crear la clase `Mascota` con atributos como `nombre`, `edad` y `tipo`, y métodos como `mostrarInfo`, pude entender cómo encapsular datos y comportamientos en un solo objeto.

Uno de los conceptos que más me ayudó a consolidar este conocimiento fue el uso de **constructores y destructores**. Al imprimir mensajes dentro de ellos, pude visualizar en qué momento exacto se crean y destruyen los objetos, lo que me dio una mejor comprensión del **ciclo de vida de un objeto**.

También logré entender la diferencia entre **paso por valor** y **paso por referencia**, algo que siempre me había parecido confuso. En mi ejemplo, hice dos métodos (`duplicarEdadPorValor` y `duplicarEdadPorReferencia`) que demostraban claramente cómo una variable podía o no ser modificada desde una función. Esto me ayudó a ver que cuando se pasa por valor, se trabaja con una copia, mientras que por referencia se trabaja con la variable original.

## 2. ¿Cuáles fueron los conceptos más desafiantes de la unidad? ¿Por qué?

Los conceptos más desafiantes para mí fueron:

- La diferencia entre **memoria en el stack y en el heap**.
- El manejo de **punteros** en combinación con objetos.

Estos temas fueron difíciles porque no basta con entenderlos teóricamente: es necesario imaginar (o visualizar) cómo se distribuye la memoria y qué ocurre cuando se reserva dinámicamente con `new`. Por ejemplo, cuando creé el objeto `mascota2` con `new`, al principio no entendía por qué debía usar `->` para acceder a sus métodos, hasta que comprendí que estaba usando un **puntero** y no una instancia directa.

## 3. ¿Qué estrategias utilicé para comprender esos conceptos desafiantes?

Usé varias estrategias, entre ellas:

- **Dibujar diagramas de memoria** para entender cómo se almacenan los objetos en el stack y en el heap.
- **Probar con código real** en programas pequeños para ver cómo cambian las variables al pasar por valor o por referencia.
- **Agregar muchos `cout`** en el programa para rastrear el flujo del código y ver el comportamiento en tiempo real.
- **Leer ejemplos de otros programas** y modificar sus partes para ver qué ocurría.

## 4. ¿Qué estrategias me resultaron más efectivas?

Las estrategias más efectivas fueron:

- **Escribir mi propio código desde cero**, porque me obligó a pensar y no solo copiar.
- **Depurar con `cout`**, ya que me permitía visualizar valores y entender lo que estaba pasando “detrás del telón”.
- **Enseñar a otra persona o explicármelo en voz alta**, algo que me obligaba a organizar mis ideas y detectar errores en mi lógica.

## 5. ¿Qué haré en las próximas unidades para mejorar mi comprensión de los conceptos más desafiantes?

Voy a seguir un plan de acción concreto que incluye:

1. **Planificación semanal de estudio práctico**: dedicaré mínimo 2 sesiones por semana de 30 minutos para escribir código que aplique lo visto en clase.
2. **Uso de esquemas visuales**: cada vez que aparezca un concepto de memoria (stack, heap, punteros), dibujaré cómo se almacena en un cuaderno.
3. **Practicar con pequeños retos**: buscaré ejercicios online o en el libro que me obliguen a usar punteros, referencias y memoria dinámica.
4. **Resolver dudas activamente**: cada vez que algo no me quede claro, lo buscaré inmediatamente (ya sea en foros, videos, o preguntando al profesor).
5. **Crear un mini-proyecto por unidad**: como lo hice con el sistema de mascotas, diseñar algo pequeño pero completo que use todos los conceptos de la unidad.
