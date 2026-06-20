# Informe Técnico de Mejora del Proceso
## Control de calidad en una planta de producción de piezas metálicas

---

## 1. Introducción

Este informe presenta el análisis estadístico de **500 registros simulados** del proceso de fabricación de piezas metálicas de la planta, con el objetivo de identificar qué factores de producción están más asociados con la aparición de defectos y proponer recomendaciones de mejora.

Las variables analizadas fueron:

| Variable | Tipo | Descripción |
|---|---|---|
| Temperatura de Producción | Numérica | Temperatura del proceso (°C) |
| Presión de Máquina | Numérica | Presión ejercida por la máquina (bar) |
| Tiempo de Operación | Numérica | Horas de funcionamiento desde el último mantenimiento |
| Velocidad de Producción | Numérica | Piezas fabricadas por hora |
| Defectuosa | Categórica (Sí/No) | Si la pieza presenta o no un defecto |

> El código completo de generación de datos y de todos los gráficos está en `caso2_control_calidad.ipynb`. El dataset generado se incluye en `piezas_metalicas_500.csv` y las figuras en la carpeta `figuras/`.

---

## 2. Metodología

1. Se generaron 500 registros sintéticos para las cuatro variables numéricas usando distribuciones normales con **NumPy** (`np.random.normal`), con parámetros típicos de un proceso industrial estable.
2. La variable `Defectuosa` se generó de forma probabilística: la probabilidad de defecto de cada pieza depende principalmente de la temperatura y del tiempo de operación (simulando desgaste de la máquina), más un componente de presión, velocidad y ruido aleatorio. Esto permite que el análisis de correlación posterior tenga una relación real que descubrir, tal como ocurriría con datos de planta.
3. Se calcularon estadísticas descriptivas con **NumPy** (media, mediana, varianza, desviación estándar).
4. Se generaron visualizaciones con **Matplotlib** (histogramas, gráfico de barras) y **Seaborn** (matriz de correlación, boxplot, pairplot).
5. Se aplicó el método del **rango intercuartílico (IQR)** para identificar valores atípicos.

---

## 3. Resultados – Estadísticas descriptivas (NumPy)

| Variable | Media | Mediana | Varianza | Desviación estándar |
|---|---|---|---|---|
| Temperatura (°C) | 180.10 | 180.19 | 216.21 | 14.70 |
| Presión (bar) | 50.25 | 50.23 | 61.09 | 7.82 |
| Tiempo de Operación (h) | 8.22 | 8.24 | 4.07 | 2.02 |
| Velocidad (piezas/h) | 120.66 | 119.82 | 386.58 | 19.66 |

**Distribución de la variable objetivo:** de las 500 piezas, **268 (53.6 %) resultaron defectuosas** y **232 (46.4 %) no defectuosas**. (Esta proporción es alta a propósito, para que el ejercicio académico muestre con claridad el efecto de las variables sobre el defecto; en una planta real se esperaría una tasa de defectos mucho menor).

En todas las variables, la media y la mediana son muy cercanas entre sí, lo que indica distribuciones aproximadamente simétricas (sin un sesgo fuerte hacia valores muy altos o muy bajos).

---

## 4. Resultados – Visualizaciones

### 4.1 Histograma de Temperatura de Producción
![Histograma de Temperatura](figuras/hist_temperatura.png)

La temperatura se distribuye de forma aproximadamente normal alrededor de 180 °C, con la mayoría de las piezas fabricadas entre 160 °C y 200 °C.

### 4.2 Histograma de Presión de Máquina
![Histograma de Presión](figuras/hist_presion.png)

La presión también sigue un comportamiento simétrico, concentrada entre 40 y 60 bar.

### 4.3 Piezas defectuosas vs. no defectuosas
![Barras de defectos](figuras/bar_defectos.png)

### 4.4 Matriz de correlación
![Matriz de correlación](figuras/heatmap_correlacion.png)

### 4.5 Boxplot de Temperatura
![Boxplot de Temperatura](figuras/boxplot_temperatura.png)

### 4.6 Pairplot de variables numéricas (coloreado por Defectuosa)
![Pairplot](figuras/pairplot.png)

En el pairplot se observa que los puntos rojos (piezas defectuosas) tienden a concentrarse en valores más altos de temperatura y, en menor medida, de tiempo de operación, mientras que en presión y velocidad ambos grupos se mezclan sin un patrón claro.

