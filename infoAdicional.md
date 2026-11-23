A continuación tienes el **resumen completo y estructurado de todas las temáticas vistas a lo largo del semestre**, organizadas cronológicamente clase por clase según tus fuentes:

---

### **1. Introducción al Aprendizaje de Máquina (Clase 1)**
* **Fundamentos del paradigma:** Definición formal de Tom Mitchell (Tarea \\(T\\), Experiencia \\(E\\), Medida de desempeño \\(P\\)) y contraste entre *Software 1.0* (programación tradicional basada en reglas) y *Software 2.0* (aprendizaje guiado por datos).
* **Estructura de datos y taxonomía:** Matriz de características (\\(X \in \mathbb{R}^{n \times m}\\)), vector de etiquetas (\\(y\\)), espacio de hipótesis y función de costo.
* **Paradigmas principales:** Aprendizaje supervisado, no supervisado y por refuerzo; distinción entre modelos predictivos e interpretativos.

---

### **2. Regresión Lineal y Optimización (Clase 2)**
* **Formulación del modelo lineal:** Hipótesis \\(h_\theta(x) = \theta^T x\\) para variables continuas.
* **Función de costo:** Error cuadrático medio (MSE / *Mean Squared Error*).
* **Métodos de ajuste:**
  * **Ecuación normal:** Solución analítica exacta \\(\theta = (X^T X)^{-1} X^T y\\) y sus restricciones computacionales.
  * **Descenso de gradiente:** Optimización iterativa, regla de actualización de parámetros y sensibilidad a la tasa de aprendizaje (\\(\alpha\\)).

---

### **3. Regresión Logística y Clasificación (Clase 3)**
* **Modelo probabilístico:** Uso de la función sigmoide/logística \\(g(z) = \frac{1}{1 + e^{-z}}\\) para mapear salidas continuas al rango \\((0, 1)\\).
* **Función de costo:** Log-verosimilitud negativa / entropía cruzada binaria (*Binary Cross-Entropy*).
* **Fronteras de decisión:** Interpretación lineal y no lineal mediante transformaciones polinomiales.
* **Métricas de evaluación para clasificación:** Matriz de confusión, Exactitud (*Accuracy*), Precisión, Sensibilidad/Exhaustividad (*Recall*), puntuación \\(F_1\\), y curvas ROC / AUC.

---

### **4. Diseño Experimental, Sesgo-Varianza y Regularización (Clase 4)**
* **Compromiso Sesgo-Varianza (*Bias-Variance Trade-off*):**
  * **Sesgo alto:** Subajuste (*underfitting*), modelo rígido con error alto en entrenamiento y validación.
  * **Varianza alta:** Sobreajuste (*overfitting*), modelo memoriza ruido con error bajo en entrenamiento pero alto en validación.
* **Metodologías de partición:** Conjuntos de entrenamiento, validación y prueba; validación cruzada (\\(k\\)-fold cross-validation).
* **Técnicas de regularización:**
  * **Ridge (\\(L_2\\)):** Penaliza \\(\sum \theta_j^2\\), contrae los pesos hacia cero sin anularlos.
  * **Lasso (\\(L_1\\)):** Penaliza \\(\sum |\theta_j|\\), induce dispersión (*sparsity*) forzando pesos a cero y funcionando como selector de variables.

---

### **5. Modelos Generativos y Clasificador Naïve Bayes (Clase 5)**
* **Fundamentos probabilísticos:** Regla de Bayes, probabilidades a priori (*priors*), verosimilitud (*likelihood*) y posterior.
* **Modelos discriminativos vs. generativos:** Modelar \\(P(y|x)\\) directamente frente a modelar la distribución conjunta \\(P(x, y) = P(x|y)P(y)\\).
* **Supuesto de independencia condicional Naïve Bayes:** Factorización \\(P(x|y) = \prod P(x_j|y)\\).
* **Variantes y correcciones:** Naïve Bayes Multinomial, Bernoulli y Gaussiano; **suavizado de Laplace** para mitigar el problema de probabilidades nulas.

