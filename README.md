# GEOG5990M
Repo for GEOG5990M module project
# Background 
This project intends to determine if there is a relationship between health outcomes and accessibility of green spaces across Dudley Metropolitan Borough Council. The code within could be repurposed to assess this relationship across any geographical unit within the Country of England. 
The intention of the study is to identify if there is such a relationship, and if it is present, present it in ways that could be useful to policy makers when planning for additional public green space or assessing proposals that would remove existing provision. 
# Data
For health outcomes, the constituent Health Deprivation domain of the English Indices of Multiple Deprivation (2019) has been utilised (1). This data was downloaded from the Ministry of Housing, Communities & Local Government via opendatacommunities.org (1) at the Lower Super Output Area (LSOA) 2011 geography. Details 
For access to green spaces a dataset compiled by the Office for National Statistics (ONS) has been utilised (3). The original dataset was downloaded from the ONS (3) as an xlsx file, the relevant sheet from that document was then saved as a CSV for further analysis. 
A shapefile of LSOA census geographies was downloaded from the ONS Open Geography Portal (4). As the datasets being used are dated 2019 and 2020, the 2011 boundaries for English LSOAs were used, to avoid issues arising from the redrawing of boundaries for the 2021 census, specifically Lower layer Super Output Areas (December 2011) Boundaries EW BFC (V3) (4). 
# Code purpose and structure
The Jupyter notebook and GitHub repository provided contain all the relevant code and files to recreate this analysis. 
## Non-spatial Data
The code will load in the relevant packages, load the non-spatial datasets referenced above from the Github repo and then begin cleaning and filtering the dataframes. For the green space dataset, this only involved removing erroneous blank columns and rows. 
The IoD19 dataset required manipulation to create single columns or the Health Deprivation Domain Score and Health Deprivation Domain Decile, as it was presented in a format where each LSOA had multiple records, for each domain and each measurement style of the domain (Rank, Decile and Score). Once the values for health deprivation score and decile are separated, they are joined into a single dataframe where each LSOA has a value for both score and decile (HDI_Score and HDI_Decile).
Additional columns are dropped from the green space access dataframe. Then green space access and HDI value datasets are then joined into a single dataframe. 
The notebook then contains a series of data visualisations in order to explore the relationships between the Health Deprivation values and green space accessibility. In doing so the dataset is filtered to just the Dudley MBC LSOAs. 
## Spatial Data
Given the size of the LSOA file downloaded from the ONS Geoportal, the whole dataset could not be uploaded to a GitHub repository. To make the data accessible, it was first downloaded to a google drive. The notebook then contains the code required to access the file from a google drive, extract a subset of it and create a downloadable geojson. This geojson was then uploaded to the Github repository for use in the analysis. 
Should it be required to assess a different Local Authority, the referenced master file should be downloaded to a google drive, and the commented-out code present in the notebook should be utilised and amended to create a more manageable dataset. This is not required to reproduce this study, however as the notebook will load in the required spatial dataset from the repository. 
The non-spatial data is then joined to this dataset to allow it to be mapped and analysed. 
Initially, all the green space accessibility fields are mapped to determine any spatial patterns. The same is then done for the Health Deprivation Deciles, using a red – blue spectrum which should be suitable for the colourblind. 
The notebook then undertakes Spearman’s Rank Correlation between the health deprivation score and accessibility fields. 
## Visualisations
Finally, two visualisations are presented. The first is a regression plot of the most highly correlated (but not related) variables. This is the Average garden size for houses within rural and built-up area and the health deprivation score. 
The second maps the two variables above to the Dudley LSOAs and presents them side by side, where LSOAs of low health score (as deciles) and low private garden space are highlighted. A third plot is provided to provide geographic context for the highlighted areas. 
The plots use yellow to orange palettes and highlight the LSOAs of interest in a highly contrasting blue to ensure the plots are readable to people with various kinds of colour-blindness. 

1: https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/835115/IoD2019_Statistical_Release.pdf

2: https://opendatacommunities.org/slice?dataset=http%3A%2F%2Fopendatacommunities.org%2Fdata%2Fsocietal-wellbeing%2Fimd2019%2Findices

3: https://www.ons.gov.uk/economy/environmentalaccounts/datasets/accesstopublicgreenspaceingreatbritain

4: https://geoportal.statistics.gov.uk/datasets/ons::lower-layer-super-output-areas-december-2011-boundaries-ew-bfc-v3/about
