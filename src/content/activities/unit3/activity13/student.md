```
#include <iostream>
#include <string>

using namespace std;

class Mascota {
private:
    string nombre;
    int edad;
    string tipo;

    static int contadorMascotas; // Variable estática

public:
    // Constructor
    Mascota(string n, int e, string t) : nombre(n), edad(e), tipo(t) {
        contadorMascotas++;
        cout << "Constructor llamado para: " << nombre << endl;
    }

    // Destructor
    ~Mascota() {
        cout << "Destructor llamado para: " << nombre << endl;
    }

    void mostrarInfo() {
        cout << "Nombre: " << nombre << ", Edad: " << edad << ", Tipo: " << tipo << endl;
    }

    void actualizarEdad(int nuevaEdad) {
        edad = nuevaEdad;
    }

    static void mostrarContador() {
        cout << "Total de mascotas creadas: " << contadorMascotas << endl;
    }

    // Paso por valor
    void duplicarEdadPorValor(int edad) {
        edad *= 2;
        cout << "Edad dentro (por valor): " << edad << endl;
    }

    // Paso por referencia
    void duplicarEdadPorReferencia(int &edad) {
        edad *= 2;
        cout << "Edad dentro (por referencia): " << edad << endl;
    }
};

// Inicializar variable estática
int Mascota::contadorMascotas = 0;

int main() {
    // Objeto en el stack
    Mascota mascota1("Luna", 3, "Perro");
    mascota1.mostrarInfo();

    // Objeto en el heap
    Mascota* mascota2 = new Mascota("Michi", 2, "Gato");
    mascota2->mostrarInfo();

    // Paso de parámetros
    int edadTest = 5;
    mascota1.duplicarEdadPorValor(edadTest);
    cout << "Edad fuera (por valor): " << edadTest << endl;

    mascota1.duplicarEdadPorReferencia(edadTest);
    cout << "Edad fuera (por referencia): " << edadTest << endl;

    // Contador de mascotas
    Mascota::mostrarContador();

    // Liberar memoria en el heap
    delete mascota2;

    return 0;
}
```
## ✅ Explicación de los Conceptos Aplicados

| **Concepto**               | **Aplicación en el ejemplo**                                                                 |
|---------------------------|----------------------------------------------------------------------------------------------|
| **Clases y objetos**       | Clase `Mascota` con atributos y métodos. Objetos creados en `main`.                         |
| **Paso por valor**         | Método `duplicarEdadPorValor` demuestra que el valor original no cambia.                   |
| **Paso por referencia**    | Método `duplicarEdadPorReferencia` modifica el valor original gracias a la referencia.     |
| **Constructores y destructores** | Se imprimen mensajes al crear y destruir objetos.                                |
| **Métodos y atributos**    | `mostrarInfo`, `actualizarEdad`, y los atributos `nombre`, `edad`, `tipo`.                 |
| **Objetos en stack y heap**| `mascota1` se crea en el stack, `mascota2` con `new` está en el heap.                      |
| **Punteros y referencias** | `mascota2` es un puntero, se accede con `->`. Se usa `&` en paso por referencia.           |
| **Variables estáticas**    | `contadorMascotas` cuenta cuántas instancias se crean, es compartida por todos.           |
| **Depuración de programas**| Se usan mensajes y `cout` para seguir el flujo de ejecución y analizar cambios.            |

## ✅ Análisis Detallado de la Memoria

| **Elemento**                  | **Segmento de Memoria**             | **Descripción**                                                                 |
|------------------------------|-------------------------------------|---------------------------------------------------------------------------------|
| `mascota1`                   | Stack                               | Objeto creado directamente en el `main`, vive hasta que la función termine.     |
| `mascota2`                   | Heap                                | Se reserva con `new`, debe ser liberado con `delete`.                          |
| `edadTest`                   | Stack                               | Variable local usada para probar paso de parámetros.                           |
| `contadorMascotas`          | Segmento de datos estáticos         | Variable estática global de clase, persiste durante toda la ejecución.         |
| Atributos internos de `Mascota` | Parte del objeto (Stack o Heap) | Depende de dónde se declare el objeto.                                         |
| Métodos de clase             | Segmento de código                  | El código de las funciones se guarda en el segmento de texto/código.           |
