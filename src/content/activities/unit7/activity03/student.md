## Actividad 3


---



###  ¿Qué pasaría si...?

Modificación del viewport:
```cpp
glViewport(0, bufferHeight/2, bufferWidth/2, bufferHeight/2);
```

**Observaciones:**
- El triángulo se renderiza más pequeño y desplazado.
- Cambiar el viewport permite recortar o reubicar el área visible.
- Es útil para dividir la pantalla o mostrar interfaces.

---



**1. ¿Qué es el contexto OpenGL?**  
Es el entorno que almacena el estado y recursos de OpenGL. Es necesario para ejecutar cualquier instrucción gráfica.

**2. ¿Qué rol cumple GLFW en el ejemplo?**  
Crea la ventana, el contexto OpenGL y maneja entradas de usuario.

**3. ¿Por qué OpenGL necesita un contexto?**  
Porque todas las operaciones gráficas ocurren dentro de un contexto. Sin él, OpenGL no tiene dónde trabajar.

**4. ¿Qué es el framebuffer?**  
Es la memoria donde se dibujan los píxeles antes de ser mostrados. Funciona como un lienzo oculto.

**5. ¿Cuál es la relación entre viewport y framebuffer?**  
El framebuffer es toda el área de dibujo; el viewport define qué parte del framebuffer se usa para mostrar en pantalla.

**6. ¿Qué rol juega la GPU en este ejemplo?**  
La GPU ejecuta los shaders, procesa los vértices y pinta el triángulo. OpenGL solo da las órdenes.

**7. ¿Por qué activamos el VSync?**  
Para sincronizar los frames con el monitor y evitar el "tearing" de imagen.

**8. ¿Qué diferencia hay entre OpenGL Legacy y moderno?**  
El Legacy usaba funciones obsoletas como `glBegin`/`glEnd`. El moderno requiere shaders, VAO y VBO, y es más eficiente y flexible.

**9. ¿Qué es un shader program?**  
Un conjunto de shaders (vertex y fragment) compilados y enlazados para usar en la GPU.

**10. ¿Qué hace setupTriangle()?**  
Define los vértices del triángulo, crea el VBO (Vertex Buffer Object) y el VAO (Vertex Array Object).

**11. ¿Es necesario llamar a `glUseProgram` y `glBindVertexArray` en cada frame?**  
Sí, es recomendable para asegurar que se use el shader y el VAO correctos, especialmente si pueden cambiar.

**12. ¿Qué pasaría si no se llama a `glfwSwapBuffers()`?**  
El triángulo nunca se mostraría en pantalla. La imagen quedaría en el buffer trasero sin ser visible.

---

### Bitácora personal

#### 1:
> Modifiqué los parámetros de `glViewport` y observé cómo cambiaba el área donde se dibuja el triángulo. Esto me ayudó a visualizar la relación entre el viewport y el framebuffer.

#### 2:
> Escribí un resumen con analogías para entender mejor los conceptos. Por ejemplo, el framebuffer es como un lienzo y el viewport como una ventana a ese lienzo. Entendí mejor la importancia del contexto y cómo la GPU ejecuta los shaders.