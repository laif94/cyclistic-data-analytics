# 🚲 Caso de Estudio: Análisis de Uso en Cyclistic Bike-Share

Un análisis analítico de extremo a extremo para transformar el comportamiento de los usuarios ocasionales en membresías recurrentes anuales. Este proyecto forma parte del **Google Data Analytics Capstone**.

Autor: Leopoldo Ibarra

---

## 🛠️ Stack Tecnológico Utilizado
* **Procesamiento y ETL:** Python, Pandas y **DuckDB** (procesamiento analítico columnar en memoria RAM).
* **Entorno de Desarrollo:** Google Colab / Jupyter Notebooks.
* **Origen de Datos (Data Lake Cloud):** Bucket oficial público de Divvy alojado en Amazon S3 (`https://divvy-tripdata.s3.amazonaws.com/index.html`).
* **Business Intelligence & Storytelling:** Tableau Public / Power BI.

---

## 📌 1. Definición del Problema (ASK)
El objetivo central de este análisis es identificar cómo difiere el comportamiento de uso de las bicicletas entre los **clientes ocasionales (casual riders)** y los **miembros anuales (annual members)** durante los últimos 12 meses.

A partir de estas diferencias, se diseñarán estrategias de marketing digital y geolocalizado orientadas a la conversión de usuarios casuales a suscripciones de largo plazo, maximizando la rentabilidad predecible de la empresa.

---

## ⚙️ 2. Pipeline de Datos y Auditoría de Calidad (PROCESS)
Debido al gran volumen de información original (~5.8 millones de filas), se utilizó **DuckDB** para ejecutar transformaciones rápidas directo en memoria, garantizando un proceso ETL óptimo y libre de desbordamientos.

### 📊 Log de Limpieza y Conciliación de Datos
* **Total de Registros Iniciales (Sucios):** 5,848,703 filas.
* **Total de Registros Finales (Limpios):** 3,839,852 filas.
* **Total de Registros Eliminados Netos:** 2,008,851 filas (34% de la base bruta).

### 🔍 Desglose de Incidencias Detectadas
Durante la auditoría se identificaron las siguientes fallas lógicas (no excluyentes entre sí):
* ❌ **Gobernanza Espacial (Estaciones Nulas):** 1,970,294 filas removidas por falta de nombre de estación de inicio o término.
* ⏱️ **Falsos Inicios (Viajes < 1 min o inconsistentes):** 161,352 filas eliminadas para limpiar errores de sistema o desanclajes accidentales.
* 🚲 **Descuidos de Anclaje / Outliers (> 24 hrs):** 5,843 filas descartadas correspondientes a bicicletas perdidas o robos.

> *Nota Metodológica:* La suma de incidencias individuales ($2,137,489$) supera al total neto eliminado debido a que 128,638 registros presentaron múltiples fallas de manera simultánea en la base original.

---

## 📈 3. Análisis Exploratorio e Insights (ANALYZE)
El dataset consolidado final revela una distribución de **64.57% Miembros Anuales** y **35.43% Usuarios Casuales**, mostrando tres patrones críticos de comportamiento:

1. **Rutina vs. Ocio (El Factor Propósito):** Los miembros mantienen un patrón estable de lunes a viernes con viajes rápidos (**12.59 minutos promedio**), lo que indica uso para traslados laborales. Los casuales explotan los **fines de semana** con trayectos extensos (**22.15 minutos promedio**), orientados netamente a la recreación.
2. **La Ventana Climática (Estacionalidad):** El segmento casual es sumamente meteorológico. Su demanda se concentra fuertemente entre **Mayo y Octubre (Verano)**, incrementando también la duración promedio de sus paseos (alcanzando 24.37 minutos en Julio).
3. **Hiper-concentración Geográfica:** El tráfico de usuarios casuales no está disperso; se agrupa masivamente en puntos turísticos y costeros, liderados por la estación **Streeter Dr & Grand Ave (Navy Pier)** y **DuSable Lake Shore Dr & Monroe St**.

---

## 📊 4. Visualización Interactiva (SHARE)
El cuadro de mando en Tableau está diseñado para ser completamente interactivo y dinámico. Para asegurar la veracidad de los promedios globales al aplicar filtros dinámicos por mes o estación, se implementó el cálculo de **Duración Promedio Ponderada Real** mediante campos calculados a medida (`SUM(Promedio * Total) / SUM(Total)`), evitando distorsiones por agregación simple.

> 🔗 **[Ver Dashboard Interactivo en Tableau Public](https://public.tableau.com/views/CyclisticCaseAnalysis/Dashboard2?:language=es-ES&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**

---

## 🎯 5. Recomendaciones Estratégicas de Negocio (ACT)
Basado en los hallazgos analíticos, se proponen tres planes de acción para la Dirección de Marketing:

* **Activación Física con Códigos QR en Hotspots:** Implementar campañas de conversión digital directa en los tótems de anclaje de *Navy Pier* y *DuSable Lake Shore*. Aprovechar que el usuario casual ya está físicamente utilizando el servicio para "engancharlo" con ofertas de registro rápidas e incentivos en tiempo real.
* **Estrategia "Weekend Warrior" y Monitoreo de Flota:** Crear una membresía específica para fines de semana enfocada en viajes largos. En paralelo, coordinar con Operaciones para **reforzar preventivamente el stock de bicicletas** en las estaciones costeras los días Sábado y Domingo para evitar quiebres de servicio.
* **Pase Estacional de Verano (Summer Pass):** Ofrecer un plan de suscripción flexible limitado a la época de calor (Mayo - Octubre). Exigir un contrato de 12 meses genera fricción innecesaria en el público de ocio; un pase estacional formaliza su flujo de caja cuando la demanda es más alta.

---

## 📂 Contenido del Repositorio
* `notebooks/`: Cuaderno de Google Colab con el desarrollo del pipeline ETL en Python y DuckDB.
* `reports/`: Documentación formal del reporte ejecutivo y la presentación final para la gerencia.
