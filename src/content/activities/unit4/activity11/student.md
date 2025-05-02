### **Concepto**
La obra se basará en **sistemas dinámicos de partículas** que se atraen y repelen entre sí, creando patrones visuales emergentes. Los usuarios podrán interactuar con el sistema modificando las fuerzas con el **mouse** y **teclado**, influyendo en el comportamiento de las partículas en tiempo real.

---

### **Boceto de la idea**  
El concepto inicial consiste en:
- Un conjunto de **partículas** que reaccionan a fuerzas de atracción y repulsión.
- El usuario podrá **alterar la intensidad de las fuerzas** con el teclado.
- Al mover el mouse, se generará una **zona gravitatoria** que atraerá las partículas cercanas.
- **Teclas de control** para modificar la cantidad de partículas y el comportamiento de la obra.

---

### **Implementación en p5.js**
Aquí tienes el código base:

```javascript
let particles = [];

function setup() {
  createCanvas(800, 600);
  for (let i = 0; i < 50; i++) {
    particles.push(new Particle(random(width), random(height)));
  }
}

function draw() {
  background(20);

  for (let p of particles) {
    p.applyForce(mouseX, mouseY);
    p.update();
    p.display();
  }
}

// Clase de Partícula
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-2, 2), random(-2, 2));
    this.acceleration = createVector(0, 0);
    this.maxForce = 0.2;
    this.size = 8;
  }

  applyForce(mx, my) {
    let mouseForce = createVector(mx, my);
    let force = p5.Vector.sub(mouseForce, this.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 150);
    let strength = map(distance, 5, 150, 1, 0);
    force.setMag(strength * this.maxForce);
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(3);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    // Rebote en los bordes del canvas
    if (this.position.x <= 0 || this.position.x >= width) {
      this.velocity.x *= -1;
    }
    if (this.position.y <= 0 || this.position.y >= height) {
      this.velocity.y *= -1;
    }
  }

  display() {
    fill(255);
    noStroke();
    ellipse(this.position.x, this.position.y, this.size);
  }
}

// Interacción con teclado
function keyPressed() {
  if (key === 'A') {
    particles.push(new Particle(random(width), random(height))); 
  }
  if (key === 'D' && particles.length > 5) {
    particles.pop();
  }
}
```

---

### **Interactividad y control**
- **Mouse:** Genera un campo gravitacional que afecta a las partículas cercanas.
- **Tecla `A`:** Agrega una nueva partícula al sistema.
- **Tecla `D`:** Elimina una partícula para modificar la dinámica.

---

### **Proceso de creación**
1. **Idea inicial:** Se pensó en un sistema generativo basado en fuerzas de atracción y repulsión.  
2. **Boceto:** Se exploró cómo representar el movimiento orgánico de las partículas y su reacción a un campo gravitatorio.  
3. **Experimentación:** Se probó el comportamiento de las partículas con distintas intensidades de fuerzas y métodos de interacción.  
4. **Resultado final:** Un sistema generativo de partículas con interacción en tiempo real, donde el usuario puede modificar el comportamiento en el canvas.  
