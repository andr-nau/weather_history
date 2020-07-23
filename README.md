## Weather project for "Python: Data Analysis" LinkedIn course

Exploring history of weather in Kyiv, using data from station "KIEV, UP", Network:ID "__GHCND:UPM00033345__". Location: Ukrainian Hydrometeorological Institute. The largest set of data: from 1881-01-01 to 2020-07-20.
(Latitude / Longitude: 50.4000° / 30.5331°, Elevation: 166 m)

I'm using open data from Global Historical Climatology Network - (GHCN).

This is data service from the USA National Oceanic and Atmospheric Administration, NOAA / National Centers for Environmental Information, NCEI (former National Climatic Data Center, NCDC)


Besides training tasks from Data Analysis cource (to find and visualize a data for US cities), I'm interested in changing of winter temperatures over the years for Kyiv city, Ukraine, - my home city.

General algorithm:

- find station in list: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt (or https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt)

- download dataset named "UPM00033345.dly" from ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/all/ (or https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/all/)

- parse the file using description in readme.txt https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt from GHCN

- to get overall picture for temperatures over all years

- to process the data - if there are gaps, NANs

- to extract needed parameters - daily TMAX, TMIN and their time references

- to build dependencies of TMAX, TMIN on specified timing