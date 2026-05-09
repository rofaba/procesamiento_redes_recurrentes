# Identificación de escenarios naturales con redes neuronales

Notebook desarrollado como parte del desafío **“Identificación de escenarios naturales del mundo”** del programa **Data Science G107**.

El objetivo del proyecto es clasificar imágenes de escenarios naturales utilizando distintos modelos de redes neuronales, comparando el rendimiento de una red Fully Connected con modelos convolucionales más adecuados para procesamiento de imágenes.

## Autor

**Rodrigo Faure**  
Data Science G107

## Descripción del proyecto

En este notebook se trabaja con conjuntos de imágenes ya preprocesados en formato `.npy`. Las imágenes pertenecen a seis categorías de escenarios naturales:

- `buildings`
- `forest`
- `glacier`
- `mountain`
- `sea`
- `street`

El flujo general incluye:

1. Carga de datos de entrenamiento, test y predicción.
2. Exploración inicial de los conjuntos.
3. Visualización de imágenes aleatorias.
4. Codificación de etiquetas con `OneHotEncoder`.
5. Entrenamiento de una red neuronal Fully Connected.
6. Entrenamiento de una red neuronal convolucional.
7. Entrenamiento de una red convolucional más profunda.
8. Evaluación de rendimiento mediante accuracy, loss, matriz de confusión y classification report.
9. Predicción sobre imágenes sin etiqueta.

## Archivos utilizados

El notebook espera encontrar los siguientes archivos:

```text
cnn_train_X.npy
cnn_train_y.npy
cnn_test_X.npy
cnn_test_y.npy
cnn_pred_X.npy

Estos archivos contienen:

Archivo	Descripción
cnn_train_X.npy	Imágenes del conjunto de entrenamiento
cnn_train_y.npy	Etiquetas del conjunto de entrenamiento
cnn_test_X.npy	Imágenes del conjunto de test
cnn_test_y.npy	Etiquetas del conjunto de test
cnn_pred_X.npy	Imágenes sin etiqueta para predicción
Tecnologías y librerías

El proyecto utiliza:

numpy
matplotlib
scikit-learn
tensorflow
keras

Librerías principales:

NumPy para carga y manipulación de datos.
Matplotlib para visualización de imágenes y curvas de entrenamiento.
Scikit-learn para codificación de etiquetas y métricas.
TensorFlow / Keras para construir y entrenar los modelos neuronales.
Modelos implementados
1. Red Fully Connected

Se implementa una red neuronal densa con al menos cinco capas ocultas.

Estructura general:

Flatten
Dense(512)
Dense(256)
Dense(128)
Dense(64)
Dense(32)
Dense(6, softmax)

Este modelo obtuvo una accuracy aproximada de 0.61 en el conjunto de test.

La conclusión principal es que, aunque logra aprender ciertos patrones, su rendimiento es limitado porque las redes densas no aprovechan bien la estructura espacial de las imágenes.

2. Red Neuronal Convolucional

Se implementa una CNN con varias capas convolucionales, pooling, dropout y capas densas finales.

Estructura general:

Bloques Conv2D
MaxPooling2D
Flatten
Dense
Dropout
Capa final softmax

El modelo fue entrenado durante 25 épocas y obtuvo una accuracy aproximada cercana al 70% en test.

También se graficaron:

Curva de pérdida.
Curva de accuracy.
Comparación entre entrenamiento y test.
3. Red Convolucional Profunda

Se implementa un modelo más profundo, con 16 o más capas entre convolucionales y densas.

El objetivo era mejorar la capacidad de generalización del modelo anterior. Sin embargo, el resultado fue inferior: el modelo profundo obtuvo una accuracy aproximada de 63% en test.

Esto muestra que aumentar la profundidad del modelo no siempre mejora el rendimiento. En este caso, el modelo más profundo no generalizó mejor que la CNN anterior.

Evaluación

Se utilizaron las siguientes métricas:

Accuracy.
Loss.
Classification report.
Matriz de confusión.
Errores por clase.

Además, se identificó la clase en la que el modelo comete más errores a partir de la matriz de confusión.

Predicción sobre nuevas imágenes

Finalmente, el modelo profundo se aplicó sobre el conjunto cnn_pred_X.npy, que contiene imágenes sin etiqueta.

El notebook muestra ocho imágenes aleatorias del conjunto de predicción junto con la etiqueta asignada por el modelo.

Ejecución en Google Colab

El notebook está preparado para ejecutarse en Google Colab.

Para usarlo:

Abrir el notebook en Colab.
Subir los archivos .npy requeridos.
Ejecutar las celdas en orden.
Revisar las métricas, gráficos y predicciones generadas.
Conclusiones

El modelo Fully Connected tuvo un rendimiento limitado, lo cual era esperable al trabajar con imágenes.

La red convolucional del punto 3 obtuvo el mejor rendimiento general, alcanzando aproximadamente un 70% de accuracy en test.

El modelo convolucional más profundo no mejoró la generalización, pese a tener más capas. Esto demuestra que un modelo más complejo no necesariamente es mejor si no está correctamente ajustado o si no cuenta con suficientes datos, regularización o estrategia de entrenamiento.

En este desafío, la CNN intermedia resultó ser la alternativa más equilibrada entre complejidad y rendimiento.
