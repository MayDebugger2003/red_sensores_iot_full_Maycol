# Bitacora individual - Semana [XX]

> Copia este archivo y renombralo como `s[XX]-[tu-nombre].md`.
> Completa todas las secciones con tus propias palabras. Esta bitacora es
> individual, aunque el codigo pueda haberse construido en equipo.

## 1. Datos de la actividad

- **Estudiante:** [Maycol Gamboa]
- **Equipo:** Solo
- **Semana:** [5]
- **Fecha del laboratorio:** [2026-10-26]
- **Fecha del taller:** [2026-10-26]
- **Tema principal:** [Listas enlazadas, contratos e implementación de repositorios.]
- **Pregunta de la semana:** [¿Cuándo conviene utilizar una lista enlazada y cuándo una estructura basada en arreglos?]

## 2. Prediccion antes de ejecutar

Antes de abrir o ejecutar el programa, responde:

1. **Que creo que va a ocurrir?**
   Creo que la lista enlazada será más rápida para insertar elementos al inicio porque solo necesita modificar enlaces entre nodos. También considero que los arreglos serán más rápidos para acceder a una posición específica porque pueden utilizar índices directamente. 

2. **Que parte del programa o del algoritmo puede fallar?**
   La operación de eliminación puede presentar errores cuando se elimina el primer nodo, el último nodo o el único nodo de la lista. También es importante verificar que las referencias primero y ultimo se actualicen correctamente.

3. **Como comprobare mi prediccion?**
   Ejecutaré los experimentos comparando ArrayList y LinkedList, observando los tiempos de inserción y acceso. Además, probaré operaciones de eliminación y compararé los resultados de tamano() con contarRecorriendo().]

## 3. Evidencia del laboratorio

### Resultado observado

Durante las pruebas se compararon estructuras basadas en arreglos y listas enlazadas.

En la inserción de 50.000 lecturas al inicio, LinkedList tardó aproximadamente 1 ms mientras que ArrayList tardó 34 ms.

Al recorrer 50.000 lecturas usando get(i), ArrayList tardó 4 ms mientras que LinkedList tardó 602 ms.

Cuando se utilizó un recorrido tipo for-each, ambas estructuras mostraron resultados similares, con aproximadamente 3 ms para ArrayList y 2 ms para LinkedList.

También se observó que la detección de duplicados mediante contains() se vuelve más lenta conforme aumenta la cantidad de elementos.



### Diferencia entre la prediccion y el resultado
La predicción coincidió con los resultados obtenidos. La lista enlazada resultó mucho más eficiente para inserciones al inicio, mientras que el arreglo fue claramente superior para acceder a posiciones específicas mediante índices.
### Error o comportamiento inesperado

¿Qué ocurrió? Se produjo una excepción ConcurrentModificationException al intentar eliminar elementos durante un recorrido for-each.
¿Por qué ocurrió? Porque la colección se modificó mientras estaba siendo recorrida por el iterador interno utilizado por el ciclo.
¿Cómo lo corregimos o qué falta corregir? Utilizando un Iterator para realizar las eliminaciones o realizando los cambios fuera del recorrido.

## 4. Explicacion en lenguaje llano
Una lista enlazada funciona como una fila de personas donde cada persona sabe quién está detrás de ella. Agregar una nueva persona al inicio es fácil porque solo hay que conectarla con la primera. Sin embargo, encontrar a una persona específica requiere revisar una por una hasta llegar a la posición deseada. Por eso algunas operaciones son muy rápidas y otras más lentas.



### Ejemplo o analogia
Una lista enlazada se parece a una cadena de vagones de tren.

Cada vagón representa un nodo. Cada vagón tiene una carga, que corresponde al dato almacenado, y un enganche que lo conecta con el siguiente vagón. Agregar un nuevo vagón al inicio es sencillo porque solo se conecta antes del primero. La analogía deja de ser exacta porque los nodos existen en memoria y pueden crearse o eliminarse dinámicamente.



## 5. El vacio que encontre

Mi duda concreta es: ¿Por qué una lista enlazada puede ser tan lenta cuando se utiliza get(i) repetidamente?
Lo que ya puedo explicar es: Cómo funcionan los nodos, los enlaces y las operaciones básicas de inserción y eliminación.
Para resolver la duda consulté: El código de RepositorioEnlazado, las pruebas de rendimiento y las explicaciones del laboratorio.
Ahora lo entiendo así: Cada llamada a get(i) obliga a recorrer la lista desde el inicio hasta la posición solicitada, por lo que repetir muchas veces esta operación incrementa considerablemente el tiempo de ejecución.
## 6. Trazado de la solucion

