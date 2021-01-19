# R-Tutorial

rm(list = ls())
# if (!requireNamespace("BiocManager", quietly = TRUE))
#   install.packages("BiocManager")
# 
# BiocManager::install("EnrichmentBrowser")
library(EnrichmentBrowser)
library(limma)
library(dplyr)
library(tidyr)
library(purrr)
library(ggplot2)
library(genefilter)
data=read.csv("covid19-GSE160435.csv")
# str(data)
data$class<-NULL
column_means<-colMeans(data)
#1 Apply normalization
normalo<-normalizeBetweenArrays(data)
normalo<-data.frame(normalo)

#2 
boxplot(data %>% select(1:100)) # boxplot on the originaldataset
boxplot(normalo %>% select(1:100)) # boxplot on the normalized data set

#3

fac <- factor(c(1,1,2,2,1,2,1,1,2,2))
fit <- lmFit(normalo, design=model.matrix(~ fac))  
colnames(coef(fit))  

