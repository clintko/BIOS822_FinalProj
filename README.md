---
title: "Duke Biostatistic Course BIOS822 Final Project
author: Kuei Yueh (Clint) Ko
---

# Goal of Final Project

This project is to perform exploratory data analysis on HIV flow cytometry data downloaded from flow repository [1]. The data was published in 2012 [2] and contains fcs file for all 466 patients [3].  


# Main Contents

- Notebook 01: Download Flow Data  
- Notebook 02: Flow Data Preprocess  
- Notebook 03: Exploratory data analysis  
- Notebook 04: Using Shiny App to wrap up EDA in notebok 03  

# Features

This project contains:

- Organization: 
    - The project is clearly divided into four parts, including download, preprocessing, exploring, and user interacting exploration. 
    
- Coding style
    - The coding styles follows the guideline provided in [Advanced R](http://adv-r.had.co.nz/). The styles include proper spacing in code statement and proper naming of variables (ex: using underscore instead of camel variable naming).
    
- Data Visualization & Shiny App
    - The visualization includes (pairwise) scatter plot, histogram, denstity plot, heatmap, and network plot. The data arrangement and wrangling are mostly based on dplyr and tidyr. The plotting is mostly done via ggplot package..

- R package: 
    - Some important functions required in the project are organized into a package, which is hosted in [the github repository](https://github.com/clintko/bios822FinalProjPackages). Those helper functions wrap up the functions in the flowCore package to preprocess fcs files.  
    

# Description
![SurvTime](/Figs/clinical01_SurvTime.png "SurvTime")
![SurvTime](/Figs/clinical02_SurvCurve.png)
![SurvTime](/Figs/flow_gating.png)
![SurvTime](/Figs/heatmap.png)
![SurvTime](/Figs/marker_CD45RO_CD3_after.png)
![SurvTime](/Figs/marker_CD45RO_CD3_before.png)
![SurvTime](/Figs/marker_CD45RO_CD3_samples.png)
![SurvTime](/Figs/marker_summary.png)
![SurvTime](/Figs/marker_summary_CD3.png)
![SurvTime](/Figs/network_cell.png)
![SurvTime](/Figs/pairwise_plot.png)
![SurvTime](/Figs/tsne_plot01.png)

[1] Data Download Link: http://flowrepository.org/id/FR-FCM-ZZZK
[2] Aghaeepour N (2012) IDCRP's HIV Natural History Study data set.
[3] Aghaeepour N (2012) Early immunologic correlates of HIV protection can be identified from computational analysis of complex multivariate T-cell flow cytometry assays
