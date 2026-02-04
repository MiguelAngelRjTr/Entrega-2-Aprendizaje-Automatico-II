# Segmentación de clientes con Clustering (PCA + KMeans + GMM)

Este proyecto implementa un flujo completo de **análisis exploratorio (EDA)**, **preprocesado**, **reducción de dimensionalidad con PCA** y **modelos de clustering** para segmentar clientes a partir de variables de comportamiento financiero.

El objetivo principal es identificar grupos homogéneos de clientes utilizando técnicas no supervisadas, apoyándose en métricas cuantitativas y visualizaciones interpretables.

**Autor:** Miguel Angel Rojas Torres

---

## 📑 Índice

1. [Descripción del proyecto](#descripción-del-proyecto)  
2. [Estructura del repositorio](#estructura-del-repositorio)  
3. [Dataset](#dataset)  
4. [Metodología](#metodología)  
   - [EDA](#eda)  
   - [Preprocesado](#preprocesado)  
   - [Reducción de dimensionalidad (PCA)](#reducción-de-dimensionalidad-pca)  
   - [Clustering](#clustering)  
5. [Modelos implementados](#modelos-implementados)  
6. [Resultados principales](#resultados-principales)  
7. [Reproducibilidad](#reproducibilidad)  
8. [Ejecución del proyecto](#ejecución-del-proyecto)  
9. [Requisitos](#requisitos)  

---

## Descripción del proyecto

La segmentación de clientes es un problema clásico en analítica de negocio y marketing. En este trabajo se emplean algoritmos de clustering para descubrir patrones de comportamiento en clientes de tarjeta de crédito.

El pipeline incluye:

- Tratamiento de valores faltantes
- Identificación de ceros estructurales
- Transformación logarítmica para variables monetarias asimétricas
- Escalado de variables
- PCA para reducción dimensional
- Clustering con **KMeans** y modelo alternativo **Gaussian Mixture Model (GMM)**

---

## Estructura del repositorio

La organización del proyecto es la siguiente:

```
├── data/
│ └── CC_GENERAL.csv # Dataset original
│
├── figures/
│ ├── images/ # Imagenes importadas
│ └── eda.html # Reporte automático generado con ydata-profiling
│
├── notebooks/
│ └── Rojas_Torres_MiguelAngel_assignment2.ipynb # Notebook principal del proyecto
│
├── environment.yml # Entorno conda reproducible

```

---

## Dataset

El dataset utilizado (`CC_GENERAL.csv`) contiene información agregada del comportamiento de clientes con tarjeta de crédito, incluyendo:

- Balance medio
- Compras totales y frecuencia
- Avances de efectivo
- Pagos realizados
- Límite de crédito
- Antigüedad del cliente (tenure)

Este tipo de variables presentan distribuciones altamente asimétricas, por lo que requieren transformaciones robustas antes de aplicar clustering.

---

## Metodología

### EDA

En primer lugar se realiza un análisis exploratorio para:

- Examinar distribuciones y escalas
- Detectar asimetrías fuertes en variables monetarias
- Evaluar valores faltantes
- Identificar ceros estructurales relevantes

Se incluye un reporte automático generado con `ydata-profiling`:

- `figures/eda.html`

---

### Preprocesado

El preprocesado se implementa mediante `Pipeline` y `ColumnTransformer` de `scikit-learn`.

Incluye:

- Imputación con mediana (`SimpleImputer(strategy="median")`)
- Transformación logarítmica `log(1+x)` en variables monetarias
- Escalado con `StandardScaler`

Este enfoque permite garantizar consistencia y reproducibilidad dentro de un pipeline completo.

---

### Reducción de dimensionalidad (PCA)

Dado que el dataset contiene múltiples variables correlacionadas, se aplica PCA para:

- Reducir redundancia
- Mejorar eficiencia del clustering
- Facilitar visualización en 2D

Se selecciona un PCA reducido reteniendo el **95% de varianza explicada**, lo que reduce el espacio a aproximadamente 12 componentes.

---

### Clustering

Se exploran modelos no supervisados mediante:

- Método del codo (inercia)
- Silhouette score
- BIC (para GMM)

Además se incluyen visualizaciones:

- Proyección PCA 2D
- Proyección t-SNE
- Tamaño relativo de clusters
- Perfil medio de variables por segmento

---

## Modelos implementados

### KMeans

Modelo principal basado en particiones, evaluado para distintos valores de *k*.

Selección final basada en:

- Punto de inflexión en inercia
- Silhouette score
- Interpretabilidad de segmentos

---

### Gaussian Mixture Model (GMM)

Modelo alternativo basado en clustering probabilístico.

Evaluación mediante:

- Silhouette score
- Bayesian Information Criterion (BIC)

Se selecciona un modelo con **k = 3** componentes como alternativa compacta.

---

## Resultados principales

Los clusters obtenidos permiten distinguir perfiles diferenciados, por ejemplo:

- Clientes con alta actividad de compras
- Clientes de perfil moderado y uso controlado
- Clientes con bajo consumo y pagos mínimos

El análisis incluye:

- Distribución de tamaños de clusters
- Interpretación mediante medias por grupo
- Comparación entre KMeans y GMM

---

## Reproducibilidad

El proyecto incluye un entorno conda exportado, `environment.yml`. Para recrearlo:

```bash
conda env create -f environment.yml
conda activate ml-core
```

---

## Ejecución del proyecto

1. Clonar repositorio:

```bash
git clone https://github.com/MiguelAngelRjTr/Entrega-2-Aprendizaje-Automatico-II.git
```

2. Crear entorno:

```bash
conda env create -f environment.yml
conda activate ml-core
```

3. Ejecutar notebook principal

---

## Requisitos

El proyecto utiliza principalmente:

- Python ≥ 3.10
- numpy
- pandas
- scikit-learn
- matplotlib
- seaborn
- ydata-profiling
- joblib

Todas las dependencias del entorno están recogidas en `environment.yml`.