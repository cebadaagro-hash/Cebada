---
icon: user-hat-tie-magnifying-glass
---

# Optimización de Rutas: Eficiencia Logística en Tiempo Real

En la distribución de cebada, el costo del flete es uno de los factores que más impacta en el margen de utilidad. La planificación de rutas basada en la intuición o en una secuencia fija de visitas suele resultar en kilómetros innecesarios, mayor consumo de combustible y desgaste de la flota.

Hemos desarrollado un algoritmo de optimización de rutas que calcula la secuencia de visitas más eficiente entre municipios. Esta herramienta no solo sugiere el camino más corto, sino que compara el "costo de oportunidad" frente a la logística tradicional.

<figure><img src="../.gitbook/assets/WhatsApp Image 2026-06-01 at 3.59.53 PM.jpeg" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/WhatsApp Image 2026-06-01 at 3.59.53 PM (1).jpeg" alt=""><figcaption></figcaption></figure>

El motor utiliza PySpark para la gestión de datos geográficos y NetworkX para la modelación de redes, permitiendo visualizar la ruta óptima de forma clara y directa:

```apache
// # --- OPTIMIZACIÓN LOGÍSTICA ---
# Cálculo de ruta mediante el algoritmo de 'Vecino más cercano'
while pendientes:
    dists = [haversine_np(coord_dict[ruta_opt[-1]][0], coord_dict[ruta_opt[-1]][1], 
             coord_dict[p][0], coord_dict[p][1]) for p in pendientes]
    idx = np.argmin(dists) # Encontrar el punto más cercano para minimizar km
    ruta_opt.append(pendientes[idx])
    pendientes.pop(idx)
```

**Aplicaciones Estratégicas para el Productor**

* Reducción de Gastos Operativos: Al minimizar la distancia total recorrida, el costo por tonelada transportada disminuye directamente, protegiendo el margen del productor.
* Toma de Decisiones basada en Datos: Ya no se improvisan las rutas de entrega. El sistema presenta una comparativa clara entre la Estrategia Tradicional y la Estrategia Optimizada, permitiendo ver el ahorro real en kilómetros y tiempo antes de iniciar el viaje.
* Flexibilidad Operativa: El tablero permite seleccionar diferentes municipios de origen y destino dinámicamente, adaptándose a las necesidades de entrega de cada día.
* Impacto Real: Esta solución transforma la logística de un centro de costos a un activo de eficiencia. Al optimizar la red de distribución, el productor puede atender a más clientes con los mismos recursos, elevando la competitividad de su cosecha frente a grandes distribuidores.

>
