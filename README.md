# Acerca del conjunto de datos
## Contexto

Los dos conjuntos de datos están relacionados con las variantes tinta y blanca del vino portugués "Vinho Verde". Para más detalles, consultar la referencia [Cortez et al., 2009]. Debido a cuestiones de privacidad y logística, solo están disponibles variables fisicoquímicas (entradas) y sensoriales (salidas) (por ejemplo, no hay datos sobre tipos de uva, marca de vino, precio de venta del vino, etc.).

Estos conjuntos de datos pueden verse como tareas de clasificación o regresión. Las clases están ordenadas y no equilibradas (por ejemplo, hay muchos más vinos normales que excelentes o malos).

Contenido

Para obtener más información, lea [Cortez et al., 2009].

Variables de entrada (basadas en pruebas fisicoquímicas):

1. acidez fija
2. acidez volátil
3. ácido cítrico
4. azúcar residual
5. cloruros
6. dióxido de azufre libre
7. dióxido de azufre total
8. densidad
9. pH
10. sulfatos
11. alcohol

Variable de salida (basada en datos sensoriales):

12. calidad (puntuación entre 0 y 10)

## Consejos

Lo que podría ser interesante, además de utilizar modelos de regresión, es establecer un límite arbitrario para la variable dependiente (calidad del vino), por ejemplo. 7 o más se clasifican como 'bueno/1' y el resto como 'no bueno/0'.
Esto le permite practicar con el ajuste de hiperparámetros, por ejemplo. Algoritmos de árbol de decisión que analizan la curva ROC y el valor AUC.
Sin realizar ningún tipo de ingeniería de funciones o sobreajuste, debería poder obtener un AUC de .88 (sin siquiera utilizar un algoritmo de bosque aleatorio)

KNIME es una gran herramienta (GUI) que se puede utilizar para esto.

1 - Lector de archivos (para csv) al nodo de correlación lineal y al histograma interactivo para EDA básico.

2- Lector de archivos al 'Nodo del motor de reglas' para convertir la escala de 10 puntos a variable díctoma (buen vino y descanso), el código para poner en el motor de reglas es algo como este:

$calidad$ > 6.5 => "buena"
VERDADERO => "malo"

3- Salida del nodo del motor de reglas a la entrada del nodo Filtro de columnas para filtrar la característica original de 10 puntos (esto evita fugas)

Salida del nodo de filtro de 4 columnas a la entrada del nodo de partición (su división estándar de tren/tes, por ejemplo, 75%/25%, elija 'aleatorio' o 'estratificado')

5- Nodo de partición, datos del tren, salida dividida a la entrada del tren de datos divididos al nodo de aprendizaje del árbol de decisión y

6- Los datos de prueba del nodo de partición dividen la salida en el nodo predictor del árbol de decisión de entrada

7- Salida del nodo de aprendizaje del árbol de decisión a entrada Entrada del nodo del árbol de decisión

8- Salida del árbol de decisión para ingresar el nodo ROC... (aquí puede evaluar la base de su modelo en el valor AUC)
Inspiración

Utilice el aprendizaje automático para determinar qué propiedades fisicoquímicas hacen que un vino sea "bueno".

## Agradecimientos

Este conjunto de datos también está disponible en el repositorio de aprendizaje automático de la UCI, https://archive.ics.uci.edu/ml/datasets/wine+quality. Lo acabo de compartir con Kaggle para mayor comodidad. Me equivoco y el tipo de licencia pública no me permite hacerlo. Lo eliminaré a la primera solicitud. No soy el propietario de este conjunto de datos.

Por favor incluya esta cita si planea utilizar esta base de datos: P. Cortez, A. Cerdeira, F. Almeida, T. Matos y J. Reis. Modelado de preferencias de vino mediante extracción de datos a partir de propiedades fisicoquímicas. En Sistemas de apoyo a la decisión, Elsevier, 47(4):547-553, 2009.

Publicación relevante

P. Cortez, A. Cerdeira, F. Almeida, T. Matos y J. Reis. Modelado de preferencias de vino mediante extracción de datos a partir de propiedades fisicoquímicas.
En Sistemas de apoyo a la decisión, Elsevier, 47(4):547-553, 2009.