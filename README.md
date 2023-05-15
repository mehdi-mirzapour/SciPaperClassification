# SciPaperClassification

# Objective
Clustering and Classification of research abstracts into an unknown number of categories

# Dataset
Public arxiv dataset - https://www.kaggle.com/datasets/Cornell-University/arxiv
# Explaination

In this project we have started with two stages:

1. Phase 1: Clustering Abstract Documents (See the jupyter file for detailed explanasion)
2. Phase 2: Classification Abstract Documents (See the jupyter file for detailed explanasion)


For each phase, we have a corresponding jupyter file. 

The following plot shows the distribution of document classes (centroids in black dots) in the document space. We can guess the classifier will have quite a hard time to distinguish the classes.

![](resources/Dist2.png?raw=true)

In the following plot, we can see how the clustering algorithm should do the job with the optimum number of clusters=20. As we can see any classifier built upon the following cluster centroids (as unknow labels) can perform better due to the fact that they are nicely distanced. 
![](resources/Dist1.png?raw=true)

Also, we can observed the same algorithm output runned on the cosine distance. 
![](resources/Dist3.png?raw=true)

We have calculated the K number of cluster with elbow methode.

![](resources/Dist4.png?raw=true)


After doing the clustering, we have created the classification phase in the second document which do the standard HuggingFace API to train our dataset using our new labels gained from previous step clustering algorithms.
