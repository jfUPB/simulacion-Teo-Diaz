``` javascript
let x, y;
let vx = 0;
let vy = 0;
let ax = 0;
let ay = 0;
let mode = 'towardsMouse'; // Inicialmente aceleración hacia el mouse

// Array para almacenar las partículas
let particles = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  x = width / 2;
  y = height / 2;
}

function draw() {
  // Fondo blanco, no transparente para que las partículas se queden visibles
  background(255);

  // Cambiar el modo de aceleración basado en la tecla presionada
  if (keyIsPressed) {
    if (key == '1') {
      mode = 'constant';
    } else if (key == '2') {
      mode = 'random';
    } else if (key == '3') {
      mode = 'towardsMouse';
    }
  }

  // Lógica de aceleración
  if (mode === 'constant') {
    ax = 0.1; // Aceleración constante en x
    ay = 0; // Sin aceleración en y
  } else if (mode === 'random') {
    ax = random(-0.5, 0.5); // Aceleración aleatoria en x
    ay = random(-0.5, 0.5); // Aceleración aleatoria en y
  } else if (mode === 'towardsMouse') {
    let angle = atan2(mouseY - y, mouseX - x);
    ax = cos(angle) * 0.1; // Aceleración hacia el mouse en x
    ay = sin(angle) * 0.1; // Aceleración hacia el mouse en y
  }

  // Actualizar la velocidad y posición
  vx += ax;
  vy += ay;
  x += vx;
  y += vy;

  // Crear partículas
  particles.push(new Particle(x, y));

  // Limitar el número de partículas para no sobrecargar la memoria
  if (particles.length > 1000) {
    particles.splice(0, 1);  // Elimina las partículas más antiguas
  }

  // Dibujar todas las partículas
  for (let i = 0; i < particles.length; i++) {
    particles[i].display();
  }

  // Mostrar la posición del objeto como un círculo
  fill(0);
  noStroke();
  ellipse(x, y, 30, 30);

  // Mostrar el texto indicando el modo actual
  fill(0);
  textSize(24);
  textAlign(CENTER);
  text("Modo: " + mode, width / 2, 30);
}

// Función para resetear la posición con el teclado
function keyPressed() {
  if (key === 'r' || key === 'R') {
    x = width / 2;
    y = height / 2;
    vx = 0;
    vy = 0;
  }
}

// Clase de partículas
class Particle {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.size = random(5, 15); // Tamaño aleatorio de la partícula
    this.color = color(random(255), random(255), random(255)); // Color aleatorio
  }

  // Muestra la partícula
  display() {
    fill(this.color);  // Mantiene el color de la partícula
    noStroke();
    ellipse(this.x, this.y, this.size, this.size);  // Dibuja la partícula
  }
}
```
