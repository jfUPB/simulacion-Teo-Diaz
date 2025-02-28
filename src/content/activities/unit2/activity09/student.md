Con la constante el objeto simplemente sigue aumentando su velocidad hasta hacer que el programa falle
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
