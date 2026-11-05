# Guía de Estudio: Machine Learning - Modelos No Supervisados

## Introducción

El aprendizaje no supervisado (*Unsupervised Learning*) constituye una de las áreas fundamentales del Machine Learning. A diferencia del aprendizaje supervisado, donde los datos contienen etiquetas o variables objetivo conocidas, en el aprendizaje no supervisado los algoritmos trabajan con datos sin etiquetar y buscan descubrir patrones, estructuras ocultas, relaciones y agrupaciones de forma automática.

Los modelos no supervisados son ampliamente utilizados en minería de datos, análisis exploratorio, segmentación de clientes, bioinformática, detección de anomalías, procesamiento de imágenes y sistemas de recomendación.

Las principales tareas del aprendizaje no supervisado son:

- Reducción de dimensionalidad.
- Agrupamiento (*Clustering*).
- Detección de anomalías.
- Descubrimiento de patrones ocultos.

---

# 1. Fundamentos del Aprendizaje No Supervisado

## 1.1 ¿Qué es el aprendizaje no supervisado?

Es una rama del aprendizaje automático cuyo propósito es identificar estructuras subyacentes en un conjunto de datos que no poseen una variable objetivo previamente definida.

Formalmente, dado un conjunto de observaciones:
\[
X = \{x_1, x_2, ..., x_n\}
\]

el objetivo es descubrir relaciones inherentes entre las observaciones sin disponer de una variable de salida \(Y\).

---

## 1.2 Diferencias entre aprendizaje supervisado y no supervisado

| Característica | Supervisado | No Supervisado |
|--------------|-------------|----------------|
| Variable objetivo | Sí | No |
| Predicción | Sí | No necesariamente |
| Clasificación | Sí | No |
| Agrupamiento | No | Sí |
| Descubrimiento de patrones | Limitado | Principal objetivo |
| Datos etiquetados | Requeridos | No requeridos |

---

## 1.3 Aplicaciones del aprendizaje no supervisado

### Segmentación de clientes

Permite identificar grupos de clientes con comportamientos similares.

### Sistemas de recomendación

Detecta preferencias y patrones de consumo.

### Bioinformática

Agrupa secuencias genéticas similares.

### Visión por computadora

Reconoce patrones en imágenes.

### Detección de fraude

Identifica comportamientos anómalos.

### Minería de textos

Agrupa documentos por similitud temática.

---

# 2. Análisis de Componentes Principales (PCA)

## 2.1 Motivación

En muchos problemas reales se dispone de grandes cantidades de variables. Sin embargo:

- Algunas variables contienen información redundante.
- Existen fuertes correlaciones entre atributos.
- Incrementa el costo computacional.
- Aparece la denominada "maldición de la dimensionalidad".

El Análisis de Componentes Principales (*Principal Component Analysis - PCA*) busca resolver este problema reduciendo la cantidad de variables y preservando la mayor cantidad posible de información.

---

## 2.2 Definición

PCA es una técnica matemática y estadística de reducción de dimensionalidad que transforma un conjunto de variables correlacionadas en un nuevo conjunto de variables no correlacionadas denominadas componentes principales.

Cada componente principal es una combinación lineal de las variables originales.

---

## 2.3 Objetivos de PCA

- Reducir dimensionalidad.
- Eliminar redundancia.
- Simplificar visualización de datos.
- Disminuir ruido.
- Facilitar el procesamiento posterior de modelos.

---

## 2.4 Conceptos fundamentales

### Varianza

Representa la dispersión de los datos.

\[
Var(X)=\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2
\]

PCA busca preservar la mayor cantidad posible de varianza.

---

### Covarianza

Mide la relación entre dos variables.

\[
Cov(X,Y)=\frac{\sum (X-\bar{X})(Y-\bar{Y})}{n-1}
\]

Una covarianza elevada indica relación entre variables.

---

### Matriz de Covarianza

Representa la covarianza entre todas las variables del conjunto de datos.

\[
\Sigma=
\begin{bmatrix}
Cov(X_1,X_1) & Cov(X_1,X_2) \\
Cov(X_2,X_1) & Cov(X_2,X_2)
\end{bmatrix}
\]

