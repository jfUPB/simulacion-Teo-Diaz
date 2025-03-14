## Cambios realizados:
Cambio en la velocidad al tocar los bordes: Ahora, cuando el objeto toca cualquiera de los bordes (izquierda, derecha, arriba o abajo), la velocidad del objeto se ajusta de manera aleatoria. Esto significa que la dirección y la rapidez del objeto pueden cambiar cada vez que rebote en el borde del canvas.

## Resultado esperado:
Movimiento más impredecible: Con este cambio, el objeto mover ya no se moverá de manera continua y predecible a través del canvas. Cada vez que toque un borde, su velocidad cambiará de manera aleatoria, lo que provocará que el objeto se mueva de manera más errática.

Efecto visual: El movimiento será menos suave y más impredecible, ya que cada vez que el objeto toque un borde, podría empezar a moverse más rápido o más lento, o incluso cambiar de dirección de manera completamente aleatoria. Esto puede crear un patrón de movimiento más "caótico" en el lienzo.

``` javascript
// Declare the Mover object.
let mover;

function setup() {
  createCanvas(640, 240); // Creamos un lienzo de 640x240 píxeles
  // Create the Mover object.
  mover = new Mover(); // Inicializamos el objeto mover
}

function draw() {
  background(255); // Limpiamos el lienzo con un color blanco en cada frame
  
  // Llamamos a los métodos del objeto mover
  mover.update();      // Actualizamos la posición del mover
  mover.checkEdges();  // Verificamos si el mover ha tocado los bordes
  mover.show();        // Dibujamos el mover en el canvas
}

class Mover {
  constructor() {
    // El objeto tiene dos vectores: posición y velocidad
    this.position = createVector(random(width), random(height));  // Posición inicial aleatoria
    this.velocity = createVector(random(-2, 2), random(-2, 2)); // Velocidad aleatoria
  }

  update() {
    // La posición cambia según la velocidad
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);           // Dibuja el contorno en negro
    strokeWeight(2);     // El grosor del contorno es 2
    fill(127);           // Color de relleno gris
    circle(this.position.x, this.position.y, 48);  // Dibuja un círculo en la posición del mover
  }

  checkEdges() {
    // Si el objeto toca los bordes, se reposiciona en el lado opuesto y cambia su velocidad aleatoriamente
    if (this.position.x > width || this.position.x < 0) {
      this.velocity.x = random(-2, 2);  // Cambio aleatorio en la velocidad X
    }

    if (this.position.y > height || this.position.y < 0) {
      this.velocity.y = random(-2, 2);  // Cambio aleatorio en la velocidad Y
    }
  }
}
```
