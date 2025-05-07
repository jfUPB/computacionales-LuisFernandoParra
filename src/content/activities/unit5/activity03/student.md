##  Actividad 03 – Aplica lo aprendido


---

###  Desarrollo

#### 1. Nuevos Tipos de `Particle`

**a) `FadingParticle`: se desvanece con el tiempo**
```cpp
class FadingParticle : public Particle {
public:
    float alpha;

    FadingParticle(ofVec2f pos) {
        position = pos;
        velocity = ofVec2f(ofRandom(-1, 1), ofRandom(-1, 1));
        alpha = 255;
    }

    void update(float dt) override {
        position += velocity * dt;
        alpha -= 100 * dt;
        if (alpha < 0) alpha = 0;
    }

    void draw() override {
        ofSetColor(255, 255, 255, alpha);
        ofDrawCircle(position, 3);
    }
};
```
### b) SpinningParticle: gira alrededor de un punto central
```
class SpinningParticle : public Particle {
public:
    float angle;
    float radius;
    ofVec2f center;

    SpinningParticle(ofVec2f c) {
        center = c;
        angle = ofRandom(TWO_PI);
        radius = ofRandom(10, 50);
    }

    void update(float dt) override {
        angle += 1.5 * dt;
        position.x = center.x + radius * cos(angle);
        position.y = center.y + radius * sin(angle);
    }

    void draw() override {
        ofSetColor(0, 255, 0);
        ofDrawCircle(position, 3);
    }
};
```
## 2. Nuevo modo de explosión: SpiralExplosion
```
class SpiralExplosion : public BaseExplosion {
public:
    SpiralExplosion(ofVec2f origin, std::vector<Particle*>& container) {
        for (int i = 0; i < 30; ++i) {
            auto* p = new SpinningParticle(origin);
            container.push_back(p);
        }
    }
};
```
###  Lista de pruebas realizadas

| Prueba | Qué se intentó probar | Resultado esperado | Resultado obtenido | ¿Funcionó? |
|--------|------------------------|---------------------|---------------------|------------|
| 1 | Verificar `FadingParticle` | Partícula se desvanece con el tiempo | Alfa disminuye hasta 0 |  Sí |
| 2 | Verificar `SpinningParticle` | Movimiento circular estable | Trayectoria circular fluida |  Sí |
| 3 | Crear `SpiralExplosion` | 30 partículas girando desde el centro | Movimiento en espiral |  Sí |
| 4 | Polimorfismo con `update()` | Ejecutar versión correcta del método | Se llama `update()` adecuado por tipo |  Sí |
| 5 | Depurador: jerarquía y _vtable | Ver campos y punteros únicos | Confirmado por Visual Studio | Sí |

