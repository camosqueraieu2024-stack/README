# Two Worlds or Four? Clustering the UN Development Indicators

K-Means clustering of 207 countries using 12 UN development indicators (fertility, life expectancy, infant mortality, GDP per capita, education, literacy and economic activity) to test whether the world can be divided into "developed vs developing", and whether the evidence supports Hans Rosling's claim in *Factfulness* that the world is better described by four levels.

## Method

1. **Data exploration:** loaded `UN.csv`; `country` and `region` are labels, and the 12 numeric indicators are used for clustering.
2. **Missing values:** replaced with the column median.
3. **Feature scaling:** `StandardScaler`, because K-Means uses Euclidean distance and GDP per capita (range ≈ 42,000) would otherwise dominate fertility (range ≈ 7).
4. **Number of clusters:** K-Means tested for k = 1 to 10; the Elbow Rule was used to pick the recommended k.
5. **Comparison:** k = 2 vs k = optimal (3), plus k = 4 to test the *Factfulness* claim.

## Research Questions

**1. Can the world be divided into only two clusters?**
Only crudely. k = 2 separates the 64 poorest, high-fertility countries from the rest, but the "developed" group lumps together countries as different as Switzerland and Tajikistan. It is really "very poor vs everyone else."

**2. How many clusters does the Elbow Rule suggest?**
**k = 3**, with k = 4 a close second. The curve bends gradually, suggesting development is a continuum.

**3. How much structure do two clusters explain compared with the optimal number?**
Two clusters explain **38.7%** of the variance; three explain **50.0%**. The gain comes from splitting the "developed" group into a high-income group (26 countries) and a large middle group (121 countries).

**4. Does the evidence support four groups, as claimed in *Factfulness*?**
Mostly. The two-group view is clearly rejected, and most countries fall in the middle, as Rosling argues. With all variables, the fourth cluster is an artefact of filling missing education data (63% missing) with the median. Without the education variables, k = 4 gives four meaningful levels similar to Rosling's. The honest statistical answer is "three or four" groups.

## Final Clusters and Representative Countries

| Level | Representative | Key features |
|---|---|---|
| 1 — Low income, high fertility | **Afghanistan** | 6.9 children per woman, female life expectancy 46, infant mortality 154 per 1,000, 85% female illiteracy |
| 2 — Lower-middle, traditional gender roles | **Belize** | Moderate income and good health, but fertility of 3.7 and low female labour participation |
| 3 — Upper-middle / converging | **Argentina** | Fertility 2.6, female life expectancy 77, illiteracy under 4%, but income well below rich countries |
| 4 — High income | **Australia** | GDP per capita ~$20,000, female life expectancy 81, infant mortality 6 |

**Surprising findings:** Saudi Arabia, Oman and Kuwait fall in Level 2 with India and Honduras, despite their wealth, because of high fertility and low female employment. Greece and South Korea fall in Level 3, and French overseas territories such as Réunion and Martinique join Level 4.

## Conclusion

The analysis does not support dividing the world into only two groups. Two clusters explain just 38.7% of the variance and force very different countries into one "developed" group. A third cluster reveals a large middle group of around 120 countries, the majority, which is the core argument of *Factfulness*.

The Elbow Rule recommends three clusters, with four almost equally supported. Once the missing-data artefact is removed, four clusters give clear levels (low, lower-middle, upper-middle and high income) that closely match Rosling's. The evidence supports his view, with the caveat that development is a continuum and the boundaries between groups are not sharp.

## Repository Contents

- `UN_clustering_analysis.ipynb`: the full analysis
- `UN.csv`: the dataset, included so the project runs without external downloads
- `README.md`: this file

## How to Reproduce

1. Install the libraries: `pip install pandas numpy scikit-learn matplotlib jupyter`
2. Open the notebook in Jupyter and select **Run All**.

Results are reproducible because K-Means uses a fixed seed (`random_state=42`).

## Data Source

UN social and economic indicators (late 1990s), from [manoelgadi/PSDMA](https://github.com/manoelgadi/PSDMA/blob/main/datasets/UN.csv).
