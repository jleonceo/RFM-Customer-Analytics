# 📊 Análisis RFM de Clientes - E-commerce

Segmentación de clientes mediante análisis RFM (Recency, Frequency, Monetary) 
para identificar patrones de comportamiento y optimizar estrategias de retención.

---

## 📋 Tabla de Contenidos

- [Resumen Ejecutivo](#-resumen-ejecutivo)
- [Resultados](#-resultados)
- [Metodología](#-metodología)
- [Visualizaciones](#-visualizaciones)
- [Recomendaciones](#-recomendaciones)
- [Cómo Reproducir](#-cómo-reproducir)

---

## 📊 Resumen Ejecutivo

Este proyecto analiza **946 clientes** y **7,741 transacciones** durante 12 meses 
usando metodología RFM para segmentar y proponer acciones de negocio.

### Hallazgos Principales

✅ **246 Champions** (26%) generan $15,447 promedio → Motor del negocio  
⚠️ **102 En Riesgo** con $4,587 están abandonando → $468K en peligro  
🌱 **59 Nuevos** con bajo engagement → Oportunidad de fidelización  
📦 **342 Otros** (36%) generan solo $550 → Bajo ROI

**Impacto potencial**: $2.3M adicionales con ROI de 35:1

---

## 🎯 Resultados

### Segmentación de Clientes

| Segmento | Clientes | % | Valor Promedio | Recency | Frequency |
|----------|----------|---|----------------|---------|-----------|
| Champions | 246 | 26% | $15,447 | 12 días | 16.8 |
| Leales | 197 | 21% | $6,212 | 33 días | 9.3 |
| En Riesgo | 102 | 11% | $4,587 | 96 días | 8.1 |
| Nuevos | 59 | 6% | $528 | 13 días | 2.5 |
| Otros | 342 | 36% | $550 | 144 días | 2.3 |

### Validación del Modelo

✅ R_Score - Recency: -0.83  
✅ F_Score - Frequency: 0.87  
✅ M_Score - Monetary: 0.76

---

## 🔧 Metodología

### ¿Qué es RFM?

| Métrica | Descripción |
|---------|-------------|
| **Recency** | Días desde última compra (menos = mejor) |
| **Frequency** | Total de compras (más = mejor) |
| **Monetary** | Valor total gastado (más = mejor) |

### Proceso

1. Calcular métricas por cliente
2. Puntuación 1-5 usando quintiles
3. Crear RFM Code (ej: "555")
4. Asignar segmentos:

Champions → R≥4, F≥4, M≥4
Leales → R≥3, F≥3, M≥3
Nuevos → R≥4, F≤2
En Riesgo → R≤2, F≥3, M≥3
Otros → Resto


---

## 📈 Visualizaciones

### 1. Segmentación de Clientes

![Segmentación](imagenes/01_segmentacion_barras.png)

Los "Otros" son mayoría (342) pero Champions generan 28x más valor.

### 2. Mapa RFM: Recency vs Monetary

![Mapa RFM](imagenes/02_rfm_scatter.png)

- **Arriba-derecha** (amarillo): Champions - recientes y alto gasto
- **Centro** (gris): Leales - buen valor
- **Izquierda** (rojo): En Riesgo - inactivos
- **Abajo** (verde/azul): Nuevos y Otros

### 3. Matriz de Correlación

![Correlación](imagenes/03_correlacion_heatmap.png)

Los scores reflejan fielmente las métricas originales.

---

## 💡 Recomendaciones

### Acción 1: Programa VIP "Elite Champions" 🏆

**Objetivo**: Retener 246 Champions ($3.8M)

**Tácticas**:
- Acceso anticipado (48h)
- Account Manager dedicado
- 5% cashback en >$5,000
- Eventos exclusivos

**Impacto**: +$2.1M | ROI: 42:1

---

### Acción 2: Campaña "Te Extrañamos" 📧

**Objetivo**: Recuperar 102 En Riesgo ($468K)

**Tácticas**:
- Email secuencial (30 días)
- Descuento 25%
- Retargeting ads

**Impacto**: $160K | ROI: 32:1

---

### Acción 3: Onboarding "Primeros 90 Días" 🌱

**Objetivo**: Convertir 59 Nuevos en Leales

**Tácticas**:
- Email automation
- Descuento progresivo
- Gamificación

**Impacto**: $42.5K | ROI: 4:1

---

### Impacto Total

| Acción | Inversión | Retorno | ROI |
|--------|-----------|---------|-----|
| VIP Champions | $50K | $2.1M | 42:1 |
| Reactivación | $5K | $160K | 32:1 |
| Onboarding | $10K | $42.5K | 4:1 |
| **TOTAL** | **$65K** | **$2.3M** | **35:1** |

---

## 📁 Estructura del Proyecto
Caso1_Customer_Analytics/
├── raw_data_12meses.csv
├── 01_Analisis_RFM_Completo.ipynb
├── README.md
├── sql/
│ └── scripts SQL de referencia
└── imagenes/
├── 01_segmentacion_barras.png
├── 02_rfm_scatter.png
└── 03_correlacion_heatmap.png
---

## 🚀 Cómo Reproducir

### Requisitos

- Python 3.9+
- Jupyter Notebook
- pandas, matplotlib, seaborn

### Instalación

```bash
# Instalar dependencias
pip install pandas matplotlib seaborn

# Ejecutar notebook
jupyter notebook 01_Analisis_RFM_Completo.ipynb

Ejecución
Ejecutar celda 1: Cargar datos
Ejecutar celdas 2-4: Calcular RFM
Ejecutar validación
Ejecutar celdas 5-7: Generar gráficos
Dataset
raw_data_12meses.csv:
7,741 transacciones
946 clientes
Período: Junio 2022 - Junio 2023
🛠️ Tecnologías
Python 3.9+
Pandas, Matplotlib, Seaborn
Jupyter Notebook
📝 Notas
Datos sintéticos: Fines educativos/portfolio
Período: 12 meses simulados
Escalabilidad: Funciona con 100K+ transacciones