Con la constante el objeto simplemente sigue aumentando su velocidad hasta hacer que el programa falle.
``` javascript
let x = 0;
let v = 0;
let a = 0.1;

function setup() {
  createCanvas(600, 400);
  frameRate(60);
}

function draw() {
  background(255);

  v += a;

  x += v;

  if (x > width) {
    x = 0;
  }

  fill(0);
  ellipse(x, height / 2, 50, 50);

  fill(0);
  textSize(16);
  text("Velocidad: " + v.toFixed(2), 10, 30);
  text("Aceleración: " + a, 10, 50);
}
```
Con aceleración aleatoria tenia valores entre -0.1 y 0.1 me di cuenta que habia una tendencia de avanzar hacia adelante.
``` javascript
let x = 0;
let v = 0;
let a = 0;

function setup() {
  createCanvas(600, 400);
  frameRate(60);
}

function draw() {
  background(255);

  // Cambiar la aceleración aleatoriamente en cada fotograma
  a = random(-0.1, 0.1);   // Aceleración aleatoria entre -0.1 y 0.1

  v += a;

  x += v;

  if (x > width) {
    x = 0; // Resetea la posición a la izquierda
  }

  if (x < 0) {
    x = width; // Resetea la posición a la derecha
  }

  fill(0);
  ellipse(x, height / 2, 50, 50);

  fill(0);
  textSize(16);
  text("Velocidad: " + v.toFixed(2), 10, 30);
  text("Aceleración: " + a.toFixed(3), 10, 50);
}
```
