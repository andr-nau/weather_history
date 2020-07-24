## Weather project for "Python: Data Analysis" LinkedIn course

### Exploring weather history in Kyiv city, Ukraine.

After the training during [Data Analysis course](https://www.linkedin.com/learning/python-data-analysis-2015) (learning NumPy by exploring weather statistics), I have been excited to extend this experience and to investigate some additional features of climate changing, specifically for Kyiv city, Ukraine - my home city.

In brief, I want to see overall behavior of climate in Kyiv during observable period, and, for example, trends for winter temperature. I would like to know if I can see a lot of snow next winter.     

I'm using dataset from station "KIEV, UP", Network:ID "GHCND:UPM00033345". Location: Ukrainian Hydrometeorological Institute. Latitude / Longitude: 50.4000° / 30.5331°, Elevation: 166 m. The largest set of data comparing to other stations: from 1881-01-01 to 2020-07-20.

Data access provided by Global Historical Climatology Network - ([GHCN](https://www.ncdc.noaa.gov/data-access/land-based-station-data/land-based-datasets/global-historical-climatology-network-ghcn)). This is data service from the USA National Oceanic and Atmospheric Administration, NOAA / National Centers for Environmental Information, NCEI (former National Climatic Data Center, NCDC)

__General algorithm of data processing:__

- get list of weather stations: [ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt](ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt) (or [https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt));

- using simple parser, find a station by city name and get a filename (Kiyv -> UPM00033345.dly);
 
- download dataset ("UPM00033345.dly" for my case) from [ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/all/](ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/daily/all/) (or [https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/all/](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/all/));

- parse the file using description in readme.txt ([https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt)) from GHCN;

- extract needed parameters - daily max/min temperature (TMAX, TMIN) and their date reference;

- plot overall picture for temperatures over all years;

- to clean the data - if there are any gaps, NANs etc.;

__My specific tasks:__

1. to plot yearly distribution of TMAX, TMIN over all years; 

2. to build dependencies of TMAX, TMIN on specified dates/seasons;

### Technologies used:

I'm using NumPy package to process the data: __genfromtxt function__ to read all data (data is fixed-field text file); __numpy arrays__ to store the data; __datetime64, timedelta64 functions__ to process the date information, __polyfit, poly1d__ to find the trends. Matplotlib package - to visualize the data (usual __plot function__, additionally __fill between function__ to show yearly distribution of temperatures stacked from all years.

***

## Workflow.

First, let's take a look on raw data. I have used structured numpy array and __genfromtxt__ function to load the full dataset, and then built a function to extract rows with specified observation parameters, e.g. TMAX or TMIN (daily max or min temperature, respectively). Raw data over all years of observation:
![Output figure](https://github.com/andr-nau/weather_history/blob/master/raw_day_temp.png "Raw dataset")

Dataset is not very accurate. After 2005 there are a lot of missing values (filled with NANs during procedure of extracting TMAX/TMIN):
![Output figure](https://github.com/andr-nau/weather_history/blob/master/raw_day_temp_2000.png "Raw dataset")

Besides of missing single values (marked as NAN after import), there are missing whole month records (rows of TMAX or TMIN for one month). By comparing number of TMAX or TMIN rows for each year (should be 12 of each type), I found missing monthly records in 12 different years. Example of badly documented years:
![Output figure](https://github.com/andr-nau/weather_history/blob/master/Bad_years.png "Bad years")

To proceed next, I filled NAN values using numpy __interp__ function. The resulting graph:
![Output figure](https://github.com/andr-nau/weather_history/blob/master/filled_day_temp.png "Filled NANs")

And detailed zoom:
![Output figure](https://github.com/andr-nau/weather_history/blob/master/interpolation_compare_raw.png "Filled NANs")

It looks reasonably. So, finally let's see an averaged picture for all period of observations. I used running mean calculations for this. 
![Output figure](https://github.com/andr-nau/weather_history/blob/master/averaged_filled_day_temp.png "Averaging over 365 days")

Some artifacts are present. For example, a dip after 1940. Or peak around 1938. It is connected with missing whole month records, not just a lot of NANs. It is visible on the next picture:

![Output figure](https://github.com/andr-nau/weather_history/blob/master/interpolation_compare_filled.png "Artifacts")



***

__Task 1. Yearly distribution of maximum and minimum temperatures over all observable period.__

I want to plot yearly distribution of maximum and minimum temperatures for all years, stacked in one graph. And additionally to compare with, say, 1980 -  my birthday year :)


![Output figure](https://github.com/andr-nau/weather_history/blob/master/Fig1.png "KYIV data")


__Task 2 - Check the trends in winter temperatures.__
 
I extracted the temperature data for the winter months for each year and averaged it over three months. Additionally, I calculated trend line over all years:

![Output figure](https://github.com/andr-nau/weather_history/blob/master/Fig2.png "Winter averaged temperatures")

From linear fitting we can obtain the slope of trend: 0.008 °C/year.

## Next steps:

- summer statistics
- comparison of trends
- comparison with Warsaw stats (my current place of residence) as well as world trends
- additional descriptive statistics