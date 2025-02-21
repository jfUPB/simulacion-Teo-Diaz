```` javascript
let v3; 
let t = 0;

function setup() {
    createCanvas(300, 300);
}

function draw() {
    background(200);

    let v0 = createVector(mouseX, mouseY);
    let scaleFactor = calculateScaleFactor(mouseX, mouseY);

    let v1 = createVector(120 * scaleFactor, 0);  
    let v2 = createVector(0, 120 * scaleFactor);  

    let v1_end = v0.copy().add(v1);
    let v2_end = v0.copy().add(v2);
    let v4 = v2_end.copy().sub(v1_end);

    v3 = p5.Vector.lerp(v1, v2, t);

    t += 0.01;
    if (t > 1) t = 0;

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
    drawArrow(v1_end, v4, 'green');
}

function calculateScaleFactor(x, y) {
    return dist(x, y, width / 2, height / 2) / 100;
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
````