---

### **6. Raíces del Aprendizaje Profundo: Neurona de McCulloch-Pitts, Perceptrón y Adaline (Clase 6)**
* **Inspiración biológica e historia:** Modelo lógico de McCulloch-Pitts y aprendizaje hebbiano.
* **Perceptrón de Rosenblatt:** Función de activación por umbral/escalón, regla de actualización basada estrictamente en errores de clasificación y prueba de convergencia para datos linealmente separables.
* **Adaline (*Adaptive Linear Neuron*):** Introducción de activación lineal continua antes del umbral, optimización mediante la regla Delta / descenso de gradiente sobre el MSE.

---

### **7. Redes Neuronales Artificiales Poco Profundas (Clase 7)**
* **Limitación histórica:** El problema del XOR y la incapacidad de separar espacios no lineales con una sola capa.
* **Perceptrón Multicapa (MLP):** Propagación hacia adelante (*feedforward*), capas ocultas y funciones de activación no lineales (Sigmoide, Tanh, ReLU).
* **Entrenamiento y retropropagación (*Backpropagation*):** Aplicación rigurosa de la regla de la cadena para derivar el gradiente del costo respecto a los pesos en cada capa.
* **Control de sobreajuste:** Parada temprana (*early stopping*), decaimiento de pesos y mini-batch SGD.

---

### **8. Redes Neuronales Modernas y Aprendizaje Profundo (Clase 8)**
* **Optimizadores avanzados:** Descenso de gradiente con Momento, RMSProp y Adam.
* **Regularización moderna:** *Dropout* y normalización por lotes (*Batch Normalization*).
* **Arquitecturas especializadas:**
  * **Redes Convolucionales (CNN):** Convolución, *pooling* e invariancia espacial para visión por computadora.
  * **Redes Recurrentes (RNN/LSTM/GRU):** Conexiones temporales y control del desvanecimiento del gradiente para secuencias.
* **Modelos de atención y Transformers:** Mecanismo de autoatención (*self-attention*) y fundamentos de modelos fundacionales.

---

### **9. Árboles de Decisión y Métodos de Ensamble (Clase 10)**
* **Árboles de decisión individuales:** Construcción mediante algoritmos voraces (*greedy*) tipo CART/ID3; métricas de impureza (Índice de Gini, Entropía y Ganancia de Información).
* **Familia de Bagging (Reducción de varianza):**
  * *Bagging clásico:* Muestreo uniforme con reemplazo (*bootstrap*) y agregación en paralelo; evaluación *Out-of-Bag* (OOB).
  * *Random Forest:* Muestreo aleatorio adicional de características por partición para forzar la descorrelación entre árboles.
  * *ExtraTrees:* Cortes totalmente aleatorios para minimizar varianza y acelerar cómputo.
* **Familia de Boosting (Reducción secuencial de sesgo):**
  * *AdaBoost:* Re-ponderación adaptativa de instancias mal clasificadas.
  * *Gradient Boosting:* Ajuste sucesivo de estimadores al gradiente negativo de la función de pérdida (pseudo-residuos).
  * *XGBoost:* Optimización con regularización explícita (\\(L_1, L_2\\)) en la función de costo y aproximación de Taylor de segundo orden.
  * *CatBoost:* Manejo nativo de variables categóricas mediante *Ordered Boosting* para prevenir fuga de información (*data leakage*).

---

### **10. Agrupamiento Particional y Jerárquico (Clase 11)**
* **Fundamentos del agrupamiento no supervisado:** Maximizar la separación inter-clúster y minimizar la dispersión intra-clúster.
* **K-Means:** Algoritmo de partición con asignación a centroides euclidianos más cercanos y actualización por media aritmética; variantes como K-Means++.
* **Métricas de selección de \\(k\\) y validación:** Método del codo (SSE), coeficiente de Silueta y criterios de separación/compactación (Davies-Bouldin).
* **Agrupamiento Jerárquico Aglomerativo (Dendrogramas):**
  * Construcción de la matriz de distancias paso a paso.
  * Métodos de vínculo (*linkage*): Vínculo simple (*Single*), completo (*Complete*), promedio (*Average*), centroide y método de Ward.

