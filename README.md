### Evaluación 4 · Inteligencia Artificial · Ingeniería Civil en Informática
**Universidad del Bío-Bío — Sede Concepción**

---

## Integrantes

| Leandro Flores | leandro.flores2201@alumnos.ubiobio.cl |
| Pablo Águila | pablo.aguila1901@alumnos.ubiobio.cl |
| Pablo Saavedra | pablo.saavedra2201@alumnos.ubiobio.cl |

---

## Descripción del proyecto

Este repositorio contiene el desarrollo de la **Evaluación 4** de la asignatura de Inteligencia Artificial, perteneciente a la carrera de Ingeniería Civil en Informática de la Universidad del Bío-Bío, sede Concepción.

El propósito del proyecto es diseñar, construir y evaluar **dos modelos de segmentación de clientes independientes** basados en algoritmos de clustering (K-Means) desde perspectivas de comportamiento y analítica de negocio diferentes para una empresa de comercio electrónico. En lugar de generar un único modelo generalizado que oculte patrones relevantes, la solución aborda el comportamiento de los clientes desde múltiples dimensiones independientes:
1. **Dimensión de Valor Económico y Lealtad (Perspectiva Financiera)**
2. **Dimensión de Comportamiento y Adopción Digital (Perspectiva de Engagement)**

---

## Estructura del repositorio

```
 620454/
│
├── README.md                        # Identificación del equipo y descripción del repositorio
│
├── data/
│   ├── ingestion/                   # Datos crudos originales
│   │   └── data_clientes.csv        # Dataset principal de clientes de e-commerce
│   └── cleaned/                     # Datos limpios generados en el notebook
│       └── data_clientes_clean.csv  # Dataset preprocesado
└── notebooks/
└── Proyecto_Inteligencia_Artificial,_leandro_F,Pablo_S,Pablo_Á.ipynb   # Notebook principal de la evaluación 4
```

> El notebook solicita o carga el dataset directamente bajo el nombre de `data_clientes.csv`.

---

## Dataset

El conjunto de datos disponible (`data_clientes.csv`) recopila información sobre hábitos de compra, características generales y comportamiento digital de los usuarios mediante las siguientes variables:

**Identificador**
- `cliente_id` — Identificador único del cliente.

**Variables numéricas de comportamiento transaccional y financiero**
- `ingreso_mensual` — Ingreso mensual estimado del cliente].
- `gasto_promedio_mensual` — Gasto promedio mensual en la plataforma.
- `frecuencia_compra` — Número de compras realizadas en un período determinado.
- `valor_promedio_compra` — Monto promedio de cada compra.
- `porcentaje_descuentos` — Porcentaje promedio de descuento utilizado.
- `antiguedad_cliente` — Tiempo que lleva siendo cliente.
- `productos_categoria` — Número de categorías de productos compradas.
- `tasa_recompra` — Proporción de compras repetidas.

**Variables numéricas de comportamiento digital**
- `visitas_web_mensuales` — Cantidad de visitas al sitio web.
- `tiempo_promedio_sesion` — Tiempo promedio de permanencia en el sitio.
- `dispositivos_registrados` — Cantidad de dispositivos asociados a la cuenta.
- `compras_movil_pct` — Porcentaje de compras realizadas desde dispositivos móviles.
- `interacciones_app` — Número de interacciones realizadas en la aplicación móvil.

**Variables numéricas de logística y demografía**
- `edad` — Edad del cliente.
- `distancia_envio_km` — Distancia promedio de envío.
- `gasto_envio_promedio` — Costo promedio de envío.

---

## Metodología

### Parte 1 — Diseño de las segmentaciones
- **Enfoque Financiero (Modelo 1):** Selección de variables orientadas al músculo económico y lealtad (`gasto_promedio_mensual`, `antiguedad_cliente`, `tasa_recompra`), justificando analíticamente su inclusión y la exclusión de métricas no relacionadas.
- **Enfoque de Engagement Digital (Modelo 2):** Selección de variables enfocadas puramente en el canal y uso tecnológico (`interacciones_app`, `tiempo_promedio_sesion`, `compras_movil_pct`), abstrayendo el valor monetario para perfilar la experiencia de usuario.

### Parte 2 — Preparación de datos
- Estandarización de nombres de columnas y eliminación de espacios en blanco.
- Detección y corrección de valores inconsistentes/negativos transformándolos mediante valores absolutos (`.abs()`).
- Imputación de nulos y verificación de registros duplicados.
- Tratamiento de valores atípicos mediante el método de **Winsorización** (transformador personalizado `Winsorizer` a percentiles extremos).
- Análisis de escala y aplicación de `StandardScaler` de manera secuencial a cada conjunto seleccionado.

### Parte 3 — Construcción de modelos
- Implementación de algoritmos de clustering utilizando `KMeans`.
- Determinación del número óptimo de clusters ($K$) de forma matemática mediante el método del codo (`KneeLocator` de la librería `kneed`).
- Validación y contraste del número de agrupaciones mediante la métrica de **Silhouette score**.

### Parte 4 — Interpretación y Negocio
- Reconstrucción de los centroides finales pasándolos a su escala original mediante `inverse_transform`.
- Visualización interactiva y gráficos analíticos tridimensionales (3D) de las agrupaciones resultantes.
- Asignación de nombres descriptivos a cada clúster y comparación cruzada de clientes entre ambos enfoques.
- Discusión de decisiones estratégicas de negocio asociadas a cada segmentación obtenida.

---

## Requisitos de software

El proyecto utiliza **Python 3.12** y requiere la instalación de la biblioteca `kneed` además de los paquetes de analítica tradicionales[cite: 4]:
