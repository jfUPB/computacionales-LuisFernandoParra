#  Actividad 4: Principios de Programación Orientada a Objetos

En esta actividad se aplican diversos principios fundamentales de la programación orientada a objetos, los cuales se explican y ejemplifican a continuación:

 **Encapsulamiento:** Este principio consiste en agrupar los atributos y comportamientos dentro de una clase específica y restringir el acceso directo desde el exterior. Así se protege la integridad de los datos internos.  
**Ejemplo aplicado:**  
`class RisingParticle : public Particle { protected: glm::vec2 position; … };`

 **Herencia:** Permite crear nuevas clases basadas en una clase existente, lo cual favorece la reutilización de código y la especialización del comportamiento según el tipo de partícula.  
**Ejemplo aplicado:**  
`class RisingParticle : public Particle { … };`  
`class CircularExplosion : public ExplosionParticle { … };`

 **Polimorfismo:** Se refiere a la capacidad de usar punteros a una clase base para manipular objetos de diferentes clases derivadas, de modo que se ejecuten automáticamente los métodos apropiados según el tipo real del objeto.  
**Ejemplo aplicado:**  
`particles[i]->update(dt);`  
`particles[i]->draw(); // llamados polimórficos`

 **Objeto y Clase:** Una clase es una plantilla de código que define la estructura y comportamiento, mientras que un objeto es una instancia concreta de esa clase que vive en memoria y contiene datos reales.  
**Ejemplo aplicado:**  
`particles.push_back(new RisingParticle(…)); // creación de un objeto`

 **Objeto en memoria con herencia:** Cuando se crea un objeto derivado, primero se almacenan en memoria los atributos de la clase base, luego los de la derivada, y si hay métodos virtuales, también se incluye un puntero a la tabla virtual de funciones (vtable).  
**Ejemplo aplicado:**  
`class CircularExplosion : public ExplosionParticle { … }; // hereda estructura en memoria`