---

## 2.5 Componentes Principales

Las componentes principales son nuevas variables que cumplen dos propiedades:

### Ortogonalidad

Las componentes son independientes entre sí.

\[
PC_i \perp PC_j
\]

---

### Máxima varianza

La primera componente captura la mayor cantidad de información disponible.

\[
Var(PC_1) > Var(PC_2) > Var(PC_3)
\]

---

## 2.6 Procedimiento de PCA

### Paso 1. Estandarización de datos

\[
z=\frac{x-\mu}{\sigma}
\]

Se realiza para evitar que las variables con mayor escala dominen el análisis.

---

### Paso 2. Construcción de la matriz de covarianza

Permite identificar relaciones entre variables.

---

### Paso 3. Obtención de autovalores y autovectores

Se calcula:

\[
Av=\lambda v
\]

Donde:

- \(\lambda\): autovalor.
- \(v\): autovector.

---

### Paso 4. Selección de componentes

Las componentes con mayor autovalor son retenidas.

---

### Paso 5. Transformación de datos

Los datos originales son proyectados sobre las nuevas componentes.

---

## 2.7 Varianza explicada

La proporción de información explicada viene dada por:

\[
VE_i=\frac{\lambda_i}{\sum_{j=1}^{p}\lambda_j}
\]

Ejemplo:

| Componente | Varianza Explicada |
|------------|--------------------|
| PC1 | 65% |
| PC2 | 20% |
| PC3 | 10% |
| PC4 | 5% |

Las dos primeras componentes explican:

\[
65\%+20\%=85\%
\]

---

## 2.8 Interpretación de PCA

Al aplicar PCA se debe responder:

- ¿Cuántas componentes conservar?
- ¿Qué porcentaje de información se preserva?
- ¿Se logró una reducción significativa?
- ¿Qué variables contribuyen más a cada componente?

---

## 2.9 Ventajas de PCA

- Reduce dimensionalidad.
- Disminuye ruido.
- Aumenta eficiencia computacional.
- Facilita visualización.

---

## 2.10 Limitaciones

- Reduce interpretabilidad.
- Solo modela relaciones lineales.
- Sensible a escalas de medición.

---

# 3. Agrupamiento (Clustering)

## 3.1 Concepto

El agrupamiento consiste en organizar observaciones similares en grupos denominados *clusters*.

La finalidad es maximizar:

\[
Similitud_{interna}
\]

y minimizar:

\[
Similitud_{externa}
\]

---

## 3.2 Conceptos importantes

### Cluster

Conjunto de observaciones similares.

### Centroide

Representante central de un grupo.

### Distancia

Medida de similitud entre observaciones.

---

## 3.3 Métricas de distancia

### Distancia Euclidiana

\[
d(x,y)=\sqrt{\sum_{i=1}^{n}(x_i-y_i)^2}
\]

Es la más utilizada.

---

### Distancia Manhattan

\[
d(x,y)=\sum_{i=1}^{n}|x_i-y_i|
\]

---

### Distancia Minkowski

\[
d(x,y)=\left(\sum_{i=1}^{n}|x_i-y_i|^p\right)^{1/p}
\]

Generalización de las anteriores.

---

### Distancia Coseno

\[
Cos(\theta)=
\frac{x \cdot y}
{|x||y|}
\]

Frecuentemente empleada en minería de textos.

---

# 4. Agrupación K-Means

## 4.1 Definición

K-Means es un algoritmo de agrupamiento particional que divide las observaciones en \(K\) grupos, donde cada observación pertenece al grupo con el centroide más cercano.

---

## 4.2 Objetivo

Minimizar la suma de cuadrados dentro de los grupos:

\[
J=\sum_{k=1}^{K}
\sum_{x_i \in C_k}
||x_i-\mu_k||^2
\]

Donde:

- \(C_k\): cluster k.
- \(\mu_k\): centroide del cluster.

---

## 4.3 Algoritmo K-Means

### Inicialización

Seleccionar K centroides.

---

### Asignación

Cada observación se asigna al centroide más cercano.

---

### Actualización

Se recalculan los centroides.

---

### Repetición

