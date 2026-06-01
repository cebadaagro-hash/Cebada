---
icon: user-hat-tie-magnifying-glass
---

# Análisis de Inteligencia Predictiva: Clasificación de Precios

La volatilidad del mercado es el mayor riesgo para la rentabilidad de la cebada. Para gestionar este riesgo, el objetivo es determinar qué factores —específicamente el volumen producido, los niveles de humedad y la proteína— influyen para que un lote sea clasificado con un Precio Alto.

**Gestión del Valor del Producto**

A diferencia de los modelos descriptivos, aquí utilizamos algoritmos de clasificación para tomar decisiones de negocio preventivas:

* Regresión Logística: Nos permite calcular la probabilidad exacta de que un lote alcance un nivel de precio superior a la mediana del mercado.
* Árboles de Decisión: Ofrecen una hoja de ruta lógica. Al identificar qué variable (como la proteína) es el factor determinante para el precio, el agricultor puede ajustar sus procesos técnicos en tiempo real para "empujar" sus lotes hacia la categoría de mayor valor.

El procesamiento se realiza mediante PySpark ML, garantizando que el modelo sea capaz de manejar grandes volúmenes de datos con la misma precisión que modelos de escritorio:

```apache
// # --- MODELADO PREDICTIVO: Clasificación de Precio ---
# Transformación de datos en vectores para el motor de ML
assembler = VectorAssembler(inputCols=["Volumenproduccion", "Humedad_Recepcion_%", "Proteina_Total_ss_%"], 
                            outputCol="features")

# Entrenamiento de modelos para segmentación de precio
lr = LogisticRegression(featuresCol="features", labelCol="Precio_Alto")
modelo_logistico = lr.fit(train_data)
```

**Aplicación Comercial**

* Priorización de Inventarios: Si el modelo predice una alta probabilidad de "Precio Alto" para ciertos lotes, estos son destinados a almacenamiento estratégico para su venta en meses de mayor valor, en lugar de venderlos inmediatamente.

<figure><img src="../.gitbook/assets/WhatsApp Image 2026-05-31 at 9.11.13 PM.jpeg" alt=""><figcaption></figcaption></figure>

* Optimización Técnica: Si el Árbol de Decisión muestra que la humedad es el factor que está bajando el precio de un municipio específico, se ajustan los procesos de recepción y secado antes de la siguiente cosecha para corregir esa brecha.

Impacto Real: Esta herramienta permite pasar de una venta reactiva a una venta orquestada. Al conocer de antemano el potencial de precio de la cosecha, el productor deja de estar a merced del mercado y comienza a gestionar su inventario como un activo financiero de alto rendimiento.

