# Tarea 6 — Clasificación según conjunto de datos

Repositorio para completar la tarea de clasificación usando el dataset de cardiotocografía `CTG.xls`.

## Objetivo

El proyecto continúa lo definido en los puntos 1, 2 y 3 del PDF de la tarea:

- análisis exploratorio inicial del dataset CTG;
- definición del problema como clasificación multiclase supervisada;
- diseño del experimento con `NSP` como variable objetivo.

Desde esa base, se completan los puntos 4 a 7: implementación del experimento, presentación ordenada de resultados, análisis y entrega mediante enlace a GitHub.

## Archivos principales

- `CTG.xls`: dataset fuente.
- `Tarea 6_ Clasificación según conjunto de datos.pdf`: consigna y desarrollo base de los puntos 1–3.
- `notebooks/ctg_nsp_experiment.ipynb`: notebook con la implementación de los puntos 4–7.
- `requirements.txt`: dependencias para ejecutar el notebook localmente.

## Experimento

El notebook usa la hoja `Data` de `CTG.xls`, limpia filas no observacionales y entrena modelos para predecir `NSP`:

- `1 = Normal`
- `2 = Suspect / Sospechoso`
- `3 = Pathologic / Patológico`

Se usan exactamente las 21 variables técnicas del bloque `LB` a `Tendency`, una columna por predictor. El notebook selecciona ese bloque por posición para evitar que los nombres duplicados del Excel (`AC`, `FM`, `UC`, `DL`, `DS`, `DP`) expandan accidentalmente la matriz de entrenamiento. Para evitar fuga de información, se excluyen metadatos, `CLASS`, etiquetas diagnósticas `A`–`SUSP` y `DR`.

Modelos comparados:

- Regresión Logística con estandarización.
- Random Forest.
- SVM RBF con estandarización.

La evaluación usa `train/test split` estratificado, validación cruzada estratificada de 5 folds y semilla fija (`RANDOM_STATE = 42`). Las métricas principales son `F1-macro` y `recall` de la clase `Pathologic`; `accuracy` se reporta solo como métrica secundaria.

## Cómo ejecutar localmente

```bash
py -3 -m venv .venv
.venv\Scripts\activate
python -m pip install -r requirements.txt
python -m jupyter nbconvert --to notebook --execute --inplace notebooks/ctg_nsp_experiment.ipynb
```

En Windows, `py -3` evita depender del alias global `python`. El notebook queda guardado con las salidas reales de la ejecución local. Este entorno instala `nbconvert` e `ipykernel` para ejecutar el notebook; si querés abrirlo con una interfaz web, instalá aparte `notebook` o `jupyterlab` en el entorno virtual.

## Cómo ejecutar en Google Colab

1. Abrir `notebooks/ctg_nsp_experiment.ipynb` en Colab.
2. Subir `CTG.xls` cuando el notebook lo solicite, si Colab no lo encuentra.
3. Ejecutar todas las celdas.

## Entrega

La entrega final solicitada en el punto 7 es el enlace a este repositorio GitHub. Cada integrante debe subir su versión según la consigna.

## Nota sobre resultados

El notebook fue ejecutado localmente con un entorno `.venv`; las tablas, reportes, matrices y gráficos quedan guardados como salidas del archivo `.ipynb`. No se incluyen métricas inventadas en este README.
