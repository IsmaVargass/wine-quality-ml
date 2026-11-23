# Wine Quality ML

Proyecto inicial para estimar si un vino Vinho Verde será de calidad alta usando los resultados de unas medidas de laboratorio.

> **Estado:** la estructura y la documentación están preparadas, pero el programa todavía no entrena modelos ni calcula predicciones. Los ficheros de `src/` son marcadores de posición.

## Índice

1. [¿Qué problema intenta resolver?](#1-qué-problema-intenta-resolver)
2. [¿Qué datos utiliza?](#2-qué-datos-utiliza)
3. [¿Cómo se instala?](#3-cómo-se-instala)
4. [¿Cómo se entrenaría el modelo?](#4-cómo-se-entrenaría-el-modelo)
5. [¿Cómo se obtendrían predicciones?](#5-cómo-se-obtendrían-predicciones)
6. [¿Qué contiene cada carpeta y archivo?](#6-qué-contiene-cada-carpeta-y-archivo)
7. [¿Qué falta para poder usarlo?](#7-qué-falta-para-poder-usarlo)
8. [Fuente de los datos y licencia](#8-fuente-de-los-datos-y-licencia)

---

## 1. ¿Qué problema intenta resolver?

Una bodega puede medir varias características de un vino antes de probarlo. Este proyecto plantea usar esas medidas para estimar si el vino obtendría una nota alta en una cata. La idea sería ayudar a decidir qué lotes conviene probar primero; el resultado no sustituiría la opinión de las personas que catan.

Para este borrador, se considera de calidad alta una nota de **7 o más**. El programa mostraría una de estas dos respuestas:

| Nota de cata | Resultado |
|---|---|
| 7 o más | Calidad alta |
| Menos de 7 | No alcanza el umbral |

## 2. ¿Qué datos utiliza?

Se propone utilizar el conjunto [Wine Quality de UCI](https://archive.ics.uci.edu/dataset/186/wine+quality). Incluye vinos portugueses Vinho Verde, tintos y blancos.

| Archivo que se descarga | Cantidad de vinos | Medidas |
|---|---:|---:|
| `winequality-red.csv` | 1.599 | 11 |
| `winequality-white.csv` | 4.898 | 11 |
| **Total** | **6.497** | **11** |

Los dos archivos originales **no están incluidos** en este repositorio. Después de descargarlos, hay que guardarlos en `data/raw/`. Los ficheros usan punto y coma (`;`) para separar las columnas.

### ¿Qué significa cada medida?

| Nombre en el archivo | Explicación sencilla |
|---|---|
| `fixed acidity` | Acidez fija |
| `volatile acidity` | Acidez volátil |
| `citric acid` | Cantidad de ácido cítrico |
| `residual sugar` | Azúcar que queda en el vino |
| `chlorides` | Cantidad de cloruros |
| `free sulfur dioxide` | Dióxido de azufre libre |
| `total sulfur dioxide` | Dióxido de azufre total |
| `density` | Densidad del vino |
| `pH` | Medida de acidez |
| `sulphates` | Cantidad de sulfatos |
| `alcohol` | Grado de alcohol |
| `quality` | Nota puesta por quienes cataron el vino |

### Ejemplo de cómo se ven los CSV

No hay capturas de los archivos reales porque no se guardan en el repositorio. Este fragmento muestra el formato de ejemplo: una fila por vino y las columnas separadas por `;`.

**Vino tinto (`winequality-red.csv`):**

```csv
fixed acidity;volatile acidity;citric acid;residual sugar;chlorides;free sulfur dioxide;total sulfur dioxide;density;pH;sulphates;alcohol;quality
7.4;0.7;0;1.9;0.076;11;34;0.9978;3.51;0.56;9.4;5
7.8;0.88;0;2.6;0.098;25;67;0.9968;3.2;0.68;9.8;5
```

**Vino blanco (`winequality-white.csv`):**

```csv
fixed acidity;volatile acidity;citric acid;residual sugar;chlorides;free sulfur dioxide;total sulfur dioxide;density;pH;sulphates;alcohol;quality
7;0.27;0.36;20.7;0.045;45;170;1.001;3;0.45;8.8;6
6.3;0.3;0.34;1.6;0.049;14;132;0.994;3.3;0.49;9.5;6
```

## 3. ¿Cómo se instala?

Se necesita Git y Python 3.10 o posterior. Primero se descarga el proyecto y se prepara un entorno propio para sus paquetes:

```bash
git clone https://github.com/IsmaVargass/wine-quality-ml.git
cd wine-quality-ml
python -m venv .venv
```

En Windows PowerShell, activa el entorno e instala los paquetes:

```powershell
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

En macOS o Linux, la activación es:

```bash
source .venv/bin/activate
python -m pip install -r requirements.txt
```

Descarga los dos CSV desde [UCI](https://archive.ics.uci.edu/dataset/186/wine+quality) y guárdalos aquí:

```text
data/raw/winequality-red.csv
data/raw/winequality-white.csv
```

## 4. ¿Cómo se entrenaría el modelo?

El comando que se usará cuando se programe el entrenamiento es:

```bash
python src/train.py --config configs/params.yaml
```

**Todavía no se puede ejecutar:** `src/train.py` es un marcador de posición. Cuando esté implementado, leerá los CSV, aprenderá a relacionar las medidas con la nota y guardará el resultado en `models/wine_model.joblib`.

El umbral de calidad, las rutas de los CSV y otras opciones están anotados en [`configs/params.yaml`](configs/params.yaml).

## 5. ¿Cómo se obtendrían predicciones?

El comando previsto para pedir una respuesta sobre vinos nuevos es:

```bash
python src/predict.py --model models/wine_model.joblib --input data/processed/nuevos_vinos.csv --output reports/predicciones.csv
```

**Todavía no se puede ejecutar:** `src/predict.py` también es un marcador de posición y primero hace falta entrenar y guardar un modelo. El archivo de entrada deberá tener las mismas 11 medidas que los CSV originales. El resultado previsto será una tabla con la respuesta para cada vino.

## 6. ¿Qué contiene cada carpeta y archivo?

```text
wine-quality-ml/
|-- README.md
|-- requirements.txt
|-- .gitignore
|-- LICENSE
|-- configs/
|   `-- params.yaml
|-- data/
|   |-- raw/
|   |   `-- .gitkeep
|   |-- interim/
|   |   `-- .gitkeep
|   `-- processed/
|       `-- .gitkeep
|-- notebooks/
|   `-- .gitkeep
|-- src/
|   |-- data.py
|   |-- features.py
|   |-- train.py
|   |-- predict.py
|   `-- evaluate.py
|-- models/
|   `-- .gitkeep
|-- reports/
|   `-- figures/
|       `-- .gitkeep
|-- tests/
|   `-- .gitkeep
`-- docs/
    |-- decisiones.md
    |-- diccionario_datos.md
    `-- entrega.pdf
```

| Carpeta o archivo | ¿Para qué sirve? |
|---|---|
| `README.md` | Esta guía: explica el objetivo, los datos, la instalación y el uso previsto. |
| `requirements.txt` | Lista los paquetes de Python que necesitará el proyecto. |
| `.gitignore` | Evita subir a Git archivos locales o generados, como los CSV y los modelos. |
| `LICENSE` | Indica las condiciones para reutilizar el código del proyecto. |
| `configs/params.yaml` | Guarda las rutas de los datos y las opciones previstas para el entrenamiento. |
| `data/raw/` | Guarda los CSV originales descargados; se mantienen sin modificar. |
| `data/interim/` | Reservada para archivos de trabajo mientras se preparan los datos. |
| `data/processed/` | Reservada para los datos preparados que se usarían al entrenar. |
| `data/*/.gitkeep` | Marcadores vacíos para que Git conserve `raw/`, `interim/` y `processed/`. No son datos. |
| `notebooks/` | Aquí irán cuadernos para explorar los datos paso a paso. Aún no se han creado. |
| `notebooks/.gitkeep` | Mantiene la carpeta de cuadernos en Git mientras está vacía. |
| `src/data.py` | Deberá leer y juntar los CSV. Aún no está implementado. |
| `src/features.py` | Deberá preparar las medidas y crear la respuesta “calidad alta”. Aún no está implementado. |
| `src/train.py` | Deberá entrenar y guardar el modelo. Aún no está implementado. |
| `src/predict.py` | Deberá usar un modelo guardado para responder sobre vinos nuevos. Aún no está implementado. |
| `src/evaluate.py` | Deberá resumir qué tan acertadas son las respuestas. Aún no está implementado. |
| `models/` y `models/.gitkeep` | Carpeta para guardar el modelo entrenado; el marcador conserva la carpeta vacía. Aún no hay ningún modelo. |
| `reports/figures/` y su `.gitkeep` | Lugar previsto para guardar gráficos; todavía no hay resultados. |
| `tests/` y `tests/.gitkeep` | Lugar previsto para pruebas que comprueben el código; aún no hay pruebas. |
| `docs/diccionario_datos.md` | Explica con más detalle los nombres de las columnas de los CSV. |
| `docs/decisiones.md` | Resume por qué se han separado los datos, el código y la documentación. |
| `docs/entrega.pdf` | Documento PDF preparado para la entrega de la actividad. |

Los archivos `.gitkeep` solo sirven para conservar carpetas vacías; no forman parte del programa.

## 7. ¿Qué falta para poder usarlo?

La estructura está preparada, pero el proyecto **todavía no está listo para entrenar un modelo ni producir resultados**:

- [x] Definir el objetivo y preparar la estructura del repositorio.
- [x] Preparar la documentación inicial, los paquetes y los parámetros.
- [ ] Descargar los datos y explorar sus columnas (`notebooks/01_exploracion.ipynb`).
- [ ] Preparar los datos y crear la respuesta de calidad alta (`src/data.py`, `src/features.py`).
- [ ] Entrenar y revisar el modelo (`src/train.py`, `src/evaluate.py`).
- [ ] Obtener respuestas para vinos nuevos (`src/predict.py`).
- [ ] Añadir y ejecutar pruebas (`tests/`).

También se debe recordar que la nota de cata es una valoración humana y que este conjunto solo representa vinos Vinho Verde. El resultado sería una orientación, no una garantía de calidad.

## 8. Fuente de los datos y licencia

Los datos proceden del [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/186/wine+quality). La publicación original es de P. Cortez, A. Cerdeira, F. Almeida, T. Matos y J. Reis, “Modeling wine preferences by data mining from physicochemical properties”, *Decision Support Systems*, 47(4), 547–553, 2009. El conjunto de datos está disponible bajo licencia CC BY 4.0.

El código de este repositorio usa licencia MIT. Autor: Ismael Vargas Duque · Sistemas de aprendizaje automático · Curso 2026/27.
