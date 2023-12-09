# data-512-final-project
DATA512 Final Project

# Goal
Estimate the impact of wildfires on the housing market of the city of Texarkana, TX.

# Data Sources
- [USGS Wildfire data](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
- [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
- [FRED Housing Price Index](https://fred.stlouisfed.org/series/ATNHPIUS45500Q)
- [FRED Real GDP](https://fred.stlouisfed.org/series/RGMP45500)
- [FRED Resident Population](https://fred.stlouisfed.org/series/TEXPOP)

# Data Terms of Use
- [USGS Terms of Use](https://www.usgs.gov/faqs/what-are-terms-uselicensing-map-services-and-data-national-map)
- [AQS Terms of Use](https://aqs.epa.gov/aqsweb/documents/data_api.html#signup)
- [FRED Terms of Use](https://fred.stlouisfed.org/legal/#full-fred-terms)

# API Documentation
- [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)

# AQS API Key
- Sign up for an API key using the link to the AQS API above.
- Store this token in a .env file stored in your local clone of the repository.
- Format it as: AQS_API = '[INSERT ACCESS TOKEN HERE]'.
- The main notebook will load the .env file to extract the API key by searching for an 'AQS_API' variable in the loaded .env file.
- The repository ignores the .env so that it will not push to any remote Git repository.

# Code
- All of the analysis lives in the notebook [analyze_wildfires.ipynb](https://github.com/jmic94/data-512-final-project/blob/main/code/analyse_wildfires.ipynb).
- [epa_air_quality_history_example.ipynb](https://github.com/jmic94/data-512-final-project/blob/main/code/epa_air_quality_history_example.ipynb) contains sample code for using the AQS API along with the code license information.
- [wildfire_geo_proximity_example.ipynb](https://github.com/jmic94/data-512-final-project/blob/main/code/wildfire_geo_proximity_example.ipynb) contains sample code for working with the USGS wildfire dataset along with the code license information.
- [wildfire](https://github.com/jmic94/data-512-final-project/tree/main/code/wildfire) contains a Python class that other notebooks import.

# Inputs
- USGS_Wildland_Fire_Combined_Dataset.json.
- Obtain this JSON file from the USGS link above.
- Download the file called 'GeoJSON Files.zip'.
- Unzip this zip file in a folder called 'input' in this repo.
- Any code that utilizes this JSON will access it from this location.
- The repo ignores the JSON since it is a very large 2 GB file.
- The rest of the data needed for analysis come from the AQS API and FRED.
- FRED files:
    - ATNHPIUS45500Q.csv
        - contains the following variables:
            - DATE: date of observation
            - ATNHPIUS45500Q: housing price index on date
    - RGMP45500.csv
        - contains the following variables:
            - DATE: date of observation
            - RGMP45500: real GDP on date
    - TEXPOP.csv
        - contains the following variables:
            - DATE: date of observation
            - TEXPOP: resident population on date

# Intermediates
- [aqs.csv](https://github.com/jmic94/data-512-final-project/blob/main/intermediate/aqs_data.csv) contains the AQI data from 1963 to 2023 for air quality monitoring stations in Texerkana TX.
    - This file contains the following variables:
        - site_number: site ID of monitoring station
        - aqi: AQI measurement
        - local_site_name: name of monitoring station
        - site_address: local address of monitoring station
        - state: state of monitoring station
        - county: county of monitoring station
        - city: city of monitoring station
- [distances.csv](https://github.com/jmic94/data-512-final-project/blob/main/intermediate/distances.csv) contains the wildfire data from USGS along with their calculated distance to Texarkana, TX.
    - This file contains the following variables:
        - year: year of wildfire
        - name: name of wildfire
        - size_acres: acres burned by wildfire
        - type: type of wildfire
        - distance_to_tx: distance in miles of wildfires to Texarkana
        - sd_lat: latitude of perimeter point with shortest distance to Texarkana
        - sd_lon: longitude of perimeter point with shortest distance to Texarkana
- Both of these intermediate files are outputs from [analyze_wildfires.ipynb](https://github.com/jmic94/data-512-final-project/blob/main/code/analyse_wildfires.ipynb).

# Outputs
- [acres_burned.png](https://github.com/jmic94/data-512-final-project/blob/main/output/acres_burned.png) is a chart showing the total number of acres burned annually by wildfires within 1,250 miles of Texarkana, TX that occurred between 1963 to 2020.
- [distance_histogram.png](https://github.com/jmic94/data-512-final-project/blob/main/output/distance_histogram.png) is a chart showing the distribution of wildfire proximity to Texarkana, TX from 1963 to 2020.
- [est_vs_aqi.png](https://github.com/jmic94/data-512-final-project/blob/main/output/est_vs_aqi.png) is a chart comparing the annual smoke estimate and the annual fire season AQI from 1999 to 2020.
- [res_vs_fitted.png](https://github.com/jmic94/data-512-final-project/blob/main/output/res_vs_fitted.png) is a chart showing the residuals versus fitted values plot of the regression model.
- [data512_final_report.pdf](https://github.com/jmic94/data-512-final-project/blob/main/data512_final_report.pdf) is the final report of the analysis.

# Data Issues
- The AQI data can be sparse for older decades. I've found that the monitoring stations in Texerkana, TX begin having reliable data starting in the year 1999.

# Notes
- There are roughly 130,000 wildfires in the USGS dataset, of which around 63,000 occurred from 1963 onwards AND occurred within 1,250 miles of Texarkana, TX.
