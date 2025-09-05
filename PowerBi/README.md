# 📊 Dashboards en Power BI
# 📘 Informe — Análisis de Catálogo y Ventas (Zara)

> **Descripción breve:** Este repositorio centraliza los artefactos del análisis del catálogo de Zara: el dataset original (`/data/Zara_Sales_Analysis.csv`) y el reporte interactivo en Power BI (`/pbix/Power Bi Katherine Reyes.pbix`). El objetivo es describir la data, documentar las transformaciones y entregables, y presentar hallazgos y recomendaciones en el estilo usado por el equipo.

---

## 🧭 Contexto del negocio

Zara mantiene un catálogo extenso y dinámico; el presente análisis proviene de un scraping puntual del catálogo (snapshot). El objetivo es entender la composición del catálogo por términos (`terms`), posiciones de producto (`Product_Position`), y analizar distribución de precios y volumen capturado. Estos insights sirven como insumo para decisiones de merchandising y priorización de scraping/monitorización.

---

## 🎯 Objetivo del análisis

1. Identificar los términos y categorías con mayor presencia en el catálogo.
2. Estimar ingresos relativos por `terms` y `product_position` (métrica derivada).
3. Detectar problemas de calidad de datos (nulos, duplicados, formatos).
4. Entregar un modelo y medidas DAX listos para replicar en Power BI.

---

## 📌 Resumen ejecutivo / KPIs (desde dashboard)

> Valores extraídos del informe Power BI incluido (representativos del snapshot):

* **Ingresos Totales (estimados):** \$409,54M
* **Ventas (unidades o score):** 396 mil
* **Ticket Promedio:** \$1,88M
* **Precio Medio:** \$1,03M
* **Transacciones (rows):** 218
* **Fecha Última Actualización:** 19-02-2024

> Nota: los valores anteriores se basan en cálculos del `.pbix`. Recomendamos validar la definición exacta (por ejemplo, si `Sales Volume` es unidades reales o un score de popularidad) antes de usar estos KPIs para decisiones operativas.

---

## 📊 Hallazgos clave (resumen)

* **Concentración por término:** `jackets` representa \~75% del ingreso relativo en el snapshot; otras categorías relevantes: `shoes`, `t-shirts`, `sweaters`, `jeans`.
* **Product Position:** las posiciones como `Aisle` y `End-cap` concentran la mayor proporción de ingresos (43% y 29% en el dashboard respectivamente).
* **Promoción y estacionalidad:** la muestra muestra una distribución pareja entre productos en promoción y estacionales (\~50% cada uno).
* **Top productos:** el top 15 de `name` muestra items con ingresos unitarios altos (ej.: PLAID OVERSHIRT, BOMBER JACKETS), útil para análisis de surtido.
* **Calidad de datos:** pocos nulos en `name` y `description`; `price` consistente y en USD. El dataset es un snapshot corto (19-02-2024), por lo que no captura dinámicas temporales.

---

## 📂 Archivos en el repositorio

* `/data/Zara_Sales_Analysis.csv` — Dataset (CSV; separador `;`).
* `/pbix/Power Bi Katherine Reyes.pbix` — Reporte y modelos en Power BI.
* `/images/` — Capturas del dashboard y visuales del informe.
* `/docs/medidas_dax.md` — Documentación de medidas DAX (recomendada).
* `/docs/diccionario_datos.md` — Diccionario de columnas y definiciones.

---

## 🛠 Cómo usar (rápido)

1. Clona el repositorio.
2. Abre `Power Bi Katherine Reyes.pbix` en Power BI Desktop.
3. En Power Query revisa la importación del CSV (selecciona `;` como separador si es necesario).
4. Verifica tabla de fechas (`DimDate`) y relaciones en star schema.
5. Revisa y valida las medidas DAX en la página de KPIs.

---

## 🧾 Metodología (ETL / Power Query)

1. **Importación:** leer CSV con `;` como separador.
2. **Normalización:** trim + lower para `terms`, `section`, `brand`.
3. **Fechas:** convertir `scraped_at` a `DateTime`; crear `DimDate` y columnas Year/Month/Day.
4. **Duplicados:** identificar por `sku` / `Product ID` y decidir agregación.
5. **Tipos:** asegurar `price` y `Sales Volume` como numéricos; revisar `currency`.
6. **Modelado:** Fact table `Fact_Catalog` (sales\_volume, price, product\_id, term\_id, date\_id) + dimensiones `Dim_Product`, `Dim_Terms`, `DimDate`.

---

## 🧮 Medidas DAX recomendadas

> Las siguientes medidas son plantillas; adapta nombres de tablas/columnas según tu modelo.

**Unidades vendidas (UnitsSold)**

```DAX
UnitsSold = SUM(Fact_Catalog[Sales Volume])
```

**Ingresos estimados (TotalSales)**

```DAX
TotalSales = SUMX(Fact_Catalog, Fact_Catalog[Sales Volume] * Fact_Catalog[price])
```

**Ticket promedio (AvgTicket)**

```DAX
AvgTicket = DIVIDE([TotalSales], [UnitsSold])
```

**% Productos en Promoción (PctPromoted)**

```DAX
PctPromoted = DIVIDE(CALCULATE(COUNTROWS(Fact_Catalog), Fact_Catalog[Promotion] = "Yes"), COUNTROWS(Fact_Catalog))
```

**Top N ventas (ejemplo)**

```DAX
TopProductsSales =
CALCULATE([TotalSales], TOPN(15, ALL(Dim_Product[name]), [TotalSales], DESC))
```

---

## 📋 Diccionario breve de columnas

* `Product ID` — Identificador único.
* `name` — Nombre del producto.
* `sku` — Código de inventario.
* `price` — Precio (USD).
* `Sales Volume` — Valor reportado por scraping (interpreta como unidades o score según nota).
* `terms` — Etiqueta de búsqueda/colección.
* `Product_Position` — Ubicación en tienda / presencia en página (Aisle, End-cap, Front of Store).
* `Promotion` — Indicador si estaba en promoción.
* `scraped_at` — Timestamp de captura.

---

## 🔎 Recomendaciones operativas

1. **Clarificar semántica de `Sales Volume`.** Si son unidades, las medidas y KPIs quedan; si son scores, ajustar interpretación.
2. **Automatizar scraping** en ventanas regulares (diarias/semanales) para análisis temporal y tendencias.
3. **Publicar dataset en OneDrive/SharePoint** y configurar gateway para refrescos automáticos del `.pbix` si se publica en Power BI Service.
4. **Extender diccionario** y documentar supuestos en `docs/medidas_dax.md`.
5. **Normalizar `terms`** y agrupar sinónimos (p.ej. `t-shirts` vs `t shirts`) para evitar dispersiones en análisis.

---

## ✍️ Conclusión

El análisis entregado permite una visión rápida del catálogo y su distribución por términos y posición de producto. Es una base adecuada para: priorizar scraping, detectar SKUs de alto impacto y generar tableros operativos. Para avanzar, recomendamos operacionalizar la recolección de datos y formalizar el modelo con dimensiones y medidas documentadas.

---

## 📞 Autor y contacto

* Archivo PBIX: *Katherine Reyes* (autor del `.pbix`).
* Soporte: Equipo de Análisis — solicita revisión de definiciones si se usará para decisiones de negocio.

---

*Si quieres, genero ahora los archivos `docs/diccionario_datos.md` y `docs/medidas_dax.md` con el detalle completo y los exporto para descargar.*
