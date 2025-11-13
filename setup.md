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

::::::::::::::::::::::::::::::::::::::: discussion

If you not have R and RStudio already installed, please download them here:

- [Download and install the latest version of R using the UniMelb mirror](https://cran.ms.unimelb.edu.au/).
- [Download and install RStudio](https://posit.co/download/rstudio-desktop/#download).


:::::::::::::::::::::::::::::::::::::::::::::::::::


## Install Libraries

```r

install.packages('ggplot2')

install.packages("BiocManager")
BiocManager::install(c("edgeR", "goseq", "fgsea", 
   "EGSEA","clusterProfiler",'org.Mm.eg.db','pathview','edgeR','STRINGdb'))
   
## If RegEnrich is not loading try installing the following:
### BiocManager::install("impute") # dependency for regenrich
### BiocManager::install("preprocessCore") # also dependency
   
```

