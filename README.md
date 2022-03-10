# VaiHomework6
---
title: "Homework6"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Github repo link:
https://github.com/vbahirat/VaiHomework6.git

```{r}
data(happy, package="productplots")
head(happy)
```


```{r}
HAPPY <- readRDS("data/HAPPY.rds")
head(HAPPY)
```
```{r}
is.na(HAPPY)<-HAPPY=="IAP"
is.na(HAPPY)<-HAPPY=="DK"
is.na(HAPPY)<-HAPPY=="NA"
head(HAPPY)
```
```{r}
str(HAPPY)
```
```{r}
library(tidyverse)

```


```{r}
HAPPY<-HAPPY%>% mutate(AGE=replace(AGE,AGE=="89 OR OLDER",89))

```

```{r}
HAPPY$AGE<-as.numeric(HAPPY$AGE)
HAPPY$HAPPY<-as.factor(HAPPY$HAPPY)
HAPPY$SEX<-as.factor(HAPPY$SEX)
HAPPY$MARITAL<-as.factor(HAPPY$MARITAL)
HAPPY$DEGREE<-as.factor(HAPPY$DEGREE)
HAPPY$FINRELA<-as.factor(HAPPY$FINRELA)
HAPPY$HEALTH<-as.factor(HAPPY$HEALTH)
HAPPY$PARTYID<-as.factor(HAPPY$PARTYID)


str(HAPPY)
```



```{r}
levels(reorder(HAPPY$MARITAL, HAPPY$AGE, na.rm=TRUE))
```
```{r}
HAPPY$DEGREE<-factor(HAPPY$DEGREE,levels=c("LT HIGH SCHOOL","HIGH SCHOOL","JUNIOR COLLEGE","BACHELOR","GRADUATE"))

HAPPY$FINRELA<-factor(HAPPY$FINRELA,levels=c("FAR BELOW","BELOW AVERAGE","AVERAGE","ABOVE AVERAGE","FAR ABOVE"))

HAPPY$HAPPY<-factor(HAPPY$HAPPY,levels=c("VERY HAPPY","PRETTY HAPPY","NOT TOO HAPPY"))

HAPPY$HEALTH<-factor(HAPPY$HEALTH,levels=c("EXCELLENT","GOOD","FAIR","POOR"))

HAPPY$SEX<-factor(HAPPY$SEX,levels=c("FEMALE","MALE"))

HAPPY$PARTID<-factor(HAPPY$PARTYID,levels=c("STRONG REPUBLICAN","NOT STR REPUBLICAN","IND NEAR REP","INDEPENDENT","IND NEAR DEM","NOT STR DEMOCRAT","STRONG DEMOCRAT","OTHER PARTY"))

```


```{r}
ggplot(HAPPY,aes(x=SEX,fill=factor(HAPPY)))+geom_bar()
```
We see a greater female population "pretty happy" and "very happy" compared to the male population. 


```{r}
ggplot(HAPPY, aes(x = SEX, y = HAPPY, fill = AGE))+  geom_col(position = "dodge")
```
Most of the very happy female populations is lower age compared to the male population. The pretty happy population for females has a higher age compared to the male. The unhappy male population is much younger than the female population.

```{r}
ggplot(data=HAPPY,aes(x=HAPPY,y=WTSSALL,))+geom_boxplot()
```
There is a very small range of people who are happy with their weight in the interquartile range. We also see most of the pretty happy people lie in lower weight probability values. We see some outliers in not too happy which may indicate people may not be happy with their weight probability values.  


```{r}
ggplot(HAPPY,aes(x=HEALTH,fill=factor(HAPPY)))+geom_bar()
```
We see lesser amount of people being pretty happy as their health goes from excellent to poor. We see a considerable higher ratio of not too happy in poor health than in excellent, fair, good. 
