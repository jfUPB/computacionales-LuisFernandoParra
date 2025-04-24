# Análisis de una LinkedList en C++

## ¿Qué pasaría si el objeto de la clase LinkedList no tuviera el puntero a head?  
- **Problema principal**: Pérdida del punto de inicio.  
- **Consecuencias**:  
  - No se podría acceder al primer nodo en el Heap.  
  - La lista quedaría inaccesible, ya que los nodos están enlazados secuencialmente.  

---

## ¿Podrías recorrer la lista?  
- **Respuesta**: No.  
- **Razón**: Sin `head`, no hay referencia para iniciar el recorrido. Los nodos quedarían "aislados" en memoria.  

---

## ¿Qué pasaría si no tuviera el puntero a tail?  
- **Impacto**:  
  - **Inserción ineficiente**: Agregar nodos al final requeriría recorrer toda la lista (O(n)).  
  - **Acceso al último nodo**: Se necesitaría iterar desde `head` hasta encontrar `next == nullptr`.  

---

## ¿Podrías agregar un nuevo nodo al final de la lista?  
**Sí**, pero con complejidad O(n):  
1. Recorrer la lista desde `head` hasta el último nodo (`next == nullptr`).  
2. Enlazar el nuevo nodo al campo `next` del último nodo.  
> ⚠️ **Nota**: Con `tail`, esta operación sería O(1).  

---

## ¿Qué pasaría si no tuviera el entero size? ¿Podrías saber cuántos nodos hay?  
- **Sin `size`**:  
  - No habría acceso directo al número de nodos.  
  - Alternativa: Contar nodos recorriendo la lista desde `head` (O(n)).  
- **Conclusión**: `size` optimiza operaciones que requieren conocer la longitud.  

---

## ¿Por qué es necesario liberar la memoria de los nodos?  
- **Memoria dinámica**: Los nodos persisten en el Heap aunque la lista se destruya.  
- **Riesgo**:  
  - **Memory Leak**: Si no se liberan, ocuparán espacio inútilmente.  
- **Solución**:  
  ```cpp
  // Ejemplo de destructor
  ~LinkedList() {
      Node* current = head;
      while (current != nullptr) {
          Node* next = current->next;
          delete current;
          current = next;
      }
  }
