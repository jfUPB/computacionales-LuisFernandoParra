# ACTIVIDAD 3

## Propósito del patrón Factory Method

El patrón Factory Method tiene como objetivo centralizar la lógica para crear objetos, separando esa responsabilidad del resto de la aplicación.  
Esto ayuda a evitar que el operador `new` se utilice repetidamente en diferentes partes del código, promoviendo una mejor organización.

## Ventajas de usar `ParticleFactory` dentro de `ofApp::setup`

El uso de `ParticleFactory` en `ofApp::setup` mejora la estructura del programa, ya que `ofApp` se encarga solamente de utilizar las partículas, sin preocuparse por cómo se configuran.  
Esto cumple con el **principio de responsabilidad única (SRP)**, lo cual hace que el código sea más claro y fácil de mantener.  
Además, permite agregar nuevos tipos de partículas sin necesidad de modificar `ofApp`.  
Otra ventaja es que la fábrica se puede reutilizar desde otras partes del código si fuera necesario.

## Añadir el tipo de partícula `black_hole`

Para incluir una nueva partícula llamada `black_hole`, basta con modificar el método `ParticleFactory::createParticle`, agregando una condición que defina sus propiedades: color negro, tamaño grande y velocidad baja.  
No se requiere hacer cambios en `ofApp::setup`, solo se debe invocar a la fábrica con el nuevo tipo.  
Esto demuestra la **extensibilidad** del patrón Factory Method, ya que permite añadir funcionalidades nuevas sin alterar el código que ya está usando las partículas.

## Implicaciones de que `createParticle` sea un método estático

Tener `createParticle` como un método estático facilita su uso, ya que no es necesario crear una instancia de `ParticleFactory` para utilizarlo.  
Sin embargo, esta decisión también tiene sus desventajas:  
- No se puede usar herencia sobre la fábrica.  
- No se puede mantener un estado interno dentro de la clase.  

Si más adelante se necesita contar con múltiples fábricas especializadas o guardar algún tipo de configuración interna, sería más adecuado convertir `createParticle` en un método de instancia.
