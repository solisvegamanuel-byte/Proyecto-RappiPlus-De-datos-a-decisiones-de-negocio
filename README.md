# 📊 RappiPlus | De datos a decisiones de negocio

**Análisis de E-commerce | Python · SQL · PostgreSQL · Power BI · Estadística**

## 1. Contexto y problema de negocio

RappiPlus es un servicio de suscripción dentro del ecosistema de Rappi, cuyo propósito es incentivar la frecuencia de compra y aumentar el valor generado por sus usuarios.

El principal desafío del proyecto consistía en comprender el desempeño comercial y la rentabilidad del servicio. La información se encontraba distribuida en diferentes fuentes y presentaba problemas de calidad que dificultaban obtener indicadores confiables.

Además, era necesario responder preguntas como:

- ¿Cuántos ingresos genera el negocio y qué tan rentable es?
- ¿Qué productos y categorías contribuyen más a los resultados?
- ¿Cómo evolucionan las ventas a lo largo del tiempo?
- ¿Qué relación existe entre la inversión en marketing y el desempeño comercial?
- ¿Dónde existen oportunidades para mejorar la conversión y retención de usuarios?

**Problema central:** transformar datos transaccionales con inconsistencias en información confiable que permitiera evaluar el negocio y detectar oportunidades de mejora.

## 2. 🎯 Objetivo y estrategia de análisis

El objetivo fue desarrollar un proceso de análisis de datos que permitiera evaluar el rendimiento de RappiPlus, identificar patrones comerciales y comunicar los resultados mediante dashboards interactivos.

Para resolverlo, organicé el proyecto en cinco etapas:

1. **Preparación:** identificar y corregir problemas de calidad mediante Python.
2. **Rentabilidad:** relacionar pedidos y catálogo para calcular ingresos, costos y utilidad bruta.
3. **Comportamiento de usuarios:** utilizar SQL para estudiar cohortes, retención y comportamiento de compra.
4. **Experimentación:** aplicar pruebas estadísticas para evaluar posibles diferencias entre variantes de producto.
5. **Business Intelligence:** construir dashboards en Power BI que facilitaran la exploración de indicadores y la toma de decisiones.

La estrategia consistió en asegurar primero la calidad de los datos, construir después indicadores de negocio y finalmente convertir los resultados en visualizaciones comprensibles.

---

## 3. 🧰 Tecnologías utilizadas

| Herramienta | Aplicación |
|---|---|
| Python / Pandas | Limpieza, transformación y validación |
| NumPy | Operaciones numéricas y tratamiento de datos |
| SQL / PostgreSQL | Consultas y análisis de cohortes |
| SciPy | Pruebas estadísticas |
| Power Query | Transformaciones y corrección de tipos |
| Power BI / DAX | Modelado, indicadores y dashboards |
| Jupyter Notebook | Desarrollo y documentación del análisis |

## 4. 🔎 Desarrollo del proyecto

### Etapa 1. Preparación y limpieza de datos

**Problema:** las fuentes originales presentaban registros duplicados, valores faltantes, cantidades negativas, diferencias en formatos y observaciones extremas que podían distorsionar los indicadores.

Trabajé con tres fuentes principales:

- `rappiplus_orders_raw.csv`: información transaccional.
- `rappiplus_catalog.csv`: información del catálogo y costos de productos.
- `rappiplus_marketing_spend.csv`: inversión en marketing.

**Acciones realizadas:**

- Exploración de la estructura y tipos de datos.
- Identificación y eliminación de duplicados.
- Tratamiento de valores faltantes según las características de cada variable.
- Estandarización de categorías y formatos.
- Detección y corrección de cantidades inconsistentes.
- Recálculo de importes a partir de precios, cantidades y descuentos.
- Exportación de datasets preparados para el análisis.

**Resultados de calidad de datos:**

| Indicador | Resultado |
|---|---:|
| Registros duplicados eliminados | 100 |
| Valores faltantes tratados | 610 |
| Valores atípicos corregidos | 10 |
| Datasets preparados | 3 |

Se generaron `orders_clean.csv`, `catalog_clean.csv` y `marketing_clean.csv`.

**Impacto:** se obtuvo una base de información más consistente para construir indicadores y reducir el riesgo de conclusiones basadas en registros erróneos.

### Etapa 2. Análisis comercial y rentabilidad

**Problema:** conocer los ingresos no era suficiente para determinar qué productos y categorías aportaban mayor valor al negocio.

