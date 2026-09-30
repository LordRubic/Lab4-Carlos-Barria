# Reflexión del equipo

**Instrucciones:** respondan **solo las 4 preguntas de su versión** (A o B), con **sus propias palabras** (3–5 líneas cada una)
y **citando nombres de métodos o líneas de SU código**. Las respuestas genéricas o iguales a las de otro grupo se califican en 0.
Escriban debajo de cada pregunta. (Se evalúa después; el autograde no califica este archivo.)

---

## VERSIÓN A

**A1.** `aplicarFactor` modifica el arreglo original, pero `copiaEscalada` no. Expliquen por qué, y qué es lo que
realmente se copia cuando le pasan un arreglo a un método.

> _Respuesta:_

**A2.** ¿Por qué Java no permite tener `double calcularCosto(double kwh)` y `int calcularCosto(double kwh)` en la misma clase?
¿Qué versión de `calcularCosto` elige Java para la llamada `calcularCosto(5, 2.5, 0.1)` y por qué?

> _Respuesta:_

**A3.** En `Medidor`, ¿para qué sirve `this(id, 0)` en el constructor de un solo parámetro? ¿Qué ventaja tiene frente a copiar y pegar el código del otro constructor?

> _Respuesta:_

**A4.** ¿Por qué los atributos de `Medidor` son `private`? ¿Qué protege `registrarLectura` y qué podría pasar si `lecturaActual` fuera público?

> _Respuesta:_

---

## VERSIÓN B

**B1.** Dibujen con texto (cajas y flechas) qué pasa en la memoria —variable `datos`, el arreglo y el parámetro del método—
cuando se ejecuta `aplicarFactor(datos, 2)`. ¿Por qué el arreglo original queda modificado?

> _Respuesta:_[Variable Datos] -----> [Arreglo en memoria] <------- [Parametro lecturas]
El arreglo original queda modificado porque en Java, cuando pasas un arreglo como parámetro, no se copia toda su información.

**B2.** `imprimirEncabezado` es `void` y `clasificarConsumo` devuelve `String`. ¿Qué error da el compilador si olvidan un `return`
en alguna rama de `clasificarConsumo`? Expliquen con un caso de su código.

> _Respuesta:_El error que daria el compilador es missing return statement,
Como el método clasificarconsumo promete devolver un String, Java exige estar seguro de que cualquier ruta que tome el código terminará entregando un texto. Por ejemplo, en mi código tengo un if para "BAJO" y un else if para "MEDIO". Si omitimos el else final que devuelve "ALTO", el compilador detecta que un consumo altísimo, no entraría en las dos primeras condiciones, llegaría al final de las llaves del método sin ejecutar ningún return y rompería el ciclo de devolver un String

**B3.** ¿Por qué `sumaRecursiva` necesita un caso base? ¿Qué error aparece en Java si se omite y por qué ocurre?

> _Respuesta:_El caso base funciona como el freno de emergencia. Es necesario para decirle al método cuándo debe dejar de llamarse a sí mismo y empezar a devolver los resultados finales.   Si se omite, ocurre el error StackOverflowError. Esto pasa porque cada vez que un método se llama, Java reserva un pequeño bloque en una sección de la memoria para guardar el estado de esa llamada. Sin un caso base, el método se llama a sí mismo infinitamente, apilando llamadas hasta que la memoria designada para la pila se agota por completo y el programa colapsa

**B4.** Si `Medidor` tuviera un atributo `double[] historial` y un getter que lo devolviera directamente, ¿qué riesgo hay para el
encapsulamiento? ¿Cómo se soluciona (idea de *copia defensiva*)?

> _Respuesta:_El riesgo es que se rompe la protección de los datos privados. Si el getter devuelve el double directamente, está entregando la referencia de memoria del arreglo original. Cualquier otra parte del programa que llame a ese getter podría modificar, borrar o alterar los datos del historial desde afuera de la clase Medidor, sin usar los métodos permitidos.

La solución consiste en que el getter no devuelva el arreglo original, sino que cree un arreglo nuevo idéntico, copie los valores uno por uno, y devuelva esa copia nueva. De esta forma, si el código externo modifica el arreglo que recibió, solo estará alterando su propia copia desechable y el historial original del medidor permanecerá intacto
