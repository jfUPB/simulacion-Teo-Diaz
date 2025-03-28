## Simulación:

**Código:**

```javascript
let bodies = [];
let G = 4.9; // Constante gravitacional

function setup() {
  createCanvas(800, 600);
  background(25);

  // Crear 10 cuerpos con diferentes masas y posiciones aleatorias
  for (let i = 0; i < 10; i++) {
    bodies.push({
      x: random(width),
      y: random(height),
      vx: random(-2, 2),
      vy: random(-2, 2),
      mass: random(5, 20),
      color: color(random(255), random(255), random(255))
    });
  }
}

function draw() {
  background(25, 10);

  // Calcular las fuerzas gravitacionales entre cada par de cuerpos
  for (let i = 0; i < bodies.length; i++) {
    for (let j = i + 1; j < bodies.length; j++) {
      let body1 = bodies[i];
      let body2 = bodies[j];

      let dx = body2.x - body1.x;
      let dy = body2.y - body1.y;
      let distance = sqrt(sq(dx) + sq(dy));

      // Evitar división por cero
      if (distance < 1) {
        distance = 1;
      }

      let force = G * body1.mass * body2.mass / sq(distance);

      // Aplicar la fuerza a la velocidad de cada cuerpo
      body1.vx += force * dx / body1.mass / distance;
      body1.vy += force * dy / body1.mass / distance;
      body2.vx -= force * dx / body2.mass / distance;
      body2.vy -= force * dy / body2.mass / distance;
    }
  }

  // Actualizar las posiciones de los cuerpos
  for (let i = 0; i < bodies.length; i++) {
    bodies[i].x += bodies[i].vx;
    bodies[i].y += bodies[i].vy;
  }

  // Dibujar los cuerpos como círculos con colores aleatorios
  for (let i = 0; i < bodies.length; i++) {
    fill(bodies[i].color);
    noStroke();
    ellipse(bodies[i].x, bodies[i].y, bodies[i].mass * 2, bodies[i].mass * 2);
  }
}
```
![captura del ejercicio](/src/assets/mi_captura.png)
**Explicación:**

* La simulación crea un conjunto de cuerpos con diferentes masas y posiciones aleatorias.
* La fuerza gravitacional se calcula entre cada par de cuerpos usando la ley de gravitación de Newton: \( F = G \frac{m_1 m_2}{r^2} \).
* La fuerza se aplica a la velocidad de cada cuerpo, haciendo que se atraigan mutuamente.
* Los cuerpos se dibujan como círculos con diferentes colores para destacar su movimiento.

**Imagen:**

**Enlace** https://editor.p5js.org/Teo-Diaz/sketches/tldUYnJVt

**Inspiración de Calder:**

La simulación busca capturar la esencia del movimiento y el equilibrio de las esculturas cinéticas de Calder. Los cuerpos en movimiento, con sus diferentes masas y colores, crean un espectáculo dinámico y fascinante que evoca la complejidad del universo.
