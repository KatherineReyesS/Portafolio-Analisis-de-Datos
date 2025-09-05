# 🛒 Análisis de Ventas Walmart

## 📝 Descripción
Este proyecto presenta un **Análisis exploratorio y visual** aplicado a un dataset de transacciones de Walmart. El objetivo es inspeccionar y limpiar los datos, identificar patrones de compra, describir comportamientos por segmento (género, edad, ciudad), y extraer conclusiones accionables para análisis posteriores (modelado o segmentación).

## 🎯 Objetivos
- Explorar y limpiar el dataset.  
- Realizar estadísticas descriptivas y visualizaciones (histogramas, boxplots, heatmaps).  
- Detectar y manejar valores atípicos (IQR) y nulos.  
- Generar insights y recomendaciones para modelado o segmentación.

## 🧰 Tecnologías
- Python (pandas, numpy)  
- Visualización: matplotlib, seaborn  
- Entorno: Google Colab (notebook reproducible)  
- Control de versiones: Git / GitHub

## 🔬 Metodología

1. **Carga y exploración inicial**
   - `df.info()`, `df.describe()`, conteo de nulos y visualización (heatmap) para revisar estructura y calidad del dataset.

2. **Limpieza y ajuste de tipos**
   - Normalización de nombres de columnas y conversión de columnas a tipos adecuados (`category`, `int`, `float`).

3. **Manejo de valores faltantes**
   - Imputación automática: mediana para variables numéricas; moda (o `'Desconocido'`) para categóricas.
   - Verificación posterior de nulos (debe quedar en 0 por columna).

4. **Detección y tratamiento de outliers**
   - Detección por IQR (Q1 - 1.5*IQR / Q3 + 1.5*IQR).
   - Opción de imputar outliers por la **mediana calculada sin outliers** para minimizar sesgos.

5. **Análisis descriptivo (univariado)**
   - Histogramas y KDE para `Purchase`, boxplots para vars numéricas, conteo de categorías para variables categóricas.

6. **Análisis bivariado**
   - Boxplots por grupo (ej. `Purchase` vs `Gender` / `Age`) y scatterplots cuando aplique.

7. **Análisis multivariado**
   - Matriz de correlación y heatmap para identificar relaciones entre variables numéricas.
   - Cruces (groupby) para promedios de `Purchase` por `Product_Category` y `City_Category`.

8. **Resúmenes y top insights**
   - Tablas con top combinaciones (categoria-ciudad) y top usuarios por gasto acumulado.

9. **Recomendaciones para pasos siguientes**
   - Crear features temporales si existe fecha (mes, día de semana).  
   - Generar features por cliente (RFM: recencia, frecuencia, monto medio).  
   - Preparar codificación de categóricas y evaluar modelos robustos a outliers.

## 🔍 Resumen

- **Registros procesados:** 550,068  
- **Variables:** 10  
- **Valores faltantes (tras imputación):** 0  
- **Outliers imputados en `Purchase` (IQR → mediana):** 2,677  
- **Estadísticas clave de `Purchase`:**
  - Media ≈ **9,189.99**
  - Mediana ≈ **8,038.00**
  - Rango: **12** (min) – **~23,961** (max)

**Hallazgos rápidos:**  
El dataset quedó limpio y sin nulos después de la imputación automática. `Purchase` presenta amplia dispersión y múltiples picos en la distribución. Entre las categóricas, se observa predominio masculino, mayor representación del grupo etario 26–35 y mayor concentración de clientes en la categoría de ciudad B. En la matriz de correlación destaca una correlación negativa entre `Product_Category` y `Purchase` (~ -0.37).

## ▶️ Cómo ejecutar
### En Google Colab
1. Abrir el notebook:  
   `https://colab.research.google.com/drive/1dYDLlIoA2wduTCRMI_QKnVT586UO9jRQ?authuser=1`  
2. `Runtime > Run all` para ejecutar todas las celdas.  
