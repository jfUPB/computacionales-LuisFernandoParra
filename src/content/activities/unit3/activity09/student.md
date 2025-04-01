## Copia en C++ y C#

### C++  
Tanto `copia` como `original` hacen referencia al mismo objeto en memoria.  
Cualquier modificación en `copia` impactará también a `original`, ya que ambas variables apuntan al mismo espacio de memoria.  
En este caso, el uso de referencias es implícito, sin necesidad de punteros explícitos.  

### C#  
Del mismo modo, en C#, `copia` y `original` apuntan al mismo objeto en memoria.  
Cualquier cambio realizado en `copia` se reflejará en `original`, dado que ambas variables funcionan como referencias al mismo espacio de memoria.  
Aquí también se emplean referencias implícitas sin requerir punteros explícitos.  
