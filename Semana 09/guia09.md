# GUÍA DE LABORATORIO N° 09: Modelos de k-vecinos y arboles con Scikit-learn
>Intitución                 |Universidad Nacional del Centro del Perú   |
>-------------------------  | ------------------------------            |
>**Programa de Estudios:**  | Ingeniería de Sistemas                    |
>**Asignatura:**            | Ingeniería de Datos            |
>**Docente:**               | Dr. Jaime Suasnábar Terrel                    |
>**Semestre:**              | X                                        |
>**Instrucciones:**              | Desarrollar el laboratorio en Google Colab, utilizando la librería Scikit-learn para implementar los modelos de clasificación. Documentar cada paso con comentarios y explicar los resultados obtenidos. Duración: 85min                   |

### I. OBJETIVOS
> | Comprender el funcionamiento de los algoritmos de K-vecinos más cercanos (K-NN) y árboles de decisión aplicados a problemas de clasificación.                        |
> |--------------------------------------------------|
> | Implementar y evaluar modelos de Bagging y Random Forest como técnicas de ensamble que mejoran la precisión y estabilidad de los clasificadores.                   |
> | Analizar y comparar métricas de desempeño (exactitud, matriz de confusión, reporte de clasificación) entre los distintos modelos.                                   |
> | Interpretar la importancia de las variables en los modelos de árboles y bosques aleatorios.             |
> | Desarrollar habilidades prácticas en el uso de Scikit-learn para la construcción, entrenamiento y validación de modelos de aprendizaje supervisado.               |

### II. FUNDAMENTO TEÓRICO

#### 2.1. K-vecinos más cercanos (K-NN)
El algoritmo de **K-Nearest Neighbors (K-NN)** es uno de los métodos más simples y efectivos para problemas de clasificación.  
Se basa en la idea de que los datos similares se encuentran cerca en el espacio de características.  
Cuando se presenta un nuevo ejemplo, el algoritmo busca los **K vecinos más cercanos** y asigna la clase más frecuente entre ellos.

**Características:**
- No requiere un modelo explícito, es un método basado en instancias.  
- La elección del parámetro **K** es crucial: valores pequeños pueden generar sobreajuste, mientras que valores grandes pueden suavizar demasiado la clasificación.  
- Utiliza métricas de distancia (Euclidiana, Manhattan, etc.) para determinar la cercanía entre puntos.  

**Ventajas:** sencillo de implementar y eficaz en datasets pequeños.  
**Desventajas:** puede ser costoso en tiempo de cómputo para grandes volúmenes de datos.  

---

#### 2.2. Modelos de Árboles de Decisión
Los **árboles de decisión** son modelos predictivos que representan decisiones en forma de estructura jerárquica.  
Cada nodo interno corresponde a una condición sobre un atributo, y cada hoja representa una clase o valor de salida.

**Características:**
- Se construyen mediante algoritmos como **ID3, C4.5, CART**, que seleccionan atributos en función de medidas como la **ganancia de información** o el **índice Gini**.  
- Son fáciles de interpretar y visualizar, lo que los hace útiles en contextos educativos y de análisis exploratorio.  
- Pueden manejar tanto variables categóricas como numéricas.  

**Ventajas:** interpretabilidad y rapidez en la clasificación.  
**Desventajas:** tienden a sobreajustarse si no se aplican técnicas de poda o regularización.  

---

#### 2.3. Métodos de Bagging
El **Bagging (Bootstrap Aggregating)** es una técnica de ensamble que busca mejorar la estabilidad y precisión de los modelos.  
Consiste en entrenar múltiples clasificadores sobre diferentes subconjuntos del dataset obtenidos mediante muestreo con reemplazo, y luego combinar sus predicciones.

**Características:**
- Reduce la varianza del modelo, evitando que dependa demasiado de un solo conjunto de datos.  
- Se aplica comúnmente a modelos inestables como los árboles de decisión.  
- La predicción final se obtiene mediante votación (clasificación) o promedio (regresión).  

**Ventajas:** mejora la robustez y disminuye el riesgo de sobreajuste.  
**Desventajas:** aumenta el costo computacional al entrenar múltiples modelos.  

---

#### 2.4. Bosque Aleatorio (Random Forest)
El **Random Forest** es una extensión del Bagging que introduce mayor aleatoriedad en la construcción de los árboles.  
En cada división del árbol, se selecciona aleatoriamente un subconjunto de atributos, lo que genera diversidad entre los modelos.

**Características:**
- Combina cientos de árboles de decisión entrenados sobre diferentes muestras y atributos.  
- La clasificación final se obtiene mediante votación mayoritaria entre los árboles.  
- Permite calcular la **importancia de las variables**, lo que ayuda a identificar los atributos más relevantes en el dataset.  

**Ventajas:** alta precisión, resistencia al sobreajuste y capacidad de manejar grandes volúmenes de datos.  
**Desventajas:** menor interpretabilidad que un árbol individual y mayor demanda de recursos computacionales.  

### III. EJERCICIOS DE LABORATORIO
La Facultad de Ingeniería de Sistemas necesita clasificar correctamente las especies de flores del dataset Iris en base a sus características morfológicas (longitud y ancho de sépalo y pétalo).