Para responderlo, relacioné la información de pedidos con el catálogo utilizando `nombre_producto`, incorporando los costos unitarios necesarios para calcular la utilidad bruta.

Los indicadores principales fueron:

| KPI | Cálculo |
|---|---|
| Revenue | Precio unitario × Cantidad − Descuento |
| Cost | Cantidad × Costo unitario |
| Gross Profit | Revenue − Cost |
| Gross Margin % | Gross Profit / Revenue × 100 |
| Ticket promedio | Revenue / Número de pedidos |
| Unidades por pedido | Unidades vendidas / Número de pedidos |

La inversión en marketing se analizó por separado, evitando confundir la utilidad bruta con la utilidad neta.

**Resultado:** se construyeron métricas que permitieron evaluar los ingresos, costos, utilidad bruta y contribución de los productos al desempeño comercial.

### Etapa 3. SQL y análisis de usuarios

**Problema:** además de conocer cuánto se vendía, era necesario estudiar el comportamiento de los usuarios y su permanencia en el servicio.

Se utilizó PostgreSQL para estructurar consultas orientadas al análisis de cohortes y actividad de usuarios.

Entre las técnicas empleadas se encuentran:

- Consultas con `JOIN` y `CTE`.
- Agrupación por fechas de registro.
- Identificación de semanas desde el registro.
- Conteo de usuarios activos mediante `COUNT DISTINCT`.
- Cálculo de tasas de retención por cohorte.

**Resultado:** se desarrolló una metodología para comparar la actividad de diferentes grupos de usuarios según su fecha de registro.

*Pendiente de incorporar: matriz final de retención, porcentajes por cohorte y principales hallazgos.*

### Etapa 4. Evaluación estadística y experimentación A/B

**Problema:** las diferencias observadas entre dos variantes de producto no necesariamente representan una mejora real.

El análisis estadístico se planteó para determinar si las diferencias en las métricas de conversión podían atribuirse al azar.

El procedimiento contempló:

1. Definir la métrica principal de conversión.
2. Formular las hipótesis nula y alternativa.
3. Calcular la conversión por grupo.
4. Seleccionar una prueba estadística apropiada.
5. Interpretar el resultado y sus implicaciones comerciales.

**Resultado pendiente de documentar:** tasas de conversión, tamaño de muestra, diferencia entre grupos, valor p e intervalo de confianza.

Sin esos resultados no sería correcto afirmar que una variante superó estadísticamente a la otra.

### Etapa 5. Dashboards ejecutivos en Power BI

**Problema:** los resultados del análisis necesitaban presentarse de forma que los responsables de negocio pudieran identificar tendencias y oportunidades sin consultar directamente los datos.

Desarrollé dos dashboards complementarios:

**Dashboard 1 — Overview Ejecutivo**

Diseñado para ofrecer una visión general del rendimiento comercial mediante:

- Ingresos y utilidad bruta.
- Inversión en marketing.
- Ticket promedio y cantidad promedio por orden.
- Evolución temporal de indicadores.
- Comparaciones con periodos anteriores.
- Filtros interactivos para explorar el desempeño.

**Dashboard 2 — Vista a Detalle**

Orientado a investigar los factores detrás de los resultados agregados:

- Rendimiento por producto y categoría.
- Distribución de ingresos y utilidad.
- Análisis por país, dispositivo y canal.
- Identificación de variaciones comerciales.
- Tabla de detalle transaccional.
- Navegación mediante *drill-through*.

Se utilizaron medidas DAX y relaciones entre tablas para permitir que los indicadores respondieran a los filtros seleccionados.

**Resultado:** una solución de Business Intelligence que permite pasar de la supervisión ejecutiva a la investigación detallada del desempeño.

*Agregar aquí capturas de ambos dashboards y sus respectivos enlaces.*

---

## 5. 📈 Resultados y hallazgos

### Resultados comerciales identificados

En la revisión del dashboard se registraron los siguientes indicadores de referencia:

| Métrica | Resultado aproximado |
|---|---:|
| Ingresos totales | $9.65 M |
| Utilidad bruta | $5.81 M |
| Inversión en marketing | $3 M |
| Ticket promedio | $386.14 |
| Pedidos analizados | 25 mil |
| Unidades vendidas | Más de 37 mil |

*Estas cifras deben contrastarse con el dashboard definitivo antes de considerarse resultados finales. También debe especificarse la moneda.*

### Hallazgos principales

