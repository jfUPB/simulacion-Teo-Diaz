``` javascript
let amplitude = 100; // Amplitud inicial
let frequency = 1; // Frecuencia inicial en Hz
let phase = 0; // Fase inicial en radianes
let angularSpeed = 2 * Math.PI * frequency; // Velocidad angular inicial
let period = 1 / frequency; // Periodo inicial

function setup() {
  createCanvas(800, 400);
  textSize(16);
}

function draw() {
  background(220);

  // Dibujar el eje x
  stroke(0);
  line(0, height / 2, width, height / 2);

  // Dibujar la función sinusoide
  stroke(0, 0, 255);
  noFill();
  beginShape();
  for (let x = 0; x < width; x++) {
    let t = x / width * period * 10; // Escalar en el tiempo para que sea visible
    let y = amplitude * sin(angularSpeed * t + phase);
    vertex(x, height / 2 - y);
  }
  endShape();

  // Mostrar los parámetros en pantalla
  fill(0);
  text(`Amplitud: ${amplitude}`, 10, 20);
  text(`Frecuencia: ${frequency} Hz`, 10, 40);
  text(`Fase: ${phase.toFixed(2)} rad`, 10, 60);
  text(`Velocidad angular: ${angularSpeed.toFixed(2)} rad/s`, 10, 80);
  text(`Periodo: ${period.toFixed(2)} s`, 10, 100);
}

// Ajustar parámetros con teclado
function keyPressed() {
  if (key === 'd') amplitude += 10;
  if (key === 'a') amplitude -= 10;
  if (key === 'w') frequency += 0.1;
  if (key === 's') frequency -= 0.1;
  if (key === 'q') phase += 0.1;
  if (key === 'e') phase -= 0.1;

  // Recalcular valores derivados
  angularSpeed = 2 * Math.PI * frequency;
  period = 1 / frequency;
}
```
![captura del ejercicio](/src/assets/Sin.png)
