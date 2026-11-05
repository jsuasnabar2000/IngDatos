# GUÍA DE LABORATORIO N.° 07: Modelos No Supervisados con Scikit-learn

> Institución | Universidad Nacional del Centro del Perú |
> ------------------------- | ------------------------------ |
> **Programa de Estudios:** | Ingeniería de Sistemas |
> **Asignatura:** | Ingeniería de Datos |
> **Docente:** | Dr. Jaime Suasnábar Terrel |
> **Semestre:** | X |
> **Instrucciones:** | Desarrollar el laboratorio en Google Colab utilizando Scikit-learn, Pandas, NumPy, Matplotlib y Seaborn. Documentar cada paso mediante comentarios en el código y analizar críticamente los resultados obtenidos. Duración: 85 min. |

<br><br>

### I. OBJETIVOS

> | Comprender los fundamentos de los modelos de aprendizaje no supervisado aplicados al descubrimiento de patrones en datos reales. |
> |--------------------------------------------------|
> | Aplicar el Análisis de Componentes Principales (PCA) para reducir la dimensionalidad de los datos preservando la mayor cantidad posible de información. |
> | Implementar técnicas de agrupamiento K-Means para identificar segmentos homogéneos dentro de un conjunto de datos. |
> | Aplicar agrupamiento jerárquico y analizar las relaciones existentes mediante dendrogramas. |
> | Utilizar modelos de mezcla gaussiana (Gaussian Mixture Models) como técnica de agrupamiento basada en modelos probabilísticos. |
> | Interpretar y comparar resultados obtenidos por diferentes algoritmos de agrupamiento utilizando métricas y visualizaciones. |

<br><br>

### II. FUNDAMENTO TEÓRICO

<br><br>

#### 2.1. Aprendizaje No Supervisado

El **aprendizaje no supervisado** (*Unsupervised Learning*) comprende técnicas que permiten descubrir patrones ocultos en conjuntos de datos que no poseen una variable objetivo o etiqueta.

Su objetivo principal consiste en identificar estructuras subyacentes en los datos, agrupaciones naturales, relaciones entre variables o representaciones compactas de la información disponible.

<br>

**Principales aplicaciones:**

- Segmentación de clientes.
- Detección de anomalías.
- Sistemas de recomendación.
- Bioinformática.
- Análisis exploratorio de datos.
- Minería de textos.

<br>

**Ventajas:** permite descubrir conocimiento oculto sin necesidad de datos etiquetados.

**Desventajas:** la interpretación de los resultados suele ser más subjetiva que en los modelos supervisados.

<br><br>

---

<br><br>

#### 2.2. Análisis de Componentes Principales (PCA)

El **Principal Component Analysis (PCA)** es una técnica de reducción de dimensionalidad que transforma un conjunto de variables correlacionadas en un nuevo conjunto de variables ortogonales denominadas componentes principales.

Cada componente principal explica una parte de la variabilidad total presente en los datos.

<br>

**Características:**

- Reduce el número de variables.
- Elimina redundancia de información.
- Facilita la visualización de datos multidimensionales.
- Conserva la mayor cantidad posible de variabilidad.

<br>

**Ventajas:** mejora el rendimiento computacional y facilita el análisis exploratorio.

**Desventajas:** puede dificultar la interpretación de las variables originales.

<br><br>

---

<br><br>

#### 2.3. Agrupación K-Means

El algoritmo **K-Means** es una técnica de particionamiento que divide las observaciones en \(K\) grupos.

Cada observación pertenece al grupo cuyo centroide se encuentra más próximo.

<br>

**Características:**

- Utiliza distancias para formar grupos.
- Requiere definir previamente el número de clusters.
- Es uno de los algoritmos de clustering más utilizados.

<br>

**Ventajas:** rápido, simple y escalable.

**Desventajas:** sensible a valores atípicos y a la selección inicial de centroides.

<br><br>

---

<br><br>

#### 2.4. Agrupación Jerárquica

La agrupación jerárquica construye una estructura de grupos organizados en forma de árbol.

Su representación gráfica se realiza mediante un **dendrograma**.

<br>

