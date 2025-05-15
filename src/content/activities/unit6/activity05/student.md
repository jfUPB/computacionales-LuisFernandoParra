# Actividad

##  Descripción del Proyecto

**“Jardín de Partículas Emocionales”** es una experiencia visual interactiva en la que el usuario cultiva un jardín abstracto lleno de partículas con emociones. Al mover el mouse o presionar teclas, el usuario crea partículas con diferentes comportamientos y colores. El jardín cambia de estado automáticamente cada ciertos segundos o mediante la interacción, alterando la forma en la que las partículas se comportan (viento, calma, crecimiento). Se aplican tres patrones de diseño: **Observer**, **Factory Method** y **State** para organizar la lógica del sistema.

---

##  Diseño con Patrones

###  Observer

- **Sujeto:** `InputManager`
- **Observadores:** `Garden`, `Logger`, `UI`
- **Evento observado:** Entrada del usuario (clic de mouse, teclas)
- **Comportamiento:** Cuando el usuario interactúa, el `InputManager` notifica a todos los observadores.

```cpp
// Observer.h
class Observer {
public:
    virtual void onNotify(string event) = 0;
};

// InputManager.h
class InputManager {
    vector<Observer*> observers;
public:
    void addObserver(Observer* o) { observers.push_back(o); }
    void notify(string event) {
        for (auto o : observers) o->onNotify(event);
    }
};
```

**Prueba:**
```cpp
inputManager.notify("mouseClicked");
// Esperado: garden recibe el evento y crea partículas.
```

---

###  Factory Method

- **Clase Factory:** `ParticleFactory`
- **Productos:** `HappyParticle`, `AngryParticle`, `SadParticle`
- **Motivación:** Desacoplar la creación de partículas del resto de la lógica.

```cpp
// ParticleFactory.h
class ParticleFactory {
public:
    static shared_ptr<Particle> createParticle(string type, ofVec2f pos) {
        if(type == "happy") return make_shared<HappyParticle>(pos);
        if(type == "angry") return make_shared<AngryParticle>(pos);
        if(type == "sad") return make_shared<SadParticle>(pos);
        return nullptr;
    }
};
```

**Prueba:**
```cpp
auto p = ParticleFactory::createParticle("happy", {100, 100});
cout << "Tipo: " << p->getType() << endl;
```

---

###  State

- **Contexto:** `Garden`
- **Estados concretos:**
  - `CalmState` (movimiento suave, colores pasteles)
  - `WindyState` (movimiento disperso y rápido)
  - `GrowthState` (más generación de partículas)
- **Motivación:** Encapsular comportamientos del jardín en clases de estado.

```cpp
// GardenState.h
class GardenState {
public:
    virtual void update(Garden* garden) = 0;
};

// CalmState.h
class CalmState : public GardenState {
public:
    void update(Garden* garden) override {
        garden->setWind(0.1);
        garden->setColorPalette("soft");
    }
};
```

```cpp
// Garden.h (fragmento)
void setState(GardenState* newState) {
    if(state) delete state;
    state = newState;
}
```

**Prueba:**
```cpp
garden.setState(new WindyState());
garden.update();
// Se observa cambio en color, velocidad, log del estado.
```

---

##  Integración

1. El usuario hace clic → `InputManager` notifica a `Garden`.
2. `Garden::onNotify()` invoca `ParticleFactory` para crear una nueva partícula del tipo actual.
3. El comportamiento de la partícula depende del estado actual del `Garden`.

```cpp
void Garden::onNotify(string event) {
    if(event == "mouseClicked") {
        auto p = ParticleFactory::createParticle(currentEmotion, mousePos);
        particles.push_back(p);
    }
}
```

---

##  Testing y Depuración

Durante el desarrollo se aplicaron pruebas básicas para cada componente:

- `std::cout` y `ofLogNotice()` para verificar cambios de estado y creación de partículas.
- Logs de notificaciones en consola para validar el patrón Observer.
- Breakpoints y seguimiento de objetos para ver estados internos.

Ejemplo:
```cpp
cout << "Estado actual: Calm" << endl;
garden.setState(new GrowthState());
cout << "Nuevo estado aplicado" << endl;
```

---

##  Interactividad

- Mouse click → emite partículas.
- Teclas (1, 2, 3) → cambian emoción: feliz, enojado, triste.
- Cada 10 segundos, el jardín cambia de estado automáticamente.
- Las partículas reaccionan visualmente según el estado: velocidad, dispersión y color.

---


---

##  Desafíos y Soluciones

**Problema:** Integrar correctamente los tres patrones sin acoplamiento excesivo.  
**Solución:** Modularización estricta: cada patrón en su archivo, clara responsabilidad por clase.

**Problema:** Sincronizar cambios de estado con el tiempo.  
**Solución:** Uso de `ofGetElapsedTimef()` y lógica condicional simple para cambiar de estado.

**Problema:** Verificar visualmente los efectos.  
**Solución:** Colores, tamaños, trayectorias y logs diferenciados por cada estado y tipo de partícula.

---


