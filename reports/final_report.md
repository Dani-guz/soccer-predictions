# Soccer Predictions: Estimación de Probabilidad de Resultados en La Liga

## Resumen Ejecutivo

Proyecto de machine learning para estimar la probabilidad de victoria, 
empate y derrota en partidos de La Liga española, con énfasis en el 
FC Barcelona.

### Resultados principales

| Modelo | Accuracy (test) | Log Loss (test) | Barcelona Accuracy |
|--------|-----------------|-----------------|-------------------|
| Baseline (siempre H) | 44.1% | 1.074 | — |
| RF Clasificador | 52.2% | 1.015 | 57.9% |
| **Poisson (mejor)** | **52.8%** | **1.007** | **76.3%** |
| Bet365 (referencia) | 54.6% | 0.953 | — |

### Conclusiones

1. **El modelo Poisson es el mejor enfoque** para este problema.
 Produce probabilidades más calibradas (mejor Log Loss) y 
 resultados interpretables (goles esperados por equipo).

2. **Accuracy del 52.8%** supera significativamente la baseline 
 naive (44.1%) y se acerca a la referencia profesional (54.6%).

3. **Para el Barcelona, el modelo alcanza 76.3% de accuracy**, 
 porque los equipos dominantes tienen patrones más predecibles.

4. **El empate es el resultado más difícil de predecir** en fútbol.
 Ningún modelo (ni las casas de apuestas) lo predice bien como 
 clase mayoritaria, aunque Poisson asigna probabilidades realistas.

5. **Más datos no siempre mejora resultados.** Agregar 4 ligas 
 europeas empeoró la accuracy general pero mejoró la predicción 
 para equipos top (Barcelona: 57.9% → 73.7%).

6. **Modelos más complejos no siempre son mejores.** XGBoost fracasó 
 por overfitting con datos limitados. La regresión logística y 
 Random Forest fueron superiores.

## Datos

- **Fuente:** football-data.co.uk
- **Período:** 5 temporadas (2020/21 a 2024/25)
- **Volumen:** ~1,900 partidos (La Liga), ~9,500 (5 ligas europeas)
- **Features:** 18 variables derivadas de forma reciente, posición 
en tabla, contexto del partido

## Metodología

### Feature Engineering
- Rolling windows (últimos 5 partidos) para forma reciente
- Simulación de tabla de posiciones jornada a jornada
- Features diferenciales (ventaja relativa entre equipos)
- Validación manual anti data-leakage

### Modelos probados
1. Regresión Logística (baseline inteligente)
2. Random Forest Clasificador
3. XGBoost (fracasó por overfitting)
4. **Modelo Poisson** (dos RF Regressors + distribución Poisson)

### Validación
- Split temporal estricto: Train (2020-23) / Val (2023-24) / Test (2024-25)
- Métricas: Accuracy, Log Loss, Confusion Matrix, Recall por clase
- Baselines: naive (siempre H), proporciones históricas, cuotas Bet365

## Estructura del proyecto

notebooks/ 01_Cleaning_&_EDA.ipynb → Descarga, limpieza, exploración 02_Feature_Engineering.ipynb → Construcción de features 03_Modeling_Baseline.ipynb → Baselines y primer modelo 04_Advanced_Models.ipynb → RF, XGBoost, comparación 05_Multi_League_Data.ipynb → Iteración con 5 ligas europeas 06_Poisson_Model.ipynb → Modelo Poisson (mejor resultado)

## Limitaciones

- No incluye datos de alineaciones, lesiones ni estado anímico
- 5 temporadas es un volumen modesto para ML
- Asume independencia de goles (Poisson) que no es perfecta
- No captura dinámicas intra-partido

## Posibles extensiones

- Incorporar Expected Goals (xG) desde FBref
- Modelo Dixon-Coles (corrige correlación en marcadores bajos)
- Calibración de probabilidades con Platt Scaling
- Despliegue con Streamlit para predicciones en tiempo real
