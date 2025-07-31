# 📊 Power BI – Dashboard de Análisis de Prestaciones Asistenciales

Este repositorio contiene un informe interactivo desarrollado en **Power BI**, orientado al análisis de prestaciones de servicios de salud brindadas en diferentes establecimientos a nivel nacional. Su objetivo es facilitar la toma de decisiones mediante visualizaciones dinámicas y métricas clave de cobertura y distribución.

---

## 📁 Estructura del Repositorio

📦PowerBI_PrestacionesAsistenciales
┣ 📂images
┃ ┣ dashboard_visual.png
┃ ┣ data_model.png
┣ 📂pbix
┃ ┗ dashboard_prestaciones.pbix
┣ README.md
┣ LICENSE
┗ informe_ejecutivo.md

yaml
Copiar
Editar

---

## 📌 Descripción General del Dashboard

- Visualización de la distribución de prestaciones por tipo y subcategoría asistencial.
- Indicador de cobertura nacional sobre el total de establecimientos analizados.
- Análisis comparativo por provincia y por institución.
- Filtros interactivos por ubicación geográfica, tipo de financiamiento, categoría de prestación y densidad poblacional.
- Herramienta adaptable para informes ejecutivos o análisis operativo.

---

## 🧩 Modelo de Datos

El modelo está basado en un enfoque de **estrella**, donde la tabla central de hechos (`tabla_unificada_de_prestaciones`) contiene registros de prestaciones asistenciales y se relaciona con múltiples tablas de dimensión:

- **Tabla de Establecimientos**
- **Tabla de Categorías de Prestación**
- **Tabla de Ubicaciones** (Provincias/Departamentos)
- **Tablas auxiliares** por tipo de servicio (ambulatorio, guardia, imágenes, etc.)

> ⚙️ Las relaciones son de tipo **uno a muchos**, con filtrado unidireccional desde las dimensiones hacia la tabla de hechos.

Se aplicó **normalización de datos** para garantizar consistencia:

- Estandarización de nombres de establecimientos y ubicaciones.
- Unificación de códigos de categorización asistencial.
- Depuración de registros duplicados o incompletos.

---

## 🧮 Principales Medidas DAX

### Total de Prestaciones
```dax
Total Prestaciones =
COUNT(tabla_unificada_de_prestaciones[ID_PRESTACION])
Prestaciones en Red de Análisis
dax
Copiar
Editar
Prestaciones en Red =
CALCULATE(
    [Total Prestaciones],
    ESTABLECIMIENTOS[EN_RED] = "SI"
)
Porcentaje de Cobertura Nacional
dax
Copiar
Editar
% Cobertura Nacional =
DIVIDE(
    DISTINCTCOUNT(FILTER(ESTABLECIMIENTOS, ESTABLECIMIENTOS[EN_RED] = "SI")[ID_ESTAB]),
    DISTINCTCOUNT(ESTABLECIMIENTOS[ID_ESTAB]),
    0
)
⚙️ Transformaciones en Power Query
El flujo de trabajo en Power Query incluyó:

Fusión de orígenes múltiples en una tabla unificada.

Transformación de campos para compatibilidad relacional.

Eliminación de valores nulos y duplicados.

Creación de columnas derivadas para facilitar el análisis agregado.

Se generó una estructura final robusta, lista para análisis dinámico y con mínima redundancia.

📊 Visualizaciones Incluidas
Visualización	Tipo	Descripción
Distribución por Tipo de Servicio	Gráfico de rosquilla	Muestra la participación de cada tipo en el total
Mapa Jerárquico por Subcategoría	Treemap	Relación entre categoría y subcategoría de prestación
Indicador de Cobertura Nacional	Tarjeta	Porcentaje de instituciones dentro de la red analizada
Ranking por Establecimiento	Barras horizontales	Muestra volumen de prestaciones por institución
Tabla Dinámica por Provincia	Tabla con totales	Detalle de prestaciones por provincia y tipo de servicio

🎛️ Segmentadores de Filtro
El informe incluye filtros para análisis personalizado:

Provincia

Tipo de establecimiento

Cobertura en Red

Financiamiento

Densidad poblacional

Categoría de prestación

🧠 Recomendaciones
Este informe puede adaptarse a:

Sistemas de monitoreo sanitario.

Paneles de control regionales o institucionales.

Proyectos de análisis de demanda o planeamiento estratégico.

Análisis de brechas en cobertura asistencial.

📄 Licencia
Este proyecto está licenciado bajo los términos de la Licencia MIT. Ver el archivo LICENSE para más información.
