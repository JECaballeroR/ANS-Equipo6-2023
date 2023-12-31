# Aprendizaje no supervisado aplicado a la calificación de competencias en maestros del sistema educativo colombiano.
## Introducción
Este proyecto fue desarrollado por el Equipo 6 de la asignatura "Aprendizaje no Supervisado" de la Maestría en Inteligencia Analítica de Datos - MIAD, en su cohorte 2023

El equipo 6 está conformado por:
* Jorge Caballero,
* Rebeca Gamboa,
* Javier Abril
* Jesus Parada

El objetivo principal es identificar grupos desconocidos de docentes basados en sus competencias multidisciplinarias y detectar diferencias en los patrones de competencia que puedan indicar áreas de mejora para los programas de formación. Para lograr esto, emplearemos técnicas de aprendizaje no supervisado, como el clustering y sistemas de recomendación. Utilizaremos un dataset proporcionado por la Fundación Future Education (se modifica el nombre de la organización para mantener la reserva) que incluye las respuestas a estas 20 preguntas, así como información socio-demográfica de un grupo de maestros. Esta encuesta se utiliza para medir el nivel de desempeño en 5 competencias docentes clave, que luego se utilizarán para guiar los procesos de capacitación de los docentes. En última instancia, nuestro objetivo es encontrar nuevos patrones en los datos que permitan una dirección más efectiva de los esfuerzos de formación y evaluar la relevancia del instrumento de medición. La aplicación de modelos de Machine Learning y la inteligencia artificial en este contexto es fundamental para el progreso en el campo de la educación, particularmente en las áreas de evaluación y enseñanza.

La base de datos contiene 5270 observaciones y 33 variables (incluidas las 20 preguntas) que muestran las respuestas de los docentes, maestros y agentes educativas de las instituciones educativas o centros de desarrollo infantil en todo el territorio colombiano donde hace presencia la Organización. Se reporta información de 2022 y lo corrido del año 2023 para personas mayores de 18 años. 

Algunas de las ideas de valor a generar fueron:

1. Evaluar si todas las preguntas son necesarias para conocer el nivel de desempeño de una competencia (por reducción de dimensionalidad)
2. Validar si es correcto que cada competencia solo es explicada por las preguntas asignadas (mediante la revisión de los niveles de cada competencia en clusters generados)
3. Revisar si existen grupos multidisciplinares en los maestros, para ajustar programas de formación a estos grupos (mediante el análisis de clusters).
## Introducción
La fundación Future Education (se modifica el nombre real de la entidad por confidencialidad) tiene como propósito promover practicas innovadores en la educación colombiana. Uno de los instrumentos que implementa en sus proyectos es una encuesta que busca medir las competencias que tienen maestros/docentes/agentes educativos y que son fundamentales para mejorar la calidad de la educación.

Las Competencias del Siglo XXI es una adaptación del capítulo latinoamericano del proyecto ATC21s por sus siglas en ingles "Assessment and Teaching of 21 st Century Skills" de la Fundación Omar Dengo. 

