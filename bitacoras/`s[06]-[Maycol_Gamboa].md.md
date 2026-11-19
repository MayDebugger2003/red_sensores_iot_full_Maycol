# Bitacora individual - Semana [06]

> Copia este archivo y renombralo como `s[XX]-[tu-nombre].md`.
> Completa todas las secciones con tus propias palabras. Esta bitacora es
> individual, aunque el codigo pueda haberse construido en equipo.

## 1. Datos de la actividad

- **Estudiante:** [  Maycol Gamboa]
- **Equipo:** [solo]
- **Semana:** [06]
- **Fecha del laboratorio:** [2026-10-29]
- **Fecha del taller:** [2026-10-29]
- **Tema principal:**Pilas, colas circulares y colas de prioridad mediante montículos (Heap).
- **Pregunta de la semana:** ¿Por qué limitar las operaciones permitidas en una estructura puede ayudar a resolver un problema de forma más eficiente?

## 2. Prediccion antes de ejecutar

Antes de abrir o ejecutar el programa, responde:

1. **Que creo que va a ocurrir?**
Creo que cada estructura resolverá mejor un problema específico debido a las restricciones que impone. La pila será útil para deshacer acciones, la cola circular permitirá procesar lecturas sin perder espacio y la cola de prioridad atenderá primero las alertas más importantes.
2. **Que parte del programa o del algoritmo puede fallar?**
Los casos límite de cada estructura. En la pila podría fallar el desapilado de una estructura vacía. En la cola circular podrían fallar los índices cuando lleguen al final del arreglo. En el montículo podrían aparecer errores al reorganizar las prioridades después de insertar o retirar alertas.


3. **Como comprobare mi prediccion?**
Ejecutaré los experimentos de BancoDeFlujo y observaré el comportamiento de las estructuras, verificando el orden de procesamiento, la cantidad de elementos descartados y las comparaciones realizadas.


## 3. Evidencia del laboratorio

### Resultado observado

En el experimento de deshacer acciones, la pila almacenó tres acciones y las devolvió exactamente en orden inverso al de inserción.

Resultado:

Desactivar EST-007
Cambiar umbral de PM2.5 a 35
Marcar EST-003 como sospechosa
En la cola circular llegaron 5.000 lecturas y se procesaron 4.997 sin perder ninguna. Solo quedaron tres lecturas esperando en el buffer y no se registraron descartes.

Posteriormente se realizó una prueba con 200.000 lecturas y tampoco se produjeron descartes, manteniendo un tiempo total de ejecución de 4 ms.

Finalmente se comparó una lista ordenada contra un montículo para manejar alertas:

Alertas	Lista ordenada	Heap
10.000	16.324.390 comparaciones - 21 ms	15.951 comparaciones - 2 ms
50.000	417.608.571 comparaciones - 599 ms	80.564 comparaciones - 2 ms


### Diferencia entre la prediccion y el resultado

La predicción fue correcta. Cada estructura resolvió eficientemente el problema para el que fue diseñada. El resultado más llamativo fue la diferencia de rendimiento entre la lista ordenada y el montículo, ya que este último necesitó muchas menos comparaciones aun con grandes cantidades de alertas.
### Error o comportamiento inesperado

- **Que ocurrio?** Inicialmente existía el riesgo de que la cola descartara lecturas aun cuando hubiera espacios libres dentro del arreglo.


- **Por que ocurrio?** Porque una implementación no circular desperdicia los espacios liberados en las primeras posiciones.


- **Como lo corregimos o que falta corregir?** Utilizando una cola circular mediante operaciones módulo (%) para reutilizar las posiciones disponibles.



## 4. Explicacion en lenguaje llano

Explica el concepto principal como se lo explicarias a una persona de doce
anos. Usa entre tres y cinco lineas y evita palabras tecnicas que no expliques.

Esta semana aprendí que algunas estructuras funcionan mejor cuando se les prohíben ciertas acciones. Una pila solo permite trabajar por arriba, una cola obliga a respetar el turno y una cola de prioridad deja pasar primero lo más importante. Estas restricciones hacen que resolver ciertos problemas sea más sencillo y rápido.
### Ejemplo o analogia

La pila es una torre de platos: el último plato que se coloca es el primero que se retira.

La cola circular es una fila de personas esperando atención, donde nadie puede saltarse el turno.

La cola de prioridad es una sala de urgencias, donde una persona con una emergencia grave puede ser atendida antes que otras que llegaron primero.

La analogía deja de ser exacta porque en programación los elementos se almacenan en memoria y las prioridades se calculan mediante algoritmos.


## 5. El vacio que encontre

Al intentar explicar el tema, identifica el punto que aun no comprendes bien.

- **Mi duda concreta es:** ¿Por qué el heap necesita tan pocas comparaciones comparado con una lista ordenada?
- **Lo que ya puedo explicar es:** Cómo funcionan las pilas, las colas y la prioridad basada en severidad.
- **Para resolver la duda consulte:** El código de ColaDeAlertas, las explicaciones de clase y los experimentos ejecutados.
- **Ahora lo entiendo asi:** El heap no necesita mantener todos los elementos completamente ordenados. Solo garantiza que el elemento más importante quede en la raíz, reduciendo significativamente la cantidad de trabajo necesario.

## 6. Trazado de la solucion

Escoge una ejecucion, recorrido o caso representativo y trazalo paso a paso.
Incluye los valores importantes despues de cada paso.

|Pila de acciones
Paso	Estado de la estructura	Resultado
1	Vacía	Estado inicial
2	Marcar sospechosa	Primera acción
3	Marcar sospechosa, Cambiar umbral	Segunda acción
4	Marcar sospechosa, Cambiar umbral, Desactivar estación	Tercera acción
5	Marcar sospechosa, Cambiar umbral	Deshacer última acción
6	Marcar sospechosa	Deshacer segunda acción
7	Vacía	Deshacer tercera acción
Cola Circular
Paso	Estado de la estructura	Resultado
1	Vacía	Inicio
2	L1	Llega lectura
3	L1, L2	Llega segunda lectura
4	L1, L2, L3	Llega tercera lectura
5	L2, L3	Se procesa L1
6	L2, L3, L4	Entra nueva lectura reutilizando espacio
7	L3, L4	Se procesa L2

**Completa o agrega filas si es necesario.** Si trabajaste con una estructura,
dibuja su estado en cada paso o inserta aqui una imagen legible.

## 7. Decision de diseño

Relaciona lo aprendido con la Plataforma de Monitoreo Ambiental Urbano.

- **Problema que debiamos resolver:** Gestionar acciones de operadores, procesar lecturas de sensores y atender alertas críticas dentro de la plataforma.


- **Estructura, algoritmo o estrategia elegida:** Pila para historial de acciones.
Cola circular para ingesta de lecturas.
Montículo (Heap) para atención de alertas.
- **Alternativa descartada:** Lista ordenada para manejar las alertas.


- **Por que elegimos la primera:** El montículo realiza muchas menos comparaciones y mantiene acceso rápido a la alerta más urgente.


- **Que evidencia respalda la decision:** Con 50.000 alertas:

Lista ordenada:
417.608.571 comparaciones
599 ms

Heap:
80.564 comparaciones
2 ms
Los resultados muestran una diferencia enorme de rendimiento.


## 8. Aporte al proyecto

- **Archivo(s) o modulo(s) trabajado(s):** Red_sensores_Iot_full_Maycol
- **Cambio realizado:**  Implementación y validación de estructuras restringidas para acciones, lecturas y alertas.
- **Como se conecta con la capa anterior:**  Permite procesar información almacenada por las estructuras desarrolladas en semanas anteriores.
- **Que queda pendiente para la siguiente semana:** Entregar proyecto finall

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

Limitar las operaciones de una estructura ayuda a resolver problemas concretos de manera más eficiente. La pila permite deshacer acciones usando LIFO, la cola circular procesa lecturas respetando FIFO y el montículo atiende primero las alertas más urgentes. Los experimentos demostraron que estas restricciones producen mejoras importantes de rendimiento frente a alternativas más generales.
## 11. Reflexion individual

Responde con honestidad:

1. **Lo que ahora puedo hacer y antes no podia:**
Identificar cuándo utilizar una pila, una cola circular o una cola de prioridad según las necesidades del sistema.

2. **El error o supuesto que mas me enseno:**
Suponer que mantener todos los datos ordenados siempre es la mejor solución.

3. **La pregunta que llevaria a la proxima clase:**
¿Cómo se comporta un heap cuando el volumen de alertas crece a millones de elementos?

4. **Que parte del trabajo fue realmente mia:**
La ejecución de experimentos, análisis de resultados y comprensión del comportamiento de cada estructura.


## Lista de verificacion antes de entregar

- [ x] Escribi la prediccion antes de consultar el resultado.
- [x ] Inclui evidencia concreta del laboratorio.
- [x ] Explique un concepto sin depender de jerga.
- [ x] Registre un vacio, una duda o un error real.
- [x ] Trace al menos un caso paso a paso.
- [x ] Justifique una decision del proyecto y una alternativa descartada.
- [x ] Registre mis commits y mi aporte individual.
- [ x] Deje claro que queda pendiente.
- [x ] Renombre el archivo con el formato `sXX-nombre.md`.
