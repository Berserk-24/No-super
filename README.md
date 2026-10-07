# Agrupación de Noticias con Aprendizaje No Supervisado

Proyecto de aprendizaje **no supervisado** que organiza automáticamente artículos reales de la BBC en grupos temáticos, sin recibir ninguna etiqueta durante el entrenamiento. El sistema descubre por sí solo que unos artículos hablan de deportes, otros de política, negocios, tecnología o entretenimiento, basándose únicamente en los patrones del lenguaje de cada texto.

## Contexto del problema

Ante grandes volúmenes de texto sin clasificar, el agrupamiento (clustering) permite descubrir la estructura temática subyacente sin intervención humana. Aquí se aplica al corpus **BBC News** para comprobar si un modelo puede recuperar, de forma autónoma, las categorías reales del periódico.

- **Dataset:** `bbc_data.csv` — 2.225 artículos en inglés distribuidos en cinco categorías: `sport`, `business`, `politics`, `tech` y `entertainment`.
- Las etiquetas originales **no se usan en el entrenamiento**; solo sirven para validar al final qué tan bien el modelo recuperó la estructura real.

## Qué se usó

- **Lenguaje y entorno:** Python (Jupyter Notebook).
- **Librerías:** `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `re`.
- **Pipeline:**
  1. **Preprocesamiento de texto:** minúsculas, eliminación de caracteres especiales y stopwords.
  2. **Vectorización TF-IDF** (unigramas y bigramas, vocabulario de 5.000 términos).
  3. **Reducción de dimensionalidad con PCA** (50 componentes para el clustering, 2 para visualización).
  4. **Selección de K** mediante la técnica del codo.
  5. **Clustering** con `KMeans` y comparación con `GaussianMixture` (GMM).
- **Evaluación:** Silhouette Score (métrica que no requiere etiquetas) y tabla cruzada contra las categorías reales.

## Qué se logró

- El modelo descubrió **5 clusters** temáticos coherentes, número que coincide con las categorías reales del corpus BBC (confirmado por la técnica del codo).
- Las palabras más representativas de cada cluster son temáticamente consistentes (deporte: *game, win, play*; economía: *market, growth, economy*; tecnología: *software, mobile, technology*; etc.), lo que permite etiquetar cada grupo sin usar ninguna etiqueta real.
- Comparación entre K-Means y GMM: ambos producen particiones similares, con Silhouette bajo (**K-Means ≈ 0,085** y **GMM ≈ 0,081**), reflejando el solapamiento natural de vocabulario entre temas como `business`, `tech` y `politics`. K-Means resultó ligeramente más estable.
- Clasificación de un artículo nuevo (no visto) en el cluster correcto, aplicando el mismo pipeline de transformación.

## Cómo ejecutar

1. Instalar dependencias:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn
   ```
2. Abrir `agrupacion_noticias.ipynb` y ejecutar las celdas en orden (el archivo `bbc_data.csv` debe estar en la misma carpeta).

## Estructura

```
No-super/
├── agrupacion_noticias.ipynb   # Notebook con el pipeline completo de clustering
├── bbc_data.csv                # Corpus BBC News (2.225 artículos)
└── README.md
```