[![](figs/atcs21.png)](https://www.mep.go.cr/evaluacion-competencias-siglo-xxi)

Este instrumento consta de 20 preguntas asociadas a 5 competencias:
* Creatividad e innovación.
* Pensamiento crítico.
* Resolución de problemas.
* Comunicación.
* Trabajo colaborativo.

El objetivo general del proyecto es la aplicación de técnicas de aprendizaje no supervisado para el análisis de los resultados de 5270 encuestas.

En un inicio, se espera encontrar grupos no conocidos de competencias multidisciplinares de acuerdo con las respuestas a sus preguntas. Utilizando estos grupos, se planea enfocar los esfuerzos de capacitación de acuerdo con estas necesidades, al estilo de un sistema de recomendación. Otra opción puede ser encontrar grupos con niveles de competencias similares, dando un “Score” basado en los grupos de respuestas de preguntas y enfocando la educación de acuerdo con el “alumno típico” de cada uno de estos grupos. El alcance de este proyecto llega hasta la obtención de estos grupos, y la validación de los grupos obtenidos, y por tanto, dar respuesta las preguntas: ¿Existen grupos formados por las respuestas y características socio demográficas de los docentes suficientemente separados para a futuro dar recomendaciones o asignar niveles de competencias multidisciplinares para brindar educación especializada? 
Al potenciar los esfuerzos de capacitación de los docentes en las competencias dadas, se puede llegar a agilizar la mejora en la calidad de educación de américa latina: mejores docentes más rápido hace que los alumnos estén más rápidamente expuestos a una mejor educación. Este tipo de acercamientos hasta ahora han empezado a emerger en américa latina, por lo que se considera un caso interesante para la aplicación de estas metodologías.


## Revisión preliminar de literatura
En la literatura, se han tenido acercamientos más que todo enfocados a estudiantes, cómo en el paper desarrollado por Bagunaid et al en el 2022.  En este paper, se utilizan diversas metodologías para llegar a un puntaje que se usa en clustering por DBSCAN con distancia Mhalanobis. Luego, se hace un ajuste para el desempeño individual del estudiante y esta información procede a un sistema de recomendación para brindar opciones de aprendizaje adicional a los estudiantes.  Igualmente, en el documento mencionan en su revisión de literatura que en las evaluaciones de estudiantes no se suele tener en cuenta las recomendaciones, sino que se da un puntaje que no necesariamente tiene en cuenta sus competencias individuales.
Revisando el Systematic Review para el Student Assessment de González-Calatayud, se observa que no existen contribuciones significativas de en américa latina sobre el uso de inteligencia artificial para evaluar al estudiante hasta su publicación en junio del 2021. No obstante, en 15 de los 22 papers que eligieron se tocan temas de Inteligencia Artificial para el assessment formativo, además de mostrar 10 papers que tratan del scoring automático de competencias afines a las evaluadas en la encuesta usada en este proyecto (por ejemplo, en Kaila et al. se evalúa el trabajo colaborativo).

## Aplicación de la metodología y resultados

### Consistencia interna del instrumento / Coeficiente Alfa de Cronbach
En términos generales la aplicación del instrumento a la encuesta da como resultados se obtuvo un valor general de Alpha de 0,726 lo que indica una confiabilidad buena. Los ítems de la escala están razonablemente correlacionados y la medida es considerada confiable para su uso en la mayoría de los casos. Sin embargo, las preguntas que miden cada competencia no son consistentes, tienen una baja confiabilidad, lo que implica que no parece ser la mejor manera de agruparlas.

### Reducción de dimensionalidad /Análisis de Componentes Principales (PCA)
Los resultados arrojan que es posible explicar el 80% de la varianza de los datos con utilización de 12 de los 20 componentes analizados. Las preguntas más representativas son las 7, 12, 5, 15, 9, 2, 17, 18, 20, 6, respectivamente. Observando la relación de las preguntas con las competencias, se concluye que las competencias Resolución de conflictos (p5-p8) y Comunicación (p17-p20) aportan  3 de sus 4 preguntas a la explicación del 80% de la varianza. Por otra parte, se puede intuir que Creatividad e Innovación, Pensamiento Crítico y Trabajo Colaborativo no necesariamente están siendo evaluadas correctamente, ya sea porque las personas no contestan esta pregunta o tienden a responder lo mismo. Por tanto, es posible que se deba realizar una diferenciación, eliminación o revisión de las preguntas que no agregan mucha variabilidad a las respuestas del instrumento.

### K Means
Se realiza clustering con 6 agrupaciones, alobservar el nivel general parece ser que los 6 están bien definidos entre puntajes medios y altos, sin embargo, las competencias de dichos grupos poblacionales muestran características diferentes. Se observan resultados La creatividad y el pensamiento crítico tienden a tener un comportamiento similar, por lo que es posible recomendar una reestructuración o unificación de ambas competencias. También las competencias de comunicación y trabajo colaborativo presentan un comportamientos similares, estás podrían ser agrupadas en un componente denominado habilidades sociales, o se podrían reestructurar las preguntas de trabajo colaborativo ya que solamente una aporta a la explicación del 80% de la varianza. En todos los clusters se encuentran desafíos en la competencia resolución de conflictos, ya que ningún cluster relaciona un puntaje general alto, con un alto nivel de resolución de conflictos.

### DBSCAN
Para el método DBSCAN se determina que el mejor valor de epsilon es 0.03 a través de revisión manual de valores entre 0.01 y 0.1 y el método sugerido por Rahmah y Sukaesih (2012). Con dicho parámetro se aplica el algoritmo a los datos. Se determina el  min_samples ajustando manualmente y revisando los clusters generados para los valores de 2 a 50, siendo el mejor el min_samples 30 para la diferenciación de los datos en los clusters.  El cluster se valida con el Silhoutte score y con observación de los niveles, obteniendo un score de 0.72, siendo min_samples=30 el equilibrio entre cluster diferenciables en el contexto de los niveles de la competencia y el máximo score de Silhoutte. Dentro de los resultados se observan clusters adicionales, pero los más grandes son similares a los encontrados por K-Means (el cluster 0 es similar al cluster 1 de kmeans, o el cluster 4 similar al 0 de Kmeans). 

## Conclusiones
* El instrumento es confiable para medir los niveles de competencias generales, pero no los específicos. Dado lo anterior, se sugiere ajustar las preguntas de acuerdo a la unificación propuesta de las competencias, removiendo aquellas que aporten menos a la varianza.
*  Se definen 3 nuevos grupos de niveles de competencia específica: 1)Habilidades sociales (Trabajo en equipo + Comunicación) 2) Pensamiento y creatividad y 3)Resolución de conflictos. Esto puede dar a entender que se deba evaluar usar 3 competencias en lugar de 5 dentro del instrumento de medición, reduciendo así el número de preguntas.
*   ado que no se tiene un “real”, es difícil hacer la evaluación de los modelos de forma objetiva. Un mejor score de Silhoutte no garantiza un mejor cluster para el caso de uso, e incluso dentro de los temas aprendidos, se hace énfasis en evaluaciones A/B o metodologías similares con un alto componente subjetivo. Se considera que los parámetros encontrados por evaluación manual y buscando la interpretabilidad de los clusters en función al contexto del problema son un buen primer acercamiento al problema.
*   Se plantea en el largo plazo y luego de iniciar un proceso de ajustes de acuerdo con los hallazgos del proyecto, realizar un análisis similar al instrumento modificado para evaluar la pertinencia:
        *   Concluir sobre la separación de los grupos y la viabilidad de a futuro aplicar sistemas de recomendación de contenido
        *   Concluir sobre si existe información suficiente en la encuesta para dar resultados, o si por el contrario hay preguntas redundantes en la clasificación, esto por medio de la evaluación del instrumento de obtención de datos con técnicas de reducción de dimensionalidad, específicamente aplicar PCA a dicha información.
        *   Dar conclusiones en relación con las ventajas y desventajas de no dar 5 puntajes sino la pertenencia a un grupo de competencias multidisciplinares.

