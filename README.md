# parcial_estructura-2

# ListVerse

Gestor de categorías de entretenimiento (videojuegos, música y streaming) desarrollado en la asignatura **Estructuras de Datos Lineales**.

## Justificación y dominio del problema (Parcial C2, Punto 1)

ListVerse gestiona categorías de entretenimiento mediante matrices de prioridad y listas. Los usuarios agregan, reproducen, reservan o cancelan elementos de su catálogo. Esto genera dos necesidades de acceso distintas:

1. Deshacer lo último que se hizo.
2. Atender las solicitudes en el orden en que llegaron.

## Pila (LIFO): historial y deshacer

**Necesidad real.** Revertir la acción más reciente: una calificación, un cambio de prioridad de categoría o un elemento movido en la matriz.

**Por qué LIFO.** Deshacer en orden cronológico inverso solo tiene sentido si la última acción es la primera en salir. Con una cola se desharía la acción más antigua y el estado quedaría inconsistente.

**Qué se guarda en cada `push`.** La tupla `(fila, columna, estadoAnterior)`, para que `pop()` restaure la matriz exactamente a como estaba.

**Por qué no es forzada.** Si el sistema permitiera revertir una acción intermedia, se rompería la coherencia de las demás. Por eso solo se expone la cima.

**Interfaz del TAD:** `push()`, `pop()`, `peek()`, `isEmpty()`, `size()`.

## Cola (FIFO): solicitudes en orden de llegada

**Necesidad real.** Las solicitudes (reproducir, agregar a una categoría, reservar un contenido) llegan de forma concurrente y deben atenderse en el orden en que llegaron.

**Por qué FIFO.** Atender primero al que llegó primero es lo justo. Si se atendiera al último en llegar, el primero podría esperar indefinidamente (inanición).

**Flujo.** `enqueue()` al llegar y `dequeue()` al procesar. Lo procesado se registra en la lista doblemente enlazada del Corte 1.

**Interfaz del TAD:** `enqueue()`, `dequeue()`, `peek()`, `isEmpty()`, `size()`.

## Resumen

| Estructura | Problema que resuelve | Criterio de acceso | Dato que maneja |
|---|---|---|---|
| Pila | Deshacer acciones | El último en entrar es el primero en salir | Cambios sobre la matriz |
| Cola | Atender solicitudes en orden | El primero en entrar es el primero en salir | Solicitudes pendientes |

## ¿Por qué no un `ArrayList`?

El problema solo requiere acceso por un extremo. Exponer más operaciones (`get(i)`, recorridos con `for`) rompería el contrato del Tipo Abstracto de Datos.
