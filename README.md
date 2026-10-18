# 🛒 Pipeline de Limpieza y Análisis Exploratorio de Datos (E-commerce de Hardware)

## 📌 1. Origen y Contexto de los Datos
Este repositorio contiene un flujo automatizado en Python desarrollado con **Pandas** para el saneamiento, perfilado y análisis exploratorio de un dataset comercial de componentes de hardware (`base_hardware_2.xlsx`). El conjunto de datos simula transacciones de e-commerce e incluye variables críticas relacionadas con ventas, logística, medios de pago y segmentación geográfica.

## 🛠️ 2. Decisiones de Limpieza y Saneamiento Riguroso
Durante la fase de diagnóstico técnico, se identificaron y resolvieron diversas anomalías aplicando criterios estrictos de negocio en lugar de imputaciones ciegas:
* **Duplicados:** Se validó la unicidad de los registros transaccionales mediante `.drop_duplicates()` para evitar distorsiones en las métricas de negocio.
* **Imputación de Precios Unitarios:** Para resolver los valores nulos en `precio_unitario`, se implementó una **imputación relacional cruzada** utilizando la mediana de precio de cada producto específico dentro del catálogo.
* **Regla de Negocio en Descuentos:** Los valores faltantes en `descuento_porcentaje` no se rellenaron con medias genéricas; se programó una función condicional que replica exactamente la regla comercial basada en el volumen de unidades compradas (`cantidad`).
* **Tratamiento de Nulos Restantes:** Las variables numéricas de soporte (`dias_demora`) se imputaron por su mediana para mitigar sesgos por valores atípicos, mientras que las categóricas (`provincia_cliente`, `genero_cliente`) se normalizaron con etiquetas de control específicas (`"Desconocida"` / `"Desconocido"`).
* **Tipos de Datos y Estructura:** Se convirtieron las columnas de fechas (`fecha_compra`, `fecha_entrega`) al tipo `datetime64` y se aplicó `.reset_index(drop=True)` para garantizar la integridad estructural del DataFrame.

## 📊 3. Agregaciones y Hallazgos Clave de Negocio
Se generaron tres agrupaciones estratégicas (`groupby`) para responder a preguntas directas del negocio:
1. **Ticket y Monto Promedio por Categoría:** Permitió identificar que las *Placas de Video* lideran ampliamente la facturación promedio frente a componentes de menor costo o periféricos.
2. **Rendimiento Geográfico:** Evaluó el volumen de operaciones y la facturación acumulada por provincia (Buenos Aires, Córdoba, Mendoza, Salta), facilitando la detección de mercados clave.
3. **Eficiencia Logística por Medio de Pago:** Cruzó los medios de pago con los días de demora para auditar y descartar fricciones operativas en la cadena de distribución.

## 🚀 4. Instrucciones de Ejecución
1. Clonar este repositorio.
2. Asegurarse de tener instaladas las dependencias necesarias (`pip install pandas openpyxl`).
3. Ejecutar el cuaderno Jupyter o script de Python de principio a fin para reproducir todo el pipeline de limpieza y análisis.
