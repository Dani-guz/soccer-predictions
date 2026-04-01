# Referencias y Fuentes

## Fuente de datos
- **football-data.co.uk** - Datos históricos de partidos de fútbol europeo
- URL: https://www.football-data.co.uk/
- Formato: CSV con resultados, estadísticas básicas y cuotas de apuestas
- Ligas descargadas: La Liga (SP1), Premier League (E0), Serie A (I1), 
  Bundesliga (D1), Ligue 1 (F1)
- Período: Temporadas 2020/21 a 2024/25
- Notas sobre columnas: https://www.football-data.co.uk/notes.txt

## Fundamentos teóricos
- **Distribución de Poisson aplicada al fútbol**
- Maher, M.J. (1982). "Modelling Association Football Scores". 
  Statistica Neerlandica, 36(3), 109-118.
- Es el paper original que propuso modelar goles con Poisson.

- **Dixon & Coles Model** (1997)
- "Modelling Association Football Scores and Inefficiencies in the 
  Football Betting Market". Applied Statistics, 46(2), 265-280.
- Extensión del modelo Poisson que corrige la correlación en 
  marcadores bajos (0-0, 1-0, 0-1, 1-1).

## Modelos de referencia (industria)
- **FiveThirtyEight Soccer Predictions** (descontinuado en 2023)
- Usaba Soccer Power Index (SPI) basado en expected goals
- Referencia de accuracy: ~52-55% en clasificación a 3 bandas

- **Casas de apuestas (Bet365)**
- Accuracy observada en nuestro dataset: ~54-55%
- Log Loss: ~0.95
- Representan el estado del arte en predicción pública

## Herramientas y librerías
- scikit-learn: https://scikit-learn.org/
- XGBoost: https://xgboost.readthedocs.io/
- SciPy (distribución Poisson): https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.poisson.html
