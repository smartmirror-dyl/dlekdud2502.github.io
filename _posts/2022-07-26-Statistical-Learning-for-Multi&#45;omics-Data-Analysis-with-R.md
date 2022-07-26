---

title : Statistical Learning for Multi&#45;omics Data Analysis with R

date : 2022-07-26 14:00:00 + 0900

categories: [R/Python,R],[Workshop/Conference,16th Asian Institute in Statistical Genetics and Genomics Workshop]

tags: [r, statistical learning, machine learning, workshop, multiomics]

---

This post is written after taking lecture "Multi-omics Data Analysis" of 16th Asian Institute in Statistical Genetics and Genomics Workshop.

## DAY 1 (21.Jul.2022)

### 1. Dimensionality Reduction

Convert high-dimensional data to low-dimentional data. 

1.Removal of uninformative features based on experience.
2.Removal of uninformative features based on computational method. ex) PCA

#### 1-1. Principal Component Analysis (PCA)
Define y_k that is orthogonal with y_(k-1).  Select n of y_k that have largest variance.  

```R
# Example R code of PCA
X <- matrix(rnorm(32000), 1000, 32)
pca_X <- prcomp(X)
```
![alt Figure 01](/assets/posts/220726_fig01.jpg)
*Figure 01. Example of PCA for TCGA Expression Data*

#### 1-2. Independent Component Analysis (ICA)
Basic idea is same with PCA, but do not need to be orthgonal. 

```R
# Example R code of ICA
library(fastICA)
s <- matrix(runif(10000),5000,2)
A <- matrix(c(1,1,-1,3), 2, 2, byrow= TRUE)
X <- s%*%A

a <- fastICA(X, 2, alg.type="parallel", fun= "logcosh", alpha = 1,
             method = "C", row.norm = FALSE, maxit = 200,
             tol = 0.0001, verbose = TRUE)
```

![alt Figure 02](/assets/posts/220726_fig02.jpg)
*Figure 02. Difference between PCA and ICA*

#### 1-3. Non-negative Matrix Factorization (NMF)
The matrix V is represented by the two smaller matrices W and H, which, when multiplied, reconstruct V.

![alt Figure 03](/assets/posts/220726_fig03.jpg)
*Figure 03. NMF*

```R
# Example R code of NMF
install.packages("NMF")
library(NMF)

max <- matrix(runif(n=200, min=0, max=100), nrow=30, ncol=10)
res <- nmf(mat, rank=2)
w <- basis(res)
h <- coef

w %*% h # ~mat
dim(w) # 30 2
```

#### 1-4. t-distributed Stochastic Neighbor Embedding (t-SNE)
Nonlinear dimensionality reduction technique.
The distribution of data is checked by distance based on t-distribution.

![alt Figure 04](/assets/posts/220726_fig04.jpg)
*Figure 04. t-SNE*

```R
# Example R code of t-SNE
install.packages("Rtsne")
library(Rtsne)
data(iris)

iris_unique <- unique(iris)
iris_matrix <- as.matrix(iris_unique[,1:4])
tsne_out <- Rtsne(iris_matrix) 

plot(tsne_out$Y, col=iris_unique$Species)
```
![alt Figure 05](/assets/posts/220726_fig05.jpg)
*Figure 05. tsne_out*


### 2. Clustering
- No labels
- Group points into clusters based on how "near" they are to one another
- Identify structure in data
- Unsupervised learning

#### 2-1. k-means clustering
1.Ask user how many clusters they'd like. (e.g. k=5)
2.Randomly guess k cluster center locations
3.Each datapoint finds out which center it's closest to.
4.Each center finds the centroid of the points it owns and jumps there.
5.Repeat until terminated.

![alt Figure 06](/assets/posts/220726_fig06.jpg)
*Figure 06. k-means Clustering Algorithm*

```R
# Example R code of k-means Clustering
iris2 <- iris
iris2$Species <- NULL
kmeans.result <- kmeans(iris2, 3)
kmeans.result # Figure 07

plot(iris2[c("Sepal.Length","Sepal.Width")], col=kmeans.result$cluster) # Figure 08
```
![alt Figure 07](/assets/posts/220726_fig07.jpg)
*Figure 07. kmeans.result*

![alt Figure 08](/assets/posts/220726_fig08.jpg)
*Figure 08. kmeans.result plot*

#### 2-2. Hierarchical Clustering
1.Select two samples and measure distance between them.
2.Make the nearest two samples into a group and regard them as one sample.
3.Repeat until terminated. 

+ How to measure distance between groups? 
1.Single Linkage
  : Dissimilarity between two clusters = Minimum dissimilarity between the members of two clusters.
2.Complete Linkage
  : Dissimilarity between two clusters = Minimum dissimilarity between the members of two clusters.
3.Average Linkage
  : Dissimilarity between two clusters = Averaged distances of all pairs of objects (one from each cluster).
4.Average Group Linkage
  : Dissimilarity between two clusters = Distance between two cluster means.

![alt Figure 09](/assets/pots/220726_fig09.jpg)
*Figure 09. Four method to measure distance between groups (a) Single Lingkage (b) Complete Linkage (c) Average Linkage (d) Average Group Linkage*
 
```R
# Example R code of Hierachical Clustering
idx <- sample(1:dim(iris)[1], 40)
irisSample <- iris[idx,] 
irisSample$Species <- NULL

hc <- hclust(dist(irisSample), method="ave")
hc # Figure 10

plot(hc, hang = -1, labels=iris$Species[idx]) # Figure 11
```
![alt Figure 10](/assets/posts/220726_fig10.jpg)
*Figure 10. hc*
![alt Figure 11](/assets/posts/220726_fig11.jpg)
*Figure 11. hc plot*

## DAY 2 (22.Jul.2022)
The contents about Day is included in the PDF file below. 

<div type="down_btn">
	<a href="/assets/posts/220726.pdf">
		<img src="/assets/posts/220726_pdf_start.jpg">
	</a>
</div>
