# Métodos de *Clustering* basados en *Deep Learning* aplicados en el Análisis Biológico de la Microbiota Intestinal 

* Autor: Juan Felipe Lancheros Carrillo.
* Asesora: María del Pilar Villamil Giraldo.
* Institución: Universidad de los Andes > Facultad de Ingeniería > Departamento de Ingeniería de Sistemas y Computación.

Este repositorio contiene los cuadernos de Jupyter y los archivos que registran las pruebas de optimización de los dos modelos de *deep clustering* implementados (Mapas Autoorganizados y *Sparse Autoencoder*), utilizados  en el marco de la investigación realizada como proyecto de grado de la carrera de Ingeniería de Sistemas y Computación de la Universidad de los Andes. El documento con el desarrollo completo de la investigación se encuentra publicado en el repositorio institucional oficial: https://hdl.handle.net/1992/77648.

El objetivo principal de esta investigación fue, mediante el uso de técnicas de *deep clustering*, identificar factores influyentes sobre la diversidad de la microbiota intestinal según las relaciones entre el sexo, la edad y las unidades taxonómicas operativas (*OTU*) correspondientes a muestras biológicas de individuos originarios de diferentes ciudades de Colombia.

## 📊 Datos utilizados
El estudio se basó en datos de 441 individuos, obtenidos del artículo "Gut microbiota is associated with obesity and cardiometabolic disease in a population in the midst of Westernization" (https://doi.org/10.1038/s41598-018-29687-x). Específicamente, se recolectaron, de la carpeta *files* del repositorio de GitHub (https://github.com/jsescobar/westernization) que referencia el artículo en la subsección *Data Availability* de la sección *Methods*, los siguientes archivos:  
* microbio_selected.meta.  
* microbio_selected.otus.  
* microbio_selected.taxonomy.   

## 🛠️ Metodología
El proyecto fue abordado por ASUM-DM. Las aproximaciones implementadas fueron las siguientes:

### 1. Mapas Autoorganizados (*SOM*)
Proyecta datos de alta dimensionalidad en una matriz 2D preservando la estructura topológica y es capaz de visualizar macrotendencias globales y gradientes de transición entre grupos.

### 2. *Sparse Autoencoder* (*SAE*) + *OPTICS*
* *SAE*: Actúa como un preprocesador avanzado para reducir la dimensionalidad, filtrar el ruido biológico y tratar efectivamente la dispersión de los datos.
* *OPTICS*: Algoritmo de agrupación basado en densidad encargado de identificar estructuras locales discretas en el espacio latente generado por *SAE*.

## 📈 Resultados principales
* Se confirmó que la procedencia geográfica es el factor dominante de la diversidad. 
* Se identificaron biomarcadores "ocultos" como *Bilophila* y *Desulfovibrio*, que tienen alta relevancia estructural a pesar de su baja abundancia global.
* *SOM* logró preservar la estructura de los datos con errores topológicos cercanos a cero (0,0 y 0,06).
* El modelo *SAE* logró reducir las dimensiones en un 81% con una pérdida mínima de información (MSE de 0,0198).
* *OPTICS* identificó siete *clusters* distintos con un coeficiente de *Silhouette* de 0,756, indicando que la separación fue de alta calidad. 

## ✍ Conclusión
Al demostrar que es posible descifrar la complejidad de la microbiota intestinal mediante el *deep learning*, se sientan las bases para un futuro donde las intervenciones nutricionales dejen de ser genéricas, se conviertan en terapias personalizadas, optimizables y basadas en evidencia, y tengan el potencial real de transformar la salud de la población.

## 📂 Estructura del repositorio y requerimientos de datos para la ejecución
* `/notebooks`
  * `official_article_data_manipulation.ipynb`: Paso a paso del procesamiento de datos original del artículo fuente.  
    * Utiliza los archivos "microbio_selected.meta", "microbio_selected.otus", "microbio_selected.tre", "microbio_selected.taxonomy", "tax4fun.Rdata" y "microbio_poles.biom", todos recolectados del repositorio de GitHub mencionado anteriormente.
  * `data_comprehension.ipynb`: Ejecución de la etapa de "4.4. Entendimiento de los datos" descrita en el documento del proyecto.
    * Utiliza los archivos "microbio_selected.meta", "microbio_selected.otus" y "microbio_selected.taxonomy".
  * `data_preparation.ipynb`: Ejecución de la etapa de "4.6. Preparación de los datos" descrita en el documento del proyecto.
    * Utiliza los archivos "microbio_selected.meta", "microbio_selected.otus" y "microbio_selected.taxonomy".
  * `DL_implementation.ipynb`: Ejecución de la etapa de "4.7. Construcción de los modelos" descrita en el documento del proyecto.
    * Utiliza los archivos "microbio_obj_csv", obtenido del *encoding* realizado en `data_preparation.ipynb`, "otus_tax_filtered.csv", obtenido después de haber aplicado el filtro de mediana en `data_preparation.ipynb` y (si se desea ejecutar *SOM*) "microbio_inicial.csv", obtenido de la unión de los metadatos con las *OTU* filtradas, llevada a cabo en `data_preparation.ipynb`.
  * `SOM_optimization.ipynb`: Proceso de la búsqueda de la mejor configuración de hiperpárametros de *SOM*.
    * Utiliza el archivo "scaled_data_robust.csv" generado en el *scaling* descrito en `DL_implementation.ipynb`.
* `/optimization record`: Registros detallados de las pruebas de hiperparámetros y métricas obtenidas.

## 💻 Tecnologías
* Lenguaje: Python.
* Librerías principales: Pandas, NumPy, MiniSom, TensorFlow Keras, Scikit-learn y SciPy.
* Apoyo de IA generativa: Para la investigación, se utilizó Logically AI, Google NotebookLM y Google Gemini; para la implementación y redacción, se utilizó Claude, Google Gemini y ChatGPT. 