---

## 5. Respuestas a las preguntas de análisis (3.4)

### 5.1. ¿Qué variable parece estar asociada con los defectos?

Al calcular la correlación de cada variable numérica con `Defectuosa` (codificada como 1 = Sí, 0 = No), se obtuvo:

| Variable | Correlación con Defectuosa |
|---|---|
| **Temperatura** | **0.44** |
| **Tiempo de Operación** | **0.33** |
| Presión | 0.05 |
| Velocidad | 0.04 |

La **Temperatura de Producción** es la variable con mayor asociación con la aparición de defectos (correlación moderada-positiva de 0.44), seguida del **Tiempo de Operación** desde el último mantenimiento (0.33). Esto sugiere que **a mayor temperatura del proceso y mayor tiempo sin mantenimiento, aumenta la probabilidad de que la pieza salga defectuosa**. La Presión y la Velocidad de Producción, en cambio, muestran una correlación muy débil (cercana a 0) con los defectos, por lo que no parecen ser factores determinantes en este conjunto de datos.

### 5.2. ¿Existen valores atípicos?

Usando el criterio del rango intercuartílico (IQR), se detectaron los siguientes valores atípicos:

| Variable | N° de outliers | Rango considerado "normal" |
|---|---|---|
| Temperatura | 4 | 139.41 °C – 219.64 °C |
| Presión | 7 | 30.28 bar – 70.17 bar |
| Tiempo de Operación | 2 | 2.72 h – 13.58 h |
| Velocidad | 6 | 68.41 – 173.35 piezas/h |

Sí existen valores atípicos en todas las variables, siendo la **Presión de Máquina** la que presenta más casos (7), seguida de la **Velocidad de Producción** (6) y la **Temperatura** (4). El **boxplot de Temperatura** confirma visualmente la presencia de algunos puntos fuera de los "bigotes" de la caja, correspondientes a lecturas inusualmente altas o bajas.

### 5.3. ¿Qué recomendaciones realizaría a la planta?

1. **Controlar y estabilizar la temperatura de producción.** Es el factor más asociado a los defectos; se recomienda instalar o calibrar sensores de temperatura con alertas automáticas cuando el proceso se aleje del rango óptimo (idealmente cerca de 180 °C, evitando superar ~200–210 °C).
2. **Reforzar el plan de mantenimiento preventivo.** Como el tiempo de operación sin mantenimiento también se asocia con más defectos, se sugiere reducir el intervalo entre mantenimientos o establecer mantenimientos programados antes de que la máquina acumule muchas horas de uso continuo.
3. **Investigar los valores atípicos de presión y velocidad**, ya que aunque no muestran una correlación fuerte con los defectos en este análisis, los outliers detectados podrían señalar fallos puntuales de sensores, picos de operación o condiciones anómalas que conviene revisar antes de descartarlos como ruido.
4. **Implementar un panel de control estadístico de procesos (SPC)** que monitoree en tiempo real temperatura y tiempo de operación, con límites de control basados en los rangos "normales" calculados (evitar que la temperatura supere ~220 °C, por ejemplo).
5. **Recolectar más variables de proceso** (p. ej. lote de materia prima, turno de trabajo, operario) para enriquecer el análisis y descartar otras causas no incluidas en este estudio inicial.
6. **Repetir este análisis periódicamente con datos reales de planta** (no solo simulados), para validar si las relaciones encontradas se mantienen y ajustar el modelo de control de calidad en consecuencia.

---

## 6. Conclusión

El análisis exploratorio con NumPy, Matplotlib y Seaborn permitió identificar que la **temperatura de producción** y, en segundo lugar, el **tiempo de operación sin mantenimiento**, son los factores más relacionados con la aparición de defectos en las piezas metálicas, mientras que la presión y la velocidad de producción no mostraron una asociación relevante. Se recomienda priorizar el control de temperatura y la frecuencia de mantenimiento como las primeras acciones de mejora del proceso.

---

## Anexos

- `caso2_control_calidad.ipynb` — notebook ejecutable en Google Colab con todo el código (generación de datos, estadísticas, gráficos).
- `piezas_metalicas_500.csv` — dataset de 500 registros generado para este análisis.
- `figuras/` — imágenes de todos los gráficos generados.
