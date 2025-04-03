# Conclusiones sobre Miembros Estáticos y de Instancia  

## Miembros de Instancia (Variables de Objeto)  

- Si el objeto es local, sus atributos se almacenan en el **stack**.  
- Si el objeto es dinámico, sus atributos se guardan en el **heap**.  
- Cada instancia de la clase tiene su **propia copia** de estos valores.  

## Miembros Estáticos (Variables de Clase)  

- Se almacenan en el **Data Segment** (memoria global).  
- No están ligados a una instancia específica, sino que **pertenecen a la clase** en su totalidad.  
- Son compartidos por **todos los objetos** de la misma clase.  

## Ventajas y Desventajas  

| Tipo de Miembro      | Ventajas                                           | Desventajas                                        |  
|----------------------|---------------------------------------------------|---------------------------------------------------|  
| **Miembros de instancia** | Cada objeto mantiene su propio estado.        | Puede consumir más memoria si hay muchas instancias. |  
| **Miembros estáticos**   | Se comparten entre todas las instancias, lo que facilita datos globales de la clase. | No pueden almacenar información específica de un solo objeto. |  

## Cuándo Usar `static`  

- Para llevar **contadores de instancias** (por ejemplo, `total`).  
- Para **constantes compartidas**, como `static const double PI = 3.14159;`.  
- Para **métodos utilitarios** que no dependen de una instancia en particular.  

## Preguntas y Respuestas Finales  

### ¿Qué se puede concluir sobre los miembros estáticos y de instancia?  

- Los **miembros estáticos** pertenecen a la **clase** y no a instancias individuales.  
- Los **miembros de instancia** son propios de cada objeto.  

### ¿Dónde se almacenan `c1`, `c2`, `c3` y `Contador::total`?  

- **`c1` y `c2`** → **Stack**  
- **`c3`** → **Stack** (pero solo como puntero)  
- **`*c3` (objeto al que apunta `c3`)** → **Heap**  
- **`Contador::total`** → **Data Segment** (memoria global para variables estáticas)  

### ¿Cuál es la diferencia entre `c3` y `*c3` en términos de memoria?  

- **`c3`** es un **puntero** almacenado en el **stack**.  
- **`*c3`** es el objeto real almacenado en el **heap**.  
