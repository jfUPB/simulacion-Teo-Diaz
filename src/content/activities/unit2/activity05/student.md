``` javascript
let v3; 
let t = 0;

function setup() {
    createCanvas(400, 400);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50); // Origen
    let v1 = createVector(200, 0); // Vector 1
    let v2 = createVector(0, 200); // Vector 2 

    let v1_end = v0.copy().add(v1);
    let v2_end = v0.copy().add(v2);
    let v4 = v2_end.copy().sub(v1_end); // Vector 4

    v3 = p5.Vector.lerp(v1, v2, t); // Vector 3 en relación a v1, v2 y el tiempo 

    t += 0.01;
    if (t > 1) t = 0;

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
    drawArrow(v1_end, v4, 'green');

}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}


```
