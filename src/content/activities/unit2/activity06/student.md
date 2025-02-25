# Punteros

### 1. ¿Qué hace esto `int *pvar;`?  
Declara un puntero llamado `pvar` que puede almacenar la dirección de una variable de tipo entero.  

### 2. ¿Qué hace esto `*pvar = var;`?  
Asigna el valor de la variable `var` a la dirección de memoria apuntada por `pvar`. En otras palabras, modifica el contenido de la dirección a la que apunta `pvar`.  

### 3. ¿Qué hace esto `var2 = *pvar;`?  
Asigna a la variable `var2` el valor almacenado en la dirección de memoria a la que apunta `pvar`.  

### 4. ¿Qué hace esto `pvar = &var3;`?  
Hace que el puntero `pvar` almacene la dirección de memoria de la variable `var3`.  
