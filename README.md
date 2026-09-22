# lube-match

Sistema de recomendación de lubricantes industriales basado en métodos multivariados.

Dada la hoja técnica de un producto de la competencia, el sistema identifica los productos del catálogo del socio formador más parecidos, respetando restricciones de uso (por ejemplo, uso en agua o contacto con alimentos) y la jerarquía de características definida con el socio.

Proyecto del reto de la materia **Análisis de métodos multivariados para la ciencia de datos**, Tecnológico de Monterrey.

> ⚠️ **Datos confidenciales.** La base de datos y las hojas técnicas son propiedad del socio formador. **Nunca** se suben al repositorio. Ver [Reglas del equipo](#reglas-del-equipo).

---

## Estado del proyecto

- [x] Estructura base del repositorio
- [ ] Recepción de la base de datos y diccionario de variables
- [ ] Análisis exploratorio (EDA)
- [ ] Reducción de dimensionalidad (PCA)
- [ ] Clustering y comparación multivariado vs. univariado
- [ ] Motor de recomendación (filtros duros + similitud ponderada)
- [ ] Evaluación (estabilidad y, si hay casos históricos, acierto en top-k)
- [ ] App en Streamlit (vista usuario + vista científico de datos)

---

## Estructura

```
lube-match/
├── data/                 # NO se sube (ignorada por git)
│   ├── raw/              # datos originales tal como llegan
│   └── processed/        # datos limpios
├── notebooks/            # exploración: EDA, PCA, clustering
├── src/                  # código reutilizable
│   ├── preprocessing.py  # limpieza, estandarización, filtros duros
│   ├── recommender.py    # distancias, pesos, top-k
│   └── evaluation.py     # métricas: ARI, Jaccard, silhouette, bootstrap
├── app/
│   └── streamlit_app.py  # interfaz: pestaña usuario + pestaña DS
├── docs/
│   └── diccionario.md    # glosario de variables y pruebas
├── requirements.txt
└── README.md
```

**Flujo de trabajo:** se explora en `notebooks/` → lo que funciona se convierte en función dentro de `src/` → los notebooks y la app importan desde `src/`.

---

## Instalación

Requisitos: Python 3.10 o superior y Git.

### Mac / Linux

```bash
git clone https://github.com/KibaSpark/lube-match.git
cd lube-match
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
nbstripout --install
```

### Windows (PowerShell)

```powershell
git clone https://github.com/KibaSpark/lube-match.git
cd lube-match
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
nbstripout --install
```

Si PowerShell no deja activar el entorno, correr una sola vez:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

### ⚠️ Paso obligatorio: `nbstripout --install`

Este comando borra los outputs de los notebooks al hacer commit, para que **no se suban tablas ni gráficas con datos del socio**. No basta con tenerlo en `requirements.txt`: cada persona debe correrlo **una vez** después de clonar.

Para verificar que quedó activo:

```bash
git config --get filter.nbstripout.clean
```

Si imprime algo, está bien. Si no imprime nada, falta correr `nbstripout --install`.

### Datos

Pedir los archivos al equipo y colocarlos manualmente en `data/raw/`. No se descargan del repositorio.

---

## Configurar el editor

**DataSpell / PyCharm:** Settings → Python Interpreter → Add → Existing → seleccionar `lube-match/.venv/bin/python` (en Windows: `.venv\Scripts\python.exe`).

**VS Code:** instalar las extensiones *Python* y *Jupyter* de Microsoft. Abrir la carpeta `lube-match`, presionar `Ctrl+Shift+P` (`Cmd+Shift+P` en Mac) → *Python: Select Interpreter* → elegir el de `.venv`.

---

## Correr la app

Con el entorno activado:

```bash
streamlit run app/streamlit_app.py
```

Se abre en el navegador en `http://localhost:8501`.

---

## Reglas del equipo

1. **Los datos nunca se suben.** Todo lo del socio vive en `data/`, que está en el `.gitignore`. Antes de cada commit, revisar `git status`.
2. **Activar el entorno antes de trabajar.** Si aparece `(.venv)` al inicio de la terminal, vas bien.
3. **Un notebook, un dueño.** Para experimentar sobre el notebook de alguien más, hacer una copia con tu nombre (`02_pca_nombre.ipynb`).
4. **Si instalas una librería nueva,** actualiza las dependencias y súbelas:
   ```bash
   pip freeze > requirements.txt
   ```
5. **Antes de empezar a trabajar,** trae los cambios del equipo:
   ```bash
   git pull
   ```
6. **Commits pequeños y con mensaje claro**, en español: `"Agrega PCA por familia de producto"`, no `"cambios"`.

---

## Equipo

| Nombre | Rol principal |
|--------|---------------|
| Oscar  |               |
|        |               |
|        |               |
|        |               |
