## Weather project for "Python: Data Analysis" LinkedIn course

### Exploring weather history in Kyiv city, Ukraine.

__Besides training tasks from [Data Analysis course](https://www.linkedin.com/learning/python-data-analysis-2015) (to find and visualize a data for US cities), I'm interested in climate changing in Kyiv city, Ukraine - my home city.__

I'm using data from station "KIEV, UP", Network:ID "GHCND:UPM00033345". Location: Ukrainian Hydrometeorological Institute. The largest set of data comparing to other stations: from 1881-01-01 to 2020-07-20. (Latitude / Longitude: 50.4000° / 30.5331°, Elevation: 166 m)

Data access provided by Global Historical Climatology Network - ([GHCN](https://www.ncdc.noaa.gov/data-access/land-based-station-data/land-based-datasets/global-historical-climatology-network-ghcn)). This is data service from the USA National Oceanic and Atmospheric Administration, NOAA / National Centers for Environmental Information, NCEI (former National Climatic Data Center, NCDC)

__General algorithm of data processing:__

- get list of weather stations: [ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt](ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt) (or [https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt));

- using simple parser, find a station by city name and get a filename (Kiyv -> UPM00033345.dly);
 
- download dataset ("UPM00033345.dly" for my case) from [ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/all/](ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/all/) (or [https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/all/](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/all/));

- parse the file using description in readme.txt ([https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt)) from GHCN;

- extract needed parameters - daily max/min temperature (TMAX, TMIN) and their time reference;

- plot overall picture for temperatures over all years;

- to clean the data - if there are gaps, NANs etc.;

__My specific tasks:__

1. to plot stacked graph of TMAX, TMIN over all period; 

2. to build dependencies of TMAX, TMIN on specified dates/seasons;

__Task 1 - summary of maximum and minimum temperature over all observable period, and comparison with my birthday year - 1980 :)__


![Output figure](https://github.com/andr-nau/weather_history/blob/master/Fig1.png "KYIV data")


__Task 2 - Check the trends in winter temperatures.__
 
I extracted the temperature data for the winter months for each year and averaged it over three months. Additionally, I calculated trend line over all years:

![Output figure](https://github.com/andr-nau/weather_history/blob/master/Fig2.png "Winter averaged temperatures")
