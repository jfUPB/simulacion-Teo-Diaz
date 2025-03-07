``` javascript
let x, y;
let vx = 0;
let vy = 0;
let ax = 0;
let ay = 0;
let mode = 'towardsMouse'; // Inicialmente aceleración hacia el mouse

// Tamaño inicial del objeto en movimiento
let objSize = 30;

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
  
  if (mode === 'towardsMouse') {
    let angle = atan2(mouseY - y, mouseX - x);
    ax = cos(angle) * 0.1; // Aceleración hacia el mouse en x
    ay = sin(angle) * 0.1; // Aceleración hacia el mouse en y
  }

  // Actualizar la velocidad y posición
  vx += ax;
  vy += ay;
  x += vx;
  y += vy;

  // Crear partículas con un tamaño relativo al tamaño del objeto
  let particleSize = objSize / 3;  // Las partículas son más pequeñas que el objeto
  particles.push(new Particle(x, y, particleSize));

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
  ellipse(x, y, objSize, objSize);  // Usar objSize para el tamaño del objeto

  // Mostrar el texto indicando el modo actual
  fill(0);
  textSize(24);
  textAlign(CENTER);
  text("" + mode, width / 2, 30);
}

// Función para resetear la posición con el teclado
function keyPressed() {
  if (key === 'r' || key === 'R') {
    x = width / 2;
    y = height / 2;
    vx = 0;
    vy = 0;
  }

  // Cambiar el tamaño del objeto al presionar 'w' o 's'
  if (key === 'w' || key === 'W') {
    objSize += 5;  // Incrementar el tamaño
  } 
  if (key === 's' || key === 'S') {
    objSize = max(5, objSize - 5);  // Reducir el tamaño sin permitir que sea menor a 5
  }
}

// Clase de partículas
class Particle {
  constructor(x, y, size) {
    this.x = x;
    this.y = y;
    this.size = size; // El tamaño de la partícula ahora se pasa como parámetro
    this.color = color(random(255), random(255), random(255)); // Color aleatorio
  }

  // Muestra la partícula
  display() {
    fill(this.color);  // Mantiene el color de la partícula
    noStroke();
    ellipse(this.x, this.y, this.size, this.size);  // Dibuja la partícula con el tamaño asignado
  }
}
```
