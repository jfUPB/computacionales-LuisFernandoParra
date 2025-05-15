# ACTIVIDAD 2

## ¿Para qué sirve el patrón Observer?

El patrón Observer se utiliza para permitir que varios objetos reciban una notificación cuando ocurre un evento, sin que el emisor del evento necesite conocer los detalles de los objetos que lo reciben.  
**¿Qué problema resuelve?**  
Evita una conexión rígida entre componentes, lo que hace que el código sea más fácil de modificar, mantener y ampliar.

## ¿Quién representa a quién?

- **Observer**: es la interfaz que define el método `onNotify()`.
- **Particle**: actúa como un `ConcreteObserver` ya que implementa `onNotify()` y responde a los eventos.
- **Subject**: mantiene una lista de observadores y contiene el método `notify()`.
- **ofApp**: representa al `ConcreteSubject`, ya que es quien invoca `notify()` cuando se presiona una tecla.

## Diagrama del patrón Observer en este contexto

```
       +-------------+
       |   Subject   |  <- Clase base que maneja observadores
       +-------------+
       | notify()    |
       | addObserver |
       +------^------+
              |
       Herencia hacia
              |
          +--------+
          | ofApp  |  <- Genera los eventos
          +--------+

              |
         notify("r")
              ↓
      +----------------+
      |   Observer     |  <- Interfaz común
      +----------------+
      | onNotify() = 0 |
              ↑
       Herencia desde
              |
        +------------+
        | Particle   |  <- Reacciona al evento recibido
        +------------+
        | setState() |
```

## ¿Qué sucede al presionar la tecla ‘r’?

Cuando se presiona la tecla `r`, el método `keyPressed()` en `ofApp` llama a `notify("repel")`.  
Luego, `notify()` ejecuta `onNotify("repel")` en cada instancia de partícula registrada.  
Cada partícula, al recibir ese mensaje, cambia su estado interno a `RepelState`.  
Durante cada actualización (`update()`), la partícula ejecuta `RepelState::update()`, lo que hace que se aleje del cursor del mouse.

## Beneficios de usar el patrón Observer en este proyecto

- Permite un código más estructurado y fácil de leer.  
- Facilita la inclusión o eliminación de partículas sin afectar otras partes del programa.
