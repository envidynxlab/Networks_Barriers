# Road networks and robustness to flooding on US Atlantic and Gulf barrier islands

This repository contains the code and instructions needed to extract the required data and explore road network robustness to coastal flooding on US Atlantic and Gulf barrier islands.

Preprint: [![Earth ArXiv Preprint
DOI](https://img.shields.io/badge/%F0%9F%8C%8D%F0%9F%8C%8F%F0%9F%8C%8E%20EarthArXiv-doi.org%2F10.31223%2FX55D1G-%23FF7F2A)](https://doi.org/10.31223/X55D1G)

OA Paper (Earth's Future): https://doi.org/10.1029/2021EF002581

Code (this repository): [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6354835.svg)](https://doi.org/10.5281/zenodo.6354835)




## Project structure

### Directories
Create the following folder in your working directory:
* Data: to hold all the required datasets.

Almost all data files must be downloaded by the user using the provided notebooks and saved in the /Data/ directory. Only three .csv files are available for direct download in the "Data" folder of this repository.

## Data
All data used in this project are open source and publicly available. To download the data, run the provided notebooks in the following order, as they rely on data generated in previous notebooks:
* Barriers.ipynb &rightarrow; With this notebook, the digitized perimeters of 702 modern barrier islands are downloaded from the semi-global database created by Mulhern et al. (2017) and available at https://hive.utah.edu/concern/datasets/cf95jb516?locale=en (Mulhern et al., 2021). From those, the 184 barrier islands located along the Atlantic and Gulf coasts of the US are selected and 200-meter buffers are created to be used in the next step.
* CUDEM.ipynb &rightarrow; This notebook downloads elevation tiles from the Continuously Updated Digital Elevation Model (CUDEM), a ninth arc-second resolution bathymetric-topographic dataset developed by NOAA's National Centers for Environmental Information (NCEI) and available at https://coast.noaa.gov/htdata/raster2/elevation/NCEI_ninth_Topobathy_2014_8483/. Because of the size of this dataset and to simplify further analysis, the corresponding tiles are clipped to the extent of each barrier island using the 200-meter buffers created before. The result will be CUDEM mosaics for each barrier island. 200-meter buffers are used to make sure that every node in the road network falls within the CUDEM mosaic and can therefore be associated with an elevation. 
* Exceedance.ipynb &rightarrow; The purpose of this notebook is to calculate exceedance probabilities of extreme water levels in the US Atlantic and Gulf barrier islands using a GEV approach. For the correct use of this notebook, download the three tables provided in the "Data" section of this repository in your /Data/ directory: 
  * Stations.csv: lists the 112 NWLON long-term water level stations used in NOAA Technical Report NOS CO-OPS 067 (Zervas, 2013) available in https://tidesandcurrents.noaa.gov/publications/NOAA_Technical_Report_NOS_COOPS_067a.pdf. (Table 1 in report).
  * Parameters.csv: provides the GEV parameters (scale, shape, and location) for the NOAA CO-OPS (Center for Operational Oceanographic Products and Services) stations calculated in NOAA's report. (Table A in report).
  * MHHW.csv> provides Mean Higher High Water levels for the closest station to each barrier island (manually extracted from https://tidesandcurrents.noaa.gov/est/).
 * Roads.ipynb &rightarrow; This notebook downloads drivable road networks from OpenStreetMap using the Python package OSMnx (Boeing, 2017). Detailed installation instructions for OSMnx package are found at https://osmnx.readthedocs.io/en/stable/. For each network node, elevation is retrieved using CUDEM mosaics and matched to the corresponding exceedance probability of extreme water levels. 

## Analysis
The following notebooks contain the analysis and figures described in the manuscript.
* Analysis.ipynb &rightarrow; The purpose of this notebook is to identify, for each barrier island, the elevation and exceedance probability of the critical node that causes the failure of the network and the overall robustness of each road network to flood-induced failures. For statistically meaningful metrics of network structure, the analysis is restricted to the 72 US Atlantic and Gulf barrier islands with drivable road networks of at least 100 nodes. This notebook also extracts basic statistics for each of these networks.
* Figures.ipynb &rightarrow; This notebook generates the figures included in the manuscript.
* Statistics.ipynb &rightarrow; This notebook contains the queries and statistics included in the manuscript.

### Dataset
A copy of the dataset (graphml files) used in the paper can be found on Zenodo:

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6354814.svg)](https://doi.org/10.5281/zenodo.6354814)


## Requirements
Disk space: 175 GB 

Python 3.4.2

### Important Python packages
- contextily 1.1.0,
- fiona 1.8.18,
- gdal 3.2.1,
- geopandas 0.9.0,
- matplotlib 3.4.2,
- matplotlib-inline 0.1.2,
- matplotlib-scalebar 0.7.2,
- networkx 2.5,
- numpy 1.21.0,
- osmnx 1.0.1,
- pandas 1.2.5,
- pycrs 1.0.2,
- rasterio 1.2.6,
- requests 2.25.1,
- seaborn 0.11.1,
- scipy 1.7.0,
- shapely 1.7.1,
- urllib3 1.26.7,
- zipp 3.4.1,

## Contributing
The code can be slow sometimes, so if anyone knows how to make it faster, please contribute!
