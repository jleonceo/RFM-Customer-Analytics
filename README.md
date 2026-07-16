# Análisis RFM de clientes · E-commerce

Segmentación de clientes mediante análisis RFM (Recency, Frequency, Monetary) para
identificar patrones de comportamiento y orientar estrategias de retención.

> Datos **sintéticos**, generados para portfolio (`Script_Datos_Sinteticos.ipynb`). Las
> cifras de impacto y ROI son **ilustrativas del método, no resultados reales**.

[Español](#español) · [English](#english)

---

## Español

### Tabla de contenidos

- [Resumen ejecutivo](#resumen-ejecutivo)
- [Resultados](#resultados)
- [Metodología](#metodología)
- [Visualizaciones](#visualizaciones)
- [Recomendaciones](#recomendaciones)
- [Cómo reproducir](#cómo-reproducir)

---

### Resumen ejecutivo

Este proyecto analiza **946 clientes** y **7.741 transacciones** durante 12 meses usando
metodología RFM para segmentar y proponer acciones de negocio. Los importes son ilustrativos
sobre un dataset sintético.

### Hallazgos principales

- **246 Champions** (26%) generan $15.447 de media: el motor del negocio.
- **102 En riesgo** con $4.587 se están marchando: $468K en peligro.
- **59 Nuevos** con bajo engagement: oportunidad de fidelización.
- **342 Otros** (36%) generan solo $550: bajo ROI.

**Impacto potencial (ilustrativo)**: $2,3M adicionales con ROI de 35:1.

---

### Resultados

### Segmentación de clientes

| Segmento | Clientes | % | Valor promedio | Recency | Frequency |
|----------|----------|---|----------------|---------|-----------|
| Champions | 246 | 26% | $15.447 | 12 días | 16,8 |
| Leales | 197 | 21% | $6.212 | 33 días | 9,3 |
| En riesgo | 102 | 11% | $4.587 | 96 días | 8,1 |
| Nuevos | 59 | 6% | $528 | 13 días | 2,5 |
| Otros | 342 | 36% | $550 | 144 días | 2,3 |

### Validación del modelo

- R_Score frente a Recency: -0,83
- F_Score frente a Frequency: 0,87
- M_Score frente a Monetary: 0,76

---

### Metodología

### Qué es RFM

| Métrica | Descripción |
|---------|-------------|
| **Recency** | Días desde la última compra (menos es mejor) |
| **Frequency** | Total de compras (más es mejor) |
| **Monetary** | Valor total gastado (más es mejor) |

### Proceso

1. Calcular métricas por cliente.
2. Puntuar de 1 a 5 usando quintiles.
3. Crear el RFM Code (por ejemplo, "555").
4. Asignar segmentos:

```
Champions → R>=4, F>=4, M>=4
Leales    → R>=3, F>=3, M>=3
Nuevos    → R>=4, F<=2
En riesgo → R<=2, F>=3, M>=3
Otros     → resto
```

---

### Visualizaciones

### 1. Segmentación de clientes

![Segmentación](01_segmentacion_barras.png)

Los "Otros" son el grupo más grande (342), pero los Champions generan 28 veces más valor.

### 2. Mapa RFM: Recency frente a Monetary

![Mapa RFM](02_rfm_scatter.png)

- **Arriba a la derecha** (amarillo): Champions, recientes y de alto gasto.
- **Centro** (gris): Leales, buen valor.
- **Izquierda** (rojo): En riesgo, inactivos.
- **Abajo** (verde/azul): Nuevos y Otros.

### 3. Matriz de correlación

![Correlación](03_correlacion_heatmap.png)

Los scores reflejan fielmente las métricas originales.

---

### Recomendaciones

### Acción 1: programa VIP "Elite Champions"

**Objetivo**: retener 246 Champions ($3,8M).

**Tácticas**: acceso anticipado (48h), account manager dedicado, 5% de cashback por encima de
$5.000, eventos exclusivos.

**Impacto**: +$2,1M · ROI 42:1.

### Acción 2: campaña "Te echamos de menos"

**Objetivo**: recuperar 102 clientes en riesgo ($468K).

**Tácticas**: email secuencial (30 días), descuento del 25%, retargeting.

**Impacto**: $160K · ROI 32:1.

### Acción 3: onboarding "Primeros 90 días"

**Objetivo**: convertir 59 Nuevos en Leales.

**Tácticas**: email automation, descuento progresivo, gamificación.

**Impacto**: $42,5K · ROI 4:1.

### Impacto total (ilustrativo)

| Acción | Inversión | Retorno | ROI |
|--------|-----------|---------|-----|
| VIP Champions | $50K | $2,1M | 42:1 |
| Reactivación | $5K | $160K | 32:1 |
| Onboarding | $10K | $42,5K | 4:1 |
| **TOTAL** | **$65K** | **$2,3M** | **35:1** |

---

### Estructura del proyecto

```
RFM-Customer-Analytics/
├── 01_Analisis_RFM_Completo.ipynb   # Análisis completo: RFM, segmentación y gráficos
├── Script_Datos_Sinteticos.ipynb    # Generador del dataset sintético
├── raw_data_12meses.csv             # Dataset principal (12 meses)
├── raw_data.csv                     # Dataset auxiliar
├── 01_segmentacion_barras.png
├── 02_rfm_scatter.png
└── 03_correlacion_heatmap.png
```

---

### Cómo reproducir

### Requisitos

- Python 3.9+
- Jupyter Notebook
- pandas, matplotlib, seaborn

### Instalación

```bash
pip install pandas matplotlib seaborn
jupyter notebook 01_Analisis_RFM_Completo.ipynb
```

### Ejecución

1. Celda 1: cargar datos.
2. Celdas 2-4: calcular RFM.
3. Validación.
4. Celdas 5-7: generar gráficos.

### Dataset

`raw_data_12meses.csv`: 7.741 transacciones, 946 clientes, 12 meses simulados.

---

### Notas

- **Datos sintéticos**: generados con `Script_Datos_Sinteticos.ipynb`, con fines educativos y
  de portfolio. Las cifras de impacto y ROI son ilustrativas del método, no resultados reales.
- **Escalabilidad**: el método funciona igual con más de 100.000 transacciones.

---

### Repos relacionados

Este análisis es una pieza de un portfolio de casos de analítica. Las piezas hermanas:

- [lead-scoring-ml](https://github.com/jleonceo/lead-scoring-ml): predecir qué lead acaba comprando, con modelos de clasificación.
- [accident-intelligent-agent](https://github.com/jleonceo/accident-intelligent-agent): ETL, exploración y modelo para predecir la gravedad de un accidente de tráfico.
- [analisis-contable](https://github.com/jleonceo/analisis-contable): análisis financiero de una empresa con Python, del libro diario a las conclusiones.

## English

RFM (Recency, Frequency, Monetary) segmentation of an e-commerce customer base, built to
surface behaviour patterns and point retention effort where it pays off.

> The data is **synthetic**, generated for portfolio purposes (`Script_Datos_Sinteticos.ipynb`).
> The impact and ROI figures **illustrate the method; they are not real results**.

### Contents

- [Executive summary](#executive-summary)
- [Results](#results)
- [Methodology](#methodology)
- [Charts](#charts)
- [Recommendations](#recommendations)
- [Reproducing it](#reproducing-it)

---

### Executive summary

946 customers and 7,741 transactions over 12 months, scored with RFM and grouped into
segments that each map to a business action. The amounts are illustrative, on a synthetic
dataset.

### Main findings

- **246 Champions** (26%) average $15,447 each: the engine of the business.
- **102 At Risk** at $4,587 are on their way out: $468K exposed.
- **59 New** customers with little engagement: room to build loyalty.
- **342 Others** (36%) average just $550: poor return on effort.

**Potential impact (illustrative)**: $2.3M on top, at 35:1.

---

### Results

### Customer segments

| Segment | Customers | % | Average value | Recency | Frequency |
|---------|-----------|---|---------------|---------|-----------|
| Champions | 246 | 26% | $15,447 | 12 days | 16.8 |
| Loyal | 197 | 21% | $6,212 | 33 days | 9.3 |
| At Risk | 102 | 11% | $4,587 | 96 days | 8.1 |
| New | 59 | 6% | $528 | 13 days | 2.5 |
| Others | 342 | 36% | $550 | 144 days | 2.3 |

### Model check

- R_Score against Recency: -0.83
- F_Score against Frequency: 0.87
- M_Score against Monetary: 0.76

---

### Methodology

### What RFM is

| Metric | Meaning |
|--------|---------|
| **Recency** | Days since the last purchase (lower is better) |
| **Frequency** | Number of purchases (higher is better) |
| **Monetary** | Total spend (higher is better) |

### Process

1. Work out the three metrics for every customer.
2. Score each metric from 1 to 5 by quintile.
3. Join the digits into an RFM Code ("555", for example).
4. Assign a segment:

```
Champions → R>=4, F>=4, M>=4
Loyal     → R>=3, F>=3, M>=3
New       → R>=4, F<=2
At Risk   → R<=2, F>=3, M>=3
Others    → everything else
```

---

### Charts

### 1. Customer segments

![Segments](01_segmentacion_barras.png)

"Others" is the largest group (342), yet Champions are worth 28 times more.

### 2. RFM map: Recency against Monetary

![RFM map](02_rfm_scatter.png)

- **Top right** (yellow): Champions, recent and high-spending.
- **Middle** (grey): Loyal, decent value.
- **Left** (red): At Risk, gone quiet.
- **Bottom** (green/blue): New and Others.

### 3. Correlation matrix

![Correlation](03_correlacion_heatmap.png)

The scores track the underlying metrics closely.

---

### Recommendations

### Action 1: "Elite Champions" VIP programme

**Goal**: hold on to the 246 Champions ($3.8M).

**Tactics**: 48-hour early access, a dedicated account manager, 5% cashback above $5,000,
invitation-only events.

**Impact**: +$2.1M · 42:1.

### Action 2: "We miss you" campaign

**Goal**: win back the 102 at-risk customers ($468K).

**Tactics**: a 30-day email sequence, 25% discount, retargeting.

**Impact**: $160K · 32:1.

### Action 3: "First 90 days" onboarding

**Goal**: turn the 59 New customers into Loyal ones.

**Tactics**: email automation, a discount that steps up, gamification.

**Impact**: $42.5K · 4:1.

### Total impact (illustrative)

| Action | Spend | Return | ROI |
|--------|-------|--------|-----|
| VIP Champions | $50K | $2.1M | 42:1 |
| Win-back | $5K | $160K | 32:1 |
| Onboarding | $10K | $42.5K | 4:1 |
| **TOTAL** | **$65K** | **$2.3M** | **35:1** |

---

### Project layout

```
RFM-Customer-Analytics/
├── 01_Analisis_RFM_Completo.ipynb   # The whole analysis: RFM, segmentation, charts
├── Script_Datos_Sinteticos.ipynb    # Generator for the synthetic dataset
├── raw_data_12meses.csv             # Main dataset (12 months)
├── raw_data.csv                     # Secondary dataset
├── 01_segmentacion_barras.png
├── 02_rfm_scatter.png
└── 03_correlacion_heatmap.png
```

---

### Reproducing it

### Requirements

- Python 3.9+
- Jupyter Notebook
- pandas, matplotlib, seaborn

### Install

```bash
pip install pandas matplotlib seaborn
jupyter notebook 01_Analisis_RFM_Completo.ipynb
```

### Running it

1. Cell 1: load the data.
2. Cells 2-4: compute RFM.
3. Check the scores.
4. Cells 5-7: draw the charts.

### Dataset

`raw_data_12meses.csv`: 7,741 transactions, 946 customers, 12 simulated months.

---

### Notes

- **Synthetic data**: generated by `Script_Datos_Sinteticos.ipynb`, for teaching and portfolio
  use. The impact and ROI figures illustrate the method; they are not real results.
- **Scale**: the method behaves the same on 100,000+ transactions.


### Related repositories

This analysis is one piece of an analytics portfolio. Its sibling projects:

- [lead-scoring-ml](https://github.com/jleonceo/lead-scoring-ml): predicting which lead ends up buying, with classification models.
- [accident-intelligent-agent](https://github.com/jleonceo/accident-intelligent-agent): ETL, exploration and a model to predict how severe a road accident is.
- [analisis-contable](https://github.com/jleonceo/analisis-contable): financial analysis of a company with Python, from the ledger to the conclusions.

---

*Parte del portfolio de [Juan Luis León](https://github.com/jleonceo) · [juanluisleon.vercel.app](https://juanluisleon.vercel.app) · Licencia [MIT](LICENSE)*
