# TFM Máster Universitario en Ciencia de Datos (UOC)

### Predicción de Edad y Género a partir de la imagen de una persona

Este trabajo consta de 4 notebooks:

* **data.ipynb:** En este notebook se realizan todas las tareas relacionadas con el conjunto de datos: se descomprimen los datos en la VM (Virtual Machine) local de *Colab*; se efectúa la carga de los datos en un `pd.DataFrame`, tomando las etiquetas de cada muestra a partir del nombre del archivo; el hace un análisis numérico y gráfico de datos de entrada y etiquetas; se adaptan al formato TFRecord y se distribuyen en 11 ficheros, para posteriormente  subirlos a un bucket de GCS repartidos en 11 carpetas distintas, de forma que estén disponibles para el proceso de entrenamiento y testeo según la estrategia de validación cruzada. Este notebook toma datos de entrada de *Google Drive* y su salida se almacena en un bucket de GCS.

* **TPU.ipynb & GPU.ipynb:** Aunque realmente existen 2 notebooks distintos, conceptualmente ambos realizan la misma función. En estos notebooks se realizan las siguientes tareas: lectura de los ficheros TFRecord de GCS y su carga en una estructura `tf.data.Dataset`, preparando cada subconjunto de datos mediante tareas como aumento de datos, agrupado de los datos en lotes o batch y prefetching; creación y compilación de los modelos unitask y multitask, permitiendo emplear distintas funciones de pérdidas, normalizaciones, etc. para buscar el mejor rendimiento en los modelos; el entrenamiento de dichos modelos y predicciones sobre el subconjunto de datos, para posteriormente volcar los resultados obtenidos en *Google Drive*. Por tanto, este notebook toma datos de GCS y vuelca sus salidas en *Google Drive*. Como se puede intuir por el nombre de los archivos, la única diferencia entre ambos es que **TPU.ipynb** está preparado para trabajar con TPU, mientras que **GPU.ipynb** está preparado para trabajar con GPU.

* **results.ipynb:** Este notebook únicamente consume datos de *Google Drive*. Su función es la de cargar los resultados del entrenamiento y las predicciones de los distintos modelos, incluso los propios modelos por si fuera necesario utilizarlos, y exponer en forma de tabla y gráficas los rendimientos de cada uno de los modelos para su análisis.

En el siguiente esquema se resume el flujo de trabajo realizado:

![Arquitectura utilizada](https://github.com/alegalalb1/TFM/blob/main/esquema.png?raw=true)
