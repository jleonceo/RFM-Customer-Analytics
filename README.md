# Análisis RFM de clientes — E-commerce

Segmentación de clientes mediante análisis RFM (Recency, Frequency, Monetary) para
identificar patrones de comportamiento y orientar estrategias de retención.

> Datos **sintéticos**, generados para portfolio (`Script_Datos_Sinteticos.ipynb`). Las
> cifras de impacto y ROI son **ilustrativas del método, no resultados reales**.

---

## Tabla de contenidos

- [Resumen ejecutivo](#resumen-ejecutivo)
- [Resultados](#resultados)
- [Metodología](#metodología)
- [Visualizaciones](#visualizaciones)
- [Recomendaciones](#recomendaciones)
- [Cómo reproducir](#cómo-reproducir)

---

## Resumen ejecutivo

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

## Resultados

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

## Metodología

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

## Visualizaciones

### 1. Segmentación de clientes

![Segmentación](01_segmentacion_barras.png)

Los "Otros" son mayoría (342), pero los Champions generan 28 veces más valor.

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

## Recomendaciones

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

## Estructura del proyecto

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

## Cómo reproducir

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

## Notas

- **Datos sintéticos**: generados con `Script_Datos_Sinteticos.ipynb`, con fines educativos y
  de portfolio. Las cifras de impacto y ROI son ilustrativas del método, no resultados reales.
- **Escalabilidad**: el método funciona igual con más de 100.000 transacciones.

---

*Parte del portfolio de [Juan Luis León](https://github.com/jleonceo) · [juanluisleon.vercel.app](https://juanluisleon.vercel.app) · Licencia [MIT](LICENSE)*
