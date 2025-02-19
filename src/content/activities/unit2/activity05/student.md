``` javascript
function setup() {
  createCanvas(400, 400);
  t = 0; // Variable de tiempo inicializada a 0
  direction = 1; // Dirección del movimiento (1 para adelante, -1 para atrás)
}

function draw() {
  background(200);

  let v0 = createVector(50, 50); // Origen
  let v1 = createVector(200, 0); // Vector rojo
  let v2 = createVector(0, 200); // Vector azul

  let v1End = p5.Vector.add(v0, v1); // Punto final de v1
  let v2End = p5.Vector.add(v0, v2); // Punto final de v2

  let v4 = p5.Vector.sub(v2End, v1End);
  
  let v3 = p5.Vector.lerp(v1End, p5.Vector.add(v2End, v4), t * direction);

  drawArrow(v0, v1, 'red');
  drawArrow(v0, v2, 'blue');
  drawArrow(v0, v3, 'purple');
  drawArrow(v1End, v4, 'green');

  t += 0.01;
  if (t >= 1) {
    t = 0;
    direction *= -1;
  }
}

function drawArrow(base, vec, myColor) {
  push();
  stroke(myColor);
  strokeWeight(3);
  fill(myColor);
  translate(base.x, base.y);
  line(0, 0, vec.x, vec.y);
  rotate(vec.heading());
  let arrowSize = 7;
  translate(vec.mag() - arrowSize, 0);
  triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
  pop();
}

```
