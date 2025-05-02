### **Enlace al Editor de p5.js**

(https://editor.p5js.org/Teo-Diaz/sketches/Iqfi7zVTW)
### **Captura de Pantalla**

![captura del ejercicio](/src/assets/2Pendulo.png)
````
let doublePendulum;

function setup() {
  createCanvas(600, 600);
  doublePendulum = new DoublePendulum(width / 2, 200, 150, 150);
}

function draw() {
  background(255);
  doublePendulum.update();
  doublePendulum.show();
}

class DoublePendulum {
  constructor(x, y, r1, r2) {
    this.pivot = createVector(x, y);

    this.r1 = r1;
    this.r2 = r2;
    this.angle1 = PI / 4;
    this.angle2 = PI / 4;
    this.angleVelocity1 = 0;
    this.angleVelocity2 = 0;
    this.angleAcceleration1 = 0;
    this.angleAcceleration2 = 0;

    this.damping = 0.995; // Factor de amortiguación
    this.mass1 = 10; // Masa del primer péndulo
    this.mass2 = 10; // Masa del segundo péndulo
  }

  update() {
    let g = 0.4; // Gravedad

    let num1 = -g * (2 * this.mass1 + this.mass2) * sin(this.angle1);
    let num2 = -this.mass2 * g * sin(this.angle1 - 2 * this.angle2);
    let num3 = -2 * sin(this.angle1 - this.angle2) * this.mass2;
    let num4 = this.angleVelocity2 * this.angleVelocity2 * this.r2 + this.angleVelocity1 * this.angleVelocity1 * this.r1 * cos(this.angle1 - this.angle2);
    let den1 = this.r1 * (2 * this.mass1 + this.mass2 - this.mass2 * cos(2 * this.angle1 - 2 * this.angle2));

    this.angleAcceleration1 = (num1 + num2 + num3 * num4) / den1;

    let num5 = 2 * sin(this.angle1 - this.angle2);
    let num6 = (this.angleVelocity1 * this.angleVelocity1 * this.r1 * (this.mass1 + this.mass2));
    let num7 = g * (this.mass1 + this.mass2) * cos(this.angle1);
    let num8 = this.angleVelocity2 * this.angleVelocity2 * this.r2 * this.mass2 * cos(this.angle1 - this.angle2);
    let den2 = this.r2 * (2 * this.mass1 + this.mass2 - this.mass2 * cos(2 * this.angle1 - 2 * this.angle2));

    this.angleAcceleration2 = (num5 * (num6 + num7 + num8)) / den2;

    this.angleVelocity1 += this.angleAcceleration1;
    this.angleVelocity2 += this.angleAcceleration2;
    this.angle1 += this.angleVelocity1;
    this.angle2 += this.angleVelocity2;

    this.angleVelocity1 *= this.damping;
    this.angleVelocity2 *= this.damping;
  }

  show() {
    let bob1 = createVector(this.r1 * sin(this.angle1), this.r1 * cos(this.angle1));
    bob1.add(this.pivot);

    let bob2 = createVector(this.r2 * sin(this.angle2), this.r2 * cos(this.angle2));
    bob2.add(bob1);

    stroke(0);
    strokeWeight(2);
    line(this.pivot.x, this.pivot.y, bob1.x, bob1.y);
    fill(127);
    circle(bob1.x, bob1.y, 20);

    line(bob1.x, bob1.y, bob2.x, bob2.y);
    fill(127);
    circle(bob2.x, bob2.y, 20);
  }
}
````
