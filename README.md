# Proyecto RappiPlus: De datos a decisiones de negocio

## 📊 Descripción del proyecto

RappiPlus es un servicio de suscripción dentro del ecosistema de Rappi diseñado para aumentar la frecuencia de compra y el valor generado por usuario.

El objetivo de este proyecto fue evaluar si el servicio realmente está cumpliendo su propósito mediante un análisis integral del negocio, combinando limpieza de datos, análisis de rentabilidad, SQL, cohortes, experimentación A/B y visualización en Power BI.

El proyecto responde preguntas clave como:

- ¿Podemos confiar en los datos?
- ¿El negocio está generando ganancias?
- ¿En qué parte del funnel se pierden los usuarios?
- ¿Los usuarios regresan después de registrarse?
- ¿Los cambios de producto generan impacto?
- ¿Cómo comunicar los resultados de forma clara para negocio?

---

## 🧰 Herramientas utilizadas

- Python
- Pandas
- NumPy
- SciPy
- SQL / PostgreSQL
- Power BI
- Jupyter Notebook

---

# 🔹 Paso 1: Preparación y calidad de datos con Python

La primera etapa consistió en limpiar y validar tres fuentes principales:

- `rappiplus_orders_raw.csv`
- `rappiplus_catalog.csv`
- `rappiplus_marketing_spend.csv`

### Trabajo realizado

Se analizaron:

- valores nulos
- registros duplicados
- inconsistencias de texto
- errores de formato
- valores extremos
- tipos de datos
- consistencia entre tablas

En `orders` se detectaron, entre otros problemas:

- filas completamente duplicadas
- países con diferencias de mayúsculas y minúsculas
- valores nulos en distintas columnas
- cantidades negativas
- outliers extremos en `cantidad`
- diferencias entre el total calculado y el total original

Los outliers de cantidad fueron identificados al encontrar valores como `10000` y `20000` frente a un comportamiento normal de `1` y `2` unidades por pedido.

También se reconstruyeron valores faltantes cuando existía suficiente información en otras columnas o registros del mismo usuario.

### Resultado

Se generaron tres datasets limpios:

- `orders_clean.csv`
- `catalog_clean.csv`
- `marketing_clean.csv`

---

# 🔹 Paso 2: Análisis de rentabilidad con Python

El objetivo fue determinar si el negocio estaba generando ganancias.

Se calcularon KPIs como:

- Revenue
- Cost
- Profit
- Ticket promedio
- Cantidad promedio por orden

Para calcular el costo por pedido se relacionó el catálogo de productos con las órdenes mediante `nombre_producto`.

La lógica principal utilizada fue:

```text
Revenue = ingresos generados por pedido

Cost = cantidad × costo_unitario

Profit = Revenue - Cost
