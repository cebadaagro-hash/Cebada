# Modelo de Series Temporales (ARIMA)

Hemos implementado un modelo estadístico ARIMA (AutoRegressive Integrated Moving Average). Este algoritmo actúa como un "estabilizador de incertidumbre", analizando los patrones históricos para proyectar con precisión cómo se comportará la cosecha en los próximos 3 años (2025-2027).

```apache
//# --- MODELO ARIMA: Pronóstico de Producción de Cebada ---
# Paso 1: Procesamiento distribuido para consolidar los datos históricos
df_clean = df_spark.withColumn('Fecha_Completa', F.to_date(F.col('Fecha_Completa'))) \
    .filter(F.col(variable_produccion).isNotNull())

# Paso 2: Conversión a serie temporal para análisis estadístico
serie_produccion = df_clean.groupby('Fecha_Completa').agg(F.mean(variable_produccion)).toPandas()
serie_produccion = serie_produccion.set_index('Fecha_Completa').asfreq('MS', method='ffill')

# Paso 3: Entrenamiento del modelo (ARIMA 8, 1, 3)
# Ajustamos el modelo para detectar tendencias pasadas y estacionalidad
modelo = ARIMA(serie_produccion[variable_produccion], order=(8, 1, 3))
resultado = modelo.fit()

# Paso 4: Proyección a 36 meses
prediccion = resultado.get_forecast(steps=36)
produccion_futura = prediccion.predicted_mean
```

El modelo nos permite obtener reportes inteligentes que guían la toma de decisiones:

1. Puntos Críticos: Identificamos el mes exacto donde la producción alcanzará su pico máximo.
2. Rango de Seguridad: Gracias al _Intervalo de Confianza_, conocemos el margen de error esperado, lo que permite a la cadena de suministro preparar su capacidad de almacenamiento sin sorpresas.

Impacto en el Negocio: Al anticipar la producción de cebada, equilibramos la oferta de los productores con la demanda de los centros de distribución (centros malteros)
