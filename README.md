# Road networks and robustness to flooding on US Atlantic and Gulf barrier islands

This repository contains the code and instructions needed to extract the required data and explore road network robustness to coastal flooding on US Atlantic and Gulf barrier islands.

## Project structure

### Directories
Create the following folder in your working directory:
* Data: this folder will hold all the required datasets.

Almost all data files must be downloaded by the user using the provided notebooks and put in the /Data/ directory. Only three .csv files are available for direct download in the "Data" folder of this repository.

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
* Analysis.ipynb &rightarrow; The purpose of this notebook is to identify, for each barrier island, the elevation and exceedance probability of the critical node that causes the failure of the network and the overall robustness of each road network to flood-induced failures. For statistically meaningful metrics of network structure, the analysis is restricted to the 71 US Atlantic and Gulf barrier islands with drivable road networks of at least 100 nodes. In this analysis, network nodes are sequentially removed, starting from the lowest elevation, to mimic a simplified, “bathtub” flooding scenario. As nodes are deactivated, the original network (connected in a large cluster known as the giant-connected component) breaks into smaller unconnected subnetworks until its complete fragmentation. The identification of the critical node that causes the failure of each road network provides an estimation of the flood high necessary to cause the collapse of the network and the probability of occurrence of such an event. Overall network robustness, estimated by systematically measuring the summed size of the giant-connected component during the entire node removal, supplements the analysis by considering the functioning of the network even after the critical node is damaged, which  allows comparisons between barrier island road networks in terms of the entire architecture, vs. solely the elevation (and exceedance) of the single critical node.

## Requirements
Disk space: 167 GB 
Python 3.4.2
### Python packages
affine 2.3.0, argon2-cffi 20.1.0, async-generator 1.10, attrs 21.2.0, backcall 0.2.0, backports.functools-lru-cache 1.6.4, basemap 1.2.1, beautifulsoup4 4.9.3, bleach 3.3.0, branca 0.4.2, brotlipy 0.7.0, cartopy 0.18.0, certifi 2021.10.8, cffi 1.14.5, chardet 4.0.0, click-plugins 1.1.1, click 7.1.2, cligj 0.7.2, colorama==0.4.4', 'contextily==1.1.0', 'cryptography==3.4.7', 'cycler==0.10.0', 'debugpy==1.3.0', 'decorator==5.0.9', 'defusedxml==0.7.1', 'descartes==1.1.0', 'entrypoints==0.3', 'fiona==1.8.18', 'folium==0.0.0', 'future==0.18.2', 'gdal==3.2.1', 'geographiclib==1.52', 'geojson==2.5.0', 'geopandas==0.9.0', 'geoplot==0.4.4', 'geopy==2.1.0', 'idna==2.10', 'importlib-metadata==4.6.0', 'ipykernel==6.0.0', 'ipython-genutils==0.2.0', 'ipython==7.25.0', 'jedi==0.18.0', 'jinja2==3.0.1', 'joblib==1.0.1', 'json5==0.9.5', 'jsonschema==3.2.0', 'jupyter-client==6.1.12', 'jupyter-core==4.7.1', 'jupyterlab-pygments==0.1.2', 'jupyterlab-server==1.2.0', 'jupyterlab==2.2.9', 'kiwisolver==1.3.1', 'libpysal==4.5.1', 'mapclassify==2.4.2', 'markupsafe==2.0.1', 'matplotlib-inline==0.1.2', 'matplotlib-scalebar==0.7.2', 'matplotlib==3.4.2', 'mercantile==1.2.1', 'mistune==0.8.4', 'momepy==0.4.3', 'mplleaflet==0.0.5', 'munch==2.5.0', 'nbclient==0.5.3', 'nbconvert==6.1.0', 'nbformat==5.1.3', 'nest-asyncio==1.5.1', 'networkx==2.5', 'notebook==6.4.0', 'numpy==1.21.0', 'olefile==0.46', 'osmnx==1.0.1', 'packaging==20.9', 'pandas==1.2.5', 'pandocfilters==1.4.2', 'parso==0.8.2', 'patsy==0.5.1', 'percolate==0.4.6', 'pickleshare==0.7.5', 'pillow==8.2.0', 'pip==21.1.3', 'plotly-express==0.4.1', 'plotly==5.1.0', 'prometheus-client==0.11.0', 'prompt-toolkit==3.0.19', 'pycparser==2.20', 'pycrs==1.0.2', 'pygeos==0.8', 'pygments==2.9.0', 'pyopenssl==20.0.1', 'pyparsing==2.4.7', 'pyproj==3.1.0', 'pyrsistent==0.17.3', 'pyshp==2.1.3', 'pysocks==1.7.1', 'python-dateutil==2.8.1', 'pytz==2021.1', 'pywin32==300', 'pywinpty==1.1.3', 'pyzmq==22.1.0', 'rasterio==1.2.6', 'requests==2.25.1', 'retrying==1.3.3', 'rtree==0.9.7', 'scikit-learn==0.24.2', 'scipy==1.7.0', 'seaborn==0.11.1', 'send2trash==1.7.1', 'setuptools==49.6.0.post20210108', 'shapely==1.7.1', 'simoa==0.4.1', 'six==1.15.0', 'snuggs==1.4.7', 'soupsieve==2.0.1', 'statsmodels==0.12.2', 'tenacity==7.0.0', 'terminado==0.10.1', 'testpath==0.5.0', 'threadpoolctl==2.1.0', 'tornado==6.1', 'tqdm==4.61.1', 'traitlets==5.0.5', 'uncertainties==3.1.5', 'urllib3==1.26.7', 'wcwidth==0.2.5', 'webencodings==0.5.1', 'wheel==0.36.2', 'win-inet-pton==1.1.0', 'wincertstore==0.2', 'zipp==3.4.1'

## Contributing
The code can be slow sometimes, so if anyone knows how to make it faster, please contribute!
