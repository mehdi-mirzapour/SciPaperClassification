# SciPaperClassification

# Objective
Clustering and Classification of research abstracts into an unknown number of categories

# Dataset
Public arxiv dataset - https://www.kaggle.com/datasets/Cornell-University/arxiv

# Introduction

As described in [1] each year, around 28,100 journals publish 2.5 million research publications. Search engines, digital libraries, and citation indexes are used extensively to search these publications. When a user submits a query, it generates a large number of documents among which just a few are relevant. Due to inadequate indexing, the resultant documents are largely unstructured. Publicly known systems
mostly index the research papers using keywords rather than using subject hierarchy. Numerous methods reported for performing single-label classification (SLC) or multi-label classification (MLC) are based on content and metadata features. Content-based techniques offer higher outcomes due to the extreme richness of features. But the drawback of content-based techniques is the unavailability of full text in most cases.

Classifying scientific abstracts by their topics is not a trivial task. As the topics are not presented in the abstracts or keywords. For example a paper in computer science normally doesn't have the keyword `computer science` in the abstract. Also having around 2 million abstracts demands more computational resources comparing to other tasks. As retraining the model by having new data is also hard, this may suggest continuous learning which is by itself a challenge. The list of challenges do not stop here. One of the problems that we will focus in this report is how we should cluster documents into similar groups that might be useful for search engines or for famous MORE-LIKE-THIS search. 

Our strategy for doing so, is not just classifying the documents by the existing topics. The reason for not taking this direction is that the topics have very close semantic distance in the embedding space and makes it quite hard for classifiers to do the job properly. More imprtantly the granularity-level of the abstracts are so dense that makes the labels extremely unbalanced. Maybe a good direction (at least to start with as inititative) is to start with coarse-grained labels. To do so we have started with 20 unknown labels that we will gain in the clustering phase of the project and then use it for our classification task.

# Literature Review

Research study [1] explains why BOW, TF, and TFIDF measures may not establish the semantic context of the words. The existing MLC techniques require a specified threshold value to map articles into predetermined categories for which domain knowledge is necessary. The objective of this paper is to get over the limitations of SLC and MLC techniques. To capture the semantic and contextual information of words, the suggested approach leverages the Word2Vec paradigm for textual representation. The suggested model determines threshold values using rigorous data analysis, obviating the necessity for domain expertise. Another direction [2] on subject categories classification is a very practical proposal that uses deep attentive neural network (DANN) that classifies scholarly papers using only their abstracts. The network is trained using nine million abstracts from Web of Science (WoS). We also use the WoS schema that covers 104 subject categories. Addressing the problem of clustering partitions cab be done [3] by two scalable algorithms designed for clustering very large datasets in distance spaces. Our first algorithm BUBBLE is, to our knowledge, the first scalable clustering algorithm for data in a distance space. Our second algorithm BUBBLE-FM improves upon BUBBLE by reducing the number of calls to the distance function, which may be computationally very expensive. Both algorithms make only a single scan over the database while producing high clustering quality. 

# Our Approach

Although current research are inspiring, but, we are interested in to take SentBERT embedding instead of BOW, TF adn TFIDF as they are SOTA embedding in different NLP tasks, and fast enough to do our job. 


# Explaination

In this project we have started with three stages:

1. Phase 1: Clustering Abstract Documents (See the jupyter file for detailed explanasion)
2. Phase 2: Classification Abstract Documents with Pytroch (See the jupyter file for detailed explanasion)
3. Phase 3: Classification Abstract Documents with TensorFlow (See the jupyter file for detailed explanasion)



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

# Conclusion and Future Work

We have tried to show why clustering the abstracts are necessary and after creating unkonwn categories without topic modeling we created two pipelines (in Pytorch and Tensorflow) that take those new labels and do the classification with 81% accuracy.


# References

[1] Mustafa, G., Usman, M., Yu, L. et al. Multi-label classification of research articles using Word2Vec and identification of similarity threshold. Sci Rep 11, 21900 (2021). https://doi.org/10.1038/s41598-021-01460-7

[2] Large Scale Subject Category Classification of Scholarly Papers With Deep Attentive Neural Networks Front. Res. Metr. Anal., 10 February 2021 Sec. Text-mining and Literature-based Discovery Volume 5 - 2020 | https://doi.org/10.3389/frma.2020.600382

[3] V. Ganti, R. Ramakrishnan, J. Gehrke, A. Powell and J. French, "Clustering large datasets in arbitrary metric spaces," Proceedings 15th International Conference on Data Engineering (Cat. No.99CB36337), Sydney, NSW, Australia, 1999, pp. 502-511, doi: 10.1109/ICDE.1999.754966.