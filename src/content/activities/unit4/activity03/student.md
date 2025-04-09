Enlace a la simulación: https://editor.p5js.org/Teo-Diaz/sketches/_fFZmalo_

``` javascript
let vehicle;

function setup() {
  createCanvas(800, 600);
  vehicle = new Vehicle(width / 2, height / 2);
}

function draw() {
  background(240);

  vehicle.update();
  vehicle.display();
}

class Vehicle {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.size = 30;
    this.angle = 0; // Dirección inicial
    this.speed = 0; // Velocidad inicial
    this.acceleration = 0.1; // Aceleración
  }

  update() {
    // Aceleración hacia la izquierda
    if (keyIsDown(LEFT_ARROW)) {
      this.speed -= this.acceleration; // Reduce la velocidad para mover a la izquierda
    }

    // Aceleración hacia la derecha
    if (keyIsDown(RIGHT_ARROW)) {
      this.speed += this.acceleration; // Aumenta la velocidad para mover a la derecha
    }

    // Movimiento hacia arriba (en la dirección del eje Y)
    if (keyIsDown(UP_ARROW)) {
      this.y -= this.acceleration; // Mueve el vehículo hacia arriba
    }

    // Movimiento hacia abajo (en la dirección del eje Y)
    if (keyIsDown(DOWN_ARROW)) {
      this.y += this.acceleration; // Mueve el vehículo hacia abajo
    }

    // Movimiento en la dirección en que apunta el vehículo (izquierda/derecha)
    let velocityX = this.speed * cos(this.angle);
    let velocityY = this.speed * sin(this.angle);

    this.x += velocityX;
    this.y += velocityY;

    // Evitar que el vehículo salga de la pantalla
    if (this.x < 0) this.x = width;
    if (this.x > width) this.x = 0;
    if (this.y < 0) this.y = height;
    if (this.y > height) this.y = 0;
  }

  display() {
    push();
    translate(this.x, this.y);
    rotate(this.angle);

    // Dibuja el triángulo
    beginShape();
    vertex(0, -this.size);  // Vértice superior
    vertex(-this.size, this.size);  // Vértice izquierdo
    vertex(this.size, this.size);  // Vértice derecho
    endShape(CLOSE);

    pop();
  }
}
```

![Captura del ejercicio](/src/assets/Captura de pantalla 2025-04-09 134149.png)
