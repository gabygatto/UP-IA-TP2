\# Models



\## Modelo entrenado



El modelo final utilizado en este proyecto corresponde a un \*\*Random Forest Classifier\*\* optimizado mediante \*\*GridSearchCV\*\*.



Los hiperparámetros seleccionados fueron:



```python

RandomForestClassifier(

&#x20;   n\_estimators=200,

&#x20;   max\_depth=None,

&#x20;   min\_samples\_split=5,

&#x20;   random\_state=42

)

```



\## Nota sobre el archivo del modelo



El archivo generado (`random\_forest\_final.joblib`) no se incluye en este repositorio debido a las limitaciones de tamaño impuestas por GitHub para archivos individuales (100 MB).



Durante el entrenamiento, el modelo persistido alcanzó un tamaño aproximado de 140 MB, por lo que no pudo ser almacenado directamente en el repositorio.



\## Cómo regenerar el modelo



Para reconstruir el archivo del modelo:



1\. Ejecutar la Notebook 03 (`03\_preprocesamiento.ipynb`).

2\. Ejecutar la Notebook 04 (`04\_entrenamiento\_y\_optimizacion.ipynb`).

3\. Ejecutar la Notebook 05 (`05\_validacion.ipynb`).



Al finalizar la Notebook 05 se ejecuta la persistencia del modelo mediante:



```python

import joblib



joblib.dump(

&#x20;   rf\_final,

&#x20;   "../models/random\_forest\_final.joblib"

)

```



Esto generará nuevamente el archivo:



```text

models/

└── random\_forest\_final.joblib

```



\## Uso del modelo



Una vez generado, puede cargarse mediante:



```python

import joblib



modelo = joblib.load(

&#x20;   "../models/random\_forest\_final.joblib"

)

```



y utilizarse para realizar predicciones sobre nuevos datos siguiendo el flujo implementado en la Notebook 06 (`06\_prediccion.ipynb`).



