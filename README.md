#  Project overview

The objective was to extract meaningful, human-interpretable topics from a dataset of news headlines.

#  Approach
Because 1975 out of 1999 headlines were labeled as “unknown”, supervised classification was not feasible.
Therefore, the project relied on unsupervised topic discovery using several clustering and topic modeling techniques.

#  Model selection

### Model Comparison 

| **DBSCAN** | **Hierarchical Clustering** | **Topic Modeling (LDA, NMF)** | **K-means** |
|------------|-----------------------------|--------------------------------|-------------|
| Worked poorly due to high-dimensional sparse TF-IDF vectors (1999 × 3707). | Produces clusters but not interpretable topics; hard to extract clear labels/keywords. | Produces interpretable topics with keyword lists; assigns each headline a topic distribution. | Doesn’t inherently produce human-readable topics like LDA/NMF. |


The final model will be based on **LDA** beacuse the dataset not consisten, and topics are not coherent therefore the model will count probabilistic topic mixing.

#  Model fitting

| **Steps**                          | **Description**                               | **Evaluation (Coherence Score)** |
|------------------------------------|-----------------------------------------------|----------------------------------|
| Simple LDA model                   | CountVectorizer, 10 topics, default params     | 0.449                           |
| TF-IDF + bigrams                   | Better weighting + Improves topic clarity for short texts | 0.487                |
| TF-IDF + bigrams + min_df = 2      |  Fitting   min_df: 5 -> 2                   | 0.511                              |
| Automatic topic number (K)         | Tune the number of topics                      | 0.5263                           |

#  Model Evaluation

1. Coherence Score: 0.52 working, but not perfect.

2. LDA model successfully identified distinct semantic clusters (left).
The overlapping pair (3 & 6) is normal: news topics often blend (e.g., “govt + statements”, “police + politics”)

3. This distribution of the topic sized is normal



<img width="1347" height="664" alt="Screenshot 2025-12-02 at 00 26 21" src="https://github.com/user-attachments/assets/d06d8a4f-7cfa-4698-aaa1-aebc44de08cc" />


# Topic Human Labeling

The final interpretation was done manually.


```python
topic_labels = {
    0: "Bollywood",
    1: "Gov Policy",
    2: "State Politics/Protests",
    3: "Sports",
    4: "Administration/Social",
    5: "Sport",
    6: "Indian-Pakistan",
    7: "Social Issues",
    8: "Urban Development/Business",
    9: "International Politics/Economy",
}
```


# Final result 

A sample of the final outcome

<img width="606" height="293" alt="Screenshot 2025-12-02 at 00 29 59" src="https://github.com/user-attachments/assets/b1bc52a9-b88e-42be-be78-043bda2f941a" />


