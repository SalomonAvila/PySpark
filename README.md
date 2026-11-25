# Computación de Alto Rendimiento (HPC): clasificación con Spark MLlib sobre Hadoop HDFS

Trabajos de la asignatura **Computación de Alto Rendimiento (HPC)** de la Maestría en Inteligencia Artificial.
Cada cuaderno resuelve un problema de **clasificación binaria supervisada** con **PySpark** y **MLlib**
(`pyspark.ml`), leyendo los datos desde **Hadoop HDFS**. Los dos siguen la metodología **CRISP-DM**.

**Autor:** Avila Larrotta

## Contenido

```
.
├── CensusIncome/
│   └── AvilaSalario.ipynb   # Predicción de ingresos > 50K USD (UCI Adult / Census Income)
├── ICTUS/
│   └── AvilaIctus.ipynb     # Predicción de ictus (Stroke Prediction Dataset)
├── adult.data               # Census Income: partición de entrenamiento original de UCI (32 561 registros)
└── adult.test               # Census Income: partición de prueba original de UCI (16 281 registros)
```

| Proyecto | Dataset | Registros | Variable objetivo | Desbalance |
|---|---|---|---|---|
| [Census Income](CensusIncome/AvilaSalario.ipynb) | UCI Adult (censo de EE. UU. de 1994) | ≈ 48 842 (`adult.data` + `adult.test`) | `income`: `>50K` / `<=50K` | Moderado (≈ 24 / 76) |
| [ICTUS](ICTUS/AvilaIctus.ipynb) | Stroke Prediction Dataset | 5 110 | `stroke`: 1 / 0 | Fuerte (≈ 5 / 95) |

## Estructura de los cuadernos

Los dos cuadernos tienen las mismas secciones:

| Fase CRISP-DM | Sección |
|---|---|
| Comprensión del negocio | Contexto (con la formulación T/E/P de Tom Mitchell) y Objetivos |
| Comprensión de los datos | **1. Conocimiento de datos**: sesión de Spark, carga desde HDFS, diccionario de datos, calidad y análisis exploratorio |
| Preparación de los datos | **2. Preparación de datos**: limpieza, imputación, ingeniería de variables, `StringIndexer` + `OneHotEncoder`, `VectorAssembler`, partición estratificada, tratamiento del desbalance y `StandardScaler` |
| Modelado | **3. Modelos de MLlib** |
| Evaluación | **4. Evaluación de modelos** y **5. Análisis de resultados** |
| Despliegue (recomendación) | **6. Conclusiones** |

### Modelos entrenados (sección 3)

- Regresión Logística, sin balanceo (línea base) y con pesos por clase
- Árbol de Decisión
- Random Forest
- Gradient-Boosted Trees (GBT)
- Máquina de Soporte Vectorial lineal (`LinearSVC`)
- Perceptrón Multicapa
- Naive Bayes Gaussiano y Multinomial con suavizado de Laplace
- SVM con expansión polinómica explícita (aproximación a un kernel polinomial)
- Ridge, Lasso y Elastic Net ajustados con validación cruzada *k-fold* (`CrossValidator` + `ParamGridBuilder`)

### Evaluación y temas complementarios (sección 4)

- Tabla comparativa con accuracy, precisión, *recall* y F1 de la clase positiva, especificidad, AUC-ROC y AUC-PR
- Curvas ROC y Precisión–Recall, matrices de confusión
- Importancia de variables y coeficientes
- Ajuste del umbral de decisión
- Diagnóstico sesgo–varianza (curva de complejidad del árbol y curva de pérdida del GBT)
- Lasso como selector de variables
- Del perceptrón al MLP: efecto de la arquitectura y del optimizador (`l-bfgs` frente a `gd`)
- Reducción de dimensionalidad con PCA
- Agrupamiento no supervisado: K-Means, Bisecting K-Means y Mezclas Gaussianas (GMM)

## Entorno de ejecución

Los cuadernos están hechos para el clúster del curso y no corren tal cual en otra máquina.

| Componente | Valor en el clúster |
|---|---|
| JupyterHub | `10.195.34.34:8000` |
| HDFS (NameNode) | `hdfs://10.195.34.34:9000` |
| Spark | `/mnt/sda1/Cluster/Spark/` (se carga con `findspark.init`) |
| Hadoop | `/mnt/sda1/Cluster/Hadoop/` |
| Puerto de la Spark UI | `37001` |
| Kernel | `rapKernel_v4` (Python 3.12) |

Bibliotecas de Python: `pyspark`, `findspark`, `numpy`, `pandas`, `matplotlib`, `seaborn` y `scikit-learn`
(solo para trazar las curvas ROC y PR a partir de las probabilidades de Spark).

### Datos en HDFS

| Proyecto | Ruta |
|---|---|
| Census Income | `/FormatosHPC/Avila/TallerModelosClasificacion/adult.data` y `adult.test` |
| ICTUS | `/csv/stroke_pyspark.csv` |

El cuaderno de Census Income también guarda el DataFrame preparado en Parquet, en
`/FormatosHPC/Avila/TallerModelosClasificacion/Parquet`.

Para subir los archivos del censo a HDFS desde la raíz del repositorio:

```bash
/mnt/sda1/Cluster/Hadoop/bin/hadoop fs -mkdir -p /FormatosHPC/Avila/TallerModelosClasificacion
/mnt/sda1/Cluster/Hadoop/bin/hadoop fs -put -f adult.data adult.test /FormatosHPC/Avila/TallerModelosClasificacion/
```

### Ejecutar en otro entorno

Hay que ajustar tres cosas al principio de cada cuaderno (sección 1.1 y 1.2):

1. La ruta de `findspark.init(...)`, o quitarla si `pyspark` está instalado con `pip`.
2. El puerto `spark.ui.port` en la `SparkConf`.
3. `urlAvila`: la ruta HDFS o local de los datos. Para Census Income se pueden usar directamente los archivos
   `adult.data` y `adult.test` de este repositorio.

Al final de cada cuaderno se libera la caché y se detiene la sesión de Spark para devolver los recursos al clúster.

## Fuentes de datos

- **Census Income (Adult):** Ronny Kohavi y Barry Becker, UCI Machine Learning Repository.
  <https://archive.ics.uci.edu/dataset/2/adult>
- **Stroke Prediction Dataset:** el archivo `stroke_pyspark.csv` se toma del DataLake del clúster del curso y no está en este repositorio.
