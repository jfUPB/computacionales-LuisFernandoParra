#  Bitácora de Exploración - Programación Orientada a Objetos en C++

##  Objeto en memoria: clase `ofApp`

**Hipótesis**: Espero ver en memoria una estructura con campos que reflejan los métodos y atributos definidos en la clase `ofApp`, especialmente el vector `particles`.

**Evidencia (captura de pantalla)**: [Pegar captura aquí]

**Observaciones**:
- El depurador muestra que `ofApp` es una instancia que hereda de `ofBaseApp`.
- El vector `particles` apunta a direcciones de memoria donde están almacenadas instancias de `Particle` o derivadas.
- Solo está en memoria mientras corre la app, como se esperaba.

**Conclusión**:
- Un objeto en memoria contiene punteros a funciones y estructuras, pero la información está organizada por jerarquía de herencia.
- El vector contiene punteros a objetos polimórficos, lo cual será importante más adelante.

---

##  Objeto en memoria: clase `CircularExplosion`

**Modificación realizada**: Forzar la creación de una instancia de `CircularExplosion` al inicio del programa.

**Evidencia (captura de pantalla)**: [Pegar captura aquí]

**Observaciones**:
- En el panel de `Auto` o `Locals`, se observa que `CircularExplosion` contiene primero un `ExplosionParticle`, que a su vez contiene un `Particle`.
- En la ventana de memoria, los campos están alineados secuencialmente según la jerarquía.
- También se detecta un puntero `vtable`.

**Conclusión**:
- La memoria refleja claramente la jerarquía de clases: los campos de `Particle` aparecen primero, luego los de `ExplosionParticle` y finalmente los de `CircularExplosion`.

---

##  Observación de la `_vtable` de `CircularExplosion`

**Evidencia (captura de pantalla)**: [Pegar captura aquí]

**Observaciones**:
- La `_vtable` contiene direcciones de funciones virtuales sobrescritas por `CircularExplosion`.
- Muestra claramente la sobrescritura de métodos como `update()` o `draw()`.

**Conclusión**:
- Cada clase que sobrescribe métodos virtuales tendrá su propia tabla con las direcciones actualizadas.
- Esto es esencial para el polimorfismo.

---

##  Observación de la `_vtable` de `StarExplosion`

**Evidencia (captura de pantalla)**: [Pegar captura aquí]

**Comparación con CircularExplosion**:
- Ambas tienen punteros a métodos similares, pero con diferentes direcciones.
- Confirma que cada clase tiene su propia implementación.

**Conclusión**:
- La tabla de funciones virtuales permite seleccionar dinámicamente el método correcto en tiempo de ejecución.

---

##  ¿Para qué sirve la tabla de funciones virtuales?

**Relación con interfaces en C#**:
- En C#, el polimorfismo se implementa con interfaces y clases abstractas.
- En C++, la `_vtable` permite que el programa determine qué función invocar sin importar el tipo declarado.

**Conclusión**:
- La `_vtable` permite el polimorfismo en tiempo de ejecución: diferentes clases pueden comportarse distinto mediante el mismo puntero base.

---

##  Encapsulamiento: experimento con modificadores de acceso

### Código original:
```cpp
class AccessControl {
private:
    int privateVar;
protected:
    int protectedVar;
public:
    int publicVar;
    AccessControl() : privateVar(1), protectedVar(2), publicVar(3) {}
};

int main() {
    AccessControl ac;
    ac.publicVar = 10; // Válido
    // ac.protectedVar = 20; // Error de compilación
    // ac.privateVar = 30; // Error de compilación
}
```

**Conclusión**:
- El compilador impide acceder a campos privados o protegidos desde fuera de la clase.

---

### Experimento violando encapsulamiento en tiempo de ejecución:

```cpp
class MyClass {
private:
    int secret1;
    float secret2;
    char secret3;
public:
    MyClass(int s1, float s2, char s3) : secret1(s1), secret2(s2), secret3(s3) {}
};

int main() {
    MyClass obj(42, 3.14f, 'A');
    int* ptrInt = reinterpret_cast<int*>(&obj);
    float* ptrFloat = reinterpret_cast<float*>(ptrInt + 1);
    char* ptrChar = reinterpret_cast<char*>(ptrFloat + 1);

    std::cout << *ptrInt << "\n";     // secret1
    std::cout << *ptrFloat << "\n";   // secret2
    std::cout << *ptrChar << "\n";    // secret3
}
```

**Resultado**:
- El programa accede a los campos privados en tiempo de ejecución, lo cual rompe el encapsulamiento.

**Conclusión**:
- El encapsulamiento solo es una garantía en tiempo de compilación, no en tiempo de ejecución.

---

##  ¿Qué es el encapsulamiento?

**Respuesta**:
- Es el principio de ocultar la implementación interna de un objeto y exponer solo lo necesario a través de interfaces públicas.
- Es importante para proteger los datos, reducir errores y facilitar el mantenimiento del código.

---

##  Herencia: análisis de `CircularExplosion`

**Observación**:
- En memoria, el objeto de tipo `CircularExplosion` muestra claramente la herencia de `ExplosionParticle` y `Particle`.

**Conclusión**:
- C++ implementa la herencia colocando en memoria primero los campos de la clase base, luego los de la clase derivada.

---

##  ¿Cómo se implementa la herencia en C++?

**Respuesta**:
- Se implementa organizando en memoria primero la parte base y luego las derivadas.
- Los punteros de clase base pueden apuntar a objetos derivados.

---

##  Herencia múltiple: experimento

```cpp
class A {
public:
    int a = 1;
};

class B {
public:
    int b = 2;
};

class C : public A, public B {
public:
    int c = 3;
};

int main() {
    C obj;
    std::cout << obj.a << ", " << obj.b << ", " << obj.c << "\n";
}
```

**Resultado**:
- El objeto tiene todos los campos de A, B y C.

**Conclusión**:
- C++ permite herencia múltiple y coloca en memoria las clases base según el orden de declaración.

---

##  Polimorfismo: método `update()` en tiempo de ejecución

**Código en `ofApp.cpp`:**
```cpp
for (int i = 0; i < particles.size(); i++) {
    particles[i]->update(dt);
}
```

**Observación con el depurador**:
- El método `update()` invoca diferentes versiones según el tipo real del objeto.

**Conclusión**:
- El polimorfismo permite que objetos derivados se comporten según su tipo real aunque el puntero sea de tipo base.



##  ¿Qué relación existe entre los métodos virtuales y el polimorfismo?

**Respuesta**:
- Los métodos virtuales permiten que una función se defina en una clase base y se sobrescriba en clases derivadas.
- En tiempo de ejecución, se selecciona la versión correcta mediante la tabla de funciones virtuales (_vtable).
- Esto permite que el comportamiento se adapte dinámicamente al tipo real del objeto.

---


