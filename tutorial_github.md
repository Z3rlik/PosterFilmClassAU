# PosterFilmClassAI 🎬 - Guía de Colaboración (Git Flow y Convenciones)

Este documento explica la estructura de ramas y el flujo de trabajo que debemos seguir para mantener el repositorio limpio, estable y listo para el despliegue, además de establecer reglas para nombrar archivos y carpetas.

---

## 🌳 1. Estructura de Ramas (La Jerarquía)

Nuestra estrategia de Git Flow se basa en dos principios clave: **Aislamiento** y **Estabilidad**.

| Rama | Propósito | Regla Clave |
| :--- | :--- | :--- |
| **`main`** | **Producción.** Código **desplegado** y estable. | Solo recibe *merges* desde `develop`. **Nunca** hagas commits directos. |
| **`develop`** | **Integración.** Base de trabajo donde se unen todas las características. | Da origen a todas las ramas `feature/` y recibe sus *merges*. **Nunca** hagas commits directos. |
| **`feature/*`** | **Tareas Específicas.** Implementar una funcionalidad (ej: `feature/model-training`). | Se crean desde `develop` y se fusionan de vuelta a `develop` vía **Pull Request (PR)**. |

---

## 🔄 2. Guía de Flujo de Trabajo (El Proceso Paso a Paso)

Sigue estos pasos cada vez que comiences a trabajar en una nueva tarea:

1.  **Actualiza `develop`:** `git checkout develop` $\rightarrow$ `git pull origin develop`
2.  **Crea tu Rama de Tarea:** `git checkout -b feature/nombre-descriptivo`
3.  **Trabaja y Haz Commits:** Implementa tu característica con *commits* frecuentes y mensajes claros (ver sección 4).
4.  **Sube tu Trabajo:** `git push origin feature/nombre-descriptivo`
5.  **Inicia el Pull Request (PR):** Ve a GitHub y crea un PR desde tu rama de tarea hacia **`develop`**.
6.  **Revisión y Fusión:** Una vez aprobado, tu código se fusiona a `develop`.
7.  **Despliegue:** El *merge* final de **`develop` a `main`** se usa para lanzar la nueva versión en producción.

---

## 📂 3. Estructura de Carpetas

Mantendremos una estructura clara para aislar datos, modelos y código principal.

| Carpeta | Contenido | Propósito |
| :--- | :--- | :--- |
| **`data/`** | Imágenes de pósters, archivos de etiquetas (CSV/JSON), datos preprocesados. | Almacenamiento y gestión de los datos brutos y limpios. |
| **`models/`** | Archivos del modelo entrenado (`.h5`, `.pth`), *checkpoints*. | Repositorio para guardar y cargar las versiones del clasificador. |
| **`notebooks/`** | Archivos `.ipynb` de experimentación, análisis EDA. | Documentación y pruebas de concepto. |
| **`src/`** | Código Python reusable (clases, funciones, *pipelines*). | Módulos principales del proyecto (ej: `src/model.py`, `src/utils.py`). |
| **`app.py`** | El archivo principal de la interfaz web (Streamlit). | El punto de entrada para la aplicación desplegada. |

---

## 📜 4. Convenciones de Nomenclatura y Commits

La consistencia hace que el proyecto sea legible y fácil de mantener.

### a) Nombres de Archivos y Carpetas (Snake Case)

Utilizaremos **snake\_case** (minúsculas y guiones bajos) para todos los nombres de archivos y carpetas, incluyendo módulos de Python.

| Elemento | Regla | Ejemplo Correcto | Ejemplo Incorrecto |
| :--- | :--- | :--- | :--- |
| **Archivos de Python** | `snake_case.py` | `model_training.py` | `ModelTraining.py` |
| **Carpetas** | `snake_case/` | `data_raw/` | `DataRaw/` |
| **Archivos de Config.** | `kebab-case.txt` | `requirements.txt` | `requirementsTXT` |

### b) Nombres de Variables, Funciones y Clases

| Elemento | Regla | Ejemplo Correcto |
| :--- | :--- | :--- |
| **Variables/Funciones** | `snake_case` | `imagen_preprocesada`, `entrenar_modelo()` |
| **Constantes (Globales)**| `CAPS_SNAKE_CASE` | `GENERO_ACCION`, `BATCH_SIZE = 32` |
| **Clases** | `PascalCase` | `ClasificadorCNN`, `DataLoader` |

### c) Mensajes de Commit (Conventional Commits)

Utilizaremos el formato **Conventional Commits** para categorizar el trabajo en el historial de Git, facilitando la comprensión de los cambios.

**Formato:** `<tipo>: <descripción concisa>`

| Tipo | Descripción | Ejemplo |
| :--- | :--- | :--- |
| **`feat`** | Una nueva característica. | `feat: Añadida la lógica de inferencia del modelo en app.py` |
| **`fix`** | Una corrección de *bug*. | `fix: Corregido el error en el preprocesamiento de imágenes` |
| **`docs`** | Cambios en la documentación (README, comentarios). | `docs: Actualizado el README con la estructura de carpetas` |
| **`style`** | Cambios que no afectan la lógica (formato, espaciado). | `style: Formateado el código según PEP8` |
| **`refactor`** | Cambio de código que no añade *feature* ni arregla *bug*. | `refactor: Mover la clase DataLoader a src/utils.py` |
| **`test`** | Añadir o corregir pruebas. | `test: Añadidos tests unitarios para la función de clasificación` |