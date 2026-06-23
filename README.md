# Taller Práctico No. 4 — Librerías NumPy, Matplotlib y Seaborn

**Universidad del Pacífico — Programa de Ingeniería de Sistemas**
**Asignatura: Inteligencia Artificial — Semestre 8, corte II**
**Caso de estudio seleccionado: CASO 2 — Control de Calidad en una Planta de Producción**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jeffer301/INTELIGENCIA-ARTIFICIAL--JEFFERSON-VALENCIA/blob/main/taller_practico_librerias_numpy_matplotlib_seaborn/Taller_NumPy_Matplotlib_Seaborn.ipynb)
[![Ver Notebook en GitHub](https://img.shields.io/badge/GitHub-Ver%20Notebook-181717?style=flat&logo=github&logoColor=white)](https://github.com/jeffer301/INTELIGENCIA-ARTIFICIAL--JEFFERSON-VALENCIA/blob/main/taller_practico_librerias_numpy_matplotlib_seaborn/Taller_NumPy_Matplotlib_Seaborn.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat)
![Seaborn](https://img.shields.io/badge/Seaborn-65A6CE?style=flat)

> 🔗 **Abrir y ejecutar el taller directamente:** haz clic en el botón **"Open In Colab"** de arriba
> para correr el notebook en la nube, sin instalar nada en tu computador.

## 👥 Integrantes

| Nombre |
|--------|
| Jefferson Manuel Valencia Riascos |
| Isnildo Equia Perteaga |
| Sebastian Rojas Cabrera |
| Yeison Stiven Lozano Angulo |

## 1. Contexto

Una empresa manufacturera produce piezas metálicas y desea analizar los factores que influyen en
los defectos de fabricación, con el fin de ajustar sus parámetros de producción y reducir el
porcentaje de piezas defectuosas.

## 2. Generación de Datos Sintéticos

Se generó un dataset sintético de **500 registros** utilizando `numpy.random` (semilla fija
`np.random.seed(42)` para reproducibilidad), con las siguientes variables:

| Variable | Tipo | Generación |
|---|---|---|
| Temperatura de Producción | Numérica | `np.random.normal(180, 15, n)` — valor óptimo ≈180°C |
| Presión de Máquina | Numérica | `np.random.normal(50, 8, n)` — valor óptimo ≈50 psi |
| Tiempo de Operación | Numérica | `np.random.uniform(1, 12, n)` horas |
| Velocidad de Producción | Numérica | `np.random.normal(100, 20, n)` — valor óptimo ≈100 u/h |
| Defectuosa | Categórica (Sí/No) | Probabilidad condicionada a la desviación de temperatura y velocidad respecto a su valor óptimo |

El código completo de generación está en la sección 3 del notebook (`Taller_NumPy_Matplotlib_Seaborn.ipynb`).

## 3. Análisis Estadístico

Se calcularon, para cada variable numérica: **media, mediana, moda, desviación estándar, varianza,
mínimo y máximo**, usando NumPy/SciPy. La temperatura promedio resulta cercana a 180°C, confirmando
que el proceso opera en torno al punto óptimo, y su dispersión (desviación estándar).

## 4. Visualización de Datos 

El notebook incluye **7 visualizaciones**, cada una con su interpretación:

1. Histograma de temperatura de producción <br>

<img width="689" height="360" alt="image" src="https://github.com/user-attachments/assets/d250fef4-e6f6-4556-b198-042c7514e6eb" />

2. Histograma de presión de máquina <br>

<img width="563" height="358" alt="image" src="https://github.com/user-attachments/assets/2fc5a3d0-e442-4012-a184-0c4695f53591" />

3. Gráfico de barras de piezas defectuosas vs sanas <br> <img width="553" height="353" alt="image" src="https://github.com/user-attachments/assets/7a4ae129-f432-4792-865c-5093e52ebbb0" />

4. Heatmap de correlación (Seaborn) <br>
<img width="663" height="342" alt="image" src="https://github.com/user-attachments/assets/20f7c6ae-a11d-41eb-a11b-12430c5234ff" />

5. Boxplot de temperatura <br>
<img width="502" height="358" alt="image" src="https://github.com/user-attachments/assets/771c12d2-f59f-48e6-bc99-faa22a7ffc02" />

6. Pairplot de variables coloreado por condición de la pieza (Seaborn) <br>
<img width="830" height="742" alt="image" src="https://github.com/user-attachments/assets/8d025c77-aa8f-4a72-a684-8e2731dde0b3" />

7. Boxplot comparativo de temperatura según defecto <br>

 <img width="608" height="360" alt="image" src="https://github.com/user-attachments/assets/b26fa42c-07c4-4988-8867-4a0b1c969187" />



## 5. Análisis Exploratorio

**Hallazgos:**
- Las piezas defectuosas muestran, en promedio, una mayor desviación respecto al valor óptimo de
  temperatura y de velocidad que las piezas sanas, aunque ambas relaciones son débiles
  (correlación ≈ 0.06 para temperatura y ≈ 0.13 para velocidad).
- La presión de máquina y el tiempo de operación no muestran una asociación relevante con los
  defectos (correlación ≈ 0.04 y cercana a 0 respectivamente).
- Visualmente, el pairplot y los boxplots comparativos no permiten distinguir con claridad a las
  piezas defectuosas de las sanas, principalmente debido al desbalance entre clases del dataset
  (69 piezas defectuosas frente a 431 sanas).

**Relaciones entre variables:** no se encontraron relaciones lineales fuertes entre las variables
del proceso entre sí (todas las correlaciones cruzadas están entre -0.08 y 0.05), lo cual es
coherente con el hecho de que fueron generadas de forma independiente. La relación más relevante
del análisis es la que existe entre la desviación de temperatura/velocidad respecto a sus valores
óptimos y la probabilidad de defecto, aunque esta relación es moderada y no determinante por sí sola.

**Variable más relevante:** la Velocidad de Producción (correlación ≈ 0.13), seguida de la
Temperatura de Producción (correlación ≈ 0.06).

## 6. Conclusiones

1. Las piezas defectuosas presentan, en promedio, una mayor desviación respecto al valor óptimo
   de temperatura (180°C) que las piezas sanas, aunque esta relación es débil (correlación ≈ 0.06),
   por lo que la temperatura por sí sola no explica completamente la aparición de defectos.
2. La velocidad de producción extrema muestra la asociación más clara con los defectos entre las
   variables analizadas (correlación ≈ 0.13), siendo el factor individual más relevante del proceso.
3. La presión de máquina, dentro del rango analizado, prácticamente no muestra relación con la
   aparición de defectos (correlación ≈ 0.04).
4. El pairplot y el boxplot comparativo no permiten distinguir visualmente, de forma clara, a las
   piezas defectuosas de las sanas, debido al desbalance entre clases (69 piezas defectuosas frente
   a 431 sanas); esto confirma que ninguna variable por sí sola separa completamente ambos grupos.
5. El control simultáneo de temperatura y velocidad parece ser más efectivo para reducir defectos
   que el control aislado de una sola variable, ya que ambas aportan información relevante, aunque
   de forma moderada y no determinante.

## 7. Recomendaciones Empresariales

1. Implementar un sistema de monitoreo en tiempo real de temperatura y velocidad, con alertas
   cuando se alejen del rango óptimo.
2. Revisar y calibrar periódicamente las máquinas asociadas a los lotes con temperaturas atípicas.
3. Establecer rangos de control estadístico de proceso (SPC) para temperatura y velocidad,
   deteniendo la producción cuando se excedan los límites definidos.

## 8. Reflexión de IA

¿Cómo podrían utilizarse técnicas de Machine Learning o Inteligencia Artificial para automatizar
la toma de decisiones en este caso?

Podríamos entrenar modelos de Inteligencia Artificial dependiendo del método de clasificación
(árboles de decisión, random forest o redes neuronales) que nos interese elegir, para que estos
predigan la probabilidad de que una pieza resulte defectuosa usando los datos de temperatura,
presión, tiempo y velocidad registrados durante su fabricación. Estos modelos podrían activar
alertas automáticas o incluso detener la línea de producción casi en tiempo real cuando se detecte
que se cumplen los parámetros asociados a un alto riesgo de defecto, lo cual reduciría el
desperdicio de materiales y mejoraría la eficiencia del control de calidad.

## 9. Librerías utilizadas

- `numpy` — generación de datos y cálculos estadísticos.
- `pandas` — estructuración de datos en DataFrame.
- `matplotlib` — histogramas, barras, boxplots.
- `seaborn` — heatmap, boxplot, pairplot.
- `scipy.stats` — cálculo de la moda.

## 10. Cómo ejecutar

**Opción 1 — En la nube (recomendado):** haz clic en el badge **Open In Colab** al inicio de este README.

**Opción 2 — Localmente:**
```bash
pip install numpy pandas matplotlib seaborn scipy jupyter
jupyter notebook Taller_NumPy_Matplotlib_Seaborn.ipynb
```
Ejecutar todas las celdas en orden (`Kernel > Restart & Run All`).
