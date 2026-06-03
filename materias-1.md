---
icon: luchador-mask
---

# Resultados

Aquí consolidamos los hallazgos más relevantes obtenidos a través de nuestros modelos de datos. Cada análisis está diseñado para transformar información cruda en decisiones estratégicas para la producción y comercialización de cebada.

Puedes navegar por las secciones del menú lateral para acceder al detalle técnico de cada análisis:

* Modelo de Series Temporales (ARIMA): Proyecciones de producción a 36 meses para anticipar los ciclos de cosecha y la oferta de mercado.
* Análisis Probabilístico (Poisson): Evaluación de la probabilidad de rendimiento por región para gestionar la incertidumbre agrícola.
* Optimización de Rutas: Algoritmos de eficiencia logística que reducen drásticamente los kilómetros recorridos y los costos de transporte.
* Análisis Estratégico de Calidad: Visualización de datos clave (proteína y calibre) para clasificar la calidad del grano y maximizar su valor comercial.
* Clasificación Predictiva (Machine Learning): Modelos de clasificación para identificar lotes de alta rentabilidad antes de su salida al mercado.
* Consejo de uso: Cada sección incluye el código fuente en PySpark para garantizar la reproducibilidad y escalabilidad de los modelos, así como interpretaciones de negocio diseñadas para facilitar la toma de decisiones.

## **¡PRUEBALO TU MISMO!**

Debido a que la base de datos de este proyecto es masiva (**10.2 GB**), intentar ejecutar el código en una computadora local convencional puede saturar la memoria RAM y congelar el equipo. Para garantizar la transparencia y reproducibilidad, se ha configurado el entorno utilizando **Apache Spark** en la nube a través de **Google Colab**, aprovechando la infraestructura de Google para procesar los datos por bloques sin pérdida de rendimiento.

Para replicar y correr el modelo de manera interactiva, por favor sigue estos 3 pasos básicos:

**1. Descarga de la Base de Datos (10.2 GB)**

Descarga el archivo original de datos desde nuestro enlace seguro de almacenamiento. **No intentes abrirlo de forma local en tu equipo**: [**Descargar Base de Datos Completa (Google Drive)**](AQU%C3%8D_PEGA_EL_LINK_DE_COMPARTIR_DE_TU_GOOGLE_DRIVE/)

**2. Carga en tu Google Drive Personal**

Una vez descargada la base de datos de 10.2 GB, súbela a tu propia cuenta de Google Drive (te sugerimos crear una carpeta llamada "ProyectoCebada" y meter ahí el archivo). Esto permitirá que Spark lea los datos en streaming directamente desde los servidores de Google.

**3. Ejecución del Código en la Nube**

Haz clic en el siguiente botón para abrir nuestro notebook interactivo de Jupyter (`.ipynb`) directamente en el entorno de Google Colab. El código mantendrá toda la configuración original de Spark:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cebadaagro-hash/Cebada/blob/main/CEBADA_PP.ipynb)

&#x20;**Nota de ejecución:** Al iniciar el notebook en Colab, las primeras celdas instalarán el entorno virtual de Spark en la nube. Solo asegúrate de activar la celda que diga:

```python
from google.colab import drive
drive.mount('/content/drive')
```

para enlazar tu carpeta y modificar la ruta de lectura de Spark (`spark.read.csv`) para que apunte al archivo que subiste en tu Drive. El resto de la lógica metodológica correrá de forma automática.

