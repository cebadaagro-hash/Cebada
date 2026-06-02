---
icon: eye-dropper-half
---

# Análisis Estratégico: Distribución y Destino de la Cosecha

En la industria de la cebada, la calidad (calibre > 2.5mm) dicta el valor comercial del grano. No toda la producción es apta para la industria maltera. El equipo comercial necesita saber exactamente cuánto producto es "Premium" (apto para malta) y cuánto es "Estándar" para ajustar sus planes de distribución y precios por estado.

Por ello se ha diseñado un modelo de segregación de inventarios en el cual se procesa toda la base de datos de producción y, mediante una fórmula de calibración aplicada en Spark, separa automáticamente el volumen en dos categorías clave por estado:

<figure><img src="../.gitbook/assets/WhatsApp Image 2026-05-31 at 9.09.19 PM.jpeg" alt=""><figcaption></figcaption></figure>

* Vendido a Malteras: Grano de alto calibre, de mayor valor comercial.
* Se Quedan (Otros Usos/Rechazo): Producto que, por especificaciones técnicas, no alcanza los estándares malteros y debe ser redirigido a mercados secundarios o alimentación animal.
*

    <figure><img src="../.gitbook/assets/WhatsApp Image 2026-05-31 at 9.09.44 PM.jpeg" alt=""><figcaption></figcaption></figure>

Para garantizar el rendimiento con millones de registros, realizamos todo el cálculo matemático directamente dentro del motor de Spark, sin extraer los datos a Pandas, maximizando la velocidad

```apache
// # --- SEGREGACIÓN DE VALOR ---
# Cálculo del destino comercial por hectárea
df_spark = df_spark.withColumn(
    "Toneladas_Maltera", 
    F.col("Produccion_Total_Ton") * (F.col("Calibre_Original") / 100.0)
).withColumn(
    "Toneladas_Se_Quedan", 
    F.col("Produccion_Total_Ton") - F.col("Toneladas_Maltera")
)
```

