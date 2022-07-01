---
title : DEG Analysis with limma
date : 2022-07-01 12:22:00 + 0900
categories: [R/Python, R]
tags: [r,deg,limma]
---

## 1) What is "limma"?

It is an R/Bioconductor software package that provides an integrated solution for analysing data from gene expression expeirments. For limma, both RNA-seq and microarray data can be used as input data. 


&nbsp;&nbsp;&nbsp;&nbsp;
## 2) What is "DEG"?

DEG is an abbreviation of "Differentially Expressed Gene." That is, genes that are differently expressed between several groups - for example, tumoral cell and normal cell, subtypeA and subtype B, and so on - are called DEGs. 


&nbsp;&nbsp;&nbsp;&nbsp;
## 3) DEG Anaylsis with limma

### Step 1. Install limma
```R
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("limma")

library(limma)
```

&nbsp;
### Step 2. Import Data
```R
Data <- read.csv("DEA_fpkm.csv") # 598 x 20,001
FPKM <- Data[2:nrow(Data)-1,2:ncol(Data)] # 579 x 20,000
FPKM <-  (2**FPKM) -1 
GeneIDs <- Data[1:nrow(Data)-1,1] 
rownames(FPKM) <- GeneIDs 
# View(FPKM) # Figure 01
```
![alt Figure 01. FPKM](/assets/posts/220701_FPKM.jpg)
*Figure 01. FPKM*

&nbsp;
### Step 3. Making Design Matrix
```R
Condition <- Data[nrow(Data),2:ncol(Data)] # 579 x 1
# View(Condition) 
lim_design <-model.matrix(~ 0 + factor(t(Condition))) # 2 x 579
colnames(lim_design) <- c("Dead","Survive")
rownames(lim_design) <- colnames(Condition)
dim(lim_design)
# View (lim_design) # Figure 02
```
![alt Figure 02. lim_design](/assets/posts/220701_limdesign.JPG) 
*Figure 02. lim_design*

&nbsp;
### Step 4. Making Contrast Matrix
```R
limma_fit <- lmFit(FPKM,lim_design)
limma_cont <- makeContrasts(Survive - Dead,levels=lim_design) # Control Group = Dead
# View(limma_cont) # Figure 03
limma_fit.cont <- contrasts.fit(limma_fit,limma_cont)
limma_fit.cont <- eBayes(limma_fit.cont)
```
![alt Figure 03. Contrast Matrix](/assets/posts/220701_contrast_matrix.jpg) 
*Figure 03. Contrast Matrix*

&nbsp;
### Step 5. Results
```R
limma_res <- topTable(limma_fit.cont, adjust.method = 'BH', number = 20000) 
# View(limma_res) # Figure 04
sum(limma_res$adj.P.Val<=0.05 & abs(limma_res$logFC) >= 0.01) # result : 163
# write.table(limma_res,"DEG_fpkm.csv",sep=',',quote=F)
```
![alt Figure 04. limma_res](/assets/posts/220701_result1.jpg)
*Figure 04. limma_res*

+ logFC : The proportion of expression of a gene in the test group compared to the control group. The base is 2. 
	ex) logFC = 1 means that expression of gene X is twice higher in Survive group than in Dead group.
	if logFC is a negative value, it means that gene X is underexpressed in the test group. 
+ adj.P.Val : FDR (False Discovery Rate)

&nbsp;
### Step 6. Label Regulated Genes
```R
limma_res$diffexpressed <- "NO"
# if log2Foldchange > 0.01 and pvalue < 0.05, set as "UP" 
limma_res$diffexpressed[limma_res$logFC >= 0.01 & limma_res$adj.P.Val <= 0.05] <- "UP"
# if log2Foldchange < -0.01 and pvalue < 0.05, set as "DOWN"
limma_res$diffexpressed[limma_res$logFC <= -0.01 & limma_res$adj.P.Val <= 0.05] <- "DOWN"
# View(limma_res) # Figure 05
```
![alt Figure 05. limma_res](/assets/posts/220701_result2.jpg)
*Figure 05. limma_res*

&nbsp;
### Step 7. Plot
```R
p <- ggplot(data=limma_res, aes(x=logFC, y=-log10(adj.P.Val), col=diffexpressed)) + geom_point() + theme_minimal()
# Add lines as before...
p2 <- p + geom_vline(xintercept=c(-0.01, 0.01), col="red") +
  geom_hline(yintercept=-log10(0.05), col="red")
p3 <- p2 + scale_color_manual(values=c("blue", "black", "red"))
# 2. to automate a bit: ceate a named vector: the values are the colors to be used, the names are the categories they will be assigned to:
mycolors <- c("blue", "red", "black")
names(mycolors) <- c("DOWN", "UP", "NO")
p3 <- p2 + scale_colour_manual(values = mycolors)
p3 # Figure 06
```
![alt Figure 06. p3](/assets/posts/220701_p3.jpg "Figure 06. p3")
*Figure 06. p3*
