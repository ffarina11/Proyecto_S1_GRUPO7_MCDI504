# Proyecto Grupo 7 — MCDI504
### *Certificación de lotes de flor cortada mediante un clasificador con opción de rechazo*

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Jupyter-Lab-orange?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter">
  <img src="https://img.shields.io/badge/Curso-MCDI504-green?style=for-the-badge" alt="MCDI504">
</p>

---

## Descripción

Este repositorio contiene el avance de la **Fase 1** del proyecto ABP del curso **MCDI504 — Machine Learning I** del **Magíster en Ciencias de Datos e Inteligencia Artificial** de la *Universidad Andrés Bello (UNAB)*.

El objetivo principal es determinar si las variables morfométricas del **Dataset Iris**  permiten implementar un certificador con opción de rechazo que etiquete automáticamente los lotes separables y derive a revisión humana la zona de solapamiento entre *Versicolor* y *Virginica*, minimizando el costo esperado de error.

> **Esta fase no incluye entrenamiento de modelos.** Su propósito es delimitar la situación de análisis, examinar el estado real de los datos y justificar con evidencia el tipo de aprendizaje seleccionado.

---

## Integrantes — Grupo 7

| Nombre | Rol | GitHub / Contacto |
| :--- | :---: | :---: |
| **Juan de Dios Díaz Ríos** | Integrante | [@juandiazr513](https://github.com/juandiazr513) |
| **Francisco Fariña Molina** | Integrante | [@ffarina11](https://github.com/ffarina11)|
| **Constanza Moreno Giacometto** | Integrante | [@ConstanzaM0](https://github.com/ConstanzaM0) |
| **Yenne Sepúlveda Jerez** | Integrante | [@yennesepulveda](https://github.com/yennesepulveda) |

- **Docente:** David Ruete Zúñiga

---

## Estructura del Repositorio

```text
MCDI504_S1_1_GRUPO7/
│
├── data/
│   └── iris.csv                      # Dataset fuente (150 registros, 4 variables + Species)
│
├── docs/
│   └── MCDI504_S1_1_GRUPO7.pdf       # Informe de la Fase 1
│
├── notebooks/
│   └── F1_Definicion.ipynb           # Notebook principal de la fase
│
├── figures/
│   ├── proceso_kdd.png               # Diagrama de etapas del proceso KDD
│   ├── boxplot_entradas.png          # Distribución de las cuatro variables de entrada
│   ├── dispersion_petalo.png         # Dispersión de pétalo por especie
│   ├── correlacion_pearson.png       # Mapa de calor de correlaciones de Pearson
│   └── pvalores_pearson.png          # Mapa de calor de p-valores
│
├── outputs/
│   ├── resumen_estadistico.csv       # Estadística descriptiva global
│   ├── descriptivo_por_especie.csv   # Media y DE por especie
│   ├── solapamiento_par.csv          # Solapamiento Versicolor / Virginica por variable
│   ├── matriz_correlacion.csv        # Matriz de correlación de Pearson
│   ├── matriz_pvalores.csv           # Matriz de p-valores asociados
│   └── base_normalizada.csv          # bbdd_norm_completa (MinMaxScaler + Species)
│
└── README.md
```

---

## Cómo Reproducir el Entorno

Sigue estos pasos en tu terminal para clonar el repositorio e instalar todas las dependencias necesarias:

### 1. Clonar el repositorio
```bash
git clone https://github.com/ffarina11/Proyecto_S1_GRUPO7_MCDI504
cd Proyecto_S1_GRUPO7_MCDI504
```

### 2. Configurar el entorno virtual
```bash
# Crear entorno virtual
python -m venv .venv

# Activar entorno virtual
# En Windows (Git Bash):
source .venv/Scripts/activate

# En macOS/Linux:
source .venv/bin/activate
```

### 3. Instalar dependencias e iniciar
```bash
# Instalar librerías
pip install pandas numpy matplotlib seaborn scikit-learn scipy

# Abrir el entorno de Jupyter
jupyter lab
```

---

## Fase 1 — Definición y Orientación de la Situación

La Fase 1 implementa un flujo exploratorio reproducible en correspondencia con las tres primeras etapas del proceso KDD: selección, preprocesamiento y transformación.

### 1. Ejecución del notebook

Con el entorno virtual activo, desde la raíz del repositorio:

```bash
jupyter lab
```

Luego abrir:

```bash
notebooks/F1_Definicion.ipynb
```

> Ejecutar con **Kernel → Restart & Run All** para garantizar la reproducibilidad completa.

### 2. Estructura del notebook

| Sección | Propósito | Etapa KDD |
| :--- | :--- | :---: |
| 1. Definición del problema | Contexto, pregunta analítica y objetivos | — |
| 2. Preparación del entorno | Instalaciones e importaciones reproducibles | — |
| 3. Selección de datos | Carga de `iris.csv` y verificación de integridad contra `load_iris()` | Selección |
| 4. Preprocesamiento | Tipos de dato, faltantes, duplicados y balance de clases | Preprocesamiento |
| 5. Estadística descriptiva | Resumen global y desagregado por especie | Preprocesamiento |
| 6. Visualización inicial | Boxplot de las cuatro variables de entrada | Preprocesamiento |
| 7. Localización de la incertidumbre | Margen Setosa y solapamiento Versicolor / Virginica | Preprocesamiento |
| 8. Codificación y correlación | `bbdd2`, matriz de Pearson y p-valores | Transformación |
| 9. Normalización | `bbdd_norm_completa` mediante `MinMaxScaler` | Transformación |
| 10. Correspondencia con KDD | Síntesis de etapas y proyección a la Fase 2 | — |
| 11. Exportación | Generación automática de archivos en `figures/` y `outputs/` | — |
| 12. Síntesis | Hallazgos y proyección | — |

### 3. Organización de salidas

Los archivos generados por el notebook se exportan automáticamente a sus carpetas correspondientes:

```text
figures/                             # Visualizaciones generadas
├── proceso_kdd.png
├── boxplot_entradas.png
├── dispersion_petalo.png
├── correlacion_pearson.png
└── pvalores_pearson.png

outputs/                             # Tablas y datos procesados
├── resumen_estadistico.csv
├── descriptivo_por_especie.csv
├── solapamiento_par.csv
├── matriz_correlacion.csv
├── matriz_pvalores.csv
└── base_normalizada.csv
```

### 4. Principales hallazgos

- **150 registros completos**, clases balanceadas (50 por especie), un duplicado conservado por variabilidad biológica legítima.
- **Setosa** queda separada por un margen de **1,1 cm** en `Petal.Length` sin ningún caso intermedio → clasificable sin ambigüedad.
- **Versicolor / Virginica** se solapan en el **15,4 %** del rango conjunto en `Petal.Length` y **26,7 %** en `Petal.Width` → incertidumbre localizada y abordable con abstención.
- `Petal.Length` y `Petal.Width` presentan correlación de **0,963** entre sí y superan **0,94** en asociación con `Species` codificada → posible redundancia a resolver en la Fase 2.
- Única pareja sin evidencia de asociación lineal: `Sepal.Length` × `Sepal.Width` (p-valor = 0,152).

---

## Tipo de Aprendizaje Seleccionado

**Aprendizaje supervisado de clasificación con opción de rechazo.**

| Criterio | Evidencia |
| :--- | :--- |
| Variable objetivo disponible | `Species` verificada en los 150 registros |
| Variable objetivo categórica | Tres clases nominales sin orden natural → clasificación, no regresión |
| Incertidumbre localizada | Solapamiento concentrado en el par Versicolor / Virginica |
| Estructura de costos | Costo de certificar mal > costo de revisión manual → justifica abstención |
| Espacio de salida | Cuatro resultados posibles: tres etiquetas + derivar a revisión |

---

## Información del Dataset

| Atributo | Detalle |
| :--- | :--- |
| **Nombre** | Iris Dataset |
| **Fuente** | Fisher, R. A. (1936) / UCI Machine Learning Repository |
| **URL Oficial** | [🔗 Acceder al Dataset](https://archive.ics.uci.edu/dataset/53/iris) |
| **Archivo incluido** | `data/iris.csv` |
| **Dimensiones** | 150 registros · 4 variables de entrada · 1 variable de decisión (3 clases) |
| **Balance** | 50 registros por especie (Setosa, Versicolor, Virginica) |


---
<p align="center"><sub>Magíster en Ciencias de Datos e Inteligencia Artificial • UNAB • 2026</sub></p>

