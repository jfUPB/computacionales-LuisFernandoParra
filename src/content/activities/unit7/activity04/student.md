**ACTIVIDAD 4**

### ¿Cómo funcionan las gráficas en una computadora?
El video explica que todo lo que vemos en pantalla está compuesto por millones de píxeles, los cuales deben recalcularse múltiples veces por segundo. Cada elemento 3D que vemos está construido a partir de triángulos, y el trabajo del sistema gráfico consiste en transformar esos triángulos (coordenadas, colores, texturas) en los píxeles que finalmente vemos.

### Diferencia entre CPU y GPU
La CPU, o Unidad Central de Procesamiento, es como un cerebro versátil que puede realizar varias tareas distintas, aunque de forma secuencial o con poca concurrencia. En cambio, la GPU, o Unidad de Procesamiento Gráfico, se asemeja a una gran cantidad de trabajadores simples capaces de ejecutar muchas tareas a la vez, siempre que sean similares. Esto la hace perfecta para trabajar con gráficos, donde hay que procesar millones de píxeles o vértices al mismo tiempo.

### ¿Cuáles son las etapas más importantes del pipeline de OpenGL?
1. **Procesamiento de vértices (Vertex Processing)**: Los vértices de los modelos 3D son transformados de su posición tridimensional original a coordenadas en la pantalla 2D, mediante el uso de matrices.
2. **Rasterización**: Se transforma cada triángulo formado por vértices en fragmentos, que son potenciales píxeles. Aquí se determina qué área del triángulo toca cada píxel.
3. **Procesamiento de fragmentos (Fragment Processing)**: A cada fragmento se le asignan características como color, textura, iluminación y visibilidad antes de convertirse en un píxel definitivo.

### ¿Qué significa que el pipeline ahora sea programable?
En versiones modernas de OpenGL, puedes escribir tus propios shaders: pequeños programas que controlan cómo se procesan los vértices y los fragmentos. Esto te permite definir cada etapa del proceso gráfico.

### Comparación entre pipeline fijo y pipeline programable
- **Pipeline fijo (OpenGL antiguo)**: Todo venía preconfigurado: iluminación, cámara, colores, etc.
- **Pipeline programable**: El desarrollador define cada etapa. Esto otorga mayor control, más libertad y potencia para personalizar el renderizado.

### Beneficios del pipeline programable
- Permite crear efectos especiales como fuego, agua, brillos de neón, entre otros.
- Facilita la optimización del código para necesidades específicas.
- Se pueden incorporar técnicas avanzadas como sombras dinámicas, reflejos, iluminación en tiempo real, etc.

### ¿Qué es exactamente la rasterización?
Es la etapa donde los triángulos ya posicionados se traducen en píxeles. Se determina qué fragmentos (posibles píxeles) representan la superficie del triángulo. Es parecido a pintar dentro de las formas, usando reglas geométricas.

### ¿Qué son los fragmentos? ¿Son iguales a los píxeles?
No, un fragmento aún no es un píxel confirmado. Es una especie de propuesta de píxel, al cual se le calculan varios atributos (color, profundidad, etc.). Solo si pasa ciertas pruebas, como la de profundidad, se convierte en un píxel final en pantalla.

### ¿Qué problema soluciona el Z-buffer y cómo funciona el depth test?
El Z-buffer guarda la distancia de cada fragmento respecto a la cámara. El depth test compara esta distancia con la de otros fragmentos que compiten por el mismo píxel. Si un fragmento está más cerca, reemplaza al que ya estaba. Esto impide que objetos más lejanos cubran a los cercanos.

### ¿Qué provoca el aliasing y cómo lo evita el anti-aliasing?
El aliasing ocurre por la forma cuadrada de los píxeles. Cuando una línea es diagonal o curva, se nota el efecto de "escalones". El anti-aliasing suaviza esas líneas aplicando colores intermedios para dar la ilusión de bordes más suaves y continuos.

### ¿Cómo se relaciona la iluminación con el fragment shader?
La iluminación se calcula directamente en el fragment shader, ya que en esa etapa se conoce con precisión el punto de la superficie y cómo le afectan las fuentes de luz.

### ¿Qué impacto tiene usar varias luces en la GPU?
Cada fuente de luz añade más operaciones por fragmento: ángulos, intensidad, sombras, etc. A mayor cantidad de luces:
- Más cálculos por cada fragmento.
- Mayor carga sobre la GPU.
- Posibles bajadas en el rendimiento.  
Por eso, se suelen aplicar técnicas como sombras precalculadas, luces ambientales o agrupamiento de luces.

### ¿Qué se necesita para dibujar un triángulo en OpenGL?
Primero se definen las coordenadas de los vértices y se cargan en un arreglo. Luego se crean dos objetos clave: el **VBO (Vertex Buffer Object)**, que guarda los datos de vértices en la GPU, y el **VAO (Vertex Array Object)**, que gestiona cómo interpretar esos datos. Después, se enlazan estos objetos, se configuran los atributos con funciones como `glVertexAttribPointer` y finalmente se llama a `glDrawArrays` para dibujar. Esto solo funciona si previamente se ha activado un shader válido.

### ¿Qué se requiere para utilizar un shader en OpenGL?
Primero se escribe el código del shader en GLSL (uno para vértices y otro para fragmentos). Luego se crean objetos shader, se les asigna el código fuente, se compilan y se revisan errores. Después, se crea un programa que agrupa ambos shaders, se enlazan (link), y si no hay problemas, se eliminan los objetos individuales. Finalmente, se activa el programa con `glUseProgram` para que la GPU lo use durante el renderizado.