``` js
class Spring {
  constructor(x, y, length) {
    this.anchor = createVector(x, y);
    this.restLength = length;
    this.k = 0.2;
  }

  connect(bob) {
    let force = p5.Vector.sub(bob.position, this.anchor);
    let currentLength = force.mag();
    let stretch = currentLength - this.restLength;
    force.setMag(-1 * this.k * stretch);
    bob.applyForce(force);
  }

  constrainLength(bob, minlen, maxlen) {
    let direction = p5.Vector.sub(bob.position, this.anchor);
    let length = direction.mag();

    if (length < minlen) {
      direction.setMag(minlen);
      bob.position = p5.Vector.add(this.anchor, direction);
      bob.velocity.mult(0);
    } else if (length > maxlen) {
      direction.setMag(maxlen);
      bob.position = p5.Vector.add(this.anchor, direction);
      bob.velocity.mult(0);
    }
  }

  show() {
    fill(127);
    circle(this.anchor.x, this.anchor.y, 10);
  }

  showLine(bob) {
    stroke(0);
    line(bob.position.x, bob.position.y, this.anchor.x, this.anchor.y);
  }
}

class Bob {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
    this.dragging = false;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    if (!this.dragging) {
      this.velocity.add(this.acceleration);
      this.position.add(this.velocity);
    }
    this.acceleration.mult(0);
  }

  show() {
    fill(175);
    stroke(0);
    ellipse(this.position.x, this.position.y, 48, 48);
  }

  handleClick(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    if (d < 24) {
      this.dragging = true;
    }
  }

  stopDragging() {
    this.dragging = false;
  }

  handleDrag(mx, my) {
    if (this.dragging) {
      this.position.set(mx, my);
    }
  }
}

// Objetos principales
let bob1, bob2;
let spring1, spring2;

function setup() {
  createCanvas(640, 400);

  spring1 = new Spring(width / 2, 10, 100);
  bob1 = new Bob(width / 2, 110);
  spring2 = new Spring(bob1.position.x, bob1.position.y, 100);
  bob2 = new Bob(width / 2, 210);
}

function draw() {
  background(255);

  let gravity = createVector(0, 2);
  bob1.applyForce(gravity);
  bob2.applyForce(gravity);

  bob1.update();
  bob2.update();

  bob1.handleDrag(mouseX, mouseY);
  bob2.handleDrag(mouseX, mouseY);

  spring1.connect(bob1);
  spring2.anchor.set(bob1.position.x, bob1.position.y); // Conectar el segundo resorte al primer bob
  spring2.connect(bob2);

  spring1.constrainLength(bob1, 30, 200);
  spring2.constrainLength(bob2, 30, 200);

  spring1.showLine(bob1);
  spring2.showLine(bob2);
  bob1.show();
  bob2.show();
  spring1.show();
  spring2.show();
}

function mousePressed() {
  bob1.handleClick(mouseX, mouseY);
  bob2.handleClick(mouseX, mouseY);
}

function mouseReleased() {
  bob1.stopDragging();
  bob2.stopDragging();
}
```
![captura del ejercicio](/
