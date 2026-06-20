# taller_numpy_matplotlib_seaborn.ipynb
# Taller de IA – NumPy, Matplotlib y Seaborn

---

## PARTE I – Investigación y Análisis

### Actividad 1. Investigación conceptual

#### NumPy

**1. ¿Qué es NumPy?**
Es la librería fundamental de Python para computación numérica. Provee el objeto `ndarray` (arreglo n‑dimensional) y un conjunto extenso de funciones matemáticas para operar de forma rápida sobre grandes volúmenes de datos numéricos.

**2. ¿Por qué NumPy es más eficiente que las listas tradicionales de Python?**
Porque almacena los datos en bloques contiguos de memoria, todos del mismo tipo, en lugar de objetos Python independientes y dispersos como hacen las listas. Además, sus operaciones están implementadas en C y se ejecutan de forma **vectorizada** (aplicadas a todo el arreglo de una sola vez), evitando los bucles `for` explícitos de Python, que son mucho más lentos.

**3. ¿Qué es un ndarray?**
Es la estructura de datos central de NumPy: un arreglo homogéneo (todos sus elementos del mismo tipo) de N dimensiones, con una forma (`shape`) y un tipo de dato (`dtype`) definidos, sobre el cual se pueden aplicar operaciones matemáticas de manera eficiente.

**4. ¿Qué relación existe entre NumPy y el álgebra lineal?**
NumPy es, en la práctica, el motor de álgebra lineal de Python: representa vectores y matrices como `ndarray` y, a través del submódulo `numpy.linalg`, ofrece operaciones como multiplicación de matrices, transposición, determinante, inversa y cálculo de autovalores/autovectores, que son la base matemática de la mayoría de los algoritmos de Machine Learning y Deep Learning.

**5. ¿Cómo utilizan los modelos de Deep Learning las matrices de NumPy?**
Los datos de entrada, los pesos, los sesgos (bias) y las salidas de una red neuronal se representan como matrices o tensores. El paso hacia adelante (forward propagation) y el ajuste de pesos (backpropagation) se calculan mediante multiplicaciones de matrices y operaciones vectorizadas, exactamente el tipo de cálculo que NumPy resuelve de forma eficiente (los frameworks como TensorFlow o PyTorch extienden esta misma idea, pero ejecutándola en GPU).

#### Matplotlib

**6. ¿Qué es Matplotlib?**
Es la librería de visualización de datos más usada en Python; permite crear gráficos estáticos, animados e interactivos a partir de datos numéricos.

**7. ¿Qué tipos de gráficos permite construir?**
Gráficos de líneas, de barras, de dispersión (scatter), histogramas, diagramas de caja (boxplots), gráficos circulares (pie charts), gráficos de superficie/3D, mapas de contorno, entre otros.

**8. ¿Por qué la visualización de datos es importante en IA?**
Porque permite comprender visualmente patrones, tendencias, distribuciones y relaciones entre variables que serían muy difíciles de detectar solo mirando números en una tabla. También ayuda a comunicar resultados, detectar errores o anomalías en los datos y respaldar decisiones sobre qué técnica de modelado usar.

**9. ¿Cómo ayuda Matplotlib en el análisis exploratorio de datos (EDA)?**
Permite graficar rápidamente la distribución de cada variable, la relación entre variables, posibles valores atípicos y tendencias, lo cual orienta el preprocesamiento (limpieza, normalización, selección de variables) antes de entrenar cualquier modelo.

#### Seaborn

**10. ¿Qué es Seaborn?**
Es una librería de visualización estadística construida sobre Matplotlib. Ofrece una interfaz de alto nivel para crear gráficos atractivos e informativos con menos líneas de código, integrándose de forma nativa con `pandas`.

**11. ¿Qué ventajas ofrece frente a Matplotlib?**
Sintaxis más simple para gráficos estadísticos complejos, estilos visuales más cuidados por defecto, integración directa con `DataFrames` de pandas, y funciones especializadas listas para usar (como `heatmap`, `boxplot`, `pairplot`, `violinplot`) que en Matplotlib puro requerirían mucho más código.

**12. ¿Qué son los mapas de calor (Heatmaps)?**
Son representaciones gráficas de una matriz de valores en las que cada celda se colorea según su magnitud. Permiten identificar de un vistazo qué valores son altos, bajos o intermedios, siendo muy útiles para visualizar matrices de correlación.

