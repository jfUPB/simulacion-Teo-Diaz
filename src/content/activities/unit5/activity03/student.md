### **Idea Inicial**
Crear una obra de arte basada en partículas que se comporten como ecos visuales del movimiento del usuario (a través del mouse). Las partículas reaccionan en tiempo real y desaparecen con el tiempo. Además, algunas cambiarán su comportamiento dependiendo de la distancia al cursor (polimorfismo). Esta pieza representa la idea de cómo dejamos rastros en nuestro entorno.

---

### **Conceptos Aplicados**

| Unidad | Concepto | Aplicación | Por qué |
|--------|----------|------------|---------|
| 1 - Fundamentos | Coordenadas y dibujo | Uso de `ellipse()`, `stroke()`, `fill()` en posiciones dinámicas | Para representar partículas en movimiento |
| 2 - Estructuras | Arrays y objetos | Manejo de partículas en un array | Permite gestionar múltiples elementos en tiempo real |
| 3 - Programación Orientada a Objetos | Herencia y polimorfismo | Clase `Particle` y subclases `SlowParticle`, `FastParticle` con métodos sobrescritos | Añade variedad de comportamiento visual y dinamismo |
| 4 - Interacción | Entrada del mouse | Uso de `mouseX`, `mouseY` para generar partículas | Hace la obra reactiva e interactiva |

---

### **Gestión del Tiempo de Vida y Memoria**

Cada partícula tiene una propiedad `lifespan`. En cada frame, disminuye. Cuando llega a 0, se elimina del array principal (`particles`). Esto mantiene la memoria optimizada y simula el paso del tiempo.

---

### **Experimentación y Proceso Creativo**
1. Bocetos en papel: líneas curvas que seguían al mouse como estelas.
2. Primer prototipo: partículas básicas que desaparecían.
3. Mejora: clases hijas con diferentes velocidades.
4. Pruebas con interacción: ajuste del número de partículas, distancia del mouse, colores.
5. Resultado final: partículas con distintos comportamientos y desaparición progresiva.

---

### **Código Completo**

```javascript
let particles = [];

function setup() {
  createCanvas(800, 600);
  background(0);
}

function draw() {
  background(0, 20); // efecto de estela
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (particles[i].isDead()) {
      particles.splice(i, 1);
    }
  }
}

// Crear partículas al mover el mouse
function mouseMoved() {
  let p;
  if (random(1) > 0.5) {
    p = new FastParticle(mouseX, mouseY);
  } else {
    p = new SlowParticle(mouseX, mouseY);
  }
  particles.push(p);
}

// Clase base
class Particle {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.lifespan = 255;
    this.size = random(5, 15);
    this.vx = random(-1, 1);
    this.vy = random(-1, 1);
    this.color = color(random(255), random(255), random(255), this.lifespan);
  }

  update() {
    this.x += this.vx;
    this.y += this.vy;
    this.lifespan -= 2;
    this.color.setAlpha(this.lifespan);
  }

  display() {
    noStroke();
    fill(this.color);
    ellipse(this.x, this.y, this.size);
  }

  isDead() {
    return this.lifespan <= 0;
  }
}

// Subclase: partícula lenta
class SlowParticle extends Particle {
  constructor(x, y) {
    super(x, y);
    this.vx *= 0.5;
    this.vy *= 0.5;
    this.size *= 1.5;
  }

  display() {
    stroke(255, this.lifespan);
    fill(this.color);
    ellipse(this.x, this.y, this.size);
  }
}

// Subclase: partícula rápida
class FastParticle extends Particle {
  constructor(x, y) {
    super(x, y);
    this.vx *= 2;
    this.vy *= 2;
    this.size *= 0.8;
  }

  display() {
    fill(255, 0, 0, this.lifespan);
    ellipse(this.x, this.y, this.size);
  }
}
```

---

### **Enlace al Editor de p5.js**
[ Ver obra en p5.js Web Editor]([https://editor.p5js.org/](https://editor.p5js.org/Teo-Diaz/sketches/PMuyQvGC3)
### **Captura de Pantalla**
![captura del ejercicio](/src/assets/generativo.png)
