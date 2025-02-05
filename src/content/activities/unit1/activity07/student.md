

### Codigo
```javascript
// Controls
let spreadSlider;
let sizeSlider;
let sizespSlider;
let baseHueSlider;
let huespSlider;
let alphaSlider;

let time = 0;  // Variable para animar el ruido

function setup() {
  createCanvas(640, 240);
  colorMode(HSB);
  background(97);
  createControls(300);
}

function draw() {
  translate(width / 2, height / 2);
  scale(height / 2);

  // Usamos ruido Perlin para las variaciones de posición (x, y)
  let x = noise(time) * width - width / 2;  // Ruido Perlin para posición x
  let y = noise(time + 1000) * height - height / 2;  // Ruido Perlin para posición y

  // Mantener el tamaño constante según el control deslizante
  let size = sizeSlider.value();
  if (size <= 0) {
    size = 0.001;
  }

  // Colores basados en el ruido Perlin
  let paintHue = noise(time + 3000) * 360;  // Ruido Perlin para matiz (hue)
  let paintSat = randomGaussian(80, 20);    // Saturación (usamos un valor aleatorio normal)
  let paintBright = randomGaussian(80, 20); // Brillo (usamos un valor aleatorio normal)
  if (paintSat > 100) paintSat = 100;
  if (paintBright > 100) paintBright = 100;
  if (paintHue < 0) paintHue += 360;         // Aseguramos que el matiz esté entre 0 y 360
  if (paintHue >= 360) paintHue -= 360;

  // Asignamos un valor de opacidad (transparencia)
  let alpha = alphaSlider.value();

  // Usamos el ruido Perlin para generar el color de la salpicadura
  noStroke();
  fill(paintHue, paintSat, paintBright, alpha);
  ellipse(x, y, size, size);

  // Incrementamos el tiempo para animar el ruido
  time += 0.01;
}

function createControls(ypos) {
  let xpos = 0;

  cpTitle = createP("Paint Splatter Simulation");
  cpTitle.position(xpos, ypos - 50);
  cpTitle.style("font-size", "14pt");
  cpTitle.style("font-weight", "bold");
  xpos += 220;

  clearButton = createButton("Clear");
  clearButton.position(xpos, ypos - 50);
  clearButton.mousePressed(clearButtonClicked);
  
  xpos = 0;
  spreadTitle = createP("Spread");
  spreadTitle.position(xpos, ypos);
  xpos += 50;

  spreadSlider = createSlider(0, 0.75, 0.25, 0);
  spreadSlider.position(xpos, ypos);
  spreadSlider.size(80);
  xpos += 100;

  sizeTitle = createP("Size");
  sizeTitle.position(xpos, ypos);
  xpos += 35;

  sizeSlider = createSlider(5, 50, 20, 0);
  sizeSlider.position(xpos, ypos);
  sizeSlider.size(80);
  xpos += 100;

  sizespTitle = createP("Size Spread");
  sizespTitle.position(xpos, ypos);
  xpos += 80;

  sizespSlider = createSlider(0, 0.1, 0.01, 0);
  sizespSlider.position(xpos, ypos);
  sizespSlider.size(80);
  xpos += 100;

  xpos = 0;
  baseHueTitle = createP("Base Hue");
  baseHueTitle.position(xpos, ypos + 30);
  xpos += 70;

  baseHueSlider = createSlider(0, 360, 250, 0);
  baseHueSlider.position(xpos, ypos + 30);
  baseHueSlider.size(80);
  xpos += 100;

  huespTitle = createP("Hue Spread");
  huespTitle.position(xpos, ypos + 30);
  xpos += 80;

  huespSlider = createSlider(0, 100, 15, 0);
  huespSlider.position(xpos, ypos + 30);
  huespSlider.size(80);
  xpos += 100;
  
  alphaTitle = createP("Transparency");
  alphaTitle.position(xpos, ypos + 30);
  xpos += 90;

  alphaSlider = createSlider(0, 1, 0.75, 0);
  alphaSlider.position(xpos, ypos + 30);
  alphaSlider.size(80);
  xpos += 100;
}

function clearButtonClicked() {
  background(97);
}

```
![captura del ejercicio](/src/assets/Perlin.png)
