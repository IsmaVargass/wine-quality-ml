# Decisiones de diseño

- **Datos separados por etapa:** `data/raw/` conserva los ficheros originales; `data/interim/` y `data/processed/` reservan espacio para transformaciones reproducibles sin mezclar resultados con las fuentes.
- **Código en `src/` y parámetros en `configs/`:** separa la lógica reutilizable de rutas, umbrales y opciones del modelo.
- **Notebooks para explorar, no para ejecutar el flujo principal:** los análisis experimentales irán en `notebooks/`; el proceso reutilizable se organizará en scripts de `src/`.
- **Modelos y CSV fuera del control de versiones:** son artefactos generados o datos de entrada; `.gitignore` los excluye y los `.gitkeep` conservan la estructura vacía.
- **Documentación y pruebas explícitas:** `docs/` concentra las decisiones y el diccionario; `tests/` queda reservado para las pruebas unitarias.
- **Clasificación binaria:** se considera de calidad alta una puntuación de catadores igual o superior a 7. El umbral es configurable y la separación de datos se plantea estratificada.

El repositorio es una estructura inicial: los módulos de `src/` describen responsabilidades previstas, pero el flujo de entrenamiento y predicción aún no está implementado.