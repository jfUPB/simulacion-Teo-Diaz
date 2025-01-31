# Actividad
### Codigo
```javascript
let walker;
let points = [];

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();

  // Almacenar las posiciones de los puntos
  points.push(createVector(walker.x, walker.y));
  
  // Limitar el número de puntos para evitar sobrecargar el canvas
  if (points.length > 1000) {
    points.shift();
  }
  
  // Mostrar los puntos con una figura geométrica
  for (let i = 0; i < points.length; i++) {
    let pt = points[i];
    let r = map(i, 0, points.length, 1, 5);  // Tamaño de los círculos
    noStroke();
    fill(0, 10);
    ellipse(pt.x, pt.y, r, r);
  }
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    // Usar randomGaussian() para la distribución normal
    let xstep = randomGaussian(); 
    let ystep = randomGaussian();
    
    // Escalar el paso para que no sea tan grande
    xstep *= 2;  
    ystep *= 2;
    
    this.x += xstep;
    this.y += ystep;
    
    // Asegurarse de que no se salga del canvas
    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}
```
### Captura
![captura del ejercicio](/src/assets/ejercicio.png)
