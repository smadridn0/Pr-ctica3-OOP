# Regresión lineal múltiple
El objetivo de nuestros códigos es hacer un modelo de regresión lineal simple que prediga, con el primer código, las ventas de helado según la temperatura de este, y con el segundo código, la calificación de cada estudiante según una variedad de factores dados. En ambos casos se usó el método de gradiente descendiente explicado en clase.
Debido a que ambos códigos tienen propósitos relativamente similares, ambos son bastante parecidos(además por razones que se elaboraran en la sección de errores y problemas).
Como se nos dio la elección de hacer el codigo en c++ o en java, se escogió java, pues consideramos que la clase de pensamiento computacional del semestre pasado nos dio unas bases bastante buenas para llevar a cabo esta practica.
## Clases:
Ambos códigos usaron las mismas clases:
### RegresionLineal 
implementa el modelo (atributos, entrenamiento y predicción).


### DivisionEntrenamientoPrueba
contenedor para los conjuntos de entrenamiento y prueba.


### AleatorioSimple
Para generar números aleatorios, pues se asumió que no se podía usar la librería random de java.


### main
Ejecuta todo el programa: Imprime encabezado, carga dataset de temperaturas y ventas, divide datos (80% entrenamiento, 20% prueba), crea modelo, entrena modelo, Muestra los weighs y bias, predice sobre el test set. evalúa los resultados y los interpreta; además de contener métodos auxiliares.

## RegresionLineal:
### **Atributos**
### Weights:
Contiene los parametros del modelo. Al ser regresión lineal simple, solo se tiene uno en el primer codigo. Actua como la w de la función y=wx+b
Bias: el intercepto de la función(la variable b).

### ajustado:
Indica que el modelo ya fue entrenado, para evitar que se use predict() antes de entrenar.

### mediaEscalador y desviacionEscalador:
guardan la media y desviación estándar de cada característica de los datos.

### TazaAprendizaje: 
El alfa de los datos, Controla qué tan grande es cada paso al ajustar los pesos.
epocas: El numero de iteraciones del algoritmo.<img width="140" height="43" alt="Captura de pantalla 2025-11-04 013028" src="https://github.com/user-attachments/assets/f80bc048-bc94-4616-877c-7a5f7d5f2fd2" />



### historialCosto: 
guarda el valor del costo o error luego de cierto numero de iteraciones.

### tamanioHistorialCosto: 
Como su nombre lo indica, mide el numero de valores de historialCosto.
## **Metodos**
### private double media(double[] arreglo):
Calcula la media aritmética:
<img width="225" height="38" alt="Captura de pantalla 2025-11-04 012742" src="https://github.com/user-attachments/assets/4fce8777-a7f4-4ed6-9705-dcb8b00a1435" />
### private double desviacionEstandar(double[] arreglo):
Calcula la desviación estándar,  Si la desviación resulta 0 la reemplaza por 1.0 para evitar división por cero.
<img width="311" height="49" alt="Captura de pantalla 2025-11-04 012826" src="https://github.com/user-attachments/assets/9e457ea7-be4a-4ee0-924f-46c4f78a7104" />
### private double[] obtenerColumna(double[][] matriz, int indiceColumna)
Extrae la columna indiceColumna de una matriz double[][] y la devuelve como double[], para calcular media y desviación por característica.
### public double[][] data_scaling(double[][] X, boolean ajustarEscalador)
Implementa la formula StandardScaler (z-score), que es:
<img width="140" height="43" alt="Captura de pantalla 2025-11-04 013028" src="https://github.com/user-attachments/assets/05d8aac7-1eeb-47ca-90bc-68e03e991e97" />!
Si ajustarEscalador es verdadero, calcula mediaEscalador y desviacionEscalador a partir de X, si es falso, eutiliza mediaEscalador y desviacionEscalador para normalizar nuevos datos (por ejemplo, datos de prueba).
### public void fit(double[][] XEntrenamiento, double[] yEntrenamiento, boolean usarEscalado)
El encargado de entrenar el modelo de regresión lineal simple utilizando el algoritmo de descenso de gradiente. Primero, toma los valores de entrada x y los valores objetivo y y, con ellos, inicializa los parámetros del modelo: el coeficiente m y la intersección b. Luego, entra en un ciclo iterativo donde, en cada paso, calcula las predicciones del modelo con la fórmula y_pred = m * x + b. Después, evalúa el error entre esas predicciones y los valores reales, y a partir de ese error calcula la derivada del costo respecto a m y b usando las fórmulas del descenso de gradiente. Con esas derivadas, ajusta los valores de m y b, moviéndose ligeramente en la dirección que reduce el error total. Este proceso se repite durante el número de iteraciones especificado, o hasta que el modelo converge. Al finalizar, el método habrá encontrado los valores de m y b que mejor se ajustan a los datos, y el modelo estará listo para hacer predicciones nuevas.

