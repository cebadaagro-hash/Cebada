---
icon: wheat-awn
---

# Análisis Probabilístico: Distribución de Rendimientos (Poisson)

En la agricultura, el rendimiento por hectárea no es una cifra estática; depende de la variabilidad del clima, la calidad del suelo y el manejo técnico. Para tomar decisiones logísticas inteligentes, no basta con saber el "promedio histórico", debemos conocer la probabilidad de obtener un rendimiento específico bajo las mejores condiciones de cosecha.

Hemos implementado un análisis basado en la Distribución de Poisson. Este modelo estadístico nos permite estimar la probabilidad de ocurrencia de distintas tasas de rendimiento (toneladas por hectárea) durante los meses de mejor cosecha por estado.

El proceso utiliza PySpark para agrupar millones de datos de rendimiento y SciPy para modelar la probabilidad de éxito en la cosecha.

```apache
// # --- ANÁLISIS DE POISSON: Probabilidad de Rendimiento ---
# Paso 1: Agregación de variables de rendimiento por estado y mes
analisis_clima_spark = df_clean.groupby(["Estado", "Mes_Cosecha"]) \
    .agg(F.mean("Rendimiento_Ton_Ha").alias("Rendimiento_Prom_Ton_Ha"))

# Paso 2: Cálculo de la Probabilidad (PMF)
# Utilizamos lambda (rendimiento promedio) para predecir la distribución
probabilidades = poisson.pmf(x_toneladas, mu=lambda_rendimiento)
```

<figure><img src="../.gitbook/assets/WhatsApp Image 2026-05-31 at 9.08.21 PM.jpeg" alt=""><figcaption></figcaption></figure>



Al visualizar las curvas de Poisson para los estados con mejores temporadas, obtenemos información estratégica:

1. Punto Óptimo (Línea Roja): Identificamos el rendimiento promedio exacto esperado (`lambda`).
2. Rango de Probabilidad: La curva nos indica qué tan probable es alcanzar un rendimiento superior o inferior al promedio. Esto permite a los productores ajustar sus expectativas y a la empresa planear la capacidad de carga de manera realista.
3. Comparativa Regional: Permite visualizar qué estados ofrecen una distribución más estable (curvas más concentradas) frente a aquellos que tienen una variabilidad mayor.

Impacto en el Negocio: Este análisis transforma datos crudos en una herramienta de gestión de riesgos. Al entender la probabilidad de rendimiento de la cebada, minimizamos la incertidumbre en la cadena de suministro y optimizamos la logística de transporte hacia los puntos de distribución.

>
