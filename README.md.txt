# Mejora de un modelo de predicción de precios de vehículos

## 1. Objetivo

El objetivo de esta actividad fue mejorar un modelo base de predicción de precios de vehículos mediante diferentes experimentos de preparación de datos, selección de variables, cambio de algoritmo y ajuste de hiperparámetros.

La variable objetivo utilizada fue `precio`.

## 2. Dataset

Se utilizó el dataset **Vehicle Dataset from CarDekho**, disponible en Kaggle:

https://www.kaggle.com/datasets/nehalbirla/vehicle-dataset-from-cardekho

El dataset contiene información sobre vehículos usados, incluyendo año, kilometraje, combustible, tipo de vendedor, transmisión y número de propietarios.

Después de la preparación inicial, el dataset utilizado tuvo **4,340 registros y 8 variables**.

## 3. Baseline

Como punto de partida se utilizó una **Regresión Lineal** con variables numéricas y categóricas procesadas mediante One-Hot Encoding.

Los resultados del Baseline fueron:

- **MAE:** $221,706 MXN
- **RMSE:** $426,787 MXN
- **R²:** 0.4031

Estos resultados fueron utilizados como referencia para comparar los siguientes experimentos.

## 4. Experimentos realizados

### Experimento 1 — Incorporación de antigüedad

Se agregó una nueva variable llamada `antiguedad`, calculada a partir del año del vehículo.

El resultado no presentó cambios respecto al Baseline. Esto puede explicarse porque la antigüedad es una transformación directa del año y la Regresión Lineal ya utilizaba esta variable.

### Experimento 2 — Tratamiento de outliers

Se identificaron valores atípicos utilizando el rango intercuartílico (IQR) para el precio y el kilometraje.

Se eliminaron 378 registros considerados outliers, pasando de 4,340 a 3,962 registros.

Este experimento produjo una mejora importante en el desempeño del modelo.

### Experimento 3 — Incorporación de `name`

Se incorporó la variable `name` como característica categórica.

El desempeño empeoró ligeramente. Esto puede deberse a la gran cantidad de categorías diferentes generadas mediante One-Hot Encoding, lo que aumentó la complejidad del modelo sin aportar suficiente información generalizable.

### Experimento 4 — Cambio a Random Forest

Se reemplazó la Regresión Lineal por un modelo **Random Forest**.

El cambio permitió capturar relaciones no lineales e interacciones entre las características de los vehículos que la Regresión Lineal no podía representar adecuadamente.

Este experimento produjo una mejora importante en las métricas.

### Experimento 5 — Ajuste de hiperparámetros

Finalmente, se realizó una búsqueda de hiperparámetros utilizando `GridSearchCV` para optimizar el modelo Random Forest.

Los mejores parámetros encontrados fueron:

- `n_estimators = 200`
- `max_depth = 10`
- `min_samples_split = 2`
- `min_samples_leaf = 2`

## 5. Comparación de resultados

| Modelo | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline - Regresión Lineal | $221,706 | $426,787 | 0.4031 |
| Experimento 1 - Antigüedad | $221,706 | $426,787 | 0.4031 |
| Experimento 2 - Tratamiento de outliers | $125,693 | $168,867 | 0.5445 |
| Experimento 3 - Incorporación de `name` | $128,556 | $171,486 | 0.5302 |
| Experimento 4 - Random Forest | $108,486 | $158,551 | 0.5984 |
| **Experimento 5 - Random Forest optimizado** | **$107,411** | **$152,010** | **0.6309** |

## 6. Mejor modelo

El mejor modelo obtenido fue el **Random Forest optimizado del Experimento 5**.

Sus resultados finales fueron:

- **MAE:** $107,411 MXN
- **RMSE:** $152,010 MXN
- **R²:** 0.6309

Comparado con el Baseline:

- El **MAE disminuyó 51.56%**.
- El **RMSE disminuyó 64.37%**.
- El **R² aumentó de 0.4031 a 0.6309**, una mejora de 22.78 puntos porcentuales.

La modificación que produjo la **mayor mejora individual** fue el tratamiento de valores atípicos.

## 7. Predicción de vehículos

El mejor modelo se utilizó para estimar el precio de tres vehículos con diferentes características.

Las predicciones obtenidas fueron:

| Vehículo | Año | Km | Combustible | Transmisión | Propietario | Precio estimado |
|---|---:|---:|---|---|---|---:|
| 1 | 2022 | 30,000 | Petrol | Manual | First Owner | $369,640.35 |
| 2 | 2019 | 60,000 | Diesel | Automatic | First Owner | $907,320.00 |
| 3 | 2015 | 120,000 | Petrol | Manual | Second Owner | $282,277.01 |

Estas cantidades representan estimaciones realizadas por el modelo y no necesariamente corresponden al precio real de mercado.

## 8. Conclusiones

Los experimentos demostraron que el desempeño del modelo puede mejorar considerablemente mediante una adecuada preparación de los datos y la selección de un algoritmo capaz de representar relaciones no lineales.

El tratamiento de valores atípicos produjo la mayor mejora individual, mientras que el cambio de Regresión Lineal a Random Forest permitió capturar relaciones más complejas entre las características de los vehículos y su precio.

El ajuste de hiperparámetros permitió obtener el mejor resultado final, alcanzando un R² de 0.6309.

En conclusión, el **Random Forest optimizado** fue el modelo con mejor desempeño entre las alternativas evaluadas y fue seleccionado como el modelo final para realizar las predicciones de precios.

## 9. Archivos incluidos

- `Clase03_Autos_Precio.ipynb` — Notebook con el código, experimentos, resultados y conclusiones.
- `vehicle_price_v1.joblib` — Pipeline del mejor modelo entrenado y persistido.