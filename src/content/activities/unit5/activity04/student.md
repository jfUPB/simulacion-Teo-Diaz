### ✅ 1. **Gestión de creación, desaparición y memoria en sistemas de partículas**
- **Creación**: En cada iteración del `draw()`, se genera una nueva partícula y se añade al arreglo `particles.push(new Particle(x, y))`. Esto garantiza un flujo constante de partículas en la simulación.
- **Desaparición**: Cada partícula tiene un tiempo de vida (`lifespan`). Cuando su valor cae por debajo de un umbral (`isDead()` devuelve `true`), se elimina usando `splice()`.
- **Gestión de memoria**: La eliminación de partículas evita que el arreglo crezca indefinidamente, y el **garbage collector** de JavaScript libera memoria automáticamente al eliminar objetos.

---

### ✅ 2. **Aplicación del marco Motion 101 en los sistemas de partículas**
El **Motion 101** establece un enfoque basado en:
- **Posición**: Representada por `this.position`, que se actualiza en cada iteración del ciclo de vida de la partícula.
- **Velocidad**: `this.velocity` cambia constantemente en función de fuerzas aplicadas.
- **Aceleración**: `this.acceleration` gestiona cambios de velocidad y dirección en respuesta a fuerzas externas.

Este marco se traduce en simulaciones fluidas donde los objetos en movimiento siguen principios naturales.

---

### ✅ 3. **Aplicación de fuerzas externas en el sistema de partículas**
Las fuerzas en el sistema de partículas se aplican mediante:
- **Gravedad**: `let gravity = createVector(0, 0.05);` afecta el desplazamiento en el eje Y, simulando caída progresiva.
- **Fuerzas de aceleración**: Se suman a `this.velocity` y alteran la dirección/magnitud del movimiento.
- **Modelado**: Las fuerzas externas se representan con vectores (`applyForce(force)`), lo que permite simular viento, gravedad o empujes direccionales de manera dinámica.

---

### ✅ 4. **Herencia y polimorfismo en sistemas de partículas**
Para mejorar la flexibilidad y reutilización del código, se pueden aplicar estos conceptos:
- **Herencia**: Se puede crear una clase base `Particle` y luego extenderla (`class SpecialParticle extends Particle`) para agregar comportamientos específicos.
- **Polimorfismo**: Métodos como `show()` pueden ser redefinidos en las clases derivadas (`SpecialParticle` podría dibujar partículas con formas diferentes, pero respetando la estructura de `Particle`).

Estos principios permiten crear múltiples tipos de partículas dentro del mismo sistema sin duplicar código.
