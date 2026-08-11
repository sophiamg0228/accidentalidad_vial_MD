# 🚦 Análisis de Accidentalidad Vial en Medellín (2018) — Clustering Geoespacial

## 📋 Descripción del Proyecto

Análisis solicitado por las autoridades locales de Medellín para apoyar la planeación de la atención y prevención de accidentes de tránsito, a partir de los datos oficiales de accidentalidad georreferenciada del año 2018. El objetivo fue identificar **dónde ubicar agentes de tránsito y ambulancias**, y **en qué horarios y fechas** se concentra la mayor accidentalidad, para dar recomendaciones de prevención basadas en datos.

## 👥 Integrantes

| Nombre | Rol |
|---|---|
| Manuela Giraldo | Desarrollo conjunto |
| Sophia Mateus | Desarrollo conjunto |

## 🗂️ Fuente de Datos

Base de datos pública de **accidentalidad georreferenciada de Medellín, año 2018** (43,306 registros, 15 columnas), con variables como clase de accidente, dirección, gravedad del incidente, comuna, barrio, diseño vial, fecha y hora.

## 🛠️ Metodología

1. **Limpieza inicial**: eliminación de columnas no relevantes y detección de "direcciones fantasma" (numeraciones inexistentes como '999') y coordenadas físicamente imposibles.
2. **Imputación de coordenadas faltantes**: estandarización del formato de las direcciones (expandiendo abreviaturas como CR, CL, TV) y geocodificación con la librería **Nominatim**, rescatando 138 de 520 registros sin coordenadas.
3. **Tratamiento de outliers geográficos**: acotamiento a los límites geográficos reales de Medellín y exclusión de registros fuera de la ciudad.
4. **Clustering geoespacial**: comparación de **K-Means** y **DBSCAN** para segmentar la ciudad en zonas operativas. Se seleccionó K-Means con **4 clusters**, alineados con los puntos cardinales de la ciudad, priorizando la interpretabilidad sobre una mejora marginal en el coeficiente de silueta que ofrecía un modelo de 5 clusters (principio de parsimonia).
5. **Enriquecimiento de variables**: creación de franjas horarias (madrugada, mañana, tarde, noche), día de la semana, fin de semana, y una variable binaria para identificar fechas de partidos del Atlético Nacional.
6. **Análisis por cluster**: mapas de calor, ubicación de accidentes con víctimas mortales, distribución por franja horaria, fecha, barrio, tipo de accidente y diseño vial.

## 📊 Hallazgos Clave

- La gravedad de los accidentes se distribuyó en **20,424 casos con heridos, 18,638 solo con daños y 197 con muertos**.
- Los 4 clusters geográficos (segmentados por zonas cardinales de la ciudad) presentan patrones diferenciados de horario, tipo de vía y gravedad de accidentes.
- **Días con partido del Atlético Nacional**: no se observó una tasa diaria de accidentes mayor a los días sin partido (de hecho fue ligeramente menor), pero sí se identificaron **franjas horarias específicas** con mayor concentración de accidentes en días de partido frente a días regulares.
- Se identificaron corredores viales críticos que requieren atención especial en horas pico por su diseño (vías estrechas, cruces complejos, tramos de alta velocidad).

## 💡 Recomendaciones de Prevención

- Reforzar la presencia de agentes de tránsito y controles de velocidad/alcoholemia en días de eventos especiales (partidos en el Atanasio Girardot, conciertos, festividades).
- Evaluar mejoras de señalización, instalación de cámaras o rediseño vial en los "hotspots" identificados durante horas pico.
- Implementar un horario estricto de cargue y descargue en zonas críticas como la Avenida Guayabal (entre calles 10 y 14 Sur).
- Instalar bandas sonoras y radares pedagógicos de velocidad en vías de diseño que permite alta velocidad (ej. Av. Las Palmas).
- Desarrollar una campaña de "puntos ciegos" enfocada en la interacción entre vehículos de carga pesada y motocicletas en intersecciones críticas (ej. Cra. 65 con Guayabal).
- Preposicionar ambulancias en los clusters de mayor accidentalidad durante horas pico, y reforzar controles nocturnos de fin de semana en zonas de alta vida nocturna.

## 🧰 Tecnologías Utilizadas

- **Python**: `pandas`, `numpy`
- **Geocodificación**: `geopy` (Nominatim)
- **Clustering**: `scikit-learn` (K-Means, DBSCAN, StandardScaler, Silhouette Score)
- **Visualización geoespacial**: `folium` (mapas de calor), `plotly express` (mapas interactivos y gráficos)
- **Visualización estadística**: `matplotlib`, `seaborn`

## 📎 Notas

Este proyecto usa datos públicos oficiales de accidentalidad de la ciudad de Medellín (año 2018), sin información personal identificable de las personas involucradas en los accidentes.
