## ¿Para qué sirve el método mag()?
El método **mag()** devuelve la magnitud (o longitud) de un vector, es decir, su distancia desde el origen (0, 0) hasta el punto que representa. Es equivalente a calcular la raíz cuadrada de la suma de los cuadrados de sus componentes (como el teorema de Pitágoras).

## ¿Cuál es la diferencia entre mag() y magSq()?

**mag():** Devuelve la magnitud del vector (raíz cuadrada de la suma de los cuadrados de sus componentes).
**magSq():** Devuelve el cuadrado de la magnitud, lo que evita calcular la raíz cuadrada, lo cual puede ser más eficiente en términos de rendimiento.
## ¿Cuál es más eficiente? 
**magSq()** es más eficiente porque no tiene que calcular la raíz cuadrada.
## ¿Para qué sirve el método normalize()?
**normalize()** ajusta un vector para que tenga una magnitud de 1, es decir, lo convierte en un vector unitario. No cambia la dirección del vector, solo su tamaño.

### El método dot(), ¿qué le responderías a un periodista?

El método **dot()** calcula el producto punto entre dos vectores, lo que nos da una medida de cuán alineados están esos vectores. Si el producto punto es 0, los vectores son perpendiculares.

## ¿Cuál es la diferencia entre la versión estática y la de instancia de dot()?

**Estática (p5.Vector.dot(v1, v2)):** Se llama sin necesidad de un objeto, pasando los dos vectores como parámetros.

**De instancia (v1.dot(v2)):** Se llama sobre un vector específico, con el otro vector como argumento.

##¿Cuál es la interpretación geométrica del producto cruz?
El **producto cruz** de dos vectores en 3D genera un vector perpendicular a los dos vectores originales. La magnitud de este vector es igual al área del paralelogramo formado por los dos vectores, y su orientación sigue la regla de la mano derecha. Si los vectores están alineados, el producto cruz es el vector nulo (0,0,0).

## ¿Para qué te puede servir el método dist()?
**dist()** calcula la distancia euclidiana entre dos puntos en el espacio. Es útil cuando necesitas saber qué tan lejos están dos puntos en un plano o en el espacio.

## ¿Para qué sirven los métodos normalize() y limit()?

**normalize():** Como mencionamos antes, convierte un vector en un vector unitario, es decir, lo reduce a una magnitud de 1 sin cambiar su dirección.
**limit():** Restringe la magnitud de un vector a un valor máximo dado. Si la magnitud del vector es mayor que el límite, se reduce al valor especificado. Es útil cuando quieres evitar que un vector sea demasiado grande.
