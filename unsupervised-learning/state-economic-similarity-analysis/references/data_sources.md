# Data Sources and Technical References

This document records the government datasets, analytical methods, and Python libraries used in the project:

**State-Level Economic Similarity and Structural Stability: An Unsupervised Learning Analysis of U.S. States Before, During, and After the 2020–2022 Economic Shock**

## 1. Study Scope

The analysis covers the 50 U.S. states and divides the data into three periods:

| Period     |     Years | Purpose                                                |
| ---------- | --------: | ------------------------------------------------------ |
| Baseline   | 2015–2019 | Represents state economic structures before the shock  |
| Shock      | 2020–2022 | Represents the pandemic and economic-disruption period |
| Post-shock | 2023–2024 | Represents the initial period following the shock      |

The post-shock period contains fewer years than the other periods. Its results should therefore be interpreted as preliminary evidence rather than a definitive long-term structural outcome.

---

## 2. U.S. Bureau of Economic Analysis

### Source

**U.S. Bureau of Economic Analysis — Regional Economic Accounts**

* Main state-data page:
  https://www.bea.gov/data/by-place-state-territory

* Interactive regional data tables:
  https://apps.bea.gov/itable/?ReqID=70&step=1

### Tables Used

| BEA table | Description               | Application in this project                                                 |
| --------- | ------------------------- | --------------------------------------------------------------------------- |
| `SAGDP9N` | Real GDP by state         | Construction of real GDP and real GDP per capita measures                   |
| `SAINC1`  | Personal Income Summary   | Personal income and per-capita income measures                              |
| `SAINC30` | Economic Profile by State | Wages, salaries, employment, population, and related state-level indicators |

The BEA data were used to construct the following final economic-capacity features:

* `real_gdp_per_capita`
* `real_personal_income_per_capita_2017`
* `real_output_per_job`
* `real_average_wages_salaries_2017`

Monetary measures were expressed in real or inflation-adjusted terms where applicable so that comparisons across years were not driven only by changes in prices.

### Recommended Citation

> U.S. Bureau of Economic Analysis. *Regional Economic Accounts*. U.S. Department of Commerce. https://www.bea.gov/data/by-place-state-territory. Accessed September 2026.

---

## 3. U.S. Bureau of Labor Statistics

### Source

**Quarterly Census of Employment and Wages**

The Quarterly Census of Employment and Wages, or QCEW, publishes employment and wage information by geographic area and industry.

* QCEW program homepage:
  https://www.bls.gov/cew/

* Downloadable data files:
  https://www.bls.gov/cew/downloadable-data-files.htm

* QCEW data-file guide:
  https://www.bls.gov/cew/about-data/data-files-guide.htm

* QCEW open-data access:
  https://www.bls.gov/cew/additional-resources/open-data/home.htm

### Variables Used

Annual average employment was aggregated into selected industry groups and divided by total state employment to construct employment shares.

The final employment-structure features were:

* `manufacturing_share`
* `professional_business_share`
* `healthcare_share`
* `natural_resources_agriculture_share`

The natural-resources and agriculture feature combined employment related to agriculture, forestry, fishing, hunting, mining, quarrying, and oil and gas extraction, according to the industry groups included in the project.

### Industry Classification

QCEW data use the **North American Industry Classification System**, or NAICS. The project used industry-level annual average employment data for each state.

Because NAICS classifications and available aggregation levels may vary across files or years, the data-cleaning notebooks document the industry codes and aggregation rules used in the analysis.

### Recommended Citation

> U.S. Bureau of Labor Statistics. *Quarterly Census of Employment and Wages*. U.S. Department of Labor. https://www.bls.gov/cew/. Accessed September 2026.

---

## 4. Final Analytical Features

The final unsupervised-learning model used eight structural features:

| Category            | Feature                                |
| ------------------- | -------------------------------------- |
| Economic capacity   | `real_gdp_per_capita`                  |
| Economic capacity   | `real_personal_income_per_capita_2017` |
| Productivity        | `real_output_per_job`                  |
| Labor compensation  | `real_average_wages_salaries_2017`     |
| Industry employment | `manufacturing_share`                  |
| Industry employment | `professional_business_share`          |
| Industry employment | `healthcare_share`                     |
| Industry employment | `natural_resources_agriculture_share`  |

These variables represent both the economic capacity and industry-employment structure of each state.

---

## 5. Data Transformations

### Period Aggregation

Annual observations were aggregated into three state-period averages:

* `Baseline_2015_2019`
* `Shock_2020_2022`
* `Post_Shock_2023_2024`

This produced 150 analytical observations:

$$
50\text{ states} \times 3\text{ periods} = 150\text{ state-period observations}
$$

### Log Transformation

The natural-resources and agriculture employment share was highly right-skewed. The following transformation was applied:

$$
x_{\text{transformed}}=\log(1+x)
$$

The transformed feature was stored as:

```text
log1p_natural_resources_agriculture_share
```

### Standardization

All model features were standardized before PCA and clustering:

$$
z=\frac{x-\mu}{\sigma}
$$

Standardization was necessary because monetary variables and employment shares use substantially different measurement scales.

---

## 6. Principal Component Analysis

Principal Component Analysis was used to:

* reduce multicollinearity;
* summarize the eight structural features;
* identify the main dimensions of variation among states; and
* create a lower-dimensional space for clustering and peer-distance analysis.

Four principal components were retained. Together, they explained approximately **91.8% of the standardized variance**.

### Technical Reference

* scikit-learn PCA documentation:
  https://scikit-learn.org/stable/modules/decomposition.html#pca

* PCA class documentation:
  https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html

---

## 7. K-Means Clustering

K-Means clustering was used to create descriptive economic-structure segments.

