# 🧠 SQL & MySQL Workbench — Amazon Bestsellers (resumen)

Breve guía práctica para trabajar con la base de datos `amazon_bestsellers`.  
Contiene instrucciones rápidas, descripción de tablas y consultas listas para copiar/pegar.

---

##📌 Ejecutar (rápido)
```sql
USE amazon_bestsellers;
SHOW TABLES;

##📁 Qué encontrarás

Script Amazon_bestseller.sql con la estructura y datos.

Tabla raw datos_crudos (csv importado) para ETL y limpieza.

Tablas normalizadas: producto, clasificacion, precio_historico, foto_producto, categoria, mercado, moneda, valoracion_historica, etc.

Archivos con ejercicios y consultas por secciones.

## 🧾 Tablas principales (resumen)

datos_crudos — Registros originales (asin, product_title, product_price, product_star_rating, product_num_ratings, product_url, product_photo, rank_change_label, country, page, fecha_import, ...).

producto — Catálogo de productos (codigo_producto, nombre, codigo_categoria, url_producto).

clasificacion — Ranking por fecha y mercado (codigo_producto, codigo_mercado, fecha_referencia, puesto, precio, valoracion, numero_valoraciones).

precio_historico — Precios guardados por fecha.

foto_producto — URLs de imagen por producto.

categoria, mercado, moneda, valoracion_historica, fuente_datos, audit_log — Metadatos y tablas auxiliares.
