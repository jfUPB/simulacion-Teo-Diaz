# Actividad 3
### que pregunta me hice ¿que pasaria si cambio las probabilidades de cada direccion?
¿Que paso? logre hacer que camine en diagonales agregando un if (else) y luego lo puse a moverse exclusivamente a la derecha
Codigo original:

```javascript
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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    let xstep = random(-2.75, 3);
    let ystep = random(-2.75, 3);
    this.x += xstep;
    this.y += ystep;
  }
}

```

Edite "step" para tener probabilidades personalizadas :D

```javascript
step() {
    let r = random(1);
    
    if (r < 0.4) {
      this.x++;
    } else if (r < 0.6) {
      this.x--;
    } else if (r < 0.8) {
    }
```
