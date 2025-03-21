``` javascript
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    // Inicializa la posición con un vector
    this.position = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y); // Usamos los componentes del vector
  }

  // El walker se mueve usando un vector aleatorio
  step() {
    // Crea un vector aleatorio para el paso
    let step = createVector(random(-2.75, 3), random(-2.75, 3));
    
    // Suma el paso al vector de la posición
    this.position.add(step);
  }
}
```
