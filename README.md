# NYC YellowCab Spark Analysis

## 1. Descripción 

Este proyecto consiste en un análisis de los datos de viajes de YellowCab en la ciudad de Nueva York, utilizando **Apache Spark** para procesar grandes volúmenes de datos. Se realizan estudios sobre:

- Velocidad media de los taxis en función de la hora.
  
- Viajes en taxi más comunes.
  
- Media de la cantidad total pagada en función del número de pasajeros.
  
Esto se consigue mediante la implementación de consultas mediante `Spark SQL, DataFrames y RDDs`. El objetivo principal es realizar un **análisis de rendimiento** comparativo entre estas técnicas.

## 2. Contenido

El contenido de este proyecto se encuentra en el archivo .ipynb

## 3. Conclusiones
En este proyecto, hemos evaluado y comparado el rendimiento de tres métodos de procesamiento en **Apache Spark** `(DataFrame, SQL y RDD)` para diferentes consultas, utilizando múltiples núcleos de procesamiento. A continuación se presentan las conclusiones generales obtenidas de los análisis de tiempos de ejecución y de speedup:

### 3.1 Eficiencia de DataFrame y SQL frente a RDD:

- Los métodos `DataFrame y SQL` demostraron consistentemente un **mejor rendimiento que RDD** en todas las consultas. Esto se debe a que ambos métodos se benefician del **optimizador Catalyst de Spark**, que aplica optimizaciones automáticas, como la reordenación de operaciones y la eliminación de redundancias. Esta ventaja permitió que DataFrame y SQL alcanzaran tiempos de ejecución más bajos y mayor estabilidad frente a la variabilidad en el número de núcleos.

- RDD, al no beneficiarse de optimizaciones avanzadas, mostró tiempos de ejecución más altos y un comportamiento más variable, lo cual hace de este enfoque una opción menos eficiente para tareas analíticas en big data.
  
### 3.2 Escalabilidad y Paralelización:

- `DataFrame y SQL` lograron una mejora inicial en el rendimiento al aumentar el número de núcleos hasta un punto de saturación (alrededor de 8-10 núcleos). A partir de ese punto, el rendimiento adicional disminuyó debido al **overhead de paralelización**. Este comportamiento indica que DataFrame y SQL escalan bien hasta un cierto número de núcleos, después del cual la eficiencia marginal de añadir más núcleos disminuye.
  
- `RDD` no aprovechó de manera efectiva la paralelización y, en muchos casos, el incremento de núcleos resultó en tiempos de ejecución más altos. Este comportamiento refleja un problema inherente en la arquitectura de RDD para consultas que requieren optimización y paralelización eficiente.

### 3.3 Análisis de Speedup:

- Los gráficos de speedup evidencian que `SQL` es generalmente el método que alcanza **mayores niveles de speedup** en las consultas, siendo particularmente eficiente en las consultas "Viajes en Taxi Más Comunes" y "Cantidad Total Media Pagada". DataFrame mostró un comportamiento estable pero no alcanzó los picos de SQL, siendo una alternativa confiable.
  
- `RDD` presentó un speedup inferior a 1.0 en la mayoría de las configuraciones de núcleos, lo que indica que añadir más núcleos no mejora su rendimiento y, en muchos casos, lo empeora. Esto reafirma la recomendación de evitar RDD para consultas donde el rendimiento es prioritario.
  
### 3.4 Elección del Método Ideal para Consultas en Apache Spark:

- `SQL y DataFrame` son las opciones recomendadas para consultas analíticas en Spark. Ambos métodos ofrecen un balance óptimo entre rendimiento, escalabilidad y facilidad de uso en grandes volúmenes de datos. SQL se destaca cuando se busca el máximo rendimiento en entornos con núcleos limitados, mientras que DataFrame proporciona una estabilidad confiable.
  
- `RDD` debería reservarse para casos específicos donde se requiera un control granular de las operaciones a nivel bajo, ya que es menos competitivo en rendimiento y escalabilidad para consultas analíticas convencionales.

## 4. Resumen Final
En resumen, este análisis confirma que **Spark SQL** y **DataFrame** son las herramientas preferidas para realizar análisis de datos en Apache Spark, ya que ofrecen una ejecución rápida, eficiente y escalable hasta un punto óptimo de paralelización. RDD, aunque es útil en algunos contextos específicos, no es la mejor opción para tareas que exigen alta eficiencia y capacidad de paralelización en grandes volúmenes de datos.
