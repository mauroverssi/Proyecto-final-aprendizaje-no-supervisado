# Análisis de la clasificación de los hogares pobres en Costa Rica, según su grado de severidad de la pobreza
1. [Resumen del proyecto](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/blob/main/README.md#resumen-del-proyecto)
2. [Datos](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/blob/main/README.md#datos)
3. [Descripción detallada de la base de datos](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/blob/main/README.md#descripci%C3%B3n-detallada-de-los-datos)
4. [Propuesta inicial de Proyecto Final](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/blob/main/README.md#propuesta-incial-de-proyecto-final)



## Resumen del proyecto
Los niveles de pobreza de Costa Rica han permanecido estancados por más de 4 décadas. Para atacar este problema, el estado costarricense ha implementado una serie de subsidios monetarios a hogares pobres, sin embargo, en febrero del 2022, un informe indicó que cerca de 200.000 personas reciben ayudas estatales, que representa el 26,5% del fondo de pobreza, pese a no calificar en condición de pobreza. Esta situación motiva a revisar si la información que se utiliza para calcular el Índice de Pobreza Multidimensional (IPM), el cual clasifica a un hogar en pobre o no pobre, puede ser objeto de mejora por medio de la aplicación de herramientas de aprendizaje no supervisado para hacer agrupamiento en clusters, permitiendo una mejor clasificación de los hogares y, en consecuencia, una mejor asignación de ayudas estatales.

## Datos

Para este proyecto se utilizará la base de datos obtenidos en la encuesta nacional de hogares realizada en julio de 2021 (INEC 2021). Dicha encuesta concentra información del ingreso de los hogares, su distribución territorial y las características de estos. Se contemplan datos sobre vivienda, educación, el trabajo de las personas y las condiciones de trabajo, entre otros. Además, para 2021 el INEC agregó un módulo adicional con el objetivo de medir los impactos de la pandemia del COVID-19 en Costa Rica. La base de datos completa está disponible acá [Datos](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/blob/main/Datos/ENAHO%202021.sav)

## Descripción detallada de los datos

En este [Notebook](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/blob/main/Notebooks/Proyecto%20-%20Revision%20datos.ipynb) pueden encontrar una la descripción detallada de la base datos. 

##  Propuesta incial de Proyecto Final

En esta carpeta se encuentra la documento de la entrega final [Documentos](https://github.com/mauroverssi/Proyecto-final-aprendizaje-no-supervisado/tree/main/Documentos)

## Análisis de resultados y conclusiones

Del análisis del coeficiente de Silouethe se concluye que la mejor calidad de agrupamiento se obtiene con 2 clusters, lo cual resulta útil para el desarrollo del proyecto dado que el IPM también hace una clasificación en dos categorías: pobre y no pobre. Con este resultado se decide analizar todos los modelos con 2 clusters. Es importante aclarar que la calificación de “pobre” y “no pobre” se retira del set de datos y no se considera en los modelos de agrupamiento. 

Gráfico, Gráfico de líneas

Descripción generada automáticamente 

Con respecto a los modelos desarrollados sobre el set de datos de la Variante 1, se obtuvo el mejor resultado con Kmedias (precisión 0,817). El modelo asocia el Cluster 0 mayoritariamente a la categoría “No pobre” (63,4% de los hogares) y el Cluster 1 a la categoría “Pobre” (18,8% de los hogares). Del 18,2% de los hogares restantes es de interés el 3,3% que están en la categoría “pobre” y que quedaron en el Cluster 0 (mayoritariamente “no pobre”) porque podrían estar mal clasificados y, en consecuencia, estarían recibiendo subsidios de manera errada. 

Variable y densidad de los clusters, desigualdad en Costa Rica. JS 

El modelo Kmedoides utilizando el set de datos de la Variante 3 (variables categóricas) y distancia Gower tuvo un desempeño regular (precisión 0,656). El tiempo de procesamiento para calcular las distancias y luego el agrupamiento fue muy alto. Por este motivo, no se exploraron otras alternativas con esta estrategia de análisis. 

El modelo de agrupamiento más preciso fue Kmedias utilizando el set de datos de la Variante 1 (ver Tabla 3). No se encontraron características que pertenecieran exclusivamente a la calificación de “pobre” o “no pobre” del IPM con respecto a los dos clusters obtenidos con Kmedias sin embargo, se identificaron características predominantes que pudieran ser las más relevantes para dar un indicio si un hogar es pobre o no pobre: 

Hogar pobre 

Hogar no pobre 

Estado de techos, pisos y paredes: Malo 

Sistema de eliminación de basura: lo queman 

Servicio de agua: sin servicio 

Seguro de salud: sin seguro 

Estado de techos, pisos y paredes: Bueno 

Área de vivienda: mayor que 151 mts2 

Fuente de agua: acueducto municipal 

Servicio sanitario: conectado a alcantarillado o cloaca 

Nivel de educación: superior o superior con posgrado 

Seguro de salud: con seguro 

Ingreso per cápita: más de 128.000 

Condición de aseguramiento: asalariado 

Por otra parte, de identifica que hay 1.064 hogares (3,3%) en la categoría “pobre” que quedaron en el Cluster 0, que es mayoritariamente de hogares “no pobre”. Estos hogares, en general, tienen niveles de educación intermedios, condiciones de servicio aceptables e ingresos bajos o medios. Se concluye que estos hogares pudieran ser objeto de revisión en su calificación del IPM porque podrían estar siendo clasificados erróneamente, afectando la correcta distribución de subsidios que da el gobierno de Costa Rica.   

Debido a la alta desviación estándar de la muestra está muy alta quiere decir que los datos están muy dispersos, así como la varianza, lo que nos habla de que en Costa Rica hay una desigualdad marcada en su población lo que nos habla de la poca concentración de densidad en la muestra, lo que nos da indicios de que se debe indagar por desglosar o revisar la varianza en PCA y SVD. 

Por parte del PCA encontramos que, los componentes principales donde se concentra el 90% de la varianza son 33. Sin embargo, hay dos puntos a revisar, el primero es que se hace un codo en las primeras 4 variables, pero estas representan el 29% de la varianza, lo que a priori nos da indicios de poder trabajar con ellas, sin embargo, y debido a la dispersión que presentan los datos antes mencionada, notamos que en los siguientes 29 componentes principales se distribuye el restante 61% de la varianza, lo que se ve reflejado en los cálculos realizados para PCA, ya que los valores dieron muy similares a los resultados sin aplicar este método, con Kmedias (precisión 0.818), Jerárquico Aglomerativo con enlace Ward (precisión 0.79), DBSCAN (precisión 0.71). 

Debido a que los resultados obtenidos explorando la varianza con el método PCA nos dio resultados similares a los anteriores, pero a sabiendas de que la naturaleza del problema nos enmarca explorar un poco más en la varianza de los datos, implementamos SVD ya que SVD puede aplicarse a cualquier matriz real, ya que en PCA el producto X’X puede generar perdidas de precisión numérica, lo que no sucede con SVD. 

A pesar de que la porción de varianza explicada para el 90% equivale a 33 valores singulares, se hizo una exploración con iteraciones bajando el número de cantidad de valores singulares hasta encontrar el mejor desempeño con 15 valores singulares, que corresponden al 58.48% de la varianza explicada, donde kmedias (precisión 0.8213) valor que ya supera las anteriores pruebas, sin embargo, no fue el mejor score, en las otras pruebas se obtuvo  Kmedoides  (precisión 0.6186), seguido por DBSCAN (precisión 0.782), finalmente el mejor score fue con Jerárquico Aglomerativo con enlace Ward (precisión 0.8312). 

Finalmente, con él algoritmo jerárquico aglomerativo se obtuvo un mejor score de precisión, teniendo en cuenta el contexto de la problemática de la pobreza dimensional y la varianza alta de estas variables, se tomaron un poco más de la mitad y se comenzaron a relacionar desde la base del dendograma con el fin de ir fusionando esas variables, hasta fusionarla y tener n-2 grupos, con lo que podemos aprovechar menos valores singulares para llegar a los dos cluster que se esperan los cuales son pobreza y no pobreza, de tal manera que obtuvimos satisfactoriamente la respuesta a uno de los objetivos principales de esta problemática, que era llegar a la misma determinación de pobreza con menos variables y de una manera más eficiente, con el fin de refinar la manera con que esta problemática se calcula en una población.  
