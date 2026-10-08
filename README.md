Pipeline ETL — Exportaciones del NEA (1993–2024)
Diplomatura Universitaria en Data Analytics e Inteligencia Artificial Aplicada

Universidad Nacional del Nordeste (UNNE) / Extender

1. Descripción del Proyecto
Este proyecto implementa un pipeline ETL (Extract, Transform, Load) modular e idempotente en Python para procesar el registro histórico de exportaciones provinciales del Nordeste Argentino (Chaco, Corrientes, Formosa y Misiones).

El pipeline extrae datos de la API pública de Series de Tiempo del INDEC (datos.gob.ar), reestructura las series crudas en formato tidy (largo), genera variables derivadas (participaciones porcentuales, variaciones interanuales, rankings por destino y clasificaciones por década), realiza un LEFT JOIN con la estructura por rubro exportador, ejecuta controles de calidad (quality checks) y persiste las salidas finales en formatos CSV, JSON y archivos de auditoría log.

2. Fuente de Datos
Origen: API de Series de Tiempo del portal de Datos Abiertos del Estado Argentino (datos.gob.ar).

Datasets utilizados:

357.1: Exportaciones por provincia y país de destino.

350.1: Exportaciones por provincia y rubro.

Período analizado: 1993 – 2024 (32 años).

Unidad de medida: Millones de dólares FOB (mUSD).

3. Instalación y Ejecución
Requisitos
Python 3.8 o superior (el proyecto utiliza únicamente la biblioteca estándar).

Instrucciones de Ejecución
Correr el pipeline ETL completo de punta a punta:
python src/main.py

Reutilizar los datos crudos ya descargados en data/raw/ (ejecución offline):
python src/main.py --sin-internet

Ejecutar los tests unitarios de la etapa de transformación:
python tests/test_transform.py

4. Archivos de Salida
El proceso genera y valida automáticamente tres salidas procesadas:

data/processed/exportaciones_nea.csv: Dataset analítico con 13 columnas y 1.408 filas exactas.

data/processed/resumen.json: Ficha técnica del proceso con métricas descriptivas y detalle de los quality checks.

data/processed/pipeline.log: Registro incremental de ejecuciones.

Muestra de Salida (Estructura de 13 Columnas)
anio,provincia,destino,region_destino,valor_musd,total_provincia_musd,participacion_pct,var_interanual_pct,decada,ranking_destino,es_top3,rubro_principal,pp_participacion_pct

2024,Chaco,China,Asia,110.93,401.74,27.61,46.36,2020s,1,True,Productos primarios,81.3

2024,Chaco,Brasil,Mercosur,18.12,401.74,4.51,30.45,2020s,6,False,Productos primarios,81.3

5. Hallazgos y Análisis del Dataset (Insights)
Al analizar las salidas generadas en exportaciones_nea.csv, se identifican tendencias clave del comercio exterior en el Nordeste Argentino:

Concentración Agrícola y Mercado Asiático: En la provincia de Chaco, para el año 2024 el principal destino de exportación fue China (con un valor de 110,93 mUSD, representando el 27,61% del total provincial), correlacionado con una alta participación de Productos Primarios en la canasta exportadora (81,3%).

Persistencia del Mercosur: Brasil se sostiene de forma continua a lo largo de las décadas (1990s a 2020s) como uno de los tres principales socios comerciales (Top 3) para la región, actuando como un mercado estratégico de proximidad para rubros manufacturados e industriales.