El proceso continúa hasta convergencia.

---

## 4.4 Método del Codo

Permite seleccionar el número óptimo de clusters.

Utiliza la métrica:

\[
WCSS
\]

(*Within Cluster Sum of Squares*)

La mejor elección suele encontrarse en el punto donde la disminución deja de ser pronunciada.

---

## 4.5 Coeficiente de Silueta

Evalúa calidad del agrupamiento.

\[
S=\frac{b-a}{\max(a,b)}
\]

Donde:

- \(a\): distancia promedio al mismo cluster.
- \(b\): distancia promedio al cluster vecino más cercano.

Interpretación:

| Valor | Calidad |
|---------|----------|
| 0.70 - 1.00 | Excelente |
| 0.50 - 0.70 | Buena |
| 0.25 - 0.50 | Aceptable |
| < 0.25 | Deficiente |

---

## 4.6 Ventajas

- Fácil implementación.
- Alta velocidad.
- Escalable.

---

## 4.7 Limitaciones

- Requiere definir K.
- Sensible a valores atípicos.
- Puede converger a soluciones locales.

---

# 5. Agrupación Jerárquica

## 5.1 Concepto

La agrupación jerárquica crea una jerarquía de grupos organizados en forma de árbol.

Su representación gráfica se realiza mediante un dendrograma.

---

## 5.2 Tipos de agrupamiento jerárquico

### Aglomerativo (*Bottom-Up*)

Cada observación inicia como un cluster individual.

Posteriormente:

1. Se calculan distancias.
2. Se fusionan grupos similares.
3. Se repite hasta obtener un único grupo.

---

### Divisivo (*Top-Down*)

Comienza con un único cluster.

Posteriormente:

1. Se dividen grupos.
2. Se generan subgrupos progresivamente.

---

## 5.3 Dendrograma

Es una estructura arbórea que representa:

- Relaciones entre grupos.
- Orden de fusiones.
- Distancias de agrupamiento.

```text
          ───────
          │     │
      ────      │
      │  │      │
      A  B      C
```

El corte horizontal del dendrograma determina el número final de clusters.

---

## 5.4 Métodos de enlace

### Single Linkage

Distancia mínima entre grupos.

\[
D(A,B)=\min(d(a,b))
\]

---

### Complete Linkage

Distancia máxima.

\[
D(A,B)=\max(d(a,b))
\]

---

### Average Linkage

Promedio de todas las distancias.

\[
D(A,B)=\frac{1}{|A||B|}
\sum d(a,b)
\]

---

### Ward Linkage

Minimiza la varianza intra-grupo.

Es uno de los métodos más utilizados.

---

## 5.5 Ventajas

- No requiere definir K inicialmente.
- Proporciona análisis visual.
- Identifica estructuras jerárquicas.

---

## 5.6 Limitaciones

- Costoso computacionalmente.
- Sensible al ruido.
- Difícil aplicación en grandes volúmenes de datos.

---

# 6. Agrupación Basada en el Modelo

## 6.1 Concepto

La agrupación basada en modelos asume que los datos fueron generados por una combinación de distribuciones probabilísticas.

Cada grupo se representa mediante un modelo estadístico.

En lugar de utilizar únicamente distancias, emplea probabilidades para describir la pertenencia de cada observación.

---

## 6.2 Fundamento Matemático

Sea:

\[
P(X)=\sum_{k=1}^{K}
\pi_k P(X|k)
\]

Donde:

- \(\pi_k\): probabilidad a priori del cluster.
- \(P(X|k)\): distribución asociada al cluster k.

---

## 6.3 Gaussian Mixture Models (GMM)

Es la técnica más representativa de agrupación basada en modelos.

Asume que los datos provienen de una combinación de distribuciones gaussianas.

\[
P(X)=
\sum_{k=1}^{K}
\pi_k
N(\mu_k,\Sigma_k)
\]

---

## 6.4 Componentes de un GMM

### Media (\(\mu\))

Centro del cluster.

### Covarianza (\(\Sigma\))

Determina forma, orientación y dispersión.

### Peso (\(\pi\))

Probabilidad de pertenencia.

---

## 6.5 Asignación probabilística

