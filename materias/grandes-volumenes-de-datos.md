---
icon: user-robot-xmarks
---

# Grandes volúmenes de datos

**¿Por que PySpark?**

El procesamiento de datos a gran escala requiere herramientas que superen las limitaciones de la memoria local. Hemos seleccionado PySpark como nuestra tecnología base porque permite el procesamiento distribuido, garantizando que nuestro modelo predictivo sea escalable y capaz de manejar miles de registros sin degradación de rendimiento.

**Implementacion**&#x20;

Nuestro flujo de trabajo se basa en un proceso de ETL (Extracción, Transformación y Carga) optimizado para Big Data:

* Extracción: Ingestión directa de archivos en formato CSV desde nuestro repositorio de datos.
* Transformación: Limpieza y unión (_join_) de bases de datos relacionales para consolidar la información de ventas y licencias.
* Carga: Preparación de DataFrames de Spark optimizados para el modelado predictivo.

Este es el script central que ejecuta la carga y consolidación de nuestras fuentes:

{% code title="" overflow="wrap" expandable="true" %}
```
// 
```
{% endcode %}
