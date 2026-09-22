# 📊 Proyecto Final de Máster: Análisis Operativo, Inteligencia de Negocio y Dashboard de E-Commerce

## 1. Introducción y Objetivos
Este repositorio contiene el trabajo realizado para mi Proyecto Final de Máster en Data Analytics. El objetivo principal del proyecto ha sido transformar un conjunto de datos transaccionales brutos de un negocio de e-commerce en un cuadro de mando ejecutivo interactivo y funcional.

A través de este análisis, se han abordado tres metas estratégicas:
1. **Evaluar la salud financiera del negocio**: Analizando la facturación total y el volumen de transacciones.
2. **Diagnosticar la eficiencia logística**: Midiendo los tiempos reales de entrega y detectando retrasos por zona geográfica.
3. **Comprender el comportamiento del consumidor**: Identificando patrones temporales de compra (meses, días de la semana y horas punta).

---

## 2. Flujo de Trabajo Detallado (Paso a Paso)

### Paso 1: Entorno de Trabajo y Procesamiento de Datos en Visual Studio Code (Python)
El proyecto comenzó descargando el archivo de datos transaccionales (`dataset_ecommerce.csv`). Para garantizar un procesamiento eficiente y reproducible, utilicé **Visual Studio Code** y el stack analítico de **Python (Pandas y NumPy)**.

* **Auditoría e Ingesta de Datos**: Se importó el conjunto de datos para inspeccionar tipos de variables, nulos y duplicados.
* **Filtrado Operativo**: Para no sesgar los cálculos de tiempos logísticos con compras canceladas o en tránsito, filtré la base de datos manteniendo únicamente los pedidos con estado completado (`order_status == 'delivered'`).
* **Ingeniería de Características (*Feature Engineering*)**:
  * `dias_entrega_real`: Calculé la latencia de envío mediante la diferencia entre la fecha de recepción del cliente (`order_delivered_customer_date`) y la fecha de compra (`order_purchase_timestamp`).
  * `retrasado`: Creé un indicador binario (1 / 0) que identifica si la entrega superó la fecha límite estimada por la plataforma.
  * **Dimensiones Temporales**: Extraje variables derivadas como el mes (`mes_compra`), el año (`ano_compra`), el día de la semana (`dia_semana_compra`) y la franja horaria (`hora_compra`).
* **Exportación**: Generé una tabla depurada y optimizada para su posterior carga en Power BI.

---

### Paso 2: Modelado de Datos y Medidas Calculadas en Power BI (DAX)
Tras importar el archivo limpio en **Power BI Desktop**, configuré las métricas clave del proyecto mediante código **DAX (Data Analysis Expressions)** para asegurar un rendimiento óptimo del informe:

* **Facturación Total (€)**:
  ```dax
  Facturación Total = SUM(ecommerce_data[valor_total_item])
  ```
* **Total Pedidos Únicos**:
  ```dax
  Total Pedidos = DISTINCTCOUNT(ecommerce_data[order_id])
  ```
* **Plazo Medio de Entrega (Días)**:
  ```dax
  Plazo Medio Entrega = AVERAGE(ecommerce_data[dias_entrega_real])
  ```
* **Tasa de Retraso (%)**:
  ```dax
  Tasa de Retraso = DIVIDE(SUM(ecommerce_data[retrasado]), COUNT(ecommerce_data[order_id]), 0)
  ```

---

### Paso 3: Diseño del Dashboard Ejecutivo
Diseñé el cuadro de mandos primando la claridad analítica, la combinación cromática coherente y la ergonomía visual en una vista única (*Lienzo Ejecutivo*):

1. **Tarjetas KPI Superiores**: Banda superior con los 4 indicadores clave del negocio (Facturación Total, Pedidos Totales, Plazo Medio de Entrega y Tasa de Retraso).
2. **Evolución Mensual de Ventas (Gráfico de Líneas)**: Muestra la trayectoria temporal de las ventas para analizar la estacionalidad del e-commerce.
3. **Distribución por Año (Gráfico de Rosca)**: Visualiza la cuota de mercado anual del negocio (2016, 2017 y 2018).
4. **Distribución Geográfica (Mapa Interactivo)**: Permite explorar espacialmente la ubicación y concentración de las ventas.
5. **Top 10 Estados por Facturación (Barras Horizontales)**: Clasificación de las regiones que generan mayores ingresos.
6. **Top 10 Estados con Envíos más Lentos (Columnas Verticales)**: Gráfico enfocado en la gestión operativa que resalta los estados con peores tiempos de entrega.
7. **Ventas por Día de la Semana (Columnas Verticales)**: Análisis de los hábitos de compra según el día de la semana.

---

## 3. Principales Conclusiones e Insights de Negocio

* **Concentración Geográfica de Ingresos**: Más del 60% de la facturación global se concentra en solo tres estados (São Paulo - SP, Rio de Janeiro - RJ y Minas Gerais - MG). Esto demuestra una gran fortaleza en la región central, pero advierte sobre una alta dependencia territorial.
* **Cuello de Botella Logístico**: Existe una brecha importante en los tiempos de envío. Mientras que en la zona metropolitana central los pedidos tardan entre 8 y 10 días, en los estados del Norte y Nordeste (como Roraima - RR o Amapá - AP) los plazos superan los 25-28 días.
* **Patrón de Compras**: Las ventas alcanzan su punto máximo entre los **lunes y los miércoles**, experimentando una caída notable durante el fin de semana.

---

## 4. Recomendaciones Estratégicas

1. **Optimización de Campañas MKT**: Programar el lanzamiento de ofertas, notificaciones push y campañas de email marketing entre el domingo por la tarde y el martes por la mañana para aprovechar la mayor disposición de compra del usuario.
2. **Reducción de Latencia en Zonas Periféricas**: Evaluar acuerdos con operadores logísticos locales o establecer centros de distribución intermedios en el Norte/Nordeste para recortar los tiempos de entrega por debajo de los 15 días.
3. **Fidelización en Regiones Core**: Negociar tarifas preferenciales de envío por volumen en las regiones SP, RJ y MG para mejorar el margen neto por transacción.

---

## 🛠️ Tecnologías Utilizadas
* **Entorno de Desarrollo**: Visual Studio Code
* **Lenguaje y Librerías**: Python 3.x (Pandas, NumPy)
* **Business Intelligence**: Power BI Desktop (Lenguaje DAX)
* **Control de Versiones y Documentación**: GitHub (Readme)