---

### **11. Modelos Basados en Densidad y Modelos de Mezclas Gaussianas (Clase 12)**
* **Agrupamiento basado en densidad:**
  * **DBSCAN:** Parámetros radio \\(\text{Eps}\\) y densidad mínima \\(\text{MinPts}\\); categorización formal de puntos en Núcleo (*Core*), Borde (*Border*) y Ruido (*Noise*); manejo de formas arbitrarias.
  * **HDBSCAN:** Extensión jerárquica con distancia de alcanzabilidad mutua (*mutual reachability*) para densidades variables.
* **Modelos de Mezcla Gaussiana (GMM):**
  * Agrupamiento probabilístico suave (*soft clustering*).
  * Algoritmo de Esperanza-Maximización (EM) para estimar pesos de mezcla, vectores de medias y matrices de covarianza.

---

### **12. Reducción de Dimensionalidad y Extracción de Características: PCA (Clase 13)**
* **La maldición de la dimensionalidad:** Pérdida de densidad espacial y dispersión de distancias en dimensiones altas.
* **Selección vs. Extracción:** Métodos de filtro/envoltorio frente a proyecciones lineales ortogonales.
* **Análisis de Componentes Principales (PCA):**
  * Necesidad obligatoria de centrado y estandarización (\\(Z\\)-score).
  * Descomposición espectral de la matriz de covarianza: \\(C u = \lambda u\\).
  * Eigenvectores (dirección de máxima variabilidad / cargas factoriales) y Eigenvalores (magnitud de la varianza explicada).
  * Proyección mediante producto punto (\\(z = X \cdot u\\)) y análisis de varianza acumulada.
  * Naturaleza no supervisada de PCA y sus limitaciones para clasificación supervisada.

---

### **13. Máquinas de Soporte Vectorial: Formulación Primal (Clase 14)**
* **Principio del Máximo Margen:** Búsqueda del hiperplano de separación óptimo \\(w^T x + b = 0\\).
* **Márgenes:** Margen funcional (\\(\hat{\gamma}\\)) vs. margen geométrico perpendicular (\\(\gamma = 1/\|w\|\\)).
* **Optimización de Margen Duro (*Hard Margin*):** Problema cuadrático convexo \\(\min \frac{1}{2}\|w\|^2\\) sujeto a \\(y^{[i]}(w^T x^{[i]} + b) \ge 1\\); propiedades de los vectores de soporte.
* **Optimización de Margen Suave (*Soft Margin*):**
  * Inclusión de variables de holgura (\\(\xi^{[i]}\\)) para tolerar violaciones del margen.
  * Función de pérdida *Hinge Loss* y penalización mediante el hiperparámetro \\(C\\).

---

### **14. Máquinas de Soporte Vectorial con Kernels: Formulación Dual (Clase 15)**
* **Dualidad de Lagrange y condiciones KKT:** Construcción del Lagrangiano, holgura complementaria (\\(\alpha_i g_i(w) = 0\\)) y demostración de por qué los vectores de soporte son los únicos con \\(\alpha_i > 0\\).
* **Problema dual de SVM:** Expresión matemática que demuestra que el entrenamiento y la inferencia dependen **exclusivamente de productos internos** \\(\langle x^{[i]}, x^{[j]} \rangle\\), con cotas \\(0 \le \alpha_i \le C\\).
* **El Truco del Kernel (*Kernel Trick*):** Mapeo implícito a espacios de mayor dimensión mediante \\(K(x, z) = \langle \phi(x), \phi(z) \rangle\\) sin calcular explícitamente \\(\phi(x)\\) (Teorema de Mercer).
* **Familias de Kernels y complejidad:** Kernel lineal, polinomial y RBF/Gaussiano (espacio de dimensión infinita), analizando el impacto del parámetro \\(\gamma\\) en el compromiso sesgo-varianza.

---
