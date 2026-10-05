# Λ Proyecto Lambda | Optimización de Inversiones Petroleras

## Descripción

OilyGiant es una compañía de exploración y extracción de petróleo que busca expandir sus operaciones mediante el desarrollo de nuevos pozos petroleros.

La empresa dispone de información geológica proveniente de tres regiones potenciales de exploración. El objetivo de este proyecto consiste en identificar la región que ofrece la mejor combinación entre rentabilidad esperada y bajo riesgo financiero, permitiendo tomar decisiones de inversión respaldadas por análisis cuantitativos.

Para ello se construyeron modelos de regresión lineal capaces de estimar las reservas de petróleo de nuevos pozos y posteriormente se evaluó el riesgo de inversión mediante simulaciones con la técnica de Bootstrapping.

---

## Objetivos

- Analizar y preparar los datos geológicos de tres regiones.
- Construir modelos de regresión para estimar reservas de petróleo.
- Evaluar el desempeño predictivo mediante RMSE.
- Seleccionar los 200 pozos con mayor potencial de producción.
- Estimar las ganancias potenciales para cada región.
- Implementar simulaciones mediante Bootstrapping.
- Calcular beneficios promedio, intervalos de confianza y riesgo de pérdidas.
- Seleccionar la región con la mejor combinación de rentabilidad y seguridad.

---

## Herramientas utilizadas

- Python
- Pandas
- NumPy
- Scikit-Learn
- Jupyter Notebook
- Linear Regression
- Bootstrapping

---

## Fuente de datos

Archivos utilizados:

- `geo_data_0.csv`
- `geo_data_1.csv`
- `geo_data_2.csv`

Variables disponibles:

- `id`: identificador único del pozo.
- `f0`, `f1`, `f2`: características geológicas.
- `product`: volumen de reservas de petróleo (miles de barriles).

---

## Metodología

### Exploración y preparación de datos

Se analizaron los tres conjuntos de datos proporcionados por la compañía para verificar:

- Calidad de la información.
- Valores ausentes.
- Tipos de datos.
- Variables relevantes para el modelado.

No se encontraron valores faltantes ni inconsistencias relevantes. La variable `id` fue eliminada al no aportar valor predictivo al modelo.

### Construcción de modelos predictivos

Se utilizaron exclusivamente modelos de Regresión Lineal, siguiendo las condiciones establecidas por el negocio.

Para cada región:

- Se dividieron los datos en entrenamiento (75%) y validación (25%).
- Se entrenó un modelo independiente.
- Se generaron predicciones sobre el conjunto de validación.
- Se calculó el RMSE y el volumen promedio de reservas estimadas.

### Evaluación del modelo

Resultados obtenidos:

| Región | Reservas promedio | RMSE |
|----------|----------:|----------:|
| Región 0 | 92.59 | 37.58 |
| Región 1 | 68.73 | 0.89 |
| Región 2 | 94.97 | 40.03 |

La Región 1 presentó el modelo más preciso al obtener el menor RMSE.

---

## Cálculo de ganancias

Condiciones de negocio:

- Inversión total: 100 millones USD.
- Número de pozos a desarrollar: 200.
- Ingreso por unidad de producto: 4500 USD.
- Producción mínima de equilibrio: 111.1 mil barriles por pozo.

Posteriormente se seleccionaron los 200 pozos con mayores reservas estimadas para cada región y se calculó la ganancia potencial asociada.

### Ganancias potenciales

| Región | Ganancia estimada |
|----------|----------:|
| Región 0 | 33.21 millones USD |
| Región 1 | 24.15 millones USD |
| Región 2 | 27.10 millones USD |

A primera vista, la Región 0 parecía ser la opción más rentable.

Sin embargo, este análisis no incorpora incertidumbre ni riesgo.

---

## Análisis de riesgo mediante Bootstrapping

Para obtener una estimación más realista de los beneficios, se aplicó la técnica de Bootstrapping con:

```text
1000 simulaciones
```

En cada iteración:

- Se seleccionaron 500 pozos aleatoriamente.
- Se eligieron los 200 pozos con mayor predicción.
- Se calculó la ganancia correspondiente.
- Se registró el resultado para construir la distribución de beneficios.

Posteriormente se calcularon:

- Ganancia promedio.
- Intervalo de confianza del 95%.
- Riesgo de pérdidas.

---

## Resultados finales

### Región 0

- Ganancia promedio: 3.96 millones USD.
- IC 95%: [-1.11M ; 9.09M]
- Riesgo de pérdidas: 6.9%

### Región 1

- Ganancia promedio: 4.56 millones USD.
- IC 95%: [0.34M ; 8.52M]
- Riesgo de pérdidas: 1.5%

### Región 2

- Ganancia promedio: 4.04 millones USD.
- IC 95%: [-1.63M ; 9.50M]
- Riesgo de pérdidas: 7.6%

---

## Principales hallazgos

- La Región 1 presentó el modelo predictivo más preciso.
- La Región 0 presentó la mayor ganancia potencial bajo condiciones ideales.
- El análisis de riesgo mostró que las regiones 0 y 2 superan el límite máximo de riesgo permitido por el negocio.
- La Región 1 fue la única que mantuvo una probabilidad de pérdida inferior al 2.5%.
- La Región 1 obtuvo además la mayor ganancia promedio entre las alternativas que cumplen las restricciones del negocio.

---

## Archivos principales

- `lambda_oil_well_investment_analysis.ipynb`
- `geo_data_0.csv`
- `geo_data_1.csv`
- `geo_data_2.csv`

---

## Conclusión

El análisis permitió identificar la región más adecuada para la inversión de 100 millones de dólares destinada al desarrollo de nuevos pozos petroleros.

Aunque la Región 0 mostró inicialmente la mayor ganancia potencial, el análisis de incertidumbre realizado mediante Bootstrapping evidenció que esta alternativa presenta un riesgo de pérdidas superior al permitido por la compañía.

La Región 1 demostró ofrecer el mejor equilibrio entre rentabilidad y seguridad financiera. Con una ganancia promedio estimada de 4.56 millones de dólares y un riesgo de pérdidas de apenas 1.5%, fue la única región que cumplió el criterio empresarial de mantener una probabilidad de pérdida inferior al 2.5%.

Por estas razones, se recomienda a OilyGiant desarrollar los nuevos pozos petrolíferos en la Región 1.
