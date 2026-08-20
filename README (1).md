
# Mejora de un modelo de predicción de precios de vehículos

## Objetivo

Modificar un modelo base de predicción de precios de vehículos y realizar diferentes experimentos para mejorar su desempeño.

## Dataset

Se utilizó el dataset **Vehicle Dataset from CarDekho** disponible en Kaggle.

## Baseline

El modelo inicial utilizado fue una **Regresión Lineal**.

- **MAE:** $221,706 MXN
- **RMSE:** $426,787 MXN
- **R²:** 0.4031

## Experimentos

Se realizaron cinco experimentos para evaluar diferentes estrategias de mejora:

1. Incorporación de la variable `antigüedad`.
2. Tratamiento de valores atípicos.
3. Incorporación de la variable `name`.
4. Cambio de Regresión Lineal a **Random Forest**.
5. Ajuste de hiperparámetros de Random Forest mediante **GridSearchCV**.

## Resultados

| Modelo | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | $221,706 | $426,787 | 0.4031 |
| Exp. 1 | $221,706 | $426,787 | 0.4031 |
| Exp. 2 | $125,693 | $168,867 | 0.5445 |
| Exp. 3 | $128,556 | $171,486 | 0.5302 |
| Exp. 4 | $108,486 | $158,551 | 0.5984 |
| Exp. 5 | $107,411 | $152,010 | 0.6309 |

## Mejor modelo

El mejor modelo obtenido fue **Random Forest optimizado mediante GridSearchCV**.

- **MAE:** $107,411 MXN
- **RMSE:** $152,010 MXN
- **R²:** 0.6309

Respecto al modelo Baseline:

- El MAE mejoró aproximadamente **51.56%**.
- El RMSE mejoró aproximadamente **64.37%**.
- El R² aumentó de **0.4031 a 0.6309**.

La modificación que produjo la mayor mejora individual fue el **tratamiento de valores atípicos**.

## Predicciones

El modelo final fue utilizado para estimar el precio de tres vehículos diferentes, utilizando sus características como entrada al modelo.

## Conclusión

Los experimentos demostraron que el tratamiento de valores atípicos y el cambio a un modelo no lineal mejoraron considerablemente el desempeño.

El ajuste de hiperparámetros mediante **GridSearchCV** permitió obtener el mejor resultado final, alcanzando un **R² de 0.6309**, un **MAE de $107,411 MXN** y un **RMSE de $152,010 MXN**.