**13. ¿Por qué las matrices de correlación son importantes en Machine Learning?**
Porque permiten detectar qué variables están relacionadas linealmente entre sí, identificar **multicolinealidad** (variables redundantes que aportan la misma información), y apoyar la selección de las características (features) más relevantes para el modelo, evitando inestabilidad o sobreajuste (overfitting).

---

## Ejercicios guía – Preguntas de análisis

### 2. Operaciones matemáticas

**¿Qué representa la desviación estándar?**
Es una medida de dispersión que indica, en promedio, cuánto se alejan los valores individuales de un conjunto de datos respecto a su media. Una desviación pequeña indica datos muy agrupados alrededor del promedio; una desviación grande indica datos muy dispersos.

**¿Por qué es importante conocer la dispersión de los datos?**
Porque dos conjuntos de datos pueden tener el mismo promedio y comportarse de forma muy distinta. Conocer la dispersión permite entender qué tan confiable o representativo es ese promedio, detectar variabilidad excesiva o valores atípicos, y es clave para decisiones como la normalización/escalado de variables antes de entrenar un modelo.

### 3. Generación de datos aleatorios (distribución normal)

**¿Qué significa distribución normal?**
Es una distribución de probabilidad simétrica con forma de campana (campana de Gauss), en la que la mayoría de los valores se concentran cerca de la media y la probabilidad de observar un valor disminuye simétricamente a medida que se aleja de ella. Queda completamente descrita por dos parámetros: la media (`loc`) y la desviación estándar (`scale`).

**¿Por qué muchos algoritmos asumen distribuciones aproximadamente normales?**
Porque, según el **teorema del límite central**, muchos fenómenos naturales y errores de medición tienden a aproximarse a una distribución normal cuando se combinan muchas variables independientes. Asumir normalidad simplifica los supuestos matemáticos de varios algoritmos (por ejemplo, regresión lineal, que asume residuos normalmente distribuidos) y permite usar propiedades estadísticas bien conocidas para hacer inferencias, calcular intervalos de confianza o detectar valores atípicos.

### 4. Matplotlib – Gráfico de líneas (concepto a investigar)

**¿Qué es el "accuracy" y qué es una "época" en el entrenamiento de un modelo?**
- **Época (epoch):** una pasada completa del algoritmo de entrenamiento por todo el conjunto de datos de entrenamiento. Entrenar "8 épocas" significa que el modelo vio el dataset completo 8 veces, ajustando sus parámetros en cada pasada.
- **Accuracy (precisión/exactitud):** es una métrica que mide el porcentaje de predicciones correctas que hace el modelo sobre el total de predicciones realizadas. En el gráfico del ejercicio, se observa cómo el accuracy va aumentando a medida que avanzan las épocas, lo cual indica que el modelo está aprendiendo (mejorando su desempeño) con el entrenamiento.

### 5. Histograma

**¿Qué representa un histograma?**
Es una representación gráfica de la distribución de frecuencias de una variable numérica: el rango de valores se divide en intervalos (bins) y se muestra, mediante barras, cuántos datos caen dentro de cada intervalo.

**¿Qué utilidad tiene para comprender un dataset?**
Permite ver de forma inmediata la forma de la distribución de una variable (simétrica, sesgada hacia un lado, con uno o varios picos), identificar dónde se concentran los datos, detectar posibles valores atípicos y evaluar si una variable se aproxima o no a una distribución conocida (como la normal), lo cual influye en qué técnicas de preprocesamiento o modelado conviene usar.

### 8. Boxplot

**¿Qué son los valores atípicos (Outliers)?**
Son observaciones que se alejan de forma notable del resto de los datos. En un boxplot suelen definirse como los valores que caen fuera del rango formado por 1.5 veces el rango intercuartílico (IQR) por encima del tercer cuartil o por debajo del primer cuartil.

**¿Por qué pueden afectar el entrenamiento de un modelo?**
Porque pueden distorsionar medidas estadísticas como la media y la desviación estándar, sesgar los parámetros que aprende el modelo (especialmente en algoritmos sensibles a la escala de los datos, como la regresión lineal o KNN), provocar que el modelo se ajuste a casos extremos poco representativos (un tipo de sobreajuste) y, en consecuencia, reducir su capacidad de generalizar correctamente sobre datos nuevos.

---