**Características:**

- No requiere especificar inicialmente el número de grupos.
- Permite visualizar relaciones jerárquicas entre observaciones.
- Puede ser aglomerativa o divisiva.

<br>

**Ventajas:** alta interpretabilidad.

**Desventajas:** elevado costo computacional para grandes volúmenes de datos.

<br><br>

---

<br><br>

#### 2.5. Agrupación Basada en Modelos

Los métodos de agrupación basados en modelos asumen que los datos fueron generados a partir de una combinación de distribuciones probabilísticas.

Uno de los enfoques más utilizados es **Gaussian Mixture Models (GMM)**.

<br>

**Características:**

- Cada grupo se modela mediante una distribución gaussiana.
- Permite pertenencia probabilística a varios grupos.
- Utiliza el algoritmo Expectation-Maximization (EM).

<br>

**Ventajas:** flexible para modelar grupos con diferentes formas y tamaños.

**Desventajas:** mayor complejidad matemática y computacional.

<br><br>

### III. CASO DE ESTUDIO

La empresa de transporte interprovincial **CentroBus Peru S.A.C.** desea analizar los patrones de viaje de sus pasajeros en la región central del Perú.

Se dispone de información histórica de usuarios con las siguientes variables:

- Edad del pasajero.
- Frecuencia mensual de viajes.
- Gasto promedio mensual (S/).
- Distancia promedio recorrida (km).
- Número de compras realizadas mediante la aplicación móvil.

El objetivo es identificar perfiles de pasajeros utilizando técnicas de aprendizaje no supervisado para diseñar campañas diferenciadas de fidelización.

Para efectos académicos se generará un conjunto de datos sintético basado en características representativas del mercado peruano.

<br><br>

### Ejercicio 01: Reducción de dimensionalidad mediante PCA

<br><br>

#### Paso 1: Importar librerías

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
```

#### Paso 2: Generar el dataset

```python
np.random.seed(42)

datos = pd.DataFrame({
    "edad": np.random.randint(18, 65, 300),
    "frecuencia_viajes": np.random.randint(1, 15, 300),
    "gasto_mensual": np.random.randint(80, 1200, 300),
    "distancia_km": np.random.randint(20, 550, 300),
    "compras_app": np.random.randint(0, 20, 300)
})

datos.head()
```

#### Paso 3: Estandarizar variables

```python
scaler = StandardScaler()

X_scaled = scaler.fit_transform(datos)
```

#### Paso 4: Aplicar PCA

```python
pca = PCA()

X_pca = pca.fit_transform(X_scaled)
```

#### Paso 5: Analizar varianza explicada

```python
varianza = pca.explained_variance_ratio_

print(varianza)
print(varianza.cumsum())
```

#### Paso 6: Graficar varianza acumulada

```python
plt.figure(figsize=(8,5))

plt.plot(
    np.cumsum(varianza),
    marker='o'
)

plt.xlabel("Número de componentes")
plt.ylabel("Varianza acumulada")
plt.title("Varianza explicada acumulada")
plt.grid()
plt.show()
```

#### Paso 7: Interpretar resultados

> Determinar cuántas componentes explican al menos el 80% de la variabilidad.
>
> Analizar si es posible reducir variables sin perder información relevante.
>
> Interpretar el significado de las componentes principales obtenidas.

<br><br>

### Ejercicio 02: Segmentación de pasajeros mediante K-Means y Agrupación Jerárquica

<br><br>

#### Paso 1: Importar librerías

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score

import seaborn as sns
```

#### Paso 2: Aplicar Método del Codo

```python
inercia = []

for k in range(1,11):
    
    modelo = KMeans(
        n_clusters=k,
        random_state=42,
        n_init=10
    )

    modelo.fit(X_scaled)

    inercia.append(modelo.inertia_)
```

#### Paso 3: Graficar el Método del Codo

```python
plt.figure(figsize=(8,5))

plt.plot(
    range(1,11),
    inercia,
    marker='o'
)

plt.xlabel("Número de clusters")
plt.ylabel("Inercia")
plt.title("Método del Codo")
plt.grid()
plt.show()
```

