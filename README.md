# 📊 Power BI – Dashboard de Análisis de Prestaciones Asistenciales

Este repositorio contiene un informe interactivo desarrollado en Power BI, orientado al análisis de prestaciones de servicios de salud brindadas en diferentes establecimientos a nivel nacional.  
Su objetivo es facilitar la toma de decisiones mediante visualizaciones dinámicas y métricas clave de cobertura y distribución.

---

## 📁 Estructura del Repositorio

```

📂 PowerBI\_PrestacionesAsistenciales
├── 📁 images
├── 📊 dashboard\_visual.png
├── 📈 data\_model.png
├── 📁 pbix
│   └── 📄 dashboard\_prestaciones.pbix
├── 📄 README.md
├── 📄 LICENSE
└── 📄 informe\_ejecutivo.md

````

---

## 📝 Descripción General del Dashboard

- Visualización de la distribución de prestaciones por tipo y subcategoría asistencial.
- Indicador de cobertura nacional sobre el total de establecimientos analizados.
- Análisis comparativo por provincia y por institución.
- Filtros interactivos por ubicación geográfica, tipo de financiamiento, categoría de prestación y densidad poblacional.
- Herramienta adaptable para informes ejecutivos o análisis operativo.

---

## 🧠 Modelo de Datos

El modelo está basado en un enfoque de estrella, donde la tabla central de hechos (`tabla_unificada_de_prestaciones`) contiene registros de prestaciones asistenciales y se relaciona con múltiples tablas de dimensión:

- **Tabla de Establecimientos**
- **Tabla de Categorías de Prestación**
- **Tabla de Ubicaciones (Provincias/Departamentos)**
- **Tablas auxiliares por tipo de servicio** (ambulatorio, guardia, imágenes, etc.)

> ⚠️ Las relaciones son de tipo uno a muchos, con filtrado unidireccional desde las dimensiones hacia la tabla de hechos.

### 🔧 Transformaciones en Power Query

- Fusión de orígenes múltiples en una tabla unificada.
- Transformación de campos para compatibilidad relacional.
- Eliminación de valores nulos y duplicados.
- Creación de columnas derivadas para facilitar el análisis agregado.

> Se generó una estructura final robusta, lista para análisis dinámico y con mínima redundancia.

### 📐 Normalización aplicada

- Estandarización de nombres de establecimientos y ubicaciones.
- Unificación de códigos de categorización asistencial.
- Depuración de registros duplicados o incompletos.

---

## 🧮 Principales Medidas DAX

### **Total de Prestaciones**
```dax
Total Prestaciones =
COUNT(tabla_unificada_de_prestaciones[ID_PRESTACION])
````

### **Prestaciones en Red de Análisis**

```dax
Prestaciones en Red =
CALCULATE(
    [Total Prestaciones],
    ESTABLECIMIENTOS[EN_RED] = "SI"
)
```

### **Porcentaje de Cobertura Nacional**

```dax
% Cobertura Nacional =
DIVIDE(
    DISTINCTCOUNT(FILTER(ESTABLECIMIENTOS, ESTABLECIMIENTOS[EN_RED] = "SI")[ID_ESTAB]),
    DISTINCTCOUNT(ESTABLECIMIENTOS[ID_ESTAB]),
    0
)
```

---

## 📊 Visualizaciones Incluidas

| Visualización                     | Tipo                | Descripción                                               |
| --------------------------------- | ------------------- | --------------------------------------------------------- |
| Distribución por Tipo de Servicio | Donut Chart         | Muestra la participación de cada tipo en el total         |
| Mapa Jerárquico por Subcategoría  | Treemap             | Relación entre categoría y subcategoría de prestación     |
| Indicador de Cobertura Nacional   | Tarjeta             | Porcentaje de establecimientos dentro de la red analizada |
| Ranking por Establecimiento       | Barras Horizontales | Ranking de volumen de prestaciones por institución        |
| Tabla Dinámica por Provincia      | Tabla con totales   | Detalle de prestaciones por provincia y tipo de servicio  |

---

## 🎛 Segmentadores de Filtro

Este informe incluye filtros para análisis personalizado:

* Provincia
* Tipo de establecimiento
* Cobertura en Red
* Financiamiento
* Densidad poblacional
* Categoría de prestación

Los filtros pueden utilizarse en conjunto o de forma independiente para aplicar segmentaciones cruzadas en los visuales.
Esto permite, por ejemplo:

* Comparar tipos de prestación en una sola provincia o región.
* Evaluar diferencias entre instituciones públicas y privadas.
* Analizar cobertura de la red sobre zonas con distinta densidad poblacional.
* Detectar brechas de servicio según combinación de filtros.

---

## 🧾 Informe Ejecutivo

Este dashboard ha sido diseñado para acompañar decisiones estratégicas mediante visualizaciones claras y segmentación interactiva.
Entre los análisis posibles:

* Identificación de prestadores con mayor volumen de actividad.
* Evaluación de desequilibrios territoriales o institucionales.
* Diagnóstico de brechas según tipo de prestación, densidad y modelo de atención.

Cada visual responde a un propósito operativo y estratégico, adaptándose al uso de filtros contextuales en tiempo real para análisis enfocados.

---

## 📌 Recomendaciones

Este informe puede adaptarse a:

* Paneles de control ejecutivos.
* Análisis geoespacial de cobertura.
* Evaluación de convenios y redistribución de recursos.
* Detección de desviaciones operativas en servicios de salud.

---

## 📄 Licencia

Este repositorio se publica bajo la licencia MIT.
Ver archivo [LICENSE](./LICENSE) para más detalles.

---
