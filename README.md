# Proyecto Properati – Parte 1: predicción de precios de propiedades en Capital Federal

Trabajo de la Diplomatura en Data Science de Acámica. A partir del dataset de publicaciones de Properati (146.660 registros) se construye un modelo para estimar el precio en dólares de departamentos, PH y casas en venta en Capital Federal.

> En el notebook este trabajo se menciona como “proyecto 2”; el “proyecto 1” es el modelo base con el que se compara. La continuación está en [Acamica-Proyecto_Properati_Part2](https://github.com/FreeAlejandria/Acamica-Proyecto_Properati_Part2).

📄 **Versión para leer sin ejecutar nada:** [`docs/Proyecto_Properati_Part1_V1.pdf`](docs/Proyecto_Properati_Part1_V1.pdf) (notebook completo con portada, resumen e índice).

## Qué incluye

1. **EDA:** distribución de publicaciones por tipo de propiedad, región y barrio; precios promedio por zona; correlaciones.
2. **Limpieza:** corrección de registros con superficie cubierta mayor a la total y eliminación escalonada de outliers por rango intercuartil (IQR) sobre superficies, precio, ambientes y baños. Dataset final: 50.112 propiedades.
3. **Preprocesamiento:** nulos e imputación, escalado con `StandardScaler`, one-hot encoding de `property_type`.
4. **Modelos simples:** regresión lineal (benchmark), KNN y árbol de decisión, con hiperparámetros elegidos por curvas de validación. La mejora en la preparación de datos redujo el RMSE más de un 65% frente al modelo del proyecto anterior.
5. **Modelos avanzados:** regresión lineal con atributos polinómicos y regularización Lasso/Ridge, y XGBoost con `GridSearchCV` y validación cruzada. El mejor desempeño se obtuvo con XGBoost usando todos los atributos, incluido el tipo de propiedad.

## Archivos

| Archivo | Descripción |
|---|---|
| `Proyecto_Properati_Part1.ipynb` | Notebook completo con código, salidas y conclusiones. |
| `docs/Proyecto_Properati_Part1_V1.pdf` | Versión PDF del notebook, lista para leer o compartir. |
| `new_properati_Capital1_All_sin_bedrooms_clean.csv` | Dataset limpio (sin outliers), resultado del EDA. |
| `new_properati_Capital2_All_sin_bedrooms_clean_normalizado.csv` | El mismo dataset con las variables numéricas escaladas. |
| `requirements.txt` | Versiones de librerías compatibles con el código. |

### Datasets grandes (en Google Drive)

Los datasets de más de 25 MB no entran en GitHub y están en Google Drive con acceso libre. Para ejecutar el notebook desde el principio hay que descargarlos en la misma carpeta que el notebook:

- `Properati.csv` (dataset original): https://drive.google.com/file/d/109_5W7r4ayq7uhG4NuSPAna6wkb5_gcD/view?usp=sharing
- `new_properati_Capital1_All_sin_bedrooms.csv`: https://drive.google.com/file/d/1VGgmzPwsgTw18no0XGALJ7TO79SqYey9/view?usp=sharing

## Cómo ejecutarlo

El notebook se escribió en 2020-2021 con Python 3.7, scikit-learn 0.24 y XGBoost 1.4. Algunas llamadas (`np.int`, `normalize=` en `LinearRegression`) ya no existen en versiones recientes, por eso conviene usar un entorno con las versiones de `requirements.txt`:

```bash
python -m venv .venv && source .venv/bin/activate   # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook Proyecto_Properati_Part1.ipynb
```

Las búsquedas de hiperparámetros con `GridSearchCV` sobre XGBoost tardan bastante (decenas de minutos cada una).

## Nota sobre las salidas

Las salidas de las secciones 3.2.1.1.2 y 3.2.1.1.3 se habían perdido en el notebook original (el kernel se reinició antes de guardar). En noviembre de 2026 se re-ejecutaron con el mismo código y datos, con versiones actuales de las librerías, y así quedan en el notebook y en el PDF. Los valores pueden diferir levemente de los citados en las conclusiones, que se escribieron con la corrida original.
