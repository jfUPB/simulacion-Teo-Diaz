El algoritmo Motion 101 primero, tiene un objeto Mover tiene dos datos, posición y velocidad, ambos objetos p5.Vector. Estos se inicializan en el constructor del objeto. En este caso, decidiré arbitrariamente inicializar el objeto Mover dándole una posición y velocidad aleatorias. Tenga en cuenta el uso de esto con todas las variables que forman parte del objeto Mover.
El objeto Mover necesita moverse (aplicando su velocidad a su posición) y debe ser visible. Implementaré estas necesidades como funciones denominadas update() y show(). Pondré todo el código de lógica de movimiento en update() y dibujaré el objeto en show()
### Ejemplo:
``` javascript
let mover;

function setup() {
  createCanvas(400, 400);
  mover = new Mover(); 
}

function draw() {
  background(220);
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-2, 2), random(-2, 2));
  }

  update() {
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    fill(175);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {
    
    if (this.position.x > width) {
      this.position.x = 0;
    } else if (this.position.x < 0) {
      this.position.x = width;
    }

    if (this.position.y > height) {
      this.position.y = 0;
    } else if (this.position.y < 0) {
      this.position.y = height;
    }
  }
}
```
![captura del ejercicio](/src/assets/canvas_capture.png)
