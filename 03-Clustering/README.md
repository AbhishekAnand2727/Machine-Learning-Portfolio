# Mall Customer Segmentation Analysis

In this repository, I have documented my data science project focused on identifying and segmenting customer groups from the "Mall Customers" dataset using unsupervised machine learning.

---

## Aim

My primary objective for this project was to perform unsupervised clustering to identify distinct customer segments within a mall's customer base. By analyzing features like age, income, and spending habits, I aimed to uncover hidden patterns.

The segments I identified can provide valuable, data-driven insights for:
* **Targeted Marketing:** Creating custom marketing campaigns for different groups.
* **Customer Engagement:** Understanding the needs of high-value vs. low-value customers.
* **Strategic Decisions:** Optimizing store placements or special offers.

---

## Dataset

I used the `mall_customers.csv` dataset, which contains the following 5 columns:

* **`CustomerID`**: A unique ID for each customer (which I excluded from the analysis).
* **`Genre`**: The gender of the customer (Male/Female).
* **`Age`**: The customer's age in years.
* **`Annual Income (k$)`**: The customer's annual income in thousands of dollars.
* **`Spending Score (1-100)`**: A score (1-100) assigned by the mall based on customer behavior and spending habits.

---

## Clustering Algorithms & Methodology

In this project, I implemented and compared two primary unsupervised clustering algorithms: **K-Means** and **Agglomerative Hierarchical Clustering**.

### Data Preprocessing

Before clustering, I preprocessed the data to be suitable for distance-based algorithms:
1.  **Feature Selection:** I selected `Age`, `Annual Income (k$)`, `Spending Score (1-100)`, and `Genre`.
2.  **Encoding:** I converted the categorical `Genre` column into numerical data using **One-Hot Encoding**.
3.  **Feature Scaling:** I scaled all features using `StandardScaler` to ensure that no single feature (like `Annual Income`) disproportionately influenced the distance calculations.

### 1. K-Means Clustering
K-Means is a partitioning algorithm I used to group data by iteratively assigning points to the nearest cluster "centroid" and then recalculating the centroid's position.

* **How I Found the Optimal 'k': The Elbow Method**
    * To find the best number of clusters, **I used the Elbow Method**.
    * For this method, I ran the K-Means algorithm for a range of `k` values (e.g., 1 to 10).
    * For each `k`, **I calculated the WCSS (Within-Cluster Sum of Squares)**. WCSS measures the total squared distance of all points from their respective cluster's centroid.
    * **I then plotted WCSS** against the number of clusters (`k`). The "elbow" of the graph—the point where the rate of decrease in WCSS slows down significantly—is what I considered the optimal number of clusters to use.

### 2. Agglomerative Hierarchical Clustering
This is the second method I implemented. It is a "bottom-up" hierarchical method that begins by treating every data point as its own cluster and then progressively merges the two closest clusters until only one single cluster remains.

* **How I Found the Optimal 'k': The Dendrogram**
    * To find the best number of clusters, **I used a Dendrogram**.
    * **I first used `scipy.cluster.hierarchy.linkage`** (with `method='ward'`) to compute the hierarchical relationships.
    * This hierarchy is visualized as a tree-like diagram (the dendrogram), where the Y-axis represents the distance (or variance) between clusters.
    * **I found the optimal `k`** by identifying the **longest vertical gap that is not crossed by a horizontal "merge" line**.
    * **I then drew a horizontal "cut" line** across this gap. The **number of vertical lines** my cut-line intersected is the optimal number of clusters.

---

## Clustering Results

### Agglomerative Hierarchical Clustering

I performed Agglomerative Hierarchical Clustering using two different sets of features to understand customer segmentation. The number of clusters for each model was determined by analyzing the dendrogram.

#### 1. Two-Dimensional (2D) Analysis

* **Features Used:** `Annual Income (k$)` and `Spending Score (1-100)`
* **Optimal Clusters:** 5

By clustering only on income and spending, **from the dendrogram I identified 5 distinct customer segments**, which represent the classic marketing profiles:
* Careful (Low Income, Low Spending)
* Standard (Average Income, Average Spending)
* Target (High Income, High Spending)
* Careless (Low Income, High Spending)
* Miser (High Income, Low Spending)

This 2D model I created provides a clear and visually intuitive segmentation based on the primary drivers of purchasing behavior.

#### 2. Four-Dimensional (4D) Analysis

* **Features Used:** `Age`, `Annual Income (k$)`, `Spending Score (1-100)`, and `Genre`
* **Optimal Clusters:** 6

When **I incorporated `Age` and `Genre`** into the model, my analysis revealed a more complex structure, suggesting **6 optimal clusters** from the dendrogram.

This 4D model I built provides a more nuanced segmentation, as it accounts for the influence of age and gender on spending habits, not just income. While this model is too complex to visualize on a 2D scatter plot, it likely captures more subtle customer groups ("Young, Low-Income Spenders" vs. "Older, Low-Income Spenders").

---

### K-Means Clustering

I performed K-Means Clustering using the 2D feature set to compare its results with the hierarchical model. The number of clusters was determined using the Elbow Method.

#### Two-Dimensional (2D) Analysis

* **Features Used:** `Annual Income (k$)` and `Spending Score (1-100)`
* **Optimal Clusters:** 5

**I determined the optimal 'k' to be 5** by using the **Elbow Method** and analyzing the WCSS plot. When **I plotted the resulting 5 clusters**, they revealed the same distinct marketing profiles identified by the Agglomerative model:
* Careful (Low Income, Low Spending)
* Standard (Average Income, Average Spending)
* Target (High Income, High Spending)
* Careless (Low Income, High Spending)
* Miser (High Income, Low Spending)

This result I found confirms that for this dataset, 5 is the optimal number of segments for the primary features.

---

## Final Result & Marketing Strategy

As it is easy to read and both algorithms I ran agree, **I selected the 2-Dimensional analysis (k=5)** as the final model for strategic decision-making.

Based on these results, I recommend targeting the individuals who are in the clusters: **Target (High Income, High Spending)** and **Miser (High Income, Low Spending)** for advertisements and marketing calls.