## 1. Fricción

**Descripción:** Esta simulación muestra un objeto que se mueve sobre una superficie con fricción. Puedes ajustar la fuerza de fricción y observar cómo afecta la velocidad y la distancia que recorre el objeto.

**Código:**

```javascript
let x = 100;
let y = 100;
let vx = 5;
let vy = 0;
let friction = 0.05; // Fuerza de fricción

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  // Calcular la fuerza de fricción
  let fx = -vx * friction;
  let fy = -vy * friction;

  // Aplicar la fuerza de fricción a la velocidad
  vx += fx;
  vy += fy;

  // Mover el objeto
  x += vx;
  y += vy;

  // Dibujar el objeto
  ellipse(x, y, 20, 20);
}
```

**Explicación:**

* La variable `friction` representa la fuerza de fricción. Puedes modificarla para ver cómo afecta el movimiento del objeto.
* En cada cuadro, se calcula la fuerza de fricción en las direcciones horizontal (`fx`) y vertical (`fy`).
* La fuerza de fricción se aplica a la velocidad del objeto, reduciendo su velocidad gradualmente.

## 2. Resistencia del aire

**Descripción:** Esta simulación muestra un objeto que se mueve a través del aire, experimentando resistencia del aire. Puedes ajustar la densidad del aire y observar cómo afecta la velocidad terminal del objeto.

**Código:**

```javascript
let x = 100;
let y = 100;
let vx = 10;
let vy = 0;
let gravity = 0.1; // Fuerza de gravedad
let airDensity = 0.1; // Densidad del aire
let dragCoefficient = 0.5; // Coeficiente de arrastre

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  // Calcular la fuerza de resistencia del aire
  let speed = sqrt(sq(vx) + sq(vy));
  let dragForce = -0.5 * airDensity * dragCoefficient * speed * speed;
  let fx = dragForce * vx / speed;
  let fy = dragForce * vy / speed;

  // Aplicar la fuerza de resistencia del aire y la gravedad a la velocidad
  vx += fx;
  vy += fy + gravity;

  // Mover el objeto
  x += vx;
  y += vy;

  // Dibujar el objeto
  ellipse(x, y, 20, 20);
}
```

**Explicación:**

* La variable `airDensity` representa la densidad del aire. Puedes modificarla para simular diferentes ambientes.
* La fuerza de resistencia del aire se calcula usando la fórmula \( F_d = \frac{1}{2} \rho v^2 C_d A \), donde \( \rho \) es la densidad del aire, \( v \) es la velocidad del objeto, \( C_d \) es el coeficiente de arrastre y \( A \) es el área de la superficie frontal del objeto.
* En esta simulación, se asume que el área de la superficie frontal del objeto es constante, por lo que el coeficiente de arrastre se ajusta para representar la forma del objeto.

## 3. Atracción gravitacional

**Descripción:** Esta simulación muestra dos objetos que se atraen mutuamente debido a la fuerza gravitacional. Puedes ajustar la masa de los objetos y observar cómo afecta la fuerza de atracción.

**Código:**

```javascript
let x1 = 100;
let y1 = 100;
let vx1 = 0;
let vy1 = 0;
let mass1 = 10; // Masa del objeto 1

let x2 = 300;
let y2 = 100;
let vx2 = 0;
let vy2 = 0;
let mass2 = 5; // Masa del objeto 2

let G = 0.1; // Constante gravitacional

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);

  // Calcular la distancia entre los objetos
  let dx = x2 - x1;
  let dy = y2 - y1;
  let distance = sqrt(sq(dx) + sq(dy));

  // Calcular la fuerza gravitacional
  let force = G * mass1 * mass2 / sq(distance);

  // Calcular las componentes de la fuerza
  let fx1 = force * dx / distance;
  let fy1 = force * dy / distance;
  let fx2 = -fx1;
  let fy2 = -fy1;

  // Aplicar la fuerza gravitacional a la velocidad de los objetos
  vx1 += fx1 / mass1;
  vy1 += fy1 / mass1;
  vx2 += fx2 / mass2;
  vy2 += fy2 / mass2;

  // Mover los objetos
  x1 += vx1;
  y1 += vy1;
  x2 += vx2;
  y2 += vy2;

  // Dibujar los objetos
  ellipse(x1, y1, 20, 20);
  ellipse(x2, y2, 10, 10);
}
```

**Explicación:**

* La variable `G` representa la constante gravitacional. Puedes modificarla para simular diferentes ambientes.
* La fuerza gravitacional se calcula usando la fórmula \( F = G \frac{m_1 m_2}{r^2} \), donde \( G \) es la constante gravitacional, \( m_1 \) y \( m_2 \) son las masas de los objetos y \( r \) es la distancia entre ellos.
* La fuerza gravitacional se aplica a la velocidad de los objetos, haciendo que se atraigan mutuamente.

