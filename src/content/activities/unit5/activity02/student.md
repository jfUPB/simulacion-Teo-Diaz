# Ejemplo 4.2

### Codigo fuente:
``` js
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

let particles = []; // Declaración del arreglo de partículas

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);

  particles.push(new Particle(width / 2, 20));

  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();

    if (particle.isDead()) {
      particles.splice(i, 1);
    }
  }
}
```
La gestión de **creación y desaparición de partículas** sigue un flujo controlado dentro del `draw()`:

1. **Creación de partículas**:
   - En cada fotograma (`draw()`), se genera una nueva partícula en `particles.push(new Particle(width / 2, 20));`.
   - Esto significa que el número de partículas puede aumentar indefinidamente si no se eliminan.

2. **Desaparición de partículas**:
   - Cada partícula tiene una propiedad `lifespan`, que comienza en `255` y disminuye en `this.lifespan -= 2;` en cada fotograma.
   - Cuando `lifespan` cae por debajo de `0`, `isDead()` devuelve `true`.
   - Se elimina del array de partículas con `particles.splice(i, 1);`.

### **Gestión de memoria en la simulación**
La memoria se maneja mediante la actualización y eliminación eficiente de partículas:
- **Evita el crecimiento descontrolado de memoria**: Como se eliminan partículas muertas, el arreglo `particles` no crece indefinidamente.
- **Cada objeto tiene una vida útil**: Al reducir `lifespan`, las partículas no permanecen en memoria más tiempo del necesario.
- **Uso de `splice()` para liberación de memoria**: Se eliminan de `particles`, permitiendo que JavaScript las recoleccione como basura (`garbage collection`).

## Codigo editado:
```js
let particles = [];

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-2, 2), random(-2, 0));
    this.lifespan = 255.0;
    this.color = color(random(255), random(255), random(255), this.lifespan); // Color aleatorio
    this.size = random(5, 15); // Tamaño aleatorio
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(this.color);
    circle(this.position.x, this.position.y, this.size); // Usa tamaño aleatorio
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  particles.push(new Particle(width / 2, 20));

  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      particles.splice(i, 1);
    }
  }
}
```

# Ejemplo 4.4

### Codigo fuente:
``` js
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

let emitters = [];

function setup() {
  createCanvas(640, 240);
  createP("Click to add particle systems");
}

function draw() {
  background(255);
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
}

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}
```
## Codigo editado
```js
class Particle {
  constructor(position) {
    this.position = position.copy();
    this.velocity = p5.Vector.random2D().mult(random(1, 3));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0;
  }

  run() {
    this.applyForce(createVector(0, 0.05)); // Simulación de gravedad
    this.update();
    this.show();
  }
}

class Emitter {
  constructor(position) {
    this.origin = position.copy();
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin));
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

let emitters = [];

function setup() {
  createCanvas(640, 240);
  createP("Click to add particle systems");
}

function draw() {
  background(255);
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
}

function mousePressed() {
  emitters.push(new Emitter(createVector(mouseX, mouseY)));
}
```
### **Gestión de Creación y Desaparición de Partículas**
1. **Creación de Partículas:**
   - Cada `Emitter` tiene un método `addParticle()`, que añade nuevas partículas a su lista (`this.particles`).
   - En cada iteración de `draw()`, se llama a `addParticle()`, generando partículas continuamente en la posición del emisor.

2. **Desaparición de Partículas:**
   - Cada `Particle` tiene una propiedad `lifespan` que disminuye en cada actualización (`update()`).
   - Cuando `lifespan` llega a cero, `isDead()` devuelve `true`.
   - En el método `run()` del `Emitter`, se revisa cada partícula: si está "muerta", se elimina con `splice()` del arreglo.

---

### **Gestión de Memoria en la Simulación**
- **Almacenamiento de Objetos:** Cada partícula es un objeto independiente almacenado en la memoria. A medida que se crean nuevas partículas, se ocupa más espacio en la RAM.
- **Eliminación de Partículas:** Se usa `splice(i, 1)` para eliminar partículas muertas, lo que reduce la carga en la memoria.
- **Fragmentación y Optimización:** En lugar de usar `splice()`, podrías usar `filter()`, que evita la reestructuración del arreglo y puede ser más eficiente:
  ```javascript
  this.particles = this.particles.filter(particle => !particle.isDead());
  ```
- **Uso de `p5.Vector`:** Este enfoque optimiza cálculos matemáticos y reduce la carga computacional en comparación con manejar coordenadas manualmente.
