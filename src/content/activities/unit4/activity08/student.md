``` js
let angle = 0;
let angleVelocity = 0.2;
let amplitude = 100;

function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  background(255); // Limpiar el fondo en cada frame para mostrar movimiento.

  stroke(0);
  strokeWeight(2);

  let tempAngle = angle; // Mantener un ángulo temporal para cada círculo.

  for (let x = 0; x <= width; x += 24) {
    // Calcular la posición 'y' según la amplitud y seno del ángulo temporal.
    let y = amplitude * sin(tempAngle);

    // Generar tonalidades que varían desde blanco hasta azul según la posición y.
    let blueShade = map(y, -amplitude, amplitude, 255, 0); // Mapear desde blanco (RGB 255) hasta azul oscuro (RGB 0).
    fill(blueShade, blueShade, 255); // Mezcla de azul y blanco.

    // Dibujar un círculo en la posición (x, y).
    circle(x, y + height / 2, 48);

    // Incrementar el ángulo temporal según la velocidad angular.
    tempAngle += angleVelocity;
  }

  // Incrementar el ángulo global para animar la onda.
  angle += 0.1;
}
```
![captura del ejercicio](/