#### Paso 4: Entrenar modelo K-Means

```python
kmeans = KMeans(
    n_clusters=3,
    random_state=42,
    n_init=10
)

clusters = kmeans.fit_predict(X_scaled)

datos["cluster"] = clusters
```

#### Paso 5: Calcular índice de silueta

```python
silhouette = silhouette_score(
    X_scaled,
    clusters
)

print("Silhouette Score:", silhouette)
```

#### Paso 6: Visualizar clusters

```python
sns.scatterplot(
    data=datos,
    x="gasto_mensual",
    y="frecuencia_viajes",
    hue="cluster",
    palette="Set1"
)

plt.title("Clusters identificados por K-Means")
plt.show()
```

#### Paso 7: Aplicar agrupación jerárquica

```python
from scipy.cluster.hierarchy import dendrogram
from scipy.cluster.hierarchy import linkage

Z = linkage(
    X_scaled,
    method="ward"
)

plt.figure(figsize=(10,5))

dendrogram(Z)

plt.title("Dendrograma")
plt.xlabel("Observaciones")
plt.ylabel("Distancia")
plt.show()
```

#### Paso 8: Analizar resultados

> Comparar el número de grupos sugeridos por el método del codo y el dendrograma.
>
> Identificar perfiles de pasajeros representados por cada cluster.
>
> Analizar la calidad de agrupamiento utilizando el índice de silueta.

<br><br>

### Ejercicio 03: Agrupación Basada en Modelos utilizando Gaussian Mixture Models (GMM)

<br><br>

#### Paso 1: Importar librerías

```python
from sklearn.mixture import GaussianMixture
```

#### Paso 2: Crear modelo GMM

```python
gmm = GaussianMixture(
    n_components=3,
    random_state=42
)

gmm.fit(X_scaled)
```

#### Paso 3: Obtener clusters

```python
cluster_gmm = gmm.predict(X_scaled)

datos["cluster_gmm"] = cluster_gmm
```

#### Paso 4: Obtener probabilidades de pertenencia

```python
probabilidades = gmm.predict_proba(
    X_scaled
)

print(probabilidades[:5])
```

#### Paso 5: Visualizar resultados

```python
sns.scatterplot(
    data=datos,
    x="gasto_mensual",
    y="frecuencia_viajes",
    hue="cluster_gmm",
    palette="Set2"
)

plt.title("Agrupamiento mediante Gaussian Mixture Models")
plt.show()
```

#### Paso 6: Comparar con K-Means

```python
print("Centroides K-Means")
print(kmeans.cluster_centers_)

print("\nMedias GMM")
print(gmm.means_)
```

#### Paso 7: Interpretar resultados

> Comparar los grupos obtenidos por K-Means y GMM.
>
> Analizar las probabilidades de pertenencia generadas por GMM.
>
> Identificar ventajas y limitaciones de cada enfoque de agrupamiento.

<br><br>

---

<br><br>

### IV. ACTIVIDADES DE ANÁLISIS Y DISCUSIÓN

1. ¿Cuántas componentes principales fueron suficientes para representar adecuadamente los datos?
2. ¿Qué porcentaje de varianza explican las componentes seleccionadas?
3. ¿Cuál fue el número óptimo de clusters sugerido por el método del codo?
4. ¿Qué perfiles de pasajeros fueron identificados mediante K-Means?
5. ¿Qué diferencias se observan entre K-Means y la agrupación jerárquica?
6. ¿Qué ventajas ofrece GMM respecto a K-Means?
7. ¿Qué algoritmo produjo agrupamientos más interpretables?
8. ¿Cómo podrían utilizarse los resultados para diseñar estrategias de fidelización de pasajeros?

<br><br>

### V. CONCLUSIONES

- Describir los conocimientos adquiridos sobre reducción de dimensionalidad mediante PCA.
- Explicar los patrones identificados mediante K-Means y agrupación jerárquica.
- Analizar las ventajas de los modelos probabilísticos basados en GMM.
- Comparar los resultados obtenidos por los distintos algoritmos no supervisados.
- Proponer aplicaciones reales de estos modelos en organizaciones peruanas.