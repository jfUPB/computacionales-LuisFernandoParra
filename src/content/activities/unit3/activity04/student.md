

## **Código 1**  
### **¿Qué ocurre y por qué?**  
- `&main` obtiene la dirección de memoria donde está almacenada la función `main()`, ubicada en el segmento de código (también llamado *text segment*).  
- `reinterpret_cast<void*>` convierte esta dirección a un puntero genérico (`void*`), lo que evita que el compilador genere advertencias.  
- Luego, el puntero `ptr` se convierte a `int*`, permitiendo tratar esa dirección como si almacenara un entero.  
- La instrucción `reinterpret_cast<int>(ptr) = 0;` intenta escribir un `0` en esa dirección de memoria.  
- Esto provoca un error porque las direcciones de memoria del segmento de código están protegidas y no se pueden modificar directamente.  

---

## **Código 2**  
- La dirección almacenada en `mensaje_ro` no puede modificarse.  
- El contenido al que apunta (`"Hola, memoria de solo lectura"`) está en un segmento de solo lectura (segmento de texto o `.rodata`).  
- `&mensaje_ro` obtiene la dirección del puntero `mensaje_ro`, no del contenido de la cadena.  
- Al convertirlo a `char*`, el compilador permite la modificación sin generar advertencias.  
- Sin embargo, la instrucción `*ptr = 0;` intenta escribir un `0` en esa dirección, lo que provoca un error porque las direcciones de memoria de solo lectura están protegidas y no pueden ser modificadas.  
