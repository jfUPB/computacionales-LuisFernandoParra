# Actividad 5

##  Descripción del Proyecto

**“Jardín de Partículas Emocionales”** es una experiencia visual interactiva en la que el usuario cultiva un jardín abstracto lleno de partículas con emociones. Al mover el mouse o presionar teclas, el usuario crea partículas con diferentes comportamientos y colores. El jardín cambia de estado automáticamente cada ciertos segundos o mediante la interacción, alterando la forma en la que las partículas se comportan (viento, calma, crecimiento). Se aplican tres patrones de diseño: **Observer**, **Factory Method** y **State** para organizar la lógica del sistema.

---
## OffApp.H
```
#pragma once

#include "ofMain.h"
#include <vector>
#include <memory>

// Forward declarations
class Particle;
class EmotionState;

// ---------- OBSERVER ----------
class EventListener {
public:
    virtual void onNotify(std::string event) = 0;
};

// ---------- SUBJECT ----------
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

// ---------- PARTICULAS ----------
class Particle {
public:
    ofVec2f pos;
    ofVec2f vel;
    ofColor color;

    Particle(ofVec2f p, ofVec2f v, ofColor c) : pos(p), vel(v), color(c) {}

    virtual void update() {
        pos += vel;
    }

    virtual void draw() {
        ofSetColor(color);
        ofDrawCircle(pos, 4);
    }

    virtual ~Particle() {}
};

// ---------- FACTORY ----------
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

// ---------- STATE INTERFACE ----------
class EmotionState {
public:
    virtual void generate(std::vector<std::shared_ptr<Particle>>& particles) = 0;
    virtual std::string getName() = 0;
    virtual ~EmotionState() {}
};

// ---------- CONCRETE STATES ----------
class HappyState : public EmotionState {
public:
    void generate(std::vector<std::shared_ptr<Particle>>& particles) override {
        for (int i = 0; i < 5; i++) {
            particles.push_back(ParticleFactory::createParticle("happy", ofVec2f(ofRandomWidth(), ofRandomHeight())));
        }
    }
    std::string getName() override { return "happy"; }
};

class SadState : public EmotionState {
public:
    void generate(std::vector<std::shared_ptr<Particle>>& particles) override {
        for (int i = 0; i < 5; i++) {
            particles.push_back(ParticleFactory::createParticle("sad", ofVec2f(ofRandomWidth(), 0)));
        }
    }
    std::string getName() override { return "sad"; }
};

class AngryState : public EmotionState {
public:
    void generate(std::vector<std::shared_ptr<Particle>>& particles) override {
        for (int i = 0; i < 5; i++) {
            particles.push_back(ParticleFactory::createParticle("angry", ofVec2f(ofRandomWidth(), ofRandomHeight())));
        }
    }
    std::string getName() override { return "angry"; }
};

// ---------- OFAPP ----------
class ofApp : public ofBaseApp, public EventListener, public EventSubject {

public:
    void setup();
    void update();
    void draw();
    void keyPressed(int key);

    // Partículas
    std::vector<std::shared_ptr<Particle>> particles;

    // Estado
    std::shared_ptr<EmotionState> currentState;

    // Estados posibles
    std::shared_ptr<HappyState> happyState;
    std::shared_ptr<SadState> sadState;
    std::shared_ptr<AngryState> angryState;

    // Observer
    void onNotify(std::string event) override;

    // Cambio de estado
    void setState(std::shared_ptr<EmotionState> newState);
};
```
OffApp.cpp
```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    ofBackground(20);
    ofSetFrameRate(60);

    // Crear estados
    happyState = std::make_shared<HappyState>();
    sadState = std::make_shared<SadState>();
    angryState = std::make_shared<AngryState>();

    // Estado inicial
    setState(happyState);

    // Registro como listener de sí mismo (Subject)
    addListener(this);
}

//--------------------------------------------------------------
void ofApp::update(){
    // Generar nuevas partículas con el estado actual
    currentState->generate(particles);

    // Actualizar partículas
    for (auto& p : particles) {
        p->update();
    }

    // Limitar tamaño de vector
    if (particles.size() > 500) {
        particles.erase(particles.begin(), particles.begin() + 5);
    }
}

//--------------------------------------------------------------
void ofApp::draw(){
    ofSetColor(255);
    ofDrawBitmapString("Estado actual: " + currentState->getName(), 20, 20);

    for (auto& p : particles) {
        p->draw();
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key){
    if (key == 'h') {
        notify("happy");
    } else if (key == 's') {
        notify("sad");
    } else if (key == 'a') {
        notify("angry");
    }
}

//--------------------------------------------------------------
void ofApp::onNotify(std::string event) {
    if (event == "happy") {
        setState(happyState);
    } else if (event == "sad") {
        setState(sadState);
    } else if (event == "angry") {
        setState(angryState);
    }
}

//--------------------------------------------------------------
void ofApp::setState(std::shared_ptr<EmotionState> newState) {
    currentState = newState;
    ofLogNotice() << "Estado cambiado a: " << currentState->getName();
}
```

---


