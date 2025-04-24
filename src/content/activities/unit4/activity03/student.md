## App.cpp
**
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0); // Fondo negro al iniciar
}

//--------------------------------------------------------------
void ofApp::update() {
    bgHue += 0.2;
    if (bgHue > 255) bgHue = 0;

    if (ofGetMousePressed()) {
        float brushSize = ofRandom(5, 15);
        ofColor brushColor = ofColor::fromHsb(ofRandom(255), 255, 255);
        float alpha = ofRandom(100, 255);

        traceQueue.add(ofGetMouseX(), ofGetMouseY(), brushSize, brushColor, alpha);
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    ofColor topColor, bottomColor;
    topColor.setHsb(bgHue, 150, 240);
    bottomColor.setHsb(fmod(bgHue + 128, 255), 150, 240);

    ofBackgroundGradient(topColor, bottomColor, OF_GRADIENT_LINEAR);

    StrokeNode* current = traceQueue.head;
    int index = 0;
    while (current) {
        float fadeAlpha = ofMap(index, 0, traceQueue.limit, 50, 255);
        ofSetColor(current->color, fadeAlpha);
        ofDrawCircle(current->x, current->y, current->radius);
        current = current->next;
        index++;
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        traceQueue.clearAll();
    } else if (key == 'a') {
        traceQueue.limit = (traceQueue.limit == 50) ? 100 : 50;
    }
}
## App.h
#pragma once
#include "ofMain.h"

// Estructura de un elemento de la cola
struct StrokeNode {
    float x, y;
    float radius;
    ofColor color;
    float alpha;
    StrokeNode* next;

    StrokeNode(float _x, float _y, float _radius, ofColor _color, float _alpha)
        : x(_x), y(_y), radius(_radius), color(_color), alpha(_alpha), next(nullptr) {}
};

// Cola personalizada (FIFO) para trazos
class StrokeQueue {
public:
    StrokeNode* head;
    StrokeNode* tail;
    int currentSize;
    int limit;

    StrokeQueue(int maxElements);
    ~StrokeQueue();

    void add(float x, float y, float radius, ofColor color, float alpha);
    void remove();
    void clearAll();
    bool isEmpty() const;
    void render() const;
};

// Constructor
StrokeQueue::StrokeQueue(int maxElements)
    : head(nullptr), tail(nullptr), currentSize(0), limit(maxElements) {}

// Destructor
StrokeQueue::~StrokeQueue() {
    clearAll();
}

// Agrega un nuevo trazo a la cola
void StrokeQueue::add(float x, float y, float radius, ofColor color, float alpha) {
    StrokeNode* node = new StrokeNode(x, y, radius, color, alpha);
    if (tail) {
        tail->next = node;
    } else {
        head = node;
    }
    tail = node;
    currentSize++;

    if (currentSize > limit) {
        remove();
    }
}

// Elimina el trazo más antiguo
void StrokeQueue::remove() {
    if (!head) return;
    StrokeNode* oldHead = head;
    head = head->next;
    if (!head) {
        tail = nullptr;
    }
    delete oldHead;
    currentSize--;
}

// Vacía todos los trazos
void StrokeQueue::clearAll() {
    while (head) {
        remove();
    }
}

// Verifica si la cola está vacía
bool StrokeQueue::isEmpty() const {
    return head == nullptr;
}

// Clase principal de la aplicación
class ofApp : public ofBaseApp {
public:
    StrokeQueue traceQueue;
    float bgHue = 0;

    ofApp() : traceQueue(50) {} // Límite de elementos en la cola

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};
#  Reporte de Depuración y Pruebas – Proyecto Cola de Trazos (StrokeQueue)

##  1. Reporte de Depuración en Visual Studio

###  Objetivo:
Verificar el correcto funcionamiento de la estructura `StrokeQueue` y comprobar que los elementos se encolan y dibujan correctamente cuando se mantiene presionado el mouse.

---

###  Herramientas utilizadas:
- **Visual Studio 2022**
- **OpenFrameworks 0.12+**
- **Modo de compilación:** Debug

---

###  Puntos de interrupción y observaciones:

####  **Punto de interrupción 1:**
- **Ubicación:** `ofApp::update()` → dentro del bloque `if (ofGetMousePressed())`
- **Objetivo:** Comprobar que los valores aleatorios (`brushSize`, `brushColor`, `alpha`) se generan correctamente.
- **Qué se inspeccionó:**
  - `brushSize`: entre 5 y 15
  - `brushColor`: color con HSB aleatorio
  - `alpha`: entre 100 y 255
  - `traceQueue.tail`: apuntando al nuevo nodo

####  **Punto de interrupción 2:**
- **Ubicación:** `StrokeQueue::add(...)`
- **Objetivo:** Confirmar que los nodos se insertan correctamente y se actualiza `tail`.
- **Inspección:**
  - Nodo creado exitosamente
  - `currentSize` incrementado
  - `remove()` llamado si el límite se supera

####  **Punto de interrupción 3:**
- **Ubicación:** `ofApp::draw()` → dentro del loop `while (current)`
- **Objetivo:** Verificar recorrido y visualización de la cola
- **Qué se inspeccionó:**
  - Cada nodo se dibuja
  - La opacidad se ajusta con `ofMap`
  - El índice `index` se incrementa correctamente

---

###  Resultados observados:
- Trazos encolados correctamente en tiempo real
- Gradiente de fondo se actualiza con `bgHue`
- Cola respeta el límite máximo de nodos
- Las teclas `'a'` y `'c'` modifican comportamiento como se esperaba

---

##  2. Lista de Pruebas Realizadas

| # | Prueba                                                         | Entrada / Acción                             | Resultado Esperado                            | Resultado Obtenido                             | Estado  |
|---|----------------------------------------------------------------|----------------------------------------------|------------------------------------------------|------------------------------------------------|---------|
| 1 | Encolar nodo al presionar clic                                 | Mouse presionado                             | Se añade un nuevo círculo en la posición       | ✅ Nodo añadido y visible                       | ✅ Aprobado |
| 2 | Opacidad gradual en los trazos                                 | Cola con múltiples nodos                     | Círculos con opacidad ascendente hacia el final| ✅ Comportamiento confirmado visualmente        | ✅ Aprobado |
| 3 | Gradiente dinámico de fondo                                    | Esperar varios segundos                      | Cambia el color del fondo                      | ✅ Color cambia suavemente                      | ✅ Aprobado |
| 4 | Borrar trazos con tecla `'c'`                                  | Presionar tecla `'c'`                        | Todos los nodos se eliminan de la pantalla     | ✅ Pantalla sin trazos                          | ✅ Aprobado |
| 5 | Alternar tamaño máximo de cola con tecla `'a'`                 | Presionar `'a'` varias veces                 | Cambia entre 50 y 100 nodos                    | ✅ Límite se actualiza correctamente            | ✅ Aprobado |
| 6 | Límite de cola respetado                                       | Dibujar más de 50 o 100 trazos               | Se eliminan los más antiguos                   | ✅ FIFO correctamente aplicado                  | ✅ Aprobado |
| 7 | Cola vacía no lanza errores                                    | Aplicación sin interacción                   | No se deben generar errores                    | ✅ Sin errores en consola                       | ✅ Aprobado |

---


