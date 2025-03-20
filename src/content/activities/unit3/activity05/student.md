# **Prueba**  
### **¿Qué ocurre y por qué?**  
- `global_inicializada = 42;` → Se almacena en el segmento de datos (`.data`) porque tiene un valor asignado explícitamente.  
- `global_no_inicializada;` → Se almacena en el segmento de variables (`.bss`) y el sistema la inicializa automáticamente en cero.  
- `global_inicializada` imprimirá `42` porque ya tenía un valor asignado.  
- `global_no_inicializada` imprimirá `0` porque el segmento `.bss` inicializa las variables no inicializadas en cero.  
- `global_inicializada` se reasigna a `69` sin problema porque está en memoria de lectura y escritura (no está protegida).  
- `global_no_inicializada` se modifica a `666` sin problema por la misma razón.  
- `global_inicializada` ahora imprimirá `69`.  
- `global_no_inicializada` ahora imprimirá `666`.  

---

# **Prueba**  
### **¿Qué ocurre, por qué, qué pasa con las variables al entrar y salir de la función y qué pasa con las variables locales estáticas?**  
- El código original genera un error de compilación porque `var_estatica` solo existe dentro de `funcionConStatic()`.  
- Las variables locales normales se destruyen al salir de la función, por lo que no conservan su valor entre llamadas.  
- Las variables locales estáticas mantienen su valor entre llamadas porque se almacenan en el segmento de datos estáticos y no se destruyen al salir de la función.  
