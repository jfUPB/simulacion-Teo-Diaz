### Codigo

[Enlace al editor de p5.js con la simulación](https://editor.p5js.org/Teo-Diaz/sketches/3d8nPcaIn)
![captura del ejercicio](/src/assets/unidad_1.png)
``` javascript
let walker;
let mode = "Gaussian"; // El modo inicial será "Gaussian"

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  // Cambiar el modo según la posición del mouse
  if (mouseX < width / 3) {
    mode = "Levy";
  } else if (mouseX < 2 * width / 3) {
    mode = "Gaussian";
  } else {
    mode = "Perlin";
  }
    
  // Llamar al método de paso según el modo
  walker.step(mode);
  walker.show();
  
  // Verificar si el walker está fuera de los límites del canvas
  if (walker.x < 0 || walker.x > width || walker.y < 0 || walker.y > height) {
    walker.resetToCenter();
  }
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.time = 0; // Variable para animar el ruido Perlin
    this.color = color(random(255), random(255), random(255)); // Color aleatorio inicial
  }

  show() {
    noFill();  // No rellenar el círculo
    stroke(this.color);  // Establecer el color del borde del círculo
    square(this.x, this.y, 20);  // Dibujar el círculo
  }

  step(mode) {
    
    print(mode)
    
    let xstep, ystep;

    if (mode === "Levy") {
      // Salto de Lévy (Levy flight)
      xstep = this.levyStep();
      ystep = this.levyStep();
    } else if (mode === "Gaussian") {
      // Distribución Gaussiana (Normal)
      xstep = randomGaussian();  // Paso de acuerdo con la distribución normal
      ystep = randomGaussian();
    } else if (mode === "Perlin") {
      // Ruido Perlin
      xstep = this.perlinStep('x');  // Paso usando ruido Perlin para x
      ystep = this.perlinStep('y');  // Paso usando ruido Perlin para y
    }

    this.x += xstep;
    this.y += ystep;
  }

  // Función para pasos con salto de Lévy (Levy flight)
  levyStep() {
    // Usamos una distribución de Ley de Potencias (exponente -1.5)
    let r = pow(random(1), 2);  // Distribución de Ley de Potencias
    return random([-1, 1]) * r * 20; // Paso aleatorio multiplicado por un valor en potencia
  }

  // Función para pasos con ruido Perlin
  perlinStep(axis) {
    let noiseVal;
    if (axis === 'x') {
      noiseVal = noise(this.time) * 2 - 1;  // Generar ruido para x
    } else {
      noiseVal = noise(this.time + 1000) * 2 - 1;  // Generar ruido para y
    }
    this.time += 0.01;  // Incrementar el tiempo para el siguiente paso
    return noiseVal * 2;  // Escalar el ruido
  }

  // Método para restablecer la posición al centro con un color aleatorio
  resetToCenter() {
    this.x = width / 2;
    this.y = height / 2;
    this.color = color(random(255), random(255), random(255)); // Nuevo color aleatorio
  }
}

````
