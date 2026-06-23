# Predicción de Hábito de Fumar mediante Machine Learning

## Descripción del Proyecto

Este trabajo práctico fue desarrollado en el marco de la Diplomatura en Inteligencia Artificial de la Universidad de Palermo y tiene como objetivo construir un modelo de Machine Learning capaz de predecir si una persona es fumadora o no a partir de información clínica, biométrica y de hábitos de salud.

Se utilizó un conjunto de datos compuesto por 50.000 registros de individuos, incluyendo variables demográficas, antropométricas y resultados de estudios médicos. El objetivo fue entrenar y evaluar distintos modelos de clasificación supervisada para determinar cuál ofrecía el mejor desempeño en la identificación de fumadores.

---

## Objetivos

* Analizar y comprender la estructura del dataset.
* Realizar un análisis exploratorio de datos (EDA).
* Aplicar técnicas de preprocesamiento.
* Entrenar y comparar distintos algoritmos de clasificación.
* Optimizar hiperparámetros del modelo seleccionado.
* Evaluar el desempeño utilizando métricas apropiadas.
* Generar predicciones sobre un conjunto de datos sin etiquetar.

---

## Estructura del Proyecto

```text
├── data
│   ├── raw
│   │   ├── smoking.csv
│   │   └── smoking_prediction_entrega.csv
│   │
│   └── processed
│       ├── dataset_preprocesado.csv
│       └── predicciones_finales.csv
│
├── models
│
├── notebooks
│   ├── 01_lectura_y_discovery.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_preprocesamiento.ipynb
│   ├── 04_entrenamiento_y_optimizacion.ipynb
│   ├── 05_validacion.ipynb
│   └── 06_prediccion.ipynb
│
├── README.md
└── requirements.txt
```

---

## Descripción de las Notebooks

### Notebook 01 - Lectura y Discovery

Se realizó una exploración inicial del dataset:

* Carga de datos.
* Verificación de tipos de datos.
* Análisis de valores faltantes.
* Identificación de variables constantes.
* Análisis preliminar de la variable objetivo.

Principales hallazgos:

* No se encontraron valores nulos.
* No se detectaron registros duplicados.
* La variable `oral` resultó constante y fue descartada.
* La variable `ID` se identificó como un identificador sin valor predictivo.

---

### Notebook 02 - Análisis Exploratorio (EDA)

Se analizaron distribuciones, relaciones y posibles patrones entre las variables y la variable objetivo.

Actividades realizadas:

* Histogramas.
* Boxplots.
* Gráficos de barras.
* Matriz de correlación.
* Análisis de variables categóricas.

Principales observaciones:

* El género mostró una fuerte relación con la condición de fumador.
* Variables como hemoglobina, triglicéridos y Gtp mostraron diferencias relevantes entre fumadores y no fumadores.
* La variable objetivo presentó un desbalance moderado (63% no fumadores y 37% fumadores).

---

### Notebook 03 - Preprocesamiento

Transformaciones realizadas:

* Eliminación de la variable `ID`.
* Eliminación de la variable constante `oral`.
* Codificación binaria de:

  * `gender`
  * `tartar`
* División en conjuntos de entrenamiento y prueba utilizando estratificación.
* Generación del dataset preprocesado.

---

### Notebook 04 - Entrenamiento y Optimización

Se entrenaron y compararon distintos algoritmos de clasificación:

#### Logistic Regression

Se evaluó tanto la versión básica como una versión con escalado mediante StandardScaler.

#### Random Forest

Se entrenó un modelo base y posteriormente se optimizaron sus hiperparámetros utilizando GridSearchCV.

#### XGBoost

Se realizó una prueba adicional utilizando Gradient Boosting basado en árboles.

Modelos evaluados:

* Logistic Regression
* Logistic Regression + StandardScaler
* Random Forest
* Random Forest optimizado mediante GridSearchCV
* XGBoost

---

### Notebook 05 - Validación

Se evaluó el modelo seleccionado utilizando:

* Classification Report
* Matriz de Confusión
* Curva ROC
* Área bajo la curva (AUC)
* Importancia de variables

Además, se persistió el modelo entrenado para su reutilización.

---

### Notebook 06 - Predicción

Se cargó el dataset de entrega sin etiquetas y se aplicó exactamente el mismo flujo de preprocesamiento utilizado durante el entrenamiento.

Posteriormente:

* Se cargó el modelo entrenado.
* Se generaron las predicciones.
* Se exportó el archivo final con la columna `smoking_prediction`.

---

## Selección de la Métrica

Debido al desbalance moderado de clases observado en la variable objetivo, se utilizó como métrica principal el **F1-score de la clase positiva (fumadores)**.

Esta métrica combina precisión y recall, permitiendo evaluar adecuadamente la capacidad del modelo para identificar fumadores sin verse excesivamente influenciada por la clase mayoritaria.

---

## Modelo Seleccionado

El modelo con mejor desempeño fue un Random Forest optimizado mediante GridSearchCV.

Hiperparámetros seleccionados:

```python
RandomForestClassifier(
    n_estimators=200,
    max_depth=None,
    min_samples_split=5,
    random_state=42
)
```

---

## Resultados

Métricas obtenidas sobre el conjunto de prueba:

| Métrica             | Valor |
| ------------------- | ----: |
| Accuracy            |  0.80 |
| Precision (Clase 1) |  0.71 |
| Recall (Clase 1)    |  0.76 |
| F1-Score (Clase 1)  | 0.736 |
| AUC ROC             | 0.887 |

---

## Variables Más Importantes

Las variables con mayor contribución al modelo fueron:

1. Gender
2. Gtp
3. Height
4. Triglyceride
5. Hemoglobin
6. LDL
7. Cholesterol
8. ALT
9. HDL
10. Fasting Blood Sugar

Estos resultados son consistentes con los hallazgos obtenidos durante el análisis exploratorio.

---

## Conclusiones

El proyecto permitió desarrollar un flujo completo de Machine Learning supervisado, desde la exploración inicial de los datos hasta la generación de predicciones sobre datos no etiquetados.

El modelo Random Forest optimizado obtuvo el mejor desempeño general, alcanzando un F1-score de 0.736 para la clase fumadora y un AUC de 0.887, demostrando una buena capacidad de discriminación entre fumadores y no fumadores.

Asimismo, se observó que variables relacionadas con características físicas y marcadores clínicos presentan una fuerte relación con el hábito de fumar, siendo especialmente relevante el género y diversos indicadores bioquímicos.
