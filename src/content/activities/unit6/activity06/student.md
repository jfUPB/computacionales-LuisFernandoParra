# Actividad 6 – Reflexión sobre el Proyecto

## 1. Patrón Observer en mi proyecto

### ¿En qué parte específica del código implementé el rol de Sujeto (Subject)?

El rol de *Sujeto* lo implementé en la clase EventSubject, que contiene la lógica para registrar y notificar observadores. Esta clase es heredada por ofApp.

```cpp
class EventSubject {
protected:
    std::vector<EventListener*> listeners;
public:
    void addListener(EventListener* l) {
        listeners.push_back(l);
    }
    void notify(std::string event) {
        for (auto& l : listeners) {
            l->onNotify(event);
        }
    }
};
```
## 2. Patrón Factory Method en mi proyecto

### ¿Dónde está definido tu método factory?

El método factory está definido en la clase ParticleFactory, que se encarga de crear partículas con diferentes propiedades dependiendo de la emoción
``` cpp
class ParticleFactory {
public:
    static std::shared_ptr<Particle> createParticle(std::string emotion, ofVec2f pos) {
        if (emotion == "happy") {
            return std::make_shared<Particle>(pos, ofVec2f(ofRandom(-1,1), ofRandom(-1,1)), ofColor::yellow);
        } else if (emotion == "sad") {
            return std::make_shared<Particle>(pos, ofVec2f(0, ofRandom(1,3)), ofColor::blue);
        } else if (emotion == "angry") {
            return std::make_shared<Particle>(pos, ofVec2f(ofRandom(-3,3), ofRandom(-3,3)), ofColor::red);
        } else {
            return std::make_shared<Particle>(pos, ofVec2f(0, 0), ofColor::white);
        }
    }
};
```
### ¿Qué tipos específicos de objetos creaba tu factory?

Crea objetos del tipo Particle, con comportamientos distintos dependiendo del tipo de emoción (posición inicial, velocidad y color).

### ¿Por qué fue beneficioso usar una factory?

Fue beneficioso porque encapsula la lógica de creación en un solo lugar. Esto hace el código más mantenible y flexible. Si quisiera agregar una nueva emoción o cambiar la forma en que se inicializan las partículas, solo tendría que modificar la factory.

### Ejemplo de uso de la factory en código cliente:

Por ejemplo, en HappyState se utiliza la factory para crear partículas felices
``` cpp
void HappyState::generate(std::vector<std::shared_ptr<Particle>>& particles) {
    for (int i = 0; i < 5; i++) {
        particles.push_back(ParticleFactory::createParticle("happy", ofVec2f(ofRandomWidth(), ofRandomHeight())));
    }
}
```
## 3. Patrón State en mi proyecto

¿Qué clase actuó como Contexto?

La clase ofApp actuó como el contexto, ya que contiene el estado actual en currentState.
``` cpp
std::shared_ptr<EmotionState> currentState;
```
Y tiene el método setState():
``` cpp
void ofApp::setState(std::shared_ptr<EmotionState> newState) {
    currentState = newState;
    ofLogNotice() << "Estado cambiado a: " << currentState->getName();
}
```
### ¿Cuáles fueron los ConcreteStates que implementaste?
#### Happy state 
``` cpp
class HappyState : public EmotionState {
public:
    void generate(std::vector<std::shared_ptr<Particle>>& particles) override {
        for (int i = 0; i < 5; i++) {
            particles.push_back(ParticleFactory::createParticle("happy", ofVec2f(ofRandomWidth(), ofRandomHeight())));
        }
    }
    std::string getName() override { return "happy"; }
};
```
#### SadState
``` cpp
class SadState : public EmotionState {
public:
    void generate(std::vector<std::shared_ptr<Particle>>& particles) override {
        for (int i = 0; i < 5; i++) {
            particles.push_back(ParticleFactory::createParticle("sad", ofVec2f(ofRandomWidth(), 0)));
        }
    }
    std::string getName() override { return "sad"; }
};
```
### ¿Por qué decidí que el patrón State era apropiado?

El patrón State fue útil porque cada emoción tenía un comportamiento distinto para generar partículas. Esto evitó el uso de múltiples if o switch, y encapsuló el comportamiento en clases separadas.

## 4. Definiciones Post-Experiencia

### ¿Qué es una clase?

Una clase es una plantilla que define atributos (variables) y métodos (funciones) comunes para un tipo de objeto. Permite organizar el código en componentes reutilizables y estructurados.

### ¿Qué es un objeto?

Un objeto es una instancia concreta de una clase. Contiene datos propios y puede ejecutar comportamientos definidos en su clase. Es la unidad funcional que interactúa en la aplicación.


## 5. Beneficios Estructurales

El uso de los patrones Observer, Factory y State aportó muchas ventajas a la organización y estructura del código:

- Observer permitió desacoplar el origen de eventos (teclado) de la lógica de respuesta (cambio de estado).
- Factory centralizó la creación de partículas, facilitando cambios y mantenimiento.
- State encapsuló comportamientos diferentes por emoción, haciendo el código más claro, extensible y modular.

Gracias a estos patrones, el código fue más fácil de entender, modificar y extender. La separación de responsabilidades permitió escalar el proyecto sin generar caos en el código base.
