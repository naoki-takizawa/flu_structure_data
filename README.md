# flu structure probing data 
## Introduction
This repository contains bigWig files of influenza A virus (IAV) structure probing data publised in [N Takizawa and RK Kawaguchi, Comput Struct Biotechnol J. (2023)](https://www.sciencedirect.com/science/article/pii/S2001037023003926).
You can view these structure probing data of IAV using genome browser.
Here, I will also show how to view these data locally using [JBrowseR](https://gmod.github.io/JBrowseR/index.html).

## probing data
bigWig files of IAV structure probing data are in dataset folder. There are 12 bigWig files in the folder.  
reactIDR_virion_SHAPE.bw  
reactIDR_vRNP_SHAPE.bw  
reactIDR_vRNA_SHAPE.bw  
BUMHMM_virion_SHAPE.bw  
BUMHMM_vRNP_SHAPE.bw  
BUMHMM_vRNA_SHAPE.bw  
reactIDR_virion_DMS.bw  
reactIDR_vRNP_DMS.bw  
reactIDR_vRNA_DMS.bw  
BUMHMM_virion_DMS.bw  
BUMHMM_vRNP_DMS.bw  
BUMHMM_vRNA_DMS.bw

## Browse using JBrowseR
### Before start
R and Rstudio must be installed.

### Install JBrowseR and shiny
You can install JBrowseR and shiny on RStudio from CRAN with:
```
install.packages("JBrowseR")
install.packages("shiny")
```
If already installed, launch shiny and JBrowseR
```
library(JBrowseR)
library(shiny)
```

### Data folder