Escoge una ejecucion, recorrido o caso representativo y trazalo paso a paso.
Incluye los valores importantes despues de cada paso.

Paso	Estado de los datos o estructura	Decisión o resultado
1	Lista vacía (null)	Estado inicial
2	A	Se agrega el primer nodo
3	A → B	Se agrega B al final
4	X → A → B	Se agrega X al inicio
5	X → B	Se elimina A
6	X	Se elimina B
7	null	Se elimina X y la lista queda vacía


**Completa o agrega filas si es necesario.** Si trabajaste con una estructura,
dibuja su estado en cada paso o inserta aqui una imagen legible.

## 7. Decision de diseño

Relaciona lo aprendido con la Plataforma de Monitoreo Ambiental Urbano.

- **Problema que debiamos resolver:** Almacenar y gestionar lecturas de sensores dentro de la Plataforma de Monitoreo Ambiental Urbano.


- **Estructura, algoritmo o estrategia elegida:** Lista enlazada implementada mediante RepositorioEnlazado.


- **Alternativa descartada:** Repositorio basado en ArrayList.


- **Por que elegimos la primera:** La lista enlazada permite insertar elementos al inicio de forma muy eficiente, evitando desplazar todos los elementos ya existentes.


- **Que evidencia respalda la decision:**Los experimentos mostraron que insertar 50.000 lecturas al inicio tomó aproximadamente 1 ms en la lista enlazada y 34 ms en la estructura basada en arreglo.



## 8. Aporte al proyecto

- **Archivo(s) o modulo(s) trabajado(s):**  Branch Cambios
- **Cambio realizado:**  Corrección y prueba de operaciones sobre la lista enlazada.
- **Como se conecta con la capa anterior:** Implementa el contrato definido por la interfaz Repositorio.
- **Que queda pendiente para la siguiente semana:** Terminar semana 6

## 9. Commits realizados

Registra los commits que muestran tu aporte individual.

| Commit | Mensaje | Que demuestra |
|---|---|---|
| `[hash corto]` | `[mensaje del commit]` | [Cambio realizado] |
| `[hash corto]` | `[mensaje del commit]` | [Cambio realizado] |

## 10. Reexplicacion final

Despues del taller, vuelve a responder la pregunta de la semana en cinco lineas
o menos. Esta respuesta debe ser mas precisa que la de la seccion 4 y debe
incluir la razon de tu decision tecnica.
La lista enlazada resulta más conveniente cuando predominan las inserciones y eliminaciones, especialmente al inicio de la estructura. Los arreglos son más eficientes cuando se realizan consultas frecuentes por posición porque permiten acceso directo mediante índices. Los experimentos realizados confirmaron estas diferencias de rendimiento y ayudaron a justificar la elección de cada estructura según el problema.

## 11. Reflexion individual

Responde con honestidad:

1. **Lo que ahora puedo hacer y antes no podia:**
   [Analizar el comportamiento de una lista enlazada y comparar su rendimiento con otras estructuras de datos.
.]
2. **El error o supuesto que mas me enseno:**
   [Pensar que todas las listas tienen el mismo rendimiento independientemente de cómo estén implementadas.

.]
3. **La pregunta que llevaria a la proxima clase:**
   [¿Cómo se comportan las listas doblemente enlazadas frente a las listas enlazadas simples?

.]
4. **Que parte del trabajo fue realmente mia:**
   [Análisis de resultados, pruebas de funcionamiento y comprensión de la implementación de la estructura enlazada.



## Lista de verificacion antes de entregar

- [ x] Escribi la prediccion antes de consultar el resultado.
- [ x] Inclui evidencia concreta del laboratorio.
- [ x] Explique un concepto sin depender de jerga.
- [ x] Registre un vacio, una duda o un error real.
- [ x] Trace al menos un caso paso a paso.
- [ x] Justifique una decision del proyecto y una alternativa descartada.
- [ x] Registre mis commits y mi aporte individual.
- [ x] Deje claro que queda pendiente.
- [ x] Renombre el archivo con el formato `sXX-nombre.md`.
