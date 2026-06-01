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
