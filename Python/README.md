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

1. **Carga y exploración inicial:** `df.info()`, `df.describe()`, conteo de nulos y heatmap para revisar estructura y calidad.  
2. **Limpieza y ajuste de tipos:** normalización de nombres y conversión a `category` / `int` / `float`.  
3. **Manejo de nulos:** en este dataset no se detectaron valores faltantes; el notebook incluye funciones de imputación (mediana/moda) por compatibilidad.  
4. **Detección y tratamiento de outliers:** IQR (Q1 - 1.5*IQR / Q3 + 1.5*IQR). Opción de imputar outliers con la mediana sin outliers.  
5. **Análisis descriptivo (univariado):** histogramas y KDE para `Purchase`, boxplots para numéricas, conteos para categóricas.  
6. **Análisis bivariado:** boxplots por grupo (ej. `Purchase` vs `Gender`, `Age`), scatter plots si procede.  
7. **Análisis multivariado:** matriz de correlación y heatmap; groupby para cruces (`Product_Category` x `City_Category`).  
8. **Resumen & recomendaciones:** top combinaciones, top usuarios por gasto y propuestas de features (RFM, variables temporales).

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

**📌 Hallazgos rápidos:**  
El dataset no presentó valores faltantes en origen. `Purchase` muestra amplia dispersión y varios picos en la distribución. Entre las categóricas, se observa predominio masculino, mayor representación del grupo etario 26–35 y mayor concentración de clientes en la categoría de ciudad B. En la matriz de correlación destaca una correlación negativa entre `Product_Category` y `Purchase` (~ -0.37).

## ▶️ Cómo ejecutar
### En Google Colab
1. Abrir el notebook:  
   `https://colab.research.google.com/drive/1dYDLlIoA2wduTCRMI_QKnVT586UO9jRQ?authuser=1`  
2. `Runtime > Run all` para ejecutar todas las celdas.  
