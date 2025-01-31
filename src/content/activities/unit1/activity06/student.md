# Actividad
El Lévy flight es útil en situaciones donde la exploración eficiente de un espacio grande y complejo es crucial, especialmente cuando la posibilidad de realizar saltos largos puede ser ventajosa. Esto se aplica tanto a contextos biológicos, como en la búsqueda de recursos, como en contextos tecnológicos, como la optimización o los algoritmos de búsqueda.

### Codigo
```javascript
let x, y;  // Posición inicial
let path = [];  // Para almacenar la trayectoria

function setup() {
  createCanvas(640, 240);
  x = width / 2;
  y = height / 2;
  background(255);
}

function draw() {
  // Generar un salto de Lévy en 2D
  let stepSize = levyStep();
  
  // Direcciones aleatorias en 2D
  let angle = random(TWO_PI);
  let dx = cos(angle) * stepSize;
  let dy = sin(angle) * stepSize;
  
  // Actualizar la posición
  x += dx;
  y += dy;
  
  // Asegurarse de que no se salga del canvas
  x = constrain(x, 0, width);
  y = constrain(y, 0, height);
  
  // Guardar la posición para mostrar la trayectoria
  path.push(createVector(x, y));
  
  // Dibujar la trayectoria
  noFill();
  stroke(0, 50);
  beginShape();
  for (let pt of path) {
    vertex(pt.x, pt.y);
  }
  endShape();
  
  // Dibujar el punto actual
  fill(0);
  noStroke();
  ellipse(x, y, 5, 5);
}

// Función para generar un salto de Lévy
function levyStep() {
  // Exponente de la distribución de Lévy (generalmente entre 1 y 3)
  let exponent = 1.5;
  
  // Generar un salto usando una distribución de Lévy
  let stepSize = pow(random(), -1 / exponent);
  
  // Escalar el salto para hacerlo más visible
  return stepSize * 10;
}
```
