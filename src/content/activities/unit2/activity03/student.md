## ¿Qué resultado esperas obtener?
Que aparezca en consola "Only once" 
## ¿Qué resultado obtuviste?
Pinto de gris y salio en texto en consola
### 1. Paso por Valor:
Definición: Cuando un valor es pasado por valor a una función, se pasa una copia del valor. Es decir, cualquier cambio hecho en la variable dentro de la función no afecta la variable original fuera de la función.
Aplicación: Este comportamiento se aplica a los tipos primitivos en JavaScript, como números, cadenas de texto, booleanos, undefined, null, etc.
#### Ejemplo:
``` javascript
function cambiarValor(x) {
    x = 10;
    console.log("Dentro de la función:", x); // Imprime 10
}

let a = 5;
cambiarValor(a);
console.log("Fuera de la función:", a); // Imprime 5
```
### 2. Paso por Referencia:
Definición: Cuando un valor es pasado por referencia a una función, se pasa una referencia al objeto en memoria. Esto significa que cualquier cambio realizado en el objeto dentro de la función sí afectará al objeto original.
Aplicación: Este comportamiento se aplica a los tipos de objetos en JavaScript, como objetos literales, arrays, funciones, y también instancias de clases.
#### Ejemplo:
``` javascript
function cambiarPropiedad(obj) {
    obj.nombre = "Juan";
    console.log("Dentro de la función:", obj.nombre); // Imprime 'Juan'
}

let persona = { nombre: "Carlos" };
cambiarPropiedad(persona);
console.log("Fuera de la función:", persona.nombre); // Imprime 'Juan'
```
## ¿Qué tipo de paso se está realizando en el código?
Paso por referencia, porque el vector posicion (un objeto) se pasa a la función y cualquier modificación que se haga dentro de la función afecta directamente al objeto original fuera de ella.
## ¿Qué aprendiste?
Como funcionan los conceptos de pasos por valor y refencia a la hora de programar y como aplicarlos.
