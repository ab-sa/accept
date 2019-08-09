[![Build Status](https://travis-ci.org/resplab/accept.svg?branch=master)](https://travis-ci.org/resplab/accept)
[![CRAN Status](https://www.r-pkg.org/badges/version/accept)](https://cran.r-project.org/web/packages/accept/index.html)
[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)

# accept
R package for the ACute COPD Exacerbation Prediction Tool (ACCEPT)

Please refer to the published paper for more information: 

Amin Adibi, Don D Sin, Abdollah Safari, Kate M Johnson, Shawn Aaron, J Mark FitzGerald, Mohsen Sadatsafavi (2019). Development and External Validation of the Acute COPD Exacerbation Prediction Tool (ACCEPT). bioRxiv 651901; doi: [https://doi.org/10.1101/651901](https://doi.org/10.1101/651901)

## Installation

The latest stable version can be downloaded from CRAN:  
`install.packages ('accept')`

Alternatively, you can download the latest development version from GitHub:

```
install.packages("devtools")
devtools::install_github("resplab/accept")
```

# Web App for ACCEPT 

ACCEPT is also available as web app, accessible at [http://resp.core.ubc.ca/ipress/accept](http://resp.core.ubc.ca/ipress/accept)

# ACCEPT in R

### Sample Data

To get started, there is an R data frame with the package of sample patient data. I have printed columns 1-13 and 14-19 separately because there isn't enough space:

```
library(accept)
samplePatients <- accept::samplePatients

```

### Exacerbation Prediction

To get a prediction for exacerbation rate, you will need to pass in a patient vector:

```
results <- predictACCEPT(samplePatients[1,])
print(t(results))
```

The **predictACCEPT()** function returns a data frame with the original patient data, along with the predictions for different treatment options. 

To visualize the data, there is a graphing function called **plotExacerbations()**, which creates a Plotly bar graph. You have the option of selecting **probability** or **rate** for which prediction you want to see, and either **CI** or **PI** to select the confidence interval or prediction interval respectively.

```
plotExacerbations(results, type="probability", interval = "CI")
```

```
plotExacerbations(results, type="probability", interval = "PI")
```

```
plotExacerbations(results, type="rate", interval = "CI")
```

### Probability of N Exacerbations (Poisson)

We can also calculate the predicted number of exacerbations in a year:

```
patientResults = predictACCEPT(samplePatients[1,])
exacerbationsMatrix = predictCountProb(patientResults, n = 10, shortened = TRUE)
print(exacerbationsMatrix)
```

The shortened parameter groups the probabilities from 3-10 exacerbations into one category, "3 or more exacerbations." To see all n exacerbation probabilities:

```
exacerbationsMatrix = predictCountProb(patientResults, n = 10, shortened = FALSE)
print(exacerbationsMatrix)
```

To visualize the matrix as a heatmap, we can use the function **plotHeatMap**:

```
plotHeatMap(patientResults, shortened = FALSE)
```

## Cloud-based API Access 

The [PRISM platform](http://prism.resp.core.ubc.ca) allows users to access ACCEPT through the cloud. A MACRO-enabled Excel-file can be used to interact with the model and see the results. To download the PRISM Excel template file for ACCEPT, please refer to the [PRISM model repository](http://resp.core.ubc.ca/ipress/prism).

## User Manual

An interactive user manual that describes the study, the web app, the API, and the R package is available [here](https://resplab.github.io/acceptManual/section-introduction.html).

## Citation

Please cite:

The manuscript is currently under peer-review. A preprint is available on bioRxiv
```Amin Adibi, Don D Sin, Abdollah Safari, Kate M Johnson, Shawn Aaron, J Mark FitzGerald, Mohsen Sadatsafavi (2019). Development and External Validation of the Acute COPD Exacerbation Prediction Tool (ACCEPT). bioRxiv 651901; doi:10.1101/651901```
