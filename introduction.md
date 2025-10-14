---
title: 'Introduction'
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What data are we using?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn what we're doing

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

Sometimes there is quite a long list of genes to interpret after a differential expression analysis, and it is usually not feasible to go through the list one gene at a time trying to understand its biological function. A common downstream procedure is gene set testing, which aims to understand which pathways/gene networks the differentially expressed genes are implicated in. There are many different gene set testing methods that can be applied and it can be useful to try several.

The purpose of this tutorial is to demonstrate how to perform gene set testing using tools in R. The data comes from a Nature Cell Biology paper, EGF-mediated induction of Mcl-1 at the switch to lactation is essential for alveolar cell survival (<https://www.ncbi.nlm.nih.gov/pubmed/25730472>), Fu et al. 2015. That study examined the expression profiles of basal and luminal cells in the mammary gland of virgin, pregnant and lactating mice.



## Load libraries and data

*Note: sometimes the loading of data of Zenodo times out so best not to use it for compiling. Should acknowledge the source though* 

We begin by loading required packages.



``` r
library(edgeR)
library(goseq)
library(fgsea)
library(EGSEA)
library(clusterProfiler)
library(org.Mm.eg.db)
library(ggplot2)
library(enrichplot)
library(pathview)
library(edgeR)
library(impute)
library(preprocessCore)
library(RegEnrich)
```

Data can be downloaded directly from Zenodo here:


``` r
# dataurl <- "https://zenodo.org/record/2596382/files/"
#     
# debasal <- read.csv(paste0(dataurl,"limma-voom_basalpregnant-basallactate"), header = TRUE, sep = "\t")
# deluminal <- read.csv(paste0(dataurl,"limma-voom_luminalpregnant-luminallactate"), header = TRUE, sep = "\t")
# seqdata <- read.csv(paste0(dataurl,"seqdata"), header = TRUE, sep = "\t")
# load(paste0(dataurl,"mouse_hallmark_sets"))
# # loads as Mm.H
# # may not load directly

# 
# factordata <- read.table(paste0(dataurl,"factordata"), header = TRUE, sep = "\t")
# filteredcounts <- read.csv(paste0(dataurl,"limma-voom_filtered_counts"), header = TRUE, sep = "\t")
```

However, we have provided this data within the github repo:


``` r
debasal <- read.csv("data/limma-voom_basalpregnant-basallactate", header = TRUE, sep = "\t")
deluminal <- read.csv("data/limma-voom_luminalpregnant-luminallactate", header = TRUE, sep = "\t")
seqdata <- read.csv("data/seqdata", header = TRUE, sep = "\t")
load("data/mouse_hallmark_sets.RData")
# loads as Mm.H

factordata <- read.table("data/factordata", header = TRUE, sep = "\t")
filteredcounts <- read.csv("data/limma-voom_filtered_counts", header = TRUE, sep = "\t")
```

We will use several files for this analysis:

-   Differentially expressed results files (genes in rows, logFC and P values in columns)
-   Sample information file (sample id, group)
-   Gene lengths file (genes, lengths)
-   Filtered counts file (genes in rows, counts for samples in columns, with lowly expressed genes removed)
-   Gene sets file for MSigDB Hallmark collection for mouse (rdata)




## Commonly used analyses

*Brief explanation of what we'll be doing and other types of analysis*


::::::::::::::::::::::::::::::::::::: keypoints 


::::::::::::::::::::::::::::::::::::::::::::::::