### public double[] predict(double[][] XPrueba)
Usa la formula: Para cada muestra.
<img width="188" height="29" alt="Captura de pantalla 2025-11-04 014008" src="https://github.com/user-attachments/assets/a73f36e2-755a-40b2-9238-a21a9387bce0" />
### public double score(double[][] XPrueba, double[] yPrueba)
Calcula (R^2) (coeficiente de determinación):
<img width="259" height="82" alt="Captura de pantalla 2025-11-04 014058" src="https://github.com/user-attachments/assets/9e90a61d-602c-43e7-8468-8f0bc0f3c3aa" />
donde SSres es la suma de cuadrados de residuos<img width="121" height="46" alt="Captura de pantalla 2025-11-04 014139" src="https://github.com/user-attachments/assets/3d45434d-0f78-46f2-98de-74b3363d46fc" />
y SStot es la suma total de cuadrados respecto a la media de y.
Devuelve double menores a 1.0. Valores cercanos a 1 indican buen ajuste; cercano a 0 o negativos indican mal ajuste.
### Getters y demas:
getWeights() y getBias() son getters, y  formatearDecimal(double valor, int decimales) es usado para convertir un double a un String.
En el segundo código también se añadieron otros métodos para métricas de error, que también estaban en el material usado para comprender cómo funciona el score a la hora de hacer el segundo código. Estos son:
### calcularECM(double[][] XPrueba, double[] yPrueba): 
Calcula el error cuadratico medio según la formula:
<img width="331" height="142" alt="Captura de pantalla 2025-11-04 221722" src="https://github.com/user-attachments/assets/da5696f7-e034-4ce4-bcf7-4255e26a5161" />