### Ejercicio 01: Implementar modelos de K-vecinos más cercanos (K-NN) y Árboles de decisión

#### Paso 1: Importar librerías necesarias
```python
import pandas as pd
import numpy as np
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
```
#### Paso 2: Cargar el dataset Iris
```python
# Cargar dataset Iris
iris = load_iris()
X = iris.data
y = iris.target

# Convertir a DataFrame para análisis
df = pd.DataFrame(X, columns=iris.feature_names)
df['target'] = y
df.head()
```
#### Paso 3: Dividir el dataset en entrenamiento y prueba
```python
# División en 70% entrenamiento y 30% prueba
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)
```
#### Paso 4: Implementar el modelo K-NN
```python
# Crear modelo K-NN con k=5
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train, y_train)

# Predicciones
y_pred_knn = knn.predict(X_test)

# Evaluación
print("Exactitud K-NN:", accuracy_score(y_test, y_pred_knn))
print("Matriz de confusión K-NN:\n", confusion_matrix(y_test, y_pred_knn))
print("Reporte de clasificación K-NN:\n", classification_report(y_test, y_pred_knn))
```
#### Paso 5: Implementar el modelo Árbol de decisión
```python
# Crear modelo Árbol de decisión
tree = DecisionTreeClassifier(random_state=42)
tree.fit(X_train, y_train)

# Predicciones
y_pred_tree = tree.predict(X_test)

# Evaluación
print("Exactitud Árbol de decisión:", accuracy_score(y_test, y_pred_tree))
print("Matriz de confusión Árbol de decisión:\n", confusion_matrix(y_test, y_pred_tree))
print("Reporte de clasificación Árbol de decisión:\n", classification_report(y_test, y_pred_tree))
```
#### Paso 6: Comparar resultados
> Revisar las métricas de exactitud de ambos modelos.
>
> Analizar las matrices de confusión para identificar qué clases se clasifican mejor o peor.
> 
> Observar si el Árbol de decisión sobreajusta (exactitud muy alta en entrenamiento pero menor en prueba).
>

### Ejercicio 02: Aplicar métodos de ensamble (Bagging y Random Forest)

#### Paso 1: Importar librerías necesarias
```python
from sklearn.ensemble import BaggingClassifier, RandomForestClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
```
#### Paso 2: Entrenar un modelo de Bagging con Árboles de decisión
```python
# Modelo base: Árbol de decisión
base_tree = DecisionTreeClassifier(random_state=42)

# Bagging con 50 estimadores
bagging = BaggingClassifier(
    base_estimator=base_tree,
    n_estimators=50,
    random_state=42
)

# Entrenamiento
bagging.fit(X_train, y_train)

# Predicciones
y_pred_bagging = bagging.predict(X_test)

# Evaluación
print("Exactitud Bagging:", accuracy_score(y_test, y_pred_bagging))
print("Matriz de confusión Bagging:\n", confusion_matrix(y_test, y_pred_bagging))
print("Reporte de clasificación Bagging:\n", classification_report(y_test, y_pred_bagging))
```

#### Paso 3: Entrenar un modelo de Random Forest
```python
# Random Forest con 100 árboles
rf = RandomForestClassifier(n_estimators=100, random_state=42)
rf.fit(X_train, y_train)

# Predicciones
y_pred_rf = rf.predict(X_test)

# Evaluación
print("Exactitud Random Forest:", accuracy_score(y_test, y_pred_rf))
print("Matriz de confusión Random Forest:\n", confusion_matrix(y_test, y_pred_rf))
print("Reporte de clasificación Random Forest:\n", classification_report(y_test, y_pred_rf))
```
#### Paso 4: Analizar la importancia de las variables en Random Forest
```python
import matplotlib.pyplot as plt

# Importancia de las características
importances = rf.feature_importances_
features = iris.feature_names

# Gráfico de importancia
plt.barh(features, importances)
plt.xlabel("Importancia")
plt.ylabel("Características")
plt.title("Importancia de las variables en Random Forest")
plt.show()
```
#### Paso 5: Comparar resultados con los modelos individuales del Ejercicio 01
> Revisar las métricas de exactitud de Bagging y Random Forest frente a K-NN y Árbol de decisión.
> 
> Observar cómo el Bagging reduce la varianza del Árbol de decisión.
> 
> Analizar cómo el Random Forest mejora la precisión y permite interpretar la relevancia de las variables
>

### Ejercicio 03: Evaluar y comparar el desempeño de los modelos utilizando métricas de clasificación
- Calcular métricas de desempeño: **exactitud, matriz de confusión y reporte de clasificación**.  
- Representar gráficamente los resultados para facilitar la interpretación.  
- Comparar el rendimiento de K-NN, Árboles de decisión, Bagging y Random Forest.  

---

### Ejercicio 04: Presentar conclusiones sobre cuál modelo resulta más robusto
- Redactar un informe breve con las conclusiones del laboratorio.  
- Indicar qué modelo ofrece mayor precisión y estabilidad.  
- Justificar la elección con base en las métricas y gráficas obtenidas. 