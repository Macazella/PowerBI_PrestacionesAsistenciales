📊 Power BI – Dashboard de Análisis de Prestaciones Asistenciales
Este repositorio contiene un informe interactivo desarrollado en Power BI, orientado al análisis de prestaciones de servicios de salud brindadas en diferentes establecimientos a nivel nacional. Su objetivo es facilitar la toma de decisiones mediante visualizaciones dinámicas y métricas clave de cobertura y distribución.

📁 Estructura del Repositorio
Copiar
Editar
📦prestaciones-asistenciales-dashboard
 ┣ 📂images
 ┃ ┣ dashboard_visual.png
 ┃ ┣ data_model.png
 ┣ 📂pbix
 ┃ ┗ dashboard_prestaciones.pbix
 ┣ README.md
 ┗ informe_ejecutivo.md
🧩 Descripción General del Dashboard
Visualización de la distribución de prestaciones por tipo y subcategoría asistencial.

Indicador de cobertura nacional sobre el total de establecimientos analizados.

Análisis comparativo por provincia y por institución.

Filtros interactivos por ubicación geográfica, tipo de financiamiento, categoría de prestación y densidad poblacional.

Herramienta adaptable para informes ejecutivos o análisis operativo.

📐 Modelo de Datos
El modelo está basado en un enfoque de estrella, donde la tabla central de hechos (tabla_unificada_de_prestaciones) contiene registros de prestaciones asistenciales y se relaciona con múltiples tablas de dimensión:

Tabla de Establecimientos

Tabla de Categorías de Prestación

Tabla de Ubicaciones (Provincias/Departamentos)

Tablas auxiliares por tipo de servicio (ambulatorio, guardia, imágenes, etc.)

Las relaciones son de tipo uno a muchos, con filtrado unidireccional desde dimensiones hacia la tabla de hechos. Se utilizó normalización para:

Estandarizar nombres de establecimientos

Uniformar códigos de ubicación

Unificar criterios de categorización de prestaciones

🧮 Medidas DAX Destacadas
Conteo total de prestaciones
dax
Copiar
Editar
Total Prestaciones = COUNT(tabla_unificada_de_prestaciones[ID_PRESTACION])
Conteo de prestaciones en red de análisis
dax
Copiar
Editar
Prestaciones en Red = CALCULATE(
    [Total Prestaciones],
    ESTABLECIMIENTOS[EN_RED] = "SI"
)
Porcentaje de cobertura nacional
dax
Copiar
Editar
% Cobertura Nacional = 
DIVIDE(
    DISTINCTCOUNT(FILTER(ESTABLECIMIENTOS, ESTABLECIMIENTOS[EN_RED] = "SI")[ID_ESTAB]),
    DISTINCTCOUNT(ESTABLECIMIENTOS[ID_ESTAB]),
    0
)
⚙️ Transformaciones Power Query
Se aplicaron transformaciones avanzadas en el editor de Power Query para:

Unificar múltiples orígenes en una única tabla de hechos con estructura estandarizada.

Limpiar y depurar registros nulos o inconsistentes.

Crear claves relacionales mediante combinación y codificación de campos.

Generar columnas derivadas para el análisis por categoría, subcategoría, y región.

Además, se incorporó una tabla auxiliar de control (tabla_filtros_genericos) para facilitar el filtrado cruzado en los reportes.

📊 Visualizaciones Principales
Visualización	Tipo	Descripción
Distribución por Tipo de Servicio	Gráfico de rosquilla	Participación de cada tipo de prestación en el total
Mapa Jerárquico de Subcategorías	Treemap	Relación entre tipo y subcategoría asistencial
Indicador de Cobertura Nacional	Tarjeta numérica	% de establecimientos en red vs total nacional
Ranking por Establecimiento	Gráfico de barras	Volumen de prestaciones por institución
Tabla dinámica por provincia	Tabla con totales	Detalle por tipo de servicio y región

🧭 Segmentadores y Filtros
El dashboard incluye segmentadores para análisis interactivo:

Provincia

Tipo de establecimiento

Participación en red

Financiamiento

Densidad poblacional

Categoría de prestación

💡 Recomendaciones de Uso
Este informe puede adaptarse a distintos contextos sanitarios, tanto públicos como privados.

Las métricas se pueden recalibrar para indicadores como eficiencia, tiempos de atención o derivaciones.

Recomendado para equipos de gestión, planificación sanitaria o unidades de monitoreo operativo.

🛠️ Requisitos Técnicos
Power BI Desktop v2024 o superior

Origen de datos en formato Excel o CSV estructurado

Campos obligatorios: ID Establecimiento, Tipo de prestación, Fecha, Ubicación

📬 Contacto
Para consultas técnicas o colaboración en proyectos similares, podés abrir un issue o contactarme por LinkedIn/GitHub.