Mientras K-Means realiza asignación rígida:

\[
x_i \rightarrow Cluster_j
\]

GMM realiza asignación probabilística:

| Cluster | Probabilidad |
|----------|--------------|
| C1 | 0.65 |
| C2 | 0.30 |
| C3 | 0.05 |

---

## 6.6 Algoritmo Expectation-Maximization (EM)

### Fase E (Expectation)

Calcula probabilidades de pertenencia:

\[
P(C_k|X_i)
\]

---

### Fase M (Maximization)

Actualiza:

\[
\mu_k,\Sigma_k,\pi_k
\]

---

### Iteración

El proceso continúa hasta alcanzar convergencia.

---

## 6.7 Ventajas

- Modela incertidumbre.
- Detecta clusters complejos.
- Permite formas elípticas.
- Posee fundamento probabilístico sólido.

---

## 6.8 Limitaciones

- Mayor costo computacional.
- Requiere más parámetros.
- Sensible a inicialización.

---

# 7. Evaluación de Agrupamientos

## 7.1 Silhouette Score

Mide simultáneamente:

- Cohesión.
- Separación.

\[
-1 \leq S \leq 1
\]

Mientras más cercano a 1, mejor será el agrupamiento.

---

## 7.2 Davies-Bouldin Index

Evalúa similitud entre clusters.

\[
DBI \rightarrow 0
\]

Valores pequeños indican mejor agrupamiento.

---

## 7.3 Calinski-Harabasz Index

Relaciona:

\[
\frac{Dispersión\ entre\ grupos}
{Dispersión\ intra-grupo}
\]

Valores altos indican mejor separación.

---

# 8. Comparación de los Métodos Estudiados

| Característica | PCA | K-Means | Jerárquico | GMM |
|---------------|------|----------|------------|------|
| Reduce dimensionalidad | Sí | No | No | No |
| Agrupa observaciones | No | Sí | Sí | Sí |
| Basado en distancia | No | Sí | Sí | Parcialmente |
| Basado en probabilidad | No | No | No | Sí |
| Requiere K | No | Sí | No | Generalmente Sí |
| Interpretabilidad | Media | Alta | Alta | Media |
| Escalabilidad | Alta | Alta | Media | Media |
| Complejidad matemática | Media | Baja | Media | Alta |

---

# 9. Resumen Conceptual

Los modelos no supervisados permiten descubrir conocimiento oculto en datos sin etiquetar.

- **PCA** reduce dimensionalidad conservando la mayor cantidad posible de información.
- **K-Means** agrupa observaciones utilizando centroides y distancias.
- **Agrupación Jerárquica** construye estructuras de grupos en forma de árbol mediante dendrogramas.
- **Agrupación Basada en Modelos (GMM)** utiliza distribuciones probabilísticas para representar clusters y asignar observaciones según probabilidades de pertenencia.

Estas técnicas constituyen herramientas fundamentales para el análisis exploratorio, la minería de datos y el descubrimiento de patrones en problemas reales de ciencia de datos e inteligencia artificial.

---

# Preguntas de Autoevaluación

1. ¿Cuál es la diferencia principal entre aprendizaje supervisado y no supervisado?
2. ¿Qué problema busca resolver PCA?
3. ¿Qué representa la varianza explicada?
4. ¿Cuál es el papel de los autovalores y autovectores en PCA?
5. ¿Qué es un centroide en K-Means?
6. ¿Cómo funciona el método del codo?
7. ¿Qué representa el coeficiente de silueta?
8. ¿Cuál es la diferencia entre clustering aglomerativo y divisivo?
9. ¿Qué información proporciona un dendrograma?
10. ¿Por qué GMM se considera un método probabilístico?
11. ¿Qué función cumple el algoritmo EM?
12. ¿Cuáles son las principales ventajas de la agrupación basada en modelos frente a K-Means?
13. ¿Cuándo es conveniente aplicar PCA antes de un algoritmo de clustering?
14. ¿Qué métricas permiten evaluar la calidad de un agrupamiento?
15. ¿Qué limitaciones presentan los métodos de clustering al trabajar con datos de alta dimensionalidad?


