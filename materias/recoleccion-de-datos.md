---
icon: database
---

# Recolección de datos

Para el manejo de nuestro dataset, el cual supera el millón de registros incluyendo la integración de datos sintéticos, hemos implementado **PySpark** como tecnología base. La elección de esta herramienta responde a la necesidad de superar las limitaciones de la memoria local, permitiendo un procesamiento distribuido que garantiza  que nuestro modelo predictivo sea escalable y capaz de manejar miles de registros sin degradación de rendimiento.

Nuestra metodología se articula a través de un flujo de ETL (Extracción, Transformación y Carga) altamente optimizado:

* Extracción: Se utilizaron datos provenientes de FAOSTAT, el Sistema Estatal de Información Agropecuaria y la Estadística de Producción Agrícola, correspondientes al periodo 2022-2024, es importante mencionar que las bases originales no contenían únicamente información de cebada, sino también de otros granos agrícolas, por lo que fue necesario realizar un proceso de selección y limpieza para conservar únicamente los registros relacionados con la cebada,además, se incorporaron datos geográficos provenientes del INEGI, Modeloramas activos en México y datos sintéticos para enriquecer el conjunto de información,finalmente, todas las fuentes fueron integradas en una sola base de datos, la cual se utilizó para el análisis y la construcción del proyecto
* Aislamiento de la variable de interés: A través de PySpark, se aplicaron filtros condicionales para separar y extraer exclusivamente los registros relacionados con el cultivo de cebada, descartando información irrelevante del dataset original.

<figure><img src="../.gitbook/assets/image.png" alt="" width="563"><figcaption><p>Fuente:Universidad de Málaga</p></figcaption></figure>

* Control de calidad: Este proceso de segregación permitió eliminar el "ruido" informativo, garantizando que el dataset final estuviera compuesto únicamente por datos de alta fidelidad, coherentes con los objetivos de nuestro modelo predictivo.
* Consistencia Metodológica: La depuración realizada asegura que, independientemente de la fuente de origen, todos los datos procesados mantengan la misma integridad estructural, facilitando el entrenamiento del modelo y mejorando la precisión de los resultados.
* Transformación (Minería de Datos): Aplicación de procesos de limpieza a gran escala, incluyendo la normalización de caracteres, eliminación de duplicados y estandarización de formatos. Este proceso asegura la integridad estadística del dataset antes de su etapa de modelado.
* Carga: Estructuración de los _DataFrames_ de Spark, optimizados para alimentar los modelos predictivos de manera eficiente.

Esta arquitectura nos permite garantizar que el pipeline de datos sea reproducible y capaz de manejar nuevas cargas de información sin degradación en el desempeño.

_Nota: Para el periodo 2022-2024, se complementó la información oficial con datos sintéticos, los cuales fueron modelados para mantener la coherencia estadística con las tendencias observadas en los datos históricos reales._

