# **Prueba**  
### **¿Qué ocurre, por qué, diferencias entre variables locales estáticas y no estáticas, y qué pasa al entrar y salir de la función?**  
- `funcionSinStatic()` siempre imprime `100` porque la variable local se destruye y se vuelve a crear en cada iteración.  
- `funcionConStatic()` imprime valores crecientes, ya que `var_estatica` mantiene su valor entre llamadas.  
- **Variables normales** (`var_no_estatica`):  
   - Se crean y destruyen en cada llamada, por lo que siempre se reinician.  
   - Se almacenan en la pila (*stack*).  
- **Variables estáticas** (`var_estatica`):  
   - Se inicializan solo una vez y mantienen su valor entre llamadas.  
   - Se almacenan en el segmento de datos estáticos.  
- **Diferencias clave:**  
   - Las variables normales se destruyen al salir de la función.  
   - Las variables estáticas permanecen en memoria y conservan su último valor.  

---

# **Prueba**  
### **¿Qué ocurre y por qué?**  
- El código asigna memoria dinámicamente en el *heap* y luego intenta acceder a ella después de liberarla.  
- **Gestión de memoria:**  
   - La memoria en el *heap* se gestiona manualmente usando `new` y `delete`.  
   - La memoria en la *stack* se gestiona automáticamente y se destruye al salir de la función.  
- **Tiempo de vida:**  
   - La memoria asignada en el *heap* permanece hasta que se libera con `delete`.  
   - La memoria en la *stack* se destruye automáticamente al salir de la función.  
- **Fugas de memoria:**  
   - Si no usamos `delete[]`, ocurre una fuga de memoria (*memory leak*), lo que provoca:  
     - La memoria reservada queda inutilizable hasta que el programa termine.  
     - Si ocurre repetidamente, el programa puede agotar la memoria RAM y volverse más lento o fallar.  
- **Importancia de `delete[]`:**  
   - `delete[]` se usa para liberar memoria asignada con `new[]`.  
   - Si usamos `delete` en lugar de `delete[]`, solo se liberaría la primera posición del arreglo, dejando una fuga de memoria.  
