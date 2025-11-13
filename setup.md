---
title: Setup
---

FIXME: Setup instructions live in this document. Please specify the tools and
the data sets the Learner needs to have installed.

## Data Sets

Data is from Zenodo
Link to paper here with description



:::: prereq

Some knowledge of R and RNA-seq analysis is assumed.

This lesson assumes you have R and RStudio installed on your computer.


::::


## Software Setup

:::: checklist

## REQUIRED SOFTWARE

Attendees are required to bring their own laptop computers. **Please ensure you have installed:**

- [Chrome](https://www.google.com/chrome/) or [FireFox](https://www.mozilla.org/en-US/)
- [R](https://cran.ms.unimelb.edu.au/) (Download and install the latest version of R using the UniMelb mirror)
- [RStudio](https://posit.co/download/rstudio-desktop/#download)
- R packages required for this workshop (see below)

::::



## Install Libraries

Please copy the following code and run prior to starting the training material:

```r

install.packages('ggplot2')

install.packages("BiocManager")
BiocManager::install(c("edgeR", "goseq", "fgsea", 
   "EGSEA","clusterProfiler",'org.Mm.eg.db','pathview','edgeR','STRINGdb'))
   
## If RegEnrich is not loading try installing the following:
### BiocManager::install("impute") # dependency for regenrich
### BiocManager::install("preprocessCore") # also dependency
   
```