## Bibliografía

* Bagunaid, W., Chilamkurti, N., & Veeraraghavan, P. (2022). AISAR: Artificial Intelligence-Based Student Assessment and Recommendation System for E-Learning in Big Data. Sustainability, 14(17), 10551. doi: 10.3390/su141710551
* González-Calatayud, V., Prendes-Espinosa, P., & Roig-Vila, R. (2021). Artificial Intelligence for Student Assessment: A Systematic Review. Appl. Sci., 11(12), 5467. doi: 10.3390/app11125467
* Minn, S. (2022). AI-assisted knowledge assessment techniques for adaptive learning environments. Computers and Education: Artificial Intelligence, 3, 100050. doi: 10.1016/j.caeai.2022.100050
* Deisenroth, M. P., Faisal, A. A., & Ong, C. S. (2020). Mathematics for machine learning. Cambridge University Press.
* Goodfellow, I., Bengio, Y., & Courville, A. (2016). Deep learning. MIT press.
* Hastie, T., Tibshirani, R., & Friedman, J. H. (2009). The elements of statistical learning: data mining, inference, and prediction. 2nd ed. New York: Springer.
* Murphy, K. P. (2012). Machine learning: a probabilistic perspective. MIT press.
* Peña, D. (2002). Análisis de datos multivariantes (Vol. 24). Madrid: McGraw-hill.
* Amat Rodrigo, Joaquín (2022). Clustering con Python. Available under a Attribution 4.0 International (CC BY 4.0) at https://www.cienciadedatos.net/documentos/py20-clustering-con-python.html. (Accedido 9 de Enero 2022)
* Hastie, T., Tibshirani, R., & Friedman, J. H. (2001). The elements of statistical learning: Data mining, inference, and prediction. New York: Springer.
* Jones, Aaron; Kruger, Christopher; Johnston, Benjamin. The Unsupervised Learning Workshop: Get started with unsupervised learning algorithms and simplify your unorganized data to help make future predictions. Packt Publishing. Kindle Edition.
* Kaufman, L. & Rousseeuw, P. (1990). Finding Groups in Data: An Introduction to Cluster Analysis, Wiley, New York.
* Macnaughton Smith, P., Williams, W., Dale, M. & Mockett, L. (1965). Dissimilarity analysis: a new technique of hierarchical subdivision, Nature 202: 1034–1035.
* Pedregosa, F. et al., 2011. Scikit-learn: Machine learning in Python. Journal of machine learning research, 12(Oct), pp.2825–2830.
* Fabila, Angelica & Minami, Hiroe & Izquierdo, Jesús. (2013). La escala de Likert en la evaluación docente: acercamiento a sus características y principios metodológicos. perspectivas docentes. 52.
* Shavelson, R.J. Biographical memoirs: Lee J. Cronbach. Washington, DC-USA: American Philosophical Society, v. 147, n. 4. p. 379-385, 2009.
