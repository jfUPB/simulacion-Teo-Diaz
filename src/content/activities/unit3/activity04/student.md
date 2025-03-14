## algoritmo aceleración
### Aceleracón al mouse
``` javascript
 // Calcular la diferencia entre la posición del mouse y el objeto
  let distance = mouseX - x;

  // La aceleración será proporcional a la distancia entre el objeto y el mouse
  // Ajustar la constante de proporcionalidad para controlar la velocidad de respuesta
  a = distance * 0.001;  // Multiplicamos por un factor para controlar la aceleración

  // Actualizar la velocidad (v = v + a)
  v += a;

  // Actualizar la posición (x = x + v)
  x += v;

```
### Aceleración normal
``` javascript
 // Cambiar la aceleración aleatoriamente en cada fotograma
  a = random(-0.1, 0.1);   // Aceleración aleatoria entre -0.1 y 0.1, tambien se puede dar un valor fijo

  v += a;

  x += v;

  if (x > width) {
    x = 0; // Resetea la posición a la izquierda
  }

  if (x < 0) {
    x = width; // Resetea la posición a la derecha
  }

```
### ¿que tiene que ver con las leyes de newton?

* **Primera Ley de Newton:**  Esta ley nos dice que un objeto en reposo permanece en reposo y un objeto en movimiento permanece en movimiento a una velocidad constante en línea recta, a menos que una fuerza externa actúe sobre él. En otras palabras, si no hay fuerza neta actuando sobre un objeto, su aceleración es cero.

* **Segunda Ley de Newton:** Esta ley establece que la fuerza neta que actúa sobre un objeto es directamente proporcional a la aceleración que experimenta y es inversamente proporcional a su masa. 
    *  \( \textbf{F} = m \textbf{a} \)
    * Esta ecuación nos dice que si aplicamos una fuerza mayor a un objeto, este acelerará más.  Si la masa del objeto es mayor, necesitará una fuerza mayor para lograr la misma aceleración.

* **Tercera Ley de Newton:**  Esta ley nos dice que por cada acción hay una reacción igual y opuesta. En términos de aceleración, esto significa que si un objeto A ejerce una fuerza sobre un objeto B, el objeto B ejercerá una fuerza igual y opuesta sobre el objeto A.  Ambos objetos experimentarán una aceleración, pero en direcciones opuestas.

**Ejemplos:**

* **Un automóvil que acelera:**  La fuerza del motor del automóvil actúa sobre el vehículo, lo que le da una aceleración en la dirección del movimiento.
* **Una pelota que cae:** La fuerza de gravedad actúa sobre la pelota, lo que le da una aceleración hacia abajo.
* **Un patinador sobre hielo que se detiene:**  La fuerza de fricción entre los patines y el hielo actúa sobre el patinador, lo que le da una aceleración en dirección opuesta a su movimiento, hasta que se detiene.

**En resumen:**

La aceleración es un concepto fundamental en las leyes de movimiento de Newton. Es la respuesta directa de un objeto a una fuerza aplicada.  Sin aceleración, no habría movimiento o cambio en el movimiento.
