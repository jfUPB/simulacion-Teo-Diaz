``` javascript
let oscillators = [];

class Oscillator {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.angle = createVector();
    this.angleVelocity = createVector(random(-0.05, 0.05), random(-0.05, 0.05));
    this.amplitude = createVector(random(20, width / 2), random(20, height / 2));
    this.mass = random(5, 15);
    this.color = this.getRandomColor(); // Color inicial aleatorio
  }

  getRandomColor() {
    return color(random(255), random(255), random(255));
  }

  changeColor() {
    this.color = this.getRandomColor(); // Cambio de color aleatorio
  }

  applyForce(force) {
    let f = force.copy().div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.angle.add(this.angleVelocity);
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    let x = sin(this.angle.x) * this.amplitude.x;
    let y = sin(this.angle.y) * this.amplitude.y;

    push();
    translate(this.position.x, this.position.y);
    stroke(0);
    strokeWeight(2);
    fill(this.color);
    line(0, 0, x, y);
    circle(x, y, 32);
    pop();
  }
}

function setup() {
  createCanvas(640, 360);
  for (let i = 0; i < 10; i++) {
    oscillators.push(new Oscillator());
  }

  // Cambiar los colores cada segundo
  setInterval(() => {
    for (let osc of oscillators) {
      osc.changeColor();
    }
  }, 1000);
}

function draw() {
  background(255);

  let wind = createVector(random(-0.01, 0.01), random(-0.01, 0.01));
  for (let osc of oscillators) {
    osc.applyForce(wind);
    osc.update();
    osc.show();
  }
}
```
![captura del ejercicio](/src/assets/colores.png)
