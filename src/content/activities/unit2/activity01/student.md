## Suma de vectores
La suma de dos vectores se puede hacer de manera muy sencilla utilizando el objeto createVector(), que permite trabajar con vectores. Para sumar dos vectores, solo debes sumar sus componentes correspondientes (es decir, la componente X con la componente X y la componente Y con la componente Y).

## ¿La línea position = position + velocity;?

La línea position = position + velocity; no funciona porque los vectores no se pueden sumar de esa manera directamente. Las variable position y velocity son vectores, y no puedes simplemente sumarlos con el operador + como lo harías con números simples.

Para sumar vectores, debes usar el método .add() que está disponible en los objetos ".Vector". Este método se asegura de que cada componente (X, Y, Z si fuera el caso) se sume correctamente.

```javascript
position = position + velocity; // Incorrecto

position.add(velocity); // Correcto
```