### calcularRCEM(double[][] XPrueba, double[] yPrueba): 
calcula la raíz del error cuadratico medio, para un resultado mas claro e intuitivo.
### calcularEAM(double[][] XPrueba, double[] yPrueba): 
calcula el error absoluto medio(el valor absoluto del ECM sin elevar al cuadrado.

## DivisionEntrenamientoPrueba
Es usada para contener los atributos públicos:


double[][] XEntrenamiento


double[][] XPrueba


double[] yEntrenamiento


double[] yPrueba

## AleatorioSimple
Usa el agoritmo LCG: semilla = (semilla * 9301 + 49297) % 233280. Devuelve (int)((semilla / 233280.0) * n), es decir un entero en [0, n-1].

## main
### **funciones auxiliares**
### repetir(String cadena, int veces) 
repite una cadena “veces” veces (concatena).

### formatearDecimal(double valor, int decimales) 
idéntico al de la clase RegresionLineal pero estático para el main.

### dividirEntrenamientoPrueba(double[] X, double[] y, double tamanoPrueba, long semilla)
Toma vectores 1D X (aquí las temperaturas) y y (ventas), luego Crea indices aleatorios usando AleatorioSimple(semilla).
Construye muestrasPrueba = (int) (n * tamanoPrueba) y muestrasEntrenamiento = n - muestrasPrueba.
Y, finalmente, rellena DivisionEntrenamientoPrueba con matrices double[][] de 1 columna (forma [muestras][1]) porque el modelo espera double[][] para X.

### arregloACadena(double[] arreglo) 
convierte vector a representación textual con formatearDecimal.
### **El flujo de main:**
1.Imprime header (líneas = y título).

2.Carga los datos: dos vectores temperatura y ventas (ambos double[] con la misma longitud).

3.Llama a dividirEntrenamientoPrueba(temperatura, ventas, 0.2, 42) ⇒ 80% entrenamiento / 20% prueba.

4.Crea RegresionLineal mlr = new RegresionLineal(0.1, 20000) — tasa de aprendizaje = 0.1, epochs = 20000.

5.Llama mlr.fit(division.XEntrenamiento, division.yEntrenamiento, true) — entrena con escalado (z-score).

6.Imprime weights y bias usando arregloACadena(mlr.getWeights()) y mlr.getBias().

7.Llama mlr.predict(division.XPrueba) y muestra las primeras 5 predicciones comparadas con los valores reales.

8.Llama mlr.score(division.XPrueba, division.yPrueba) — imprime R².

9.Interpreta R² con reglas sencillas:
  0.8 : "Ajuste excelente!"
  0.6 : "Buen ajuste."
  0 : "Ajuste moderado."
  ≤ 0 : "Ajuste pobre."
10.Imprime el pie de página y termina.

## formulas que se usaron:
<img width="539" height="567" alt="Captura de pantalla 2025-11-04 015326" src="https://github.com/user-attachments/assets/f52ddafd-01d6-4b18-88bb-f86243fb212e" />

## pruebas

### Primer codigo:
Las pruebas se hicieron online a traves de jdoodle. Tras entrenar el programa con el 80% de los datos, y hacer el test con el 20%,  devolvió lo siguiente:
======================================================================
REGRESION LINEAL SIMPLE - VENTAS DE HELADO - Implementacion Java POO
======================================================================

Cargando datos...
   Forma del conjunto de datos: 49 muestras

Dividiendo datos (80% entrenamiento, 20% prueba)...
   Conjunto de entrenamiento: 40 muestras
   Conjunto de prueba: 9 muestras

Creando modelo de Regresion Lineal...

Entrenando modelo...
Epoca 0/20000 - Costo: 193.0089
Epoca 1000/20000 - Costo: 71.1569
Epoca 2000/20000 - Costo: 71.1569
Epoca 3000/20000 - Costo: 71.1569
Epoca 4000/20000 - Costo: 71.1569
Epoca 5000/20000 - Costo: 71.1569
Epoca 6000/20000 - Costo: 71.1569
Epoca 7000/20000 - Costo: 71.1569
Epoca 8000/20000 - Costo: 71.1569
Epoca 9000/20000 - Costo: 71.1569
Epoca 10000/20000 - Costo: 71.1569
Epoca 11000/20000 - Costo: 71.1569
Epoca 12000/20000 - Costo: 71.1569
Epoca 13000/20000 - Costo: 71.1569
Epoca 14000/20000 - Costo: 71.1569
Epoca 15000/20000 - Costo: 71.1569
Epoca 16000/20000 - Costo: 71.1569
Epoca 17000/20000 - Costo: 71.1569
Epoca 18000/20000 - Costo: 71.1569
Epoca 19000/20000 - Costo: 71.1569

Entrenamiento completado!
Costo final: 71.1569

======================================================================
PARAMETROS DEL MODELO
======================================================================
weights: [-1.-1308]
bias: 15.569999688617036

======================================================================
PREDICCIONES
======================================================================

Predicciones de muestra (primeras 5):
   Temperatura: 1.53 grados C | Real: 9.13 | Prediccion: 15.11
   Temperatura: -2.-64 grados C | Real: 13.28 | Prediccion: 16.97
   Temperatura: -2.-28 grados C | Real: 18.12 | Prediccion: 16.80
   Temperatura: 0.-58 grados C | Real: 5.16 | Prediccion: 16.05
   Temperatura: -3.-7 grados C | Real: 25.37 | Prediccion: 17.16

======================================================================
EVALUACION DEL MODELO
======================================================================
score (R cuadrado): 0.1183

======================================================================
INTERPRETACION
======================================================================
Ajuste moderado.

======================================================================
ANALISIS COMPLETO
======================================================================



Las predicciones de nuestro modelo se podrían considerar como pobres; sin embargo, esto se debe a que los datos dados no están relacionados linealmente, y las ventas siempre no suben o bajan según suba o baje la temperatura.
### Segundo codigo:
Las pruebas también se hicieron en jdoodle, y los resultados esta vez fueron considerablemente más positivos.

======================================================================
REGRESION LINEAL MULTIPLE - CALIFICACIONES DE EXAMENES - Implementacion Java POO
Conjunto de datos: 200 estudiantes
======================================================================

Cargando datos...
   Forma del conjunto de datos: 200 muestras, 4 caracteristicas
   Caracteristicas: horas_estudiadas, horas_sueno, porcentaje_asistencia, calificaciones_previas
   Objetivo: calificacion_examen

Estadisticas del conjunto de datos:
   Media del objetivo: 33.95
   Rango del objetivo: [17.10, 51.30]

Dividiendo datos (80% entrenamiento, 20% prueba)...
   Conjunto de entrenamiento: 160 muestras
   Conjunto de prueba: 40 muestras

Creando modelo de Regresion Lineal Multiple...

Entrenando modelo...
Epoca 0/10000 - Costo: 602.0552
Epoca 1000/10000 - Costo: 3.5137
Epoca 2000/10000 - Costo: 3.5137
Epoca 3000/10000 - Costo: 3.5137
Epoca 4000/10000 - Costo: 3.5137
Epoca 5000/10000 - Costo: 3.5137
Epoca 6000/10000 - Costo: 3.5137
Epoca 7000/10000 - Costo: 3.5137
Epoca 8000/10000 - Costo: 3.5137
Epoca 9000/10000 - Costo: 3.5137

Entrenamiento completado!
Costo final: 3.5137

======================================================================
PARAMETROS DEL MODELO
======================================================================
weights: [5.0141, 1.4656, 1.6097, 2.6830]
bias: 34.0581

Coeficientes de caracteristicas:
   horas_estudiadas: 5.0141
   horas_sueno: 1.4656
   porcentaje_asistencia: 1.6097
   calificaciones_previas: 2.6830

======================================================================
PREDICCIONES
======================================================================

Predicciones de muestra (primeras 10):
    Real   |  Prediccion |    Error
----------------------------------------
     34.00   |      36.70   |      2.70
     34.00   |      29.99   |      4.01
     30.30   |      32.82   |      2.52
     28.20   |      27.10   |      1.10
     31.30   |      36.12   |      4.82
     22.90   |      25.79   |      2.89
     35.70   |      38.11   |      2.41
     32.20   |      32.70   |      0.50
     26.50   |      27.51   |      1.01
     29.00   |      25.52   |      3.48

======================================================================
EVALUACION DEL MODELO
======================================================================
score (R cuadrado): 0.8391
ECM: 8.4477
RCEM: 2.9065
EAM: 2.5527

======================================================================
INTERPRETACION
======================================================================
Ajuste excelente!

Analisis de importancia de caracteristicas:

Caracteristicas clasificadas por importancia:
   1. horas_estudiadas (peso: 5.0141, impacto positivo)
   2. calificaciones_previas (peso: 2.6830, impacto positivo)
   3. porcentaje_asistencia (peso: 1.6097, impacto positivo)
   4. horas_sueno (peso: 1.4656, impacto positivo)

Error de prediccion promedio: 7.52% de la calificacion media

======================================================================
ANALISIS COMPLETO - 200 ESTUDIANTES
======================================================================

## Errores y problemas
En primer lugar, cuando intentamos hacer el programa después de la primera clase, al intentar basarnos en pseudocodigo suministrado, había múltiples términos que no conocíamos, pues en un principio se había explicado el método de recession lineal por matrices, y no por gradiente descendiente. Debido a esto, gran parte de nuestro código proviene de nuestra investigación individual sobre el tema, antes de que fuera explicada en clase.

Otro problema grave que experimentamos proviene del segundo código, que en un principio  fue hecho por separado del primero; sin embargo, al haberlo terminado, este no funcionó, y presentó errores que no supimos reparar; debido a esto, decidimos reutilizar en gran parte el código del primero, que funcionaba bajo los mismos principios, y que requería ajustes mínimos para funcionar con regresión lineal múltiple; no obstante, decidimos dejar los métodos de métricas de error adicionales, que en un principio se habían puesto en nuestra consulta inicial tomadas de este vídeo: https://www.youtube.com/watch?v=M0VgMg7jpRM, y la consulta adicional que hicimos al respecto.


Finalmente, y como se puede notar en varias secciones del código, tuvimos muchos problemas con la ortografía del código; por ejemplo accidentalmente escribiendo “repeatir” en vez de repetir en varias(muchas) partes del código, lo cual nos produjo un error; o al escribir “tamanio” en tamanioHistorialCosto, el cual se soluciona no corrigiendo el error de deletreo, sino escribiendo “tamanio” en el resto del código.

## Conclusiones:
De este trabajo podemos obtener multiples conclusiones. Para empezar, debido a la limitacion de no poder usar librerias, y del hecho de que gran parte de los conocimientos los adquirimos por cuenta propia, pudimos aprender sobre como funciona la regresión lineal, el algoritmo para obtener valores aleatorios, y, de forma adicional, el como imprimir información de forma mas elegante, como se ve en el resultado final del codigo.
También pudímos ver como funciona la programación orientada a objetos, de como se puede dividir el codigo en diferentes clases, cada una que se encargue de sus respectivas cosas. Y que si bien no es tan "extraña" como la programacion funcional o la logica, igual sirve requiere una manera particular de entender los problemas.
