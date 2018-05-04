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

- **Organization** 
    - The project is clearly divided into four parts, including download, preprocessing, exploring, and user interacting exploration. Note that the functional programming and parallel computing are used in preprocessing.
    
- **Coding style**
    - The coding styles follows the guideline provided in [Advanced R](http://adv-r.had.co.nz/). The styles include proper spacing in code statement and proper naming of variables (ex: using underscore instead of camel variable naming). 
    
- **Data Visualization & Shiny App**
    - The visualization includes (pairwise) scatter plot, histogram, denstity plot, heatmap, and network plot. The data arrangement and wrangling are mostly based on dplyr and tidyr. The plotting is mostly done via ggplot package. Most of the data visualization is incorporate into a Shiny App in "*Notebook 04: Using Shiny App to wrap up EDA in notebok 03*"

- **R package**
    - Some important functions required in the project are organized into a package, which is hosted in [the github repository](https://github.com/clintko/bios822FinalProjPackages). Those helper functions wrap up the functions in the flowCore package to preprocess fcs files.  
    

# Description
Below are some descriptions and figures plotted in the projects. More details are in the R notebooks of the project.

### Preprocessing (Compensation and Transformation)

The emission wavelength of different fluorochrome usually overlap to each other. That is, multiple fluorescence spectra may be detected by one flurochrome. Since we need to get the values of each flurorochrome, the spectral overlap should be corrected. Beside compensation, due to the heavily-skewed flow cytometry measurements, transformation of flow cytometry measurements is performed before analysis. Below are figures that demonstrate the change of data points in the data preprocessing.

The scatter plot of marker CD45Ro vs CD3 in the file 100715.fcs before preprocessing (compensation and transformation). In this visualization before preprocessing, one can notice that the data points are squeezed in the left below corner.
![FlowMarker before](/Figs/marker_CD45RO_CD3_before.png)

The scatter plot of marker CD45Ro vs CD3 in the file 100715.fcs after preprocessing.
![FlowMarker after](/Figs/marker_CD45RO_CD3_after.png)

### Clinical data

The data contains survival time and the patient IDs, which correspond to the file name of fcs files.

Visualization of survival time in every patients.
![SurvTime](/Figs/clinical01_SurvTime.png)

The Kaplan-meier curve is acquired after fitting the survival model of clinical data.
![SurvCurv](/Figs/clinical02_SurvCurve.png)

### Global pattern of each flow cytometry sample

The global pattern can be explored using heatmap and dimensional reduction plot.

Each intensity matrix belongs to [tidy data defined in R for data science](http://r4ds.had.co.nz/tidy-data.html), where each row represents a observation (cell) and each column is a variable (marker). For a sample, a certain fraction of cells were randomly selected for plotting. Here I plotted the first fcs file. In the shiny app, users can choose which file to plot. 
![FlowHeatmap](/Figs/heatmap.png)

Dimensional reduction plot allows researcher to visualize the distribution of high dimensional data at lower dimensional space. Here I used t-distributed stochastic neighbor embedding (t-SNE) to reduce the dimension of data. The advantage of t-SNE plot does not use linear transformation to preserved the distance of observation in high dimensional space. Therefore, it is better to visualize the complex pattern compared to other methods that applied linear transformation such as PCA, which applied eigendecomposition to decompose the covariance matris. Unlike PCA, the axes of t-SNE plot does not have obvious meaning, while in PCA, each axes represents a linear combination of variables. In the data visualization below, the color was specified by the intensity of CD3 marker (High: red; Low: blue)
![FlowTSNE](/Figs/tsne_plot01.png)


### Exploring Markers distribution in one sample

Density plot of each marker in the sample "100715"
![FlowMarker Summary](/Figs/marker_summary.png)

Pairwise scatter plot of markers in the sample "100715"
![FlowMarker pairwise](/Figs/pairwise_plot.png)


### Comparing markers in different fcs files

The density plot of one marker (ex: CD3) in different samples
![FlowMarker summary CD3](/Figs/marker_summary_CD3.png)

**Gating in Flow Cytometry Analysis**

The [CD3 marker](https://en.wikipedia.org/wiki/CD3_(immunology)) is a co-receptor specific to T-cells. CD3 is involved in T-cells activation, including cytotoxic T-cells (CD8+) and helper T-cells (CD4+). Therefore, the possible T-cells can be selected by selecting high intensity of the CD3 marker. 
![FlowGate](/Figs/flow_gating.png)

**Visualize clincal information in scatter plots**

Scatter plots between CD45RO and CD3 in multiple samples.
![FlowMarker CD45RO CD3 samples](/Figs/marker_CD45RO_CD3_samples.png)

The clinical data can be merged with flow cytometry data and visualized with the scatter plots. The clinical information is added into the plot to provide detailed exploration than the plot above. Note that to simplified the plot, only the 50% of the cell proportion in 1st quadrant was visualized in each sample.
![FlowMarker CD45RO CD3 SurvTime](/Figs/marker_CD45RO_CD3_SurvTime.png)


### Construct sample network
In the heatmap and scatter plot, it may not be easy to visualize the relationship among cells / observations. In this section, I used a different perspective to explore a cell population. For a sample, I first compared the cells (observations; rows) using correlation as distance function. The distance matrix was then converted to simiality matrix and further converted into adjacency matrix of a network by selecting an arbitrary cutoff value (which can be specify easily in the shiny app).

Note that I plotted one fcs file in this section. In the shiny app, users are allowed to choose any fcs file / sample.
![FlowNetwork](/Figs/network_cell.png)


# Reference
- [1] Data Download Link: http://flowrepository.org/id/FR-FCM-ZZZK
- [2] Aghaeepour N (2012) IDCRP's HIV Natural History Study data set.
- [3] Aghaeepour N (2012) Early immunologic correlates of HIV protection can be identified from computational analysis of complex multivariate T-cell flow cytometry assays
