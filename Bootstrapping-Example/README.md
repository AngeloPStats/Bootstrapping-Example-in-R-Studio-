# Bootstrapping-Example
This R code showcases bootstrapping, ideal for situations with limited data. By resampling with replacement, it allows for reliable predictions and inferences. Additionally, it enhances estimate accuracy by replicating tables multiple times.

# The R Studio code is below

---
title: "Bootstrapping"
author: "Angelo"
date: "March 20, 2022"
output: html_document
---


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```{r}
## Bootstrapping example
## This dataset is available in R

data("attenu")
dim(attenu)
attach(attenu)
head(attenu)

## Original dataset

lm0 = lm(accel ~ dist + mag , data = attenu)
summary(lm0)
plot(lm0)

# Replicating 1000 time the dataset 

index = seq(1,182,1)
index

boot.out=NULL


for(j in 1:1000)
{
  index.new = sample(index,182,replace=T)
  
  atte.new = attenu[index.new,]
  
  lm1 =lm(accel ~ dist + mag, data = atte.new)
  
  ##Collects coefficients
  
  boot.out=rbind(boot.out,coef(lm1))
}



##Plotting 

par(mfrow=c(3,1))

hist(boot.out[,1])
hist(boot.out[,2])
hist(boot.out[,3])


bt1=mean(boot.out[,1])
bt2=mean(boot.out[,2])
bt3=mean(boot.out[,3])

print(c(bt1,bt2,bt3))

##Original Coefficients

coef(lm0)

```

*.rmd linguist-language=R
