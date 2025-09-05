# 📘 Informe — Análisis de Catálogo y Ventas - Zara

## 🏷️ Sobre Zara
Zara es una compañía internacional de moda fundada en 1975 en Arteixo, España, integrante del grupo Inditex. Su modelo de fast fashion se caracteriza por ciclos de diseño y reposición muy cortos y una alta rotación de productos, lo que hace que el catálogo sea extremadamente dinámico. Por eso, los snapshots de catálogo (scraping) son herramientas útiles para entender surtido, precios y presencia de productos en un momento dado, pero no deben confundirse con series históricas de ventas.

## 🧭 Contexto del análisis
Zara mantiene un catálogo extenso y dinámico; el presente análisis proviene de un scraping puntual del catálogo (snapshot). El objetivo es entender la composición del catálogo por términos (`terms`), posiciones de producto (`Product_Position`), y analizar distribución de precios y volumen capturado. Estos insights sirven como insumo para decisiones de merchandising y priorización de scraping/monitorización.

## 🎯 Objetivo del análisis

1. Identificar términos y productos con mayor incidencia en el catálogo.
2. Calcular KPIs clave (Ingresos estimados, Ventas, Ticket Promedio, Precio Medio, Transacciones).
3. Detectar problemas de calidad de datos (nulos, duplicados, formatos).
4. Entregar un modelo y medidas DAX listos para replicar en Power BI.


## 📌 Resumen ejecutivo / KPIs (desde dashboard)

* **Ingresos Totales (estimados):** \$444.66 M
* **Ventas (unidades o scor):** 460 mil
* **Ticket Promedio:** \$1,76M
* **Precio Medio:** \$967,5495
* **Transacciones (rows):** 252
* **Fecha Última Actualización:** 19-02-2024

## 📊 Hallazgos clave 

* **% Ingresos:** muestra que `jackets` concentra la mayoría del ingreso relativo en el snapshot (~68–75% según vista y selección).; otras categorías relevantes: `shoes`, `t-shirts`, `sweaters`, `jeans`.
* **Product Position:** la participación por posición de producto, según el panel actual, es: Aisle 37,74%, End-cap 32,51%, Front of Store 29,75% — lo que indica que la mayor parte del ingreso estimado proviene de productos en pasillos y end-caps.
* **Promoción y estacionalidad:** la muestra muestra una distribución pareja entre productos en promoción y estacionales. Yes ≈ 51,96% / No ≈ 48,04%.
* **Top productos:** el top 15 muestra líderes como PLAID OVERSHIRT (≈10,9 mil), seguido por varios bomber/overshirts en el rango 7–7.4 mil. Estos items concentran ingresos unitarios altos y son prioritarios para análisis de surtido.
* **Calidad de datos:** pocos nulos en `name` y `description`; `price` consistente y en USD.


## 🛠 Cómo usar 

1. Descarga el archivo .pbix desde la carpeta /pbix/.
2. Abre `Power Bi Katherine Reyes.pbix` en Power BI Desktop.
3. Explora las distintas páginas y filtros interactivos.


## 🧮 Medidas DAX recomendadas

**%Ingresos**
```% Ingresos = 
DIVIDE(
    [Ingresos Totales],
    CALCULATE([Ingresos Totales], ALLSELECTED(Zara_Sales_Analysis)),
    0
)```

**Unidades vendidas**

```Ventas = SUM(Zara_Sales_Analysis[Sales_Volume])
```

**Ingresos totales**

```Ingresos Totales = SUMX(Zara_Sales_Analysis, Zara_Sales_Analysis[Sales_Volume] * Zara_Sales_Analysis[price])
```

**Ticket promedio**

```Ticket Promedio = DIVIDE([Ingresos Totales], [Transacciones], 0)
```

## 📋 Diccionario breve de columnas

* `Product ID` — Identificador único.
* `name` — Nombre del producto.
* `sku` — Código de inventario.
* `price` — Precio (USD).
* `Sales Volume` — Valor reportado por scraping (interpreta como unidades o score según nota).
* `terms` — Etiqueta de búsqueda/colección.
* `Product_Position` — Ubicación en tienda / presencia en página (Aisle, End-cap, Front of Store).
* `Promotion` — Indicador si estaba en promoción.


## ✍️ Conclusión

El análisis entregado permite una visión rápida del catálogo y su distribución por términos y posición de producto. Es una base adecuada para: priorizar scraping, detectar SKUs de alto impacto y generar tableros operativos. Para avanzar, recomendamos operacionalizar la recolección de datos y formalizar el modelo con dimensiones y medidas documentadas.