Candidate models containing two through eight clusters were evaluated using:

* inertia and the elbow method;
* silhouette score;
* Calinski–Harabasz score;
* Davies–Bouldin score;
* cluster-size balance; and
* cluster stability across random seeds.

A seven-cluster solution was selected based on the combined statistical evidence and economic interpretability.

The clusters are descriptive segments and should not be interpreted as permanent, official, or definitive classifications of the states.

### Technical References

* scikit-learn clustering documentation:
  https://scikit-learn.org/stable/modules/clustering.html#k-means

* KMeans class documentation:
  https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html

* Silhouette score:
  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html

* Calinski–Harabasz score:
  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.calinski_harabasz_score.html

* Davies–Bouldin score:
  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.davies_bouldin_score.html

---

## 8. Hierarchical Clustering

Ward-linkage hierarchical clustering was used as a comparison with the K-Means results.

The method was used to:

* examine the hierarchical relationships among states;
* visualize state similarities with dendrograms;
* compare cluster membership with K-Means; and
* evaluate whether the broad structural segments were supported by another clustering approach.

### Technical References

* SciPy hierarchical clustering documentation:
  https://docs.scipy.org/doc/scipy/reference/cluster.hierarchy.html

* Ward linkage:
  https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.ward.html

* Dendrogram function:
  https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.dendrogram.html

* Agglomerative clustering:
  https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AgglomerativeClustering.html

---

## 9. Illinois Peer-Distance Analysis

Illinois’s closest economic peers were identified using Euclidean distance in the four-dimensional PCA space.

For state \(j\), the distance from Illinois was calculated as:

$$
d_{IL,j}
=
\sqrt{
(PC1_{IL}-PC1_j)^2+
(PC2_{IL}-PC2_j)^2+
(PC3_{IL}-PC3_j)^2+
(PC4_{IL}-PC4_j)^2
}
$$

A smaller distance indicates greater similarity to Illinois across the four retained principal components.

Peer distance and cluster membership answer different questions:

* Cluster membership compares a state with each cluster centroid.
* Peer distance compares a state directly with Illinois.

A state can therefore be one of Illinois’s closest peers without belonging to the same cluster.

---

## 10. Peer-List Stability

Jaccard similarity was used to compare Illinois’s top-five peer lists between periods:

$$
J(A,B)=\frac{|A\cap B|}{|A\cup B|}
$$

Where:

* \(A\) is the peer set from one period;
* \(B\) is the peer set from another period;
* \(J=1\) indicates identical peer lists; and
* \(J=0\) indicates that the two lists have no states in common.

### Technical Reference

* scikit-learn Jaccard similarity documentation:
  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.jaccard_score.html

The project calculated set-based Jaccard similarity directly from the state peer lists.

---

## 11. Cluster Stability

Adjusted Rand Index was used to evaluate the stability of K-Means solutions across different random seeds.

The index compares two cluster assignments while adjusting for agreement that could occur by chance.

### Technical Reference

* Adjusted Rand score:
  https://scikit-learn.org/stable/modules/generated/sklearn.metrics.adjusted_rand_score.html

---

## 12. Python Libraries

| Library        | Application                                                                         |
| -------------- | ----------------------------------------------------------------------------------- |
| `pandas`       | Data loading, cleaning, aggregation, merging, and table construction                |
| `numpy`        | Numerical calculations, arrays, transformations, and distance calculations          |
| `scikit-learn` | Standardization, PCA, K-Means, clustering metrics, and stability analysis           |
| `scipy`        | Hierarchical clustering, linkage calculations, and dendrograms                      |
| `matplotlib`   | Static charts and figure customization                                              |
| `seaborn`      | Distribution plots, box plots, correlation heatmaps, and statistical visualizations |
| `plotly`       | Interactive U.S. choropleth maps and comparison visualizations                      |
| `jupyter`      | Reproducible notebook-based analysis                                                |
| `openpyxl`     | Reading or writing Excel files where applicable                                     |

### Official Documentation

* Python: https://docs.python.org/3/
* pandas: https://pandas.pydata.org/docs/
* NumPy: https://numpy.org/doc/
* SciPy: https://docs.scipy.org/doc/scipy/
* scikit-learn: https://scikit-learn.org/stable/
* Matplotlib: https://matplotlib.org/stable/
* Seaborn: https://seaborn.pydata.org/
* Plotly Python: https://plotly.com/python/
* Jupyter: https://docs.jupyter.org/
* openpyxl: https://openpyxl.readthedocs.io/

---

## 13. Data and Interpretation Limitations

The following limitations should be considered when interpreting the results:

1. The post-shock period is shorter than the baseline and shock periods.
2. Period averages can hide important annual fluctuations.
3. Cluster assignments depend on the selected variables, transformations, retained principal components, and number of clusters.
4. K-Means divides observations into discrete groups even though state economic structures may exist on a continuum.
5. States near cluster boundaries may change clusters following relatively small movements.
6. PCA components are statistical combinations of variables and require interpretive judgment.
7. Employment shares describe the composition of employment but do not capture every aspect of a state economy.
8. Peer distance measures similarity, not causal relationships.
9. The analysis does not prove that the 2020–2022 shock caused the observed structural changes.
10. The results should be treated as exploratory and descriptive.

---

## 14. Data Use Statement

BEA and BLS data are publicly available U.S. government statistics. The original data remain subject to the definitions, revision schedules, disclosure rules, and usage policies of their respective agencies.

The processed datasets and analytical results in this repository were created for educational and portfolio purposes.

---

## 15. Access Information

Sources were accessed during the development of this project in 2026.

Government economic data may be revised after their original release. Therefore, users downloading the same tables later may observe small differences from the values stored in this repository.