**1. El negocio presenta resultados comerciales positivos a nivel de utilidad bruta.**

Los indicadores permiten analizar la diferencia entre ingresos y costos directos de producto. Sin embargo, una utilidad bruta positiva no garantiza rentabilidad neta, ya que deben considerarse otros gastos operativos.

**2. Se identificaron variaciones relevantes en los ingresos mensuales.**

La evolución temporal mostró una caída en febrero seguida de una recuperación en marzo. Este comportamiento merece un análisis adicional para identificar posibles factores estacionales, comerciales o promocionales.

**3. El desempeño no fue uniforme entre productos.**

La vista detallada permitió comparar productos según ingresos, unidades vendidas y utilidad bruta, ofreciendo una base para priorizar investigaciones comerciales.

**4. La inversión en marketing debe evaluarse junto con el rendimiento.**

El dashboard permite comparar ambas magnitudes. No obstante, para medir retorno atribuible sería necesario contar con información suficiente sobre conversiones y ventas generadas por campañas.

**5. La calidad de los datos era un factor determinante.**

Los 100 duplicados eliminados, 610 valores faltantes tratados y 10 outliers corregidos evidenciaron la necesidad de depurar la información antes de construir los indicadores.

---

## 6. ✅ Validación y confiabilidad del análisis

Para aumentar la confiabilidad del proyecto se aplicaron controles de calidad y consistencia.

| Control | Evidencia que debe conservarse |
|---|---|
| Duplicados | Comparación de registros antes y después de la limpieza |
| Valores faltantes | Resumen de nulos iniciales y finales |
| Outliers | Registro de valores identificados y criterios de corrección |
| Cálculos financieros | Comparación entre importes originales y recalculados |
| Relaciones de datos | Revisión de claves y coincidencias entre pedidos y catálogo |
| Indicadores en Power BI | Conciliación de totales con resultados obtenidos en Python |
| Retención | Comprobación de usuarios únicos y denominadores por cohorte |
| A/B testing | Revisión de muestra, supuestos, prueba estadística e interpretación |

**Criterio de validación:** los indicadores deben poder reproducirse a partir de los datasets limpios y sus reglas de cálculo.

Las correcciones realizadas no constituyen por sí solas una certificación de exactitud. La evidencia más sólida consiste en mostrar resultados reproducibles, verificaciones cruzadas y documentación de los supuestos empleados.

---

## 7. 💡 Conclusiones y recomendaciones de negocio

El proyecto permitió construir una visión integrada del rendimiento de RappiPlus a partir de información que inicialmente presentaba problemas de calidad.

Los resultados proporcionan una base para evaluar ingresos, utilidad bruta, productos, tendencias comerciales y gasto en marketing.

A partir del análisis, las principales recomendaciones son:

- **Rentabilidad:** priorizar el seguimiento de productos y categorías con mayor contribución a la utilidad bruta.
- **Desempeño temporal:** investigar las causas de las caídas mensuales antes de atribuirlas a factores específicos.
- **Marketing:** complementar el análisis del gasto con indicadores de adquisición y retorno atribuible.
- **Retención:** utilizar las cohortes para detectar posibles problemas de permanencia y orientar estrategias de fidelización.
- **Calidad de datos:** implementar controles periódicos para detectar errores antes de alimentar los reportes.

### Valor aportado

El principal aporte del proyecto fue transformar información transaccional en una herramienta de análisis que facilita comprender el desempeño del negocio y fundamentar decisiones comerciales.

Además, permitió aplicar un flujo de trabajo que integra preparación de datos, análisis financiero, SQL, estadística, modelado y visualización.

---

## 8. 📁 Recursos del proyecto

- **Datasets preparados:** `orders_clean.csv`, `catalog_clean.csv`, `marketing_clean.csv`.
- **Notebooks de Python:** limpieza y análisis exploratorio.
- **Consultas SQL:** análisis de usuarios y cohortes.
- **Power BI:** Overview Ejecutivo y Vista a Detalle.
- **Evidencia:** capturas, tablas de validación y resultados de pruebas estadísticas.

*Incorporar los enlaces correspondientes a los archivos que estén disponibles en el repositorio.*

---

### 👨‍💻 Autor

**Manuel Eduardo Solís Vega**

Data Analyst Jr. | Python · SQL · Power BI · Business Intelligence

Proyecto desarrollado como parte de mi portafolio profesional, con enfoque en análisis de datos, desempeño comercial y toma de decisiones basada en evidencia.
