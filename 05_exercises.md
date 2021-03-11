---
title: 'Weekly Exercises #5'
author: "Brian Lee"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
## ✓ tibble  3.0.5     ✓ dplyr   1.0.2
## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
## ✓ readr   1.4.0     ✓ forcats 0.5.0
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.8.1, GDAL 3.1.1, PROJ 6.3.1
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
library(babynames)     # baby names dataset
```

```
## 
## Attaching package: 'babynames'
```

```
## The following object is masked from 'package:openintro':
## 
##     births
```

```r
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   year = col_double(),
##   month = col_double(),
##   service = col_character(),
##   departure_station = col_character(),
##   arrival_station = col_character(),
##   journey_time_avg = col_double(),
##   total_num_trips = col_double(),
##   avg_delay_all_departing = col_double(),
##   avg_delay_all_arriving = col_double(),
##   num_late_at_departure = col_double(),
##   num_arriving_late = col_double(),
##   delay_cause = col_character(),
##   delayed_number = col_double()
## )
```

```r
# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele.num = col_double(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = ""),
##   time_hr = col_double(),
##   dist_km = col_double(),
##   speed = col_double()
## )
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele = col_logical(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   date = col_date(format = ""),
##   state = col_character(),
##   fips = col_character(),
##   cases = col_double(),
##   deaths = col_double()
## )
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  

```r
namegraph <- babynames %>%
  group_by(year, sex) %>%
  summarize(numNames = n()) %>%
  ggplot(aes(x = year, y = numNames, color = sex)) +
  geom_line()
```

```
## `summarise()` regrouping output by 'year' (override with `.groups` argument)
```

```r
ggplotly(namegraph)
```

<!--html_preserve--><div id="htmlwidget-ad07ffb34d542d2d9c6b" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-ad07ffb34d542d2d9c6b">{"x":{"data":[{"x":[1880,1881,1882,1883,1884,1885,1886,1887,1888,1889,1890,1891,1892,1893,1894,1895,1896,1897,1898,1899,1900,1901,1902,1903,1904,1905,1906,1907,1908,1909,1910,1911,1912,1913,1914,1915,1916,1917,1918,1919,1920,1921,1922,1923,1924,1925,1926,1927,1928,1929,1930,1931,1932,1933,1934,1935,1936,1937,1938,1939,1940,1941,1942,1943,1944,1945,1946,1947,1948,1949,1950,1951,1952,1953,1954,1955,1956,1957,1958,1959,1960,1961,1962,1963,1964,1965,1966,1967,1968,1969,1970,1971,1972,1973,1974,1975,1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],"y":[942,938,1028,1054,1172,1197,1282,1306,1474,1479,1534,1533,1661,1652,1702,1808,1825,1799,1975,1842,2224,1943,2042,2083,2165,2234,2220,2399,2434,2548,2790,2868,3445,3707,4206,4967,5162,5312,5586,5559,5765,5871,5789,5739,5899,5771,5621,5603,5436,5275,5248,4977,5100,4858,4973,4892,4856,4927,4994,4952,5025,5085,5380,5368,5245,5241,5686,6103,6040,6065,6111,6211,6391,6499,6616,6725,6885,7012,7022,7196,7331,7529,7583,7663,7803,7533,7616,7849,8194,8708,9350,9638,9661,9805,10239,10609,10900,11324,11470,11967,12157,12186,12327,12065,12171,12500,12823,13255,13877,14546,15235,15459,15611,15797,15751,15753,15891,16160,16598,16941,17653,17970,18081,18430,18826,19182,20050,20560,20457,20179,19811,19560,19498,19231,19181,19074,18817,18309],"text":["year: 1880<br />numNames:   942<br />sex: F","year: 1881<br />numNames:   938<br />sex: F","year: 1882<br />numNames:  1028<br />sex: F","year: 1883<br />numNames:  1054<br />sex: F","year: 1884<br />numNames:  1172<br />sex: F","year: 1885<br />numNames:  1197<br />sex: F","year: 1886<br />numNames:  1282<br />sex: F","year: 1887<br />numNames:  1306<br />sex: F","year: 1888<br />numNames:  1474<br />sex: F","year: 1889<br />numNames:  1479<br />sex: F","year: 1890<br />numNames:  1534<br />sex: F","year: 1891<br />numNames:  1533<br />sex: F","year: 1892<br />numNames:  1661<br />sex: F","year: 1893<br />numNames:  1652<br />sex: F","year: 1894<br />numNames:  1702<br />sex: F","year: 1895<br />numNames:  1808<br />sex: F","year: 1896<br />numNames:  1825<br />sex: F","year: 1897<br />numNames:  1799<br />sex: F","year: 1898<br />numNames:  1975<br />sex: F","year: 1899<br />numNames:  1842<br />sex: F","year: 1900<br />numNames:  2224<br />sex: F","year: 1901<br />numNames:  1943<br />sex: F","year: 1902<br />numNames:  2042<br />sex: F","year: 1903<br />numNames:  2083<br />sex: F","year: 1904<br />numNames:  2165<br />sex: F","year: 1905<br />numNames:  2234<br />sex: F","year: 1906<br />numNames:  2220<br />sex: F","year: 1907<br />numNames:  2399<br />sex: F","year: 1908<br />numNames:  2434<br />sex: F","year: 1909<br />numNames:  2548<br />sex: F","year: 1910<br />numNames:  2790<br />sex: F","year: 1911<br />numNames:  2868<br />sex: F","year: 1912<br />numNames:  3445<br />sex: F","year: 1913<br />numNames:  3707<br />sex: F","year: 1914<br />numNames:  4206<br />sex: F","year: 1915<br />numNames:  4967<br />sex: F","year: 1916<br />numNames:  5162<br />sex: F","year: 1917<br />numNames:  5312<br />sex: F","year: 1918<br />numNames:  5586<br />sex: F","year: 1919<br />numNames:  5559<br />sex: F","year: 1920<br />numNames:  5765<br />sex: F","year: 1921<br />numNames:  5871<br />sex: F","year: 1922<br />numNames:  5789<br />sex: F","year: 1923<br />numNames:  5739<br />sex: F","year: 1924<br />numNames:  5899<br />sex: F","year: 1925<br />numNames:  5771<br />sex: F","year: 1926<br />numNames:  5621<br />sex: F","year: 1927<br />numNames:  5603<br />sex: F","year: 1928<br />numNames:  5436<br />sex: F","year: 1929<br />numNames:  5275<br />sex: F","year: 1930<br />numNames:  5248<br />sex: F","year: 1931<br />numNames:  4977<br />sex: F","year: 1932<br />numNames:  5100<br />sex: F","year: 1933<br />numNames:  4858<br />sex: F","year: 1934<br />numNames:  4973<br />sex: F","year: 1935<br />numNames:  4892<br />sex: F","year: 1936<br />numNames:  4856<br />sex: F","year: 1937<br />numNames:  4927<br />sex: F","year: 1938<br />numNames:  4994<br />sex: F","year: 1939<br />numNames:  4952<br />sex: F","year: 1940<br />numNames:  5025<br />sex: F","year: 1941<br />numNames:  5085<br />sex: F","year: 1942<br />numNames:  5380<br />sex: F","year: 1943<br />numNames:  5368<br />sex: F","year: 1944<br />numNames:  5245<br />sex: F","year: 1945<br />numNames:  5241<br />sex: F","year: 1946<br />numNames:  5686<br />sex: F","year: 1947<br />numNames:  6103<br />sex: F","year: 1948<br />numNames:  6040<br />sex: F","year: 1949<br />numNames:  6065<br />sex: F","year: 1950<br />numNames:  6111<br />sex: F","year: 1951<br />numNames:  6211<br />sex: F","year: 1952<br />numNames:  6391<br />sex: F","year: 1953<br />numNames:  6499<br />sex: F","year: 1954<br />numNames:  6616<br />sex: F","year: 1955<br />numNames:  6725<br />sex: F","year: 1956<br />numNames:  6885<br />sex: F","year: 1957<br />numNames:  7012<br />sex: F","year: 1958<br />numNames:  7022<br />sex: F","year: 1959<br />numNames:  7196<br />sex: F","year: 1960<br />numNames:  7331<br />sex: F","year: 1961<br />numNames:  7529<br />sex: F","year: 1962<br />numNames:  7583<br />sex: F","year: 1963<br />numNames:  7663<br />sex: F","year: 1964<br />numNames:  7803<br />sex: F","year: 1965<br />numNames:  7533<br />sex: F","year: 1966<br />numNames:  7616<br />sex: F","year: 1967<br />numNames:  7849<br />sex: F","year: 1968<br />numNames:  8194<br />sex: F","year: 1969<br />numNames:  8708<br />sex: F","year: 1970<br />numNames:  9350<br />sex: F","year: 1971<br />numNames:  9638<br />sex: F","year: 1972<br />numNames:  9661<br />sex: F","year: 1973<br />numNames:  9805<br />sex: F","year: 1974<br />numNames: 10239<br />sex: F","year: 1975<br />numNames: 10609<br />sex: F","year: 1976<br />numNames: 10900<br />sex: F","year: 1977<br />numNames: 11324<br />sex: F","year: 1978<br />numNames: 11470<br />sex: F","year: 1979<br />numNames: 11967<br />sex: F","year: 1980<br />numNames: 12157<br />sex: F","year: 1981<br />numNames: 12186<br />sex: F","year: 1982<br />numNames: 12327<br />sex: F","year: 1983<br />numNames: 12065<br />sex: F","year: 1984<br />numNames: 12171<br />sex: F","year: 1985<br />numNames: 12500<br />sex: F","year: 1986<br />numNames: 12823<br />sex: F","year: 1987<br />numNames: 13255<br />sex: F","year: 1988<br />numNames: 13877<br />sex: F","year: 1989<br />numNames: 14546<br />sex: F","year: 1990<br />numNames: 15235<br />sex: F","year: 1991<br />numNames: 15459<br />sex: F","year: 1992<br />numNames: 15611<br />sex: F","year: 1993<br />numNames: 15797<br />sex: F","year: 1994<br />numNames: 15751<br />sex: F","year: 1995<br />numNames: 15753<br />sex: F","year: 1996<br />numNames: 15891<br />sex: F","year: 1997<br />numNames: 16160<br />sex: F","year: 1998<br />numNames: 16598<br />sex: F","year: 1999<br />numNames: 16941<br />sex: F","year: 2000<br />numNames: 17653<br />sex: F","year: 2001<br />numNames: 17970<br />sex: F","year: 2002<br />numNames: 18081<br />sex: F","year: 2003<br />numNames: 18430<br />sex: F","year: 2004<br />numNames: 18826<br />sex: F","year: 2005<br />numNames: 19182<br />sex: F","year: 2006<br />numNames: 20050<br />sex: F","year: 2007<br />numNames: 20560<br />sex: F","year: 2008<br />numNames: 20457<br />sex: F","year: 2009<br />numNames: 20179<br />sex: F","year: 2010<br />numNames: 19811<br />sex: F","year: 2011<br />numNames: 19560<br />sex: F","year: 2012<br />numNames: 19498<br />sex: F","year: 2013<br />numNames: 19231<br />sex: F","year: 2014<br />numNames: 19181<br />sex: F","year: 2015<br />numNames: 19074<br />sex: F","year: 2016<br />numNames: 18817<br />sex: F","year: 2017<br />numNames: 18309<br />sex: F"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)","dash":"solid"},"hoveron":"points","name":"F","legendgroup":"F","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1880,1881,1882,1883,1884,1885,1886,1887,1888,1889,1890,1891,1892,1893,1894,1895,1896,1897,1898,1899,1900,1901,1902,1903,1904,1905,1906,1907,1908,1909,1910,1911,1912,1913,1914,1915,1916,1917,1918,1919,1920,1921,1922,1923,1924,1925,1926,1927,1928,1929,1930,1931,1932,1933,1934,1935,1936,1937,1938,1939,1940,1941,1942,1943,1944,1945,1946,1947,1948,1949,1950,1951,1952,1953,1954,1955,1956,1957,1958,1959,1960,1961,1962,1963,1964,1965,1966,1967,1968,1969,1970,1971,1972,1973,1974,1975,1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],"y":[1058,997,1099,1030,1125,1097,1110,1067,1177,1111,1161,1127,1260,1179,1239,1241,1266,1229,1289,1200,1506,1210,1320,1306,1395,1421,1413,1549,1584,1679,1839,1999,2906,3261,3759,4390,4534,4602,4813,4810,4990,4986,4967,4904,4970,4867,4837,4803,4724,4543,4541,4320,4284,4154,4207,4145,4037,4019,4036,3967,3936,4000,4045,4040,3909,3783,4019,4268,4199,4203,4191,4251,4257,4339,4352,4388,4450,4552,4499,4573,4590,4652,4623,4619,4593,4420,4536,4550,4741,5040,5430,5655,5750,5876,6005,6335,6491,6851,6759,7071,7288,7286,7364,7338,7332,7581,7826,8148,8487,9227,9484,9646,9816,10169,10244,10327,10532,10811,11301,11609,12116,12299,12482,12753,13220,13364,14032,14390,14613,14523,14256,14343,14234,14038,14047,14024,14162,14160],"text":["year: 1880<br />numNames:  1058<br />sex: M","year: 1881<br />numNames:   997<br />sex: M","year: 1882<br />numNames:  1099<br />sex: M","year: 1883<br />numNames:  1030<br />sex: M","year: 1884<br />numNames:  1125<br />sex: M","year: 1885<br />numNames:  1097<br />sex: M","year: 1886<br />numNames:  1110<br />sex: M","year: 1887<br />numNames:  1067<br />sex: M","year: 1888<br />numNames:  1177<br />sex: M","year: 1889<br />numNames:  1111<br />sex: M","year: 1890<br />numNames:  1161<br />sex: M","year: 1891<br />numNames:  1127<br />sex: M","year: 1892<br />numNames:  1260<br />sex: M","year: 1893<br />numNames:  1179<br />sex: M","year: 1894<br />numNames:  1239<br />sex: M","year: 1895<br />numNames:  1241<br />sex: M","year: 1896<br />numNames:  1266<br />sex: M","year: 1897<br />numNames:  1229<br />sex: M","year: 1898<br />numNames:  1289<br />sex: M","year: 1899<br />numNames:  1200<br />sex: M","year: 1900<br />numNames:  1506<br />sex: M","year: 1901<br />numNames:  1210<br />sex: M","year: 1902<br />numNames:  1320<br />sex: M","year: 1903<br />numNames:  1306<br />sex: M","year: 1904<br />numNames:  1395<br />sex: M","year: 1905<br />numNames:  1421<br />sex: M","year: 1906<br />numNames:  1413<br />sex: M","year: 1907<br />numNames:  1549<br />sex: M","year: 1908<br />numNames:  1584<br />sex: M","year: 1909<br />numNames:  1679<br />sex: M","year: 1910<br />numNames:  1839<br />sex: M","year: 1911<br />numNames:  1999<br />sex: M","year: 1912<br />numNames:  2906<br />sex: M","year: 1913<br />numNames:  3261<br />sex: M","year: 1914<br />numNames:  3759<br />sex: M","year: 1915<br />numNames:  4390<br />sex: M","year: 1916<br />numNames:  4534<br />sex: M","year: 1917<br />numNames:  4602<br />sex: M","year: 1918<br />numNames:  4813<br />sex: M","year: 1919<br />numNames:  4810<br />sex: M","year: 1920<br />numNames:  4990<br />sex: M","year: 1921<br />numNames:  4986<br />sex: M","year: 1922<br />numNames:  4967<br />sex: M","year: 1923<br />numNames:  4904<br />sex: M","year: 1924<br />numNames:  4970<br />sex: M","year: 1925<br />numNames:  4867<br />sex: M","year: 1926<br />numNames:  4837<br />sex: M","year: 1927<br />numNames:  4803<br />sex: M","year: 1928<br />numNames:  4724<br />sex: M","year: 1929<br />numNames:  4543<br />sex: M","year: 1930<br />numNames:  4541<br />sex: M","year: 1931<br />numNames:  4320<br />sex: M","year: 1932<br />numNames:  4284<br />sex: M","year: 1933<br />numNames:  4154<br />sex: M","year: 1934<br />numNames:  4207<br />sex: M","year: 1935<br />numNames:  4145<br />sex: M","year: 1936<br />numNames:  4037<br />sex: M","year: 1937<br />numNames:  4019<br />sex: M","year: 1938<br />numNames:  4036<br />sex: M","year: 1939<br />numNames:  3967<br />sex: M","year: 1940<br />numNames:  3936<br />sex: M","year: 1941<br />numNames:  4000<br />sex: M","year: 1942<br />numNames:  4045<br />sex: M","year: 1943<br />numNames:  4040<br />sex: M","year: 1944<br />numNames:  3909<br />sex: M","year: 1945<br />numNames:  3783<br />sex: M","year: 1946<br />numNames:  4019<br />sex: M","year: 1947<br />numNames:  4268<br />sex: M","year: 1948<br />numNames:  4199<br />sex: M","year: 1949<br />numNames:  4203<br />sex: M","year: 1950<br />numNames:  4191<br />sex: M","year: 1951<br />numNames:  4251<br />sex: M","year: 1952<br />numNames:  4257<br />sex: M","year: 1953<br />numNames:  4339<br />sex: M","year: 1954<br />numNames:  4352<br />sex: M","year: 1955<br />numNames:  4388<br />sex: M","year: 1956<br />numNames:  4450<br />sex: M","year: 1957<br />numNames:  4552<br />sex: M","year: 1958<br />numNames:  4499<br />sex: M","year: 1959<br />numNames:  4573<br />sex: M","year: 1960<br />numNames:  4590<br />sex: M","year: 1961<br />numNames:  4652<br />sex: M","year: 1962<br />numNames:  4623<br />sex: M","year: 1963<br />numNames:  4619<br />sex: M","year: 1964<br />numNames:  4593<br />sex: M","year: 1965<br />numNames:  4420<br />sex: M","year: 1966<br />numNames:  4536<br />sex: M","year: 1967<br />numNames:  4550<br />sex: M","year: 1968<br />numNames:  4741<br />sex: M","year: 1969<br />numNames:  5040<br />sex: M","year: 1970<br />numNames:  5430<br />sex: M","year: 1971<br />numNames:  5655<br />sex: M","year: 1972<br />numNames:  5750<br />sex: M","year: 1973<br />numNames:  5876<br />sex: M","year: 1974<br />numNames:  6005<br />sex: M","year: 1975<br />numNames:  6335<br />sex: M","year: 1976<br />numNames:  6491<br />sex: M","year: 1977<br />numNames:  6851<br />sex: M","year: 1978<br />numNames:  6759<br />sex: M","year: 1979<br />numNames:  7071<br />sex: M","year: 1980<br />numNames:  7288<br />sex: M","year: 1981<br />numNames:  7286<br />sex: M","year: 1982<br />numNames:  7364<br />sex: M","year: 1983<br />numNames:  7338<br />sex: M","year: 1984<br />numNames:  7332<br />sex: M","year: 1985<br />numNames:  7581<br />sex: M","year: 1986<br />numNames:  7826<br />sex: M","year: 1987<br />numNames:  8148<br />sex: M","year: 1988<br />numNames:  8487<br />sex: M","year: 1989<br />numNames:  9227<br />sex: M","year: 1990<br />numNames:  9484<br />sex: M","year: 1991<br />numNames:  9646<br />sex: M","year: 1992<br />numNames:  9816<br />sex: M","year: 1993<br />numNames: 10169<br />sex: M","year: 1994<br />numNames: 10244<br />sex: M","year: 1995<br />numNames: 10327<br />sex: M","year: 1996<br />numNames: 10532<br />sex: M","year: 1997<br />numNames: 10811<br />sex: M","year: 1998<br />numNames: 11301<br />sex: M","year: 1999<br />numNames: 11609<br />sex: M","year: 2000<br />numNames: 12116<br />sex: M","year: 2001<br />numNames: 12299<br />sex: M","year: 2002<br />numNames: 12482<br />sex: M","year: 2003<br />numNames: 12753<br />sex: M","year: 2004<br />numNames: 13220<br />sex: M","year: 2005<br />numNames: 13364<br />sex: M","year: 2006<br />numNames: 14032<br />sex: M","year: 2007<br />numNames: 14390<br />sex: M","year: 2008<br />numNames: 14613<br />sex: M","year: 2009<br />numNames: 14523<br />sex: M","year: 2010<br />numNames: 14256<br />sex: M","year: 2011<br />numNames: 14343<br />sex: M","year: 2012<br />numNames: 14234<br />sex: M","year: 2013<br />numNames: 14038<br />sex: M","year: 2014<br />numNames: 14047<br />sex: M","year: 2015<br />numNames: 14024<br />sex: M","year: 2016<br />numNames: 14162<br />sex: M","year: 2017<br />numNames: 14160<br />sex: M"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)","dash":"solid"},"hoveron":"points","name":"M","legendgroup":"M","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":54.7945205479452},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1873.15,2023.85],"tickmode":"array","ticktext":["1880","1920","1960","2000"],"tickvals":[1880,1920,1960,2000],"categoryorder":"array","categoryarray":["1880","1920","1960","2000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"year","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-43.1,21541.1],"tickmode":"array","ticktext":["0","5000","10000","15000","20000"],"tickvals":[-7.105427357601e-15,5000,10000,15000,20000],"categoryorder":"array","categoryarray":["0","5000","10000","15000","20000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"numNames","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"sex","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"331125b7c5e7":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"331125b7c5e7","visdat":{"331125b7c5e7":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


```r
home_owner <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-02-09/home_owner.csv')
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   year = col_double(),
##   race = col_character(),
##   home_owner_pct = col_double()
## )
```

```r
homes <- home_owner %>%
  ggplot(aes(x = year, y = home_owner_pct, color = race)) +
  theme(plot.title.position = "plot",
        plot.title = element_text(size = 10, face = "bold"),
        plot.subtitle = element_text(size = 12, face = "italic"),
        legend.title = element_text(size = 10),
        legend.text = element_text(size = 8),
        plot.caption = element_text(size = 12)) +
  labs(title = "Percentage of Home Ownership by Race From 1976 - 2016",
       x = "", y = "",
       color = "Race",
       caption = "Brian Lee") +
  geom_line()

ggplotly(homes)
```

<!--html_preserve--><div id="htmlwidget-476d91d812c8e9c3fcb5" style="width:816px;height:499.2px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-476d91d812c8e9c3fcb5">{"x":{"data":[{"x":[1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[0.44238216050207,0.441229423868313,0.445405540930174,0.481899330523184,0.486023759608665,0.478128179043744,0.472045530632742,0.45345446388515,0.455175400606323,0.441455696202532,0.44513626620394,0.454041523886313,0.424406047516199,0.418236909383581,0.423898531375167,0.424140193046575,0.422539023730037,0.422341376228776,0.424696392163815,0.419390819390819,0.43923296190723,0.455033446197044,0.459756293089626,0.454964623578981,0.471242898280022,0.476848337634735,0.48171235448742,0.47694021537319,0.490644948272067,0.491273806937505,0.472789601485502,0.481677581162045,0.471445261494055,0.464131551901336,0.459945689069925,0.443301670488045,0.432843483283065,0.428112399193548,0.42753984063745,0.423,0.416],"text":["year: 1976<br />home_owner_pct: 0.4423822<br />race: Black","year: 1977<br />home_owner_pct: 0.4412294<br />race: Black","year: 1978<br />home_owner_pct: 0.4454055<br />race: Black","year: 1979<br />home_owner_pct: 0.4818993<br />race: Black","year: 1980<br />home_owner_pct: 0.4860238<br />race: Black","year: 1981<br />home_owner_pct: 0.4781282<br />race: Black","year: 1982<br />home_owner_pct: 0.4720455<br />race: Black","year: 1983<br />home_owner_pct: 0.4534545<br />race: Black","year: 1984<br />home_owner_pct: 0.4551754<br />race: Black","year: 1985<br />home_owner_pct: 0.4414557<br />race: Black","year: 1986<br />home_owner_pct: 0.4451363<br />race: Black","year: 1987<br />home_owner_pct: 0.4540415<br />race: Black","year: 1988<br />home_owner_pct: 0.4244060<br />race: Black","year: 1989<br />home_owner_pct: 0.4182369<br />race: Black","year: 1990<br />home_owner_pct: 0.4238985<br />race: Black","year: 1991<br />home_owner_pct: 0.4241402<br />race: Black","year: 1992<br />home_owner_pct: 0.4225390<br />race: Black","year: 1993<br />home_owner_pct: 0.4223414<br />race: Black","year: 1994<br />home_owner_pct: 0.4246964<br />race: Black","year: 1995<br />home_owner_pct: 0.4193908<br />race: Black","year: 1996<br />home_owner_pct: 0.4392330<br />race: Black","year: 1997<br />home_owner_pct: 0.4550334<br />race: Black","year: 1998<br />home_owner_pct: 0.4597563<br />race: Black","year: 1999<br />home_owner_pct: 0.4549646<br />race: Black","year: 2000<br />home_owner_pct: 0.4712429<br />race: Black","year: 2001<br />home_owner_pct: 0.4768483<br />race: Black","year: 2002<br />home_owner_pct: 0.4817124<br />race: Black","year: 2003<br />home_owner_pct: 0.4769402<br />race: Black","year: 2004<br />home_owner_pct: 0.4906449<br />race: Black","year: 2005<br />home_owner_pct: 0.4912738<br />race: Black","year: 2006<br />home_owner_pct: 0.4727896<br />race: Black","year: 2007<br />home_owner_pct: 0.4816776<br />race: Black","year: 2008<br />home_owner_pct: 0.4714453<br />race: Black","year: 2009<br />home_owner_pct: 0.4641316<br />race: Black","year: 2010<br />home_owner_pct: 0.4599457<br />race: Black","year: 2011<br />home_owner_pct: 0.4433017<br />race: Black","year: 2012<br />home_owner_pct: 0.4328435<br />race: Black","year: 2013<br />home_owner_pct: 0.4281124<br />race: Black","year: 2014<br />home_owner_pct: 0.4275398<br />race: Black","year: 2015<br />home_owner_pct: 0.4230000<br />race: Black","year: 2016<br />home_owner_pct: 0.4160000<br />race: Black"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)","dash":"solid"},"hoveron":"points","name":"Black","legendgroup":"Black","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[0.427069199457259,0.422590068159688,0.426150121065375,0.460042540261319,0.475841476655809,0.466461853558628,0.465326633165829,0.412239902080783,0.404299583911234,0.41101781691583,0.40571647803568,0.405684754521964,0.402246402246402,0.415736040609137,0.411764705882353,0.389549839228296,0.399278883837592,0.400543314216722,0.415647921760391,0.423787976729153,0.412394508124449,0.430759878419453,0.449010477299185,0.452097130242826,0.455306363343706,0.455850109627267,0.47471187732165,0.474909604021519,0.473742730071844,0.49293808507144,0.487499001517693,0.493023972866723,0.491191243721418,0.478063314711359,0.475635433899835,0.465349432857666,0.46117076550052,0.459535444139501,0.453589069215472,0.456,0.46],"text":["year: 1976<br />home_owner_pct: 0.4270692<br />race: Hispanic","year: 1977<br />home_owner_pct: 0.4225901<br />race: Hispanic","year: 1978<br />home_owner_pct: 0.4261501<br />race: Hispanic","year: 1979<br />home_owner_pct: 0.4600425<br />race: Hispanic","year: 1980<br />home_owner_pct: 0.4758415<br />race: Hispanic","year: 1981<br />home_owner_pct: 0.4664619<br />race: Hispanic","year: 1982<br />home_owner_pct: 0.4653266<br />race: Hispanic","year: 1983<br />home_owner_pct: 0.4122399<br />race: Hispanic","year: 1984<br />home_owner_pct: 0.4042996<br />race: Hispanic","year: 1985<br />home_owner_pct: 0.4110178<br />race: Hispanic","year: 1986<br />home_owner_pct: 0.4057165<br />race: Hispanic","year: 1987<br />home_owner_pct: 0.4056848<br />race: Hispanic","year: 1988<br />home_owner_pct: 0.4022464<br />race: Hispanic","year: 1989<br />home_owner_pct: 0.4157360<br />race: Hispanic","year: 1990<br />home_owner_pct: 0.4117647<br />race: Hispanic","year: 1991<br />home_owner_pct: 0.3895498<br />race: Hispanic","year: 1992<br />home_owner_pct: 0.3992789<br />race: Hispanic","year: 1993<br />home_owner_pct: 0.4005433<br />race: Hispanic","year: 1994<br />home_owner_pct: 0.4156479<br />race: Hispanic","year: 1995<br />home_owner_pct: 0.4237880<br />race: Hispanic","year: 1996<br />home_owner_pct: 0.4123945<br />race: Hispanic","year: 1997<br />home_owner_pct: 0.4307599<br />race: Hispanic","year: 1998<br />home_owner_pct: 0.4490105<br />race: Hispanic","year: 1999<br />home_owner_pct: 0.4520971<br />race: Hispanic","year: 2000<br />home_owner_pct: 0.4553064<br />race: Hispanic","year: 2001<br />home_owner_pct: 0.4558501<br />race: Hispanic","year: 2002<br />home_owner_pct: 0.4747119<br />race: Hispanic","year: 2003<br />home_owner_pct: 0.4749096<br />race: Hispanic","year: 2004<br />home_owner_pct: 0.4737427<br />race: Hispanic","year: 2005<br />home_owner_pct: 0.4929381<br />race: Hispanic","year: 2006<br />home_owner_pct: 0.4874990<br />race: Hispanic","year: 2007<br />home_owner_pct: 0.4930240<br />race: Hispanic","year: 2008<br />home_owner_pct: 0.4911912<br />race: Hispanic","year: 2009<br />home_owner_pct: 0.4780633<br />race: Hispanic","year: 2010<br />home_owner_pct: 0.4756354<br />race: Hispanic","year: 2011<br />home_owner_pct: 0.4653494<br />race: Hispanic","year: 2012<br />home_owner_pct: 0.4611708<br />race: Hispanic","year: 2013<br />home_owner_pct: 0.4595354<br />race: Hispanic","year: 2014<br />home_owner_pct: 0.4535891<br />race: Hispanic","year: 2015<br />home_owner_pct: 0.4560000<br />race: Hispanic","year: 2016<br />home_owner_pct: 0.4600000<br />race: Hispanic"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,186,56,1)","dash":"solid"},"hoveron":"points","name":"Hispanic","legendgroup":"Hispanic","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[0.677537582308361,0.675531345156305,0.676651626975827,0.701931557593932,0.705324590905237,0.705935552092609,0.701626741711854,0.676177202044218,0.672999354630526,0.672538763806287,0.666227016297534,0.668404844469748,0.67156456689903,0.673953395038503,0.674800094806831,0.673438889437803,0.674833180287726,0.681200735840552,0.678250209377693,0.686064702580699,0.689638035285348,0.691590543034835,0.697396232550577,0.703458239691786,0.708067662054727,0.714795068310563,0.718433647250833,0.720934038954662,0.725092973184576,0.730383290267011,0.723853485489593,0.720711683649227,0.718563377912356,0.712068585579819,0.710144623988103,0.706010009760555,0.698712924384308,0.694416867099944,0.690776322767511,0.682,0.682],"text":["year: 1976<br />home_owner_pct: 0.6775376<br />race: White","year: 1977<br />home_owner_pct: 0.6755313<br />race: White","year: 1978<br />home_owner_pct: 0.6766516<br />race: White","year: 1979<br />home_owner_pct: 0.7019316<br />race: White","year: 1980<br />home_owner_pct: 0.7053246<br />race: White","year: 1981<br />home_owner_pct: 0.7059356<br />race: White","year: 1982<br />home_owner_pct: 0.7016267<br />race: White","year: 1983<br />home_owner_pct: 0.6761772<br />race: White","year: 1984<br />home_owner_pct: 0.6729994<br />race: White","year: 1985<br />home_owner_pct: 0.6725388<br />race: White","year: 1986<br />home_owner_pct: 0.6662270<br />race: White","year: 1987<br />home_owner_pct: 0.6684048<br />race: White","year: 1988<br />home_owner_pct: 0.6715646<br />race: White","year: 1989<br />home_owner_pct: 0.6739534<br />race: White","year: 1990<br />home_owner_pct: 0.6748001<br />race: White","year: 1991<br />home_owner_pct: 0.6734389<br />race: White","year: 1992<br />home_owner_pct: 0.6748332<br />race: White","year: 1993<br />home_owner_pct: 0.6812007<br />race: White","year: 1994<br />home_owner_pct: 0.6782502<br />race: White","year: 1995<br />home_owner_pct: 0.6860647<br />race: White","year: 1996<br />home_owner_pct: 0.6896380<br />race: White","year: 1997<br />home_owner_pct: 0.6915905<br />race: White","year: 1998<br />home_owner_pct: 0.6973962<br />race: White","year: 1999<br />home_owner_pct: 0.7034582<br />race: White","year: 2000<br />home_owner_pct: 0.7080677<br />race: White","year: 2001<br />home_owner_pct: 0.7147951<br />race: White","year: 2002<br />home_owner_pct: 0.7184336<br />race: White","year: 2003<br />home_owner_pct: 0.7209340<br />race: White","year: 2004<br />home_owner_pct: 0.7250930<br />race: White","year: 2005<br />home_owner_pct: 0.7303833<br />race: White","year: 2006<br />home_owner_pct: 0.7238535<br />race: White","year: 2007<br />home_owner_pct: 0.7207117<br />race: White","year: 2008<br />home_owner_pct: 0.7185634<br />race: White","year: 2009<br />home_owner_pct: 0.7120686<br />race: White","year: 2010<br />home_owner_pct: 0.7101446<br />race: White","year: 2011<br />home_owner_pct: 0.7060100<br />race: White","year: 2012<br />home_owner_pct: 0.6987129<br />race: White","year: 2013<br />home_owner_pct: 0.6944169<br />race: White","year: 2014<br />home_owner_pct: 0.6907763<br />race: White","year: 2015<br />home_owner_pct: 0.6820000<br />race: White","year: 2016<br />home_owner_pct: 0.6820000<br />race: White"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(97,156,255,1)","dash":"solid"},"hoveron":"points","name":"White","legendgroup":"White","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":41.2259156368745,"r":7.30593607305936,"b":27.284861257464,"l":28.4931506849315},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"<b> Percentage of Home Ownership by Race From 1976 - 2016 <\/b>","font":{"color":"rgba(0,0,0,1)","family":"","size":13.2835201328352},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1974,2018],"tickmode":"array","ticktext":["1980","1990","2000","2010"],"tickvals":[1980,1990,2000,2010],"categoryorder":"array","categoryarray":["1980","1990","2000","2010"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.37250816667636,0.747424962818947],"tickmode":"array","ticktext":["0.4","0.5","0.6","0.7"],"tickvals":[0.4,0.5,0.6,0.7],"categoryorder":"array","categoryarray":["0.4","0.5","0.6","0.7"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":10.6268161062682},"y":0.924288310115082},"annotations":[{"text":"Race","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":13.2835201328352},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"33115719e7dd":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"33115719e7dd","visdat":{"33115719e7dd":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).



## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, date, fill = list(daily_harvest_lb = 0))
```

```
## `summarise()` regrouping output by 'date' (override with `.groups` argument)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["variety"],"name":[1],"type":["chr"],"align":["left"]},{"label":["date"],"name":[2],"type":["date"],"align":["right"]},{"label":["daily_harvest_lb"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Amish Paste","2":"2020-07-11","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-21","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-24","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-25","3":"1.02073906"},{"1":"Amish Paste","2":"2020-07-26","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-27","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-28","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-29","3":"0.46076558"},{"1":"Amish Paste","2":"2020-07-30","3":"0.00000000"},{"1":"Amish Paste","2":"2020-07-31","3":"0.43431014"},{"1":"Amish Paste","2":"2020-08-01","3":"0.21384814"},{"1":"Amish Paste","2":"2020-08-02","3":"1.12215158"},{"1":"Amish Paste","2":"2020-08-03","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-04","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-05","3":"0.84216484"},{"1":"Amish Paste","2":"2020-08-06","3":"0.38580850"},{"1":"Amish Paste","2":"2020-08-07","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-08","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-09","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-10","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-11","3":"1.11553772"},{"1":"Amish Paste","2":"2020-08-13","3":"1.41536604"},{"1":"Amish Paste","2":"2020-08-14","3":"1.15742550"},{"1":"Amish Paste","2":"2020-08-16","3":"1.23458720"},{"1":"Amish Paste","2":"2020-08-17","3":"1.29631656"},{"1":"Amish Paste","2":"2020-08-18","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-19","3":"2.19800614"},{"1":"Amish Paste","2":"2020-08-20","3":"2.22666620"},{"1":"Amish Paste","2":"2020-08-21","3":"0.94357736"},{"1":"Amish Paste","2":"2020-08-23","3":"3.39952404"},{"1":"Amish Paste","2":"2020-08-24","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-25","3":"3.08646800"},{"1":"Amish Paste","2":"2020-08-26","3":"4.15791332"},{"1":"Amish Paste","2":"2020-08-29","3":"0.00000000"},{"1":"Amish Paste","2":"2020-08-30","3":"6.46835508"},{"1":"Amish Paste","2":"2020-09-01","3":"3.38850094"},{"1":"Amish Paste","2":"2020-09-03","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-04","3":"4.76197920"},{"1":"Amish Paste","2":"2020-09-06","3":"2.90348454"},{"1":"Amish Paste","2":"2020-09-10","3":"1.52559704"},{"1":"Amish Paste","2":"2020-09-15","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-17","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-18","3":"0.50265336"},{"1":"Amish Paste","2":"2020-09-19","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-21","3":"0.00000000"},{"1":"Amish Paste","2":"2020-09-25","3":"6.03624956"},{"1":"Amish Paste","2":"2020-09-30","3":"3.19008514"},{"1":"Amish Paste","2":"2020-10-03","3":"0.55556424"},{"1":"Amish Paste","2":"2020-10-07","3":"1.57630330"},{"1":"Amish Paste","2":"2020-10-10","3":"0.00000000"},{"1":"Amish Paste","2":"2020-10-11","3":"5.46304836"},{"1":"Amish Paste","2":"2020-10-14","3":"2.59042850"},{"1":"Better Boy","2":"2020-07-11","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-21","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-24","3":"0.48501640"},{"1":"Better Boy","2":"2020-07-25","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-26","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-27","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-28","3":"0.68784144"},{"1":"Better Boy","2":"2020-07-29","3":"0.97444204"},{"1":"Better Boy","2":"2020-07-30","3":"0.00000000"},{"1":"Better Boy","2":"2020-07-31","3":"0.63933980"},{"1":"Better Boy","2":"2020-08-01","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-02","3":"0.46517482"},{"1":"Better Boy","2":"2020-08-03","3":"0.67902296"},{"1":"Better Boy","2":"2020-08-04","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-05","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-06","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-07","3":"2.30382790"},{"1":"Better Boy","2":"2020-08-08","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-09","3":"2.42949124"},{"1":"Better Boy","2":"2020-08-10","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-11","3":"0.78043548"},{"1":"Better Boy","2":"2020-08-13","3":"1.60275874"},{"1":"Better Boy","2":"2020-08-14","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-16","3":"0.52469956"},{"1":"Better Boy","2":"2020-08-17","3":"1.68432968"},{"1":"Better Boy","2":"2020-08-18","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-19","3":"1.35584130"},{"1":"Better Boy","2":"2020-08-20","3":"0.50706260"},{"1":"Better Boy","2":"2020-08-21","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-23","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-24","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-25","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-26","3":"0.68122758"},{"1":"Better Boy","2":"2020-08-29","3":"0.00000000"},{"1":"Better Boy","2":"2020-08-30","3":"0.86641566"},{"1":"Better Boy","2":"2020-09-01","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-03","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-04","3":"6.39119338"},{"1":"Better Boy","2":"2020-09-06","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-10","3":"3.06883104"},{"1":"Better Boy","2":"2020-09-15","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-17","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-18","3":"1.47709540"},{"1":"Better Boy","2":"2020-09-19","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-21","3":"0.00000000"},{"1":"Better Boy","2":"2020-09-25","3":"2.73152418"},{"1":"Better Boy","2":"2020-09-30","3":"1.08908228"},{"1":"Better Boy","2":"2020-10-03","3":"0.00000000"},{"1":"Better Boy","2":"2020-10-07","3":"0.00000000"},{"1":"Better Boy","2":"2020-10-10","3":"0.00000000"},{"1":"Better Boy","2":"2020-10-11","3":"1.15963012"},{"1":"Better Boy","2":"2020-10-14","3":"1.42418452"},{"1":"Big Beef","2":"2020-07-11","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-21","3":"0.30203294"},{"1":"Big Beef","2":"2020-07-24","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-25","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-26","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-27","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-28","3":"0.44753786"},{"1":"Big Beef","2":"2020-07-29","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-30","3":"0.00000000"},{"1":"Big Beef","2":"2020-07-31","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-01","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-02","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-03","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-04","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-05","3":"0.49163026"},{"1":"Big Beef","2":"2020-08-06","3":"0.67681834"},{"1":"Big Beef","2":"2020-08-07","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-08","3":"0.35714844"},{"1":"Big Beef","2":"2020-08-09","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-10","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-11","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-13","3":"0.91050806"},{"1":"Big Beef","2":"2020-08-14","3":"0.58642892"},{"1":"Big Beef","2":"2020-08-16","3":"0.87523414"},{"1":"Big Beef","2":"2020-08-17","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-18","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-19","3":"0.58201968"},{"1":"Big Beef","2":"2020-08-20","3":"0.75838928"},{"1":"Big Beef","2":"2020-08-21","3":"1.85629004"},{"1":"Big Beef","2":"2020-08-23","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-24","3":"0.00000000"},{"1":"Big Beef","2":"2020-08-25","3":"2.18918766"},{"1":"Big Beef","2":"2020-08-26","3":"1.09569614"},{"1":"Big Beef","2":"2020-08-29","3":"2.27737246"},{"1":"Big Beef","2":"2020-08-30","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-01","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-03","3":"2.78884430"},{"1":"Big Beef","2":"2020-09-04","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-06","3":"3.63541838"},{"1":"Big Beef","2":"2020-09-10","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-15","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-17","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-18","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-19","3":"0.67020448"},{"1":"Big Beef","2":"2020-09-21","3":"0.00000000"},{"1":"Big Beef","2":"2020-09-25","3":"1.45284458"},{"1":"Big Beef","2":"2020-09-30","3":"0.00000000"},{"1":"Big Beef","2":"2020-10-03","3":"0.00000000"},{"1":"Big Beef","2":"2020-10-07","3":"0.59965664"},{"1":"Big Beef","2":"2020-10-10","3":"0.00000000"},{"1":"Big Beef","2":"2020-10-11","3":"0.69665992"},{"1":"Big Beef","2":"2020-10-14","3":"1.74385442"},{"1":"Black Krim","2":"2020-07-11","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-21","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-24","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-25","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-26","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-27","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-28","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-29","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-30","3":"0.00000000"},{"1":"Black Krim","2":"2020-07-31","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-01","3":"0.96121432"},{"1":"Black Krim","2":"2020-08-02","3":"1.88935934"},{"1":"Black Krim","2":"2020-08-03","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-04","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-05","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-06","3":"0.86641566"},{"1":"Black Krim","2":"2020-08-07","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-08","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-09","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-10","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-11","3":"0.79145858"},{"1":"Black Krim","2":"2020-08-13","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-14","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-16","3":"0.64154442"},{"1":"Black Krim","2":"2020-08-17","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-18","3":"0.69886454"},{"1":"Black Krim","2":"2020-08-19","3":"1.27647498"},{"1":"Black Krim","2":"2020-08-20","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-21","3":"3.39070556"},{"1":"Black Krim","2":"2020-08-23","3":"3.46786726"},{"1":"Black Krim","2":"2020-08-24","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-25","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-26","3":"0.47619792"},{"1":"Black Krim","2":"2020-08-29","3":"0.00000000"},{"1":"Black Krim","2":"2020-08-30","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-01","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-03","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-04","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-06","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-10","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-15","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-17","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-18","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-19","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-21","3":"0.00000000"},{"1":"Black Krim","2":"2020-09-25","3":"0.52029032"},{"1":"Black Krim","2":"2020-09-30","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-03","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-07","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-10","3":"0.00000000"},{"1":"Black Krim","2":"2020-10-11","3":"0.82673250"},{"1":"Black Krim","2":"2020-10-14","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-11","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-21","3":"0.74736618"},{"1":"Bonny Best","2":"2020-07-24","3":"0.30864680"},{"1":"Bonny Best","2":"2020-07-25","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-26","3":"0.32628376"},{"1":"Bonny Best","2":"2020-07-27","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-28","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-29","3":"0.33730686"},{"1":"Bonny Best","2":"2020-07-30","3":"0.00000000"},{"1":"Bonny Best","2":"2020-07-31","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-01","3":"0.95900970"},{"1":"Bonny Best","2":"2020-08-02","3":"0.34392072"},{"1":"Bonny Best","2":"2020-08-03","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-04","3":"0.85318794"},{"1":"Bonny Best","2":"2020-08-05","3":"1.24120106"},{"1":"Bonny Best","2":"2020-08-06","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-07","3":"0.79145858"},{"1":"Bonny Best","2":"2020-08-08","3":"1.24340568"},{"1":"Bonny Best","2":"2020-08-09","3":"0.39462698"},{"1":"Bonny Best","2":"2020-08-10","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-11","3":"0.67681834"},{"1":"Bonny Best","2":"2020-08-13","3":"0.73193384"},{"1":"Bonny Best","2":"2020-08-14","3":"1.56748482"},{"1":"Bonny Best","2":"2020-08-16","3":"1.19710866"},{"1":"Bonny Best","2":"2020-08-17","3":"0.80248168"},{"1":"Bonny Best","2":"2020-08-18","3":"0.59745202"},{"1":"Bonny Best","2":"2020-08-19","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-20","3":"1.39331984"},{"1":"Bonny Best","2":"2020-08-21","3":"0.72752460"},{"1":"Bonny Best","2":"2020-08-23","3":"0.59304278"},{"1":"Bonny Best","2":"2020-08-24","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-25","3":"1.38670598"},{"1":"Bonny Best","2":"2020-08-26","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-29","3":"0.00000000"},{"1":"Bonny Best","2":"2020-08-30","3":"0.34171610"},{"1":"Bonny Best","2":"2020-09-01","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-03","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-04","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-06","3":"1.56528020"},{"1":"Bonny Best","2":"2020-09-10","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-15","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-17","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-18","3":"2.31926024"},{"1":"Bonny Best","2":"2020-09-19","3":"0.00000000"},{"1":"Bonny Best","2":"2020-09-21","3":"1.57409868"},{"1":"Bonny Best","2":"2020-09-25","3":"1.05160374"},{"1":"Bonny Best","2":"2020-09-30","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-03","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-07","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-10","3":"0.00000000"},{"1":"Bonny Best","2":"2020-10-11","3":"0.85098332"},{"1":"Bonny Best","2":"2020-10-14","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-11","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-21","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-24","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-25","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-26","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-27","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-28","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-29","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-30","3":"0.00000000"},{"1":"Brandywine","2":"2020-07-31","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-01","3":"0.70547840"},{"1":"Brandywine","2":"2020-08-02","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-03","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-04","3":"0.50926722"},{"1":"Brandywine","2":"2020-08-05","3":"0.63933980"},{"1":"Brandywine","2":"2020-08-06","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-07","3":"0.78484472"},{"1":"Brandywine","2":"2020-08-08","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-09","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-10","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-11","3":"0.48060716"},{"1":"Brandywine","2":"2020-08-13","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-14","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-16","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-17","3":"0.67240910"},{"1":"Brandywine","2":"2020-08-18","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-19","3":"0.73854770"},{"1":"Brandywine","2":"2020-08-20","3":"1.06483146"},{"1":"Brandywine","2":"2020-08-21","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-23","3":"0.98326052"},{"1":"Brandywine","2":"2020-08-24","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-25","3":"1.92022402"},{"1":"Brandywine","2":"2020-08-26","3":"2.29721404"},{"1":"Brandywine","2":"2020-08-29","3":"0.00000000"},{"1":"Brandywine","2":"2020-08-30","3":"1.01412520"},{"1":"Brandywine","2":"2020-09-01","3":"0.39242236"},{"1":"Brandywine","2":"2020-09-03","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-04","3":"0.94798660"},{"1":"Brandywine","2":"2020-09-06","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-10","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-15","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-17","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-18","3":"1.57409868"},{"1":"Brandywine","2":"2020-09-19","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-21","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-25","3":"0.00000000"},{"1":"Brandywine","2":"2020-09-30","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-03","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-07","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-10","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-11","3":"0.00000000"},{"1":"Brandywine","2":"2020-10-14","3":"0.92153116"},{"1":"Cherokee Purple","2":"2020-07-11","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-21","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-24","3":"0.54454114"},{"1":"Cherokee Purple","2":"2020-07-25","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-26","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-27","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-28","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-29","3":"0.52910880"},{"1":"Cherokee Purple","2":"2020-07-30","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-07-31","3":"0.67681834"},{"1":"Cherokee Purple","2":"2020-08-01","3":"1.36465978"},{"1":"Cherokee Purple","2":"2020-08-02","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-03","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-04","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-05","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-06","3":"0.66799986"},{"1":"Cherokee Purple","2":"2020-08-07","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-08","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-09","3":"0.67902296"},{"1":"Cherokee Purple","2":"2020-08-10","3":"0.47619792"},{"1":"Cherokee Purple","2":"2020-08-11","3":"1.76810524"},{"1":"Cherokee Purple","2":"2020-08-13","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-14","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-16","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-17","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-18","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-19","3":"1.92242864"},{"1":"Cherokee Purple","2":"2020-08-20","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-21","3":"3.52959662"},{"1":"Cherokee Purple","2":"2020-08-23","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-24","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-25","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-26","3":"1.30733966"},{"1":"Cherokee Purple","2":"2020-08-29","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-08-30","3":"1.32056738"},{"1":"Cherokee Purple","2":"2020-09-01","3":"0.44312862"},{"1":"Cherokee Purple","2":"2020-09-03","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-04","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-06","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-10","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-15","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-17","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-18","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-19","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-21","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-25","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-09-30","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-03","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-07","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-10","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-11","3":"0.00000000"},{"1":"Cherokee Purple","2":"2020-10-14","3":"0.48281178"},{"1":"grape","2":"2020-07-11","3":"0.05291088"},{"1":"grape","2":"2020-07-21","3":"0.18959732"},{"1":"grape","2":"2020-07-24","3":"0.06834322"},{"1":"grape","2":"2020-07-25","3":"0.23368972"},{"1":"grape","2":"2020-07-26","3":"0.00000000"},{"1":"grape","2":"2020-07-27","3":"0.00000000"},{"1":"grape","2":"2020-07-28","3":"0.28880522"},{"1":"grape","2":"2020-07-29","3":"0.08818480"},{"1":"grape","2":"2020-07-30","3":"0.20062042"},{"1":"grape","2":"2020-07-31","3":"0.22046200"},{"1":"grape","2":"2020-08-01","3":"0.37037616"},{"1":"grape","2":"2020-08-02","3":"0.22487124"},{"1":"grape","2":"2020-08-03","3":"0.00000000"},{"1":"grape","2":"2020-08-04","3":"0.26014516"},{"1":"grape","2":"2020-08-05","3":"0.47840254"},{"1":"grape","2":"2020-08-06","3":"0.00000000"},{"1":"grape","2":"2020-08-07","3":"0.64374904"},{"1":"grape","2":"2020-08-08","3":"0.17857422"},{"1":"grape","2":"2020-08-09","3":"0.14109568"},{"1":"grape","2":"2020-08-10","3":"0.00000000"},{"1":"grape","2":"2020-08-11","3":"0.66579524"},{"1":"grape","2":"2020-08-13","3":"0.92814502"},{"1":"grape","2":"2020-08-14","3":"0.27778212"},{"1":"grape","2":"2020-08-16","3":"1.05160374"},{"1":"grape","2":"2020-08-17","3":"0.96121432"},{"1":"grape","2":"2020-08-18","3":"0.29982832"},{"1":"grape","2":"2020-08-19","3":"0.99428362"},{"1":"grape","2":"2020-08-20","3":"1.08687766"},{"1":"grape","2":"2020-08-21","3":"0.58422430"},{"1":"grape","2":"2020-08-23","3":"0.96121432"},{"1":"grape","2":"2020-08-24","3":"0.16534650"},{"1":"grape","2":"2020-08-25","3":"1.11553772"},{"1":"grape","2":"2020-08-26","3":"1.80558378"},{"1":"grape","2":"2020-08-29","3":"0.83775560"},{"1":"grape","2":"2020-08-30","3":"1.83644846"},{"1":"grape","2":"2020-09-01","3":"0.00000000"},{"1":"grape","2":"2020-09-03","3":"2.49342522"},{"1":"grape","2":"2020-09-04","3":"0.97444204"},{"1":"grape","2":"2020-09-06","3":"1.35584130"},{"1":"grape","2":"2020-09-10","3":"1.12215158"},{"1":"grape","2":"2020-09-15","3":"0.56879196"},{"1":"grape","2":"2020-09-17","3":"0.00000000"},{"1":"grape","2":"2020-09-18","3":"0.00000000"},{"1":"grape","2":"2020-09-19","3":"2.33248796"},{"1":"grape","2":"2020-09-21","3":"0.00000000"},{"1":"grape","2":"2020-09-25","3":"1.80558378"},{"1":"grape","2":"2020-09-30","3":"1.49473236"},{"1":"grape","2":"2020-10-03","3":"0.00000000"},{"1":"grape","2":"2020-10-07","3":"0.00000000"},{"1":"grape","2":"2020-10-10","3":"3.03576174"},{"1":"grape","2":"2020-10-11","3":"0.00000000"},{"1":"grape","2":"2020-10-14","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-11","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-21","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-24","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-25","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-26","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-27","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-28","3":"0.69445530"},{"1":"Jet Star","2":"2020-07-29","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-30","3":"0.00000000"},{"1":"Jet Star","2":"2020-07-31","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-01","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-02","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-03","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-04","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-05","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-06","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-07","3":"1.23899644"},{"1":"Jet Star","2":"2020-08-08","3":"0.40565008"},{"1":"Jet Star","2":"2020-08-09","3":"1.30293042"},{"1":"Jet Star","2":"2020-08-10","3":"0.53131342"},{"1":"Jet Star","2":"2020-08-11","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-13","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-14","3":"0.39903622"},{"1":"Jet Star","2":"2020-08-16","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-17","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-18","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-19","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-20","3":"0.79366320"},{"1":"Jet Star","2":"2020-08-21","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-23","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-24","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-25","3":"1.27427036"},{"1":"Jet Star","2":"2020-08-26","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-29","3":"0.00000000"},{"1":"Jet Star","2":"2020-08-30","3":"1.65787424"},{"1":"Jet Star","2":"2020-09-01","3":"1.70417126"},{"1":"Jet Star","2":"2020-09-03","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-04","3":"2.59704236"},{"1":"Jet Star","2":"2020-09-06","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-10","3":"1.66228348"},{"1":"Jet Star","2":"2020-09-15","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-17","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-18","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-19","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-21","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-25","3":"0.00000000"},{"1":"Jet Star","2":"2020-09-30","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-03","3":"0.76279852"},{"1":"Jet Star","2":"2020-10-07","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-10","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-11","3":"0.00000000"},{"1":"Jet Star","2":"2020-10-14","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-11","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-21","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-24","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-25","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-26","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-27","3":"1.76590062"},{"1":"Mortgage Lifter","2":"2020-07-28","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-29","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-30","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-07-31","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-01","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-02","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-03","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-04","3":"0.74736618"},{"1":"Mortgage Lifter","2":"2020-08-05","3":"1.72180822"},{"1":"Mortgage Lifter","2":"2020-08-06","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-07","3":"0.80248168"},{"1":"Mortgage Lifter","2":"2020-08-08","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-09","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-10","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-11","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-13","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-14","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-16","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-17","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-18","3":"1.34040896"},{"1":"Mortgage Lifter","2":"2020-08-19","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-20","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-21","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-23","3":"1.55205248"},{"1":"Mortgage Lifter","2":"2020-08-24","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-25","3":"2.26194012"},{"1":"Mortgage Lifter","2":"2020-08-26","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-08-29","3":"2.41846814"},{"1":"Mortgage Lifter","2":"2020-08-30","3":"1.29852118"},{"1":"Mortgage Lifter","2":"2020-09-01","3":"2.64995324"},{"1":"Mortgage Lifter","2":"2020-09-03","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-04","3":"0.56217810"},{"1":"Mortgage Lifter","2":"2020-09-06","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-10","3":"0.69665992"},{"1":"Mortgage Lifter","2":"2020-09-15","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-17","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-18","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-19","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-21","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-09-25","3":"4.42246772"},{"1":"Mortgage Lifter","2":"2020-09-30","3":"0.72091074"},{"1":"Mortgage Lifter","2":"2020-10-03","3":"0.46958406"},{"1":"Mortgage Lifter","2":"2020-10-07","3":"0.55997348"},{"1":"Mortgage Lifter","2":"2020-10-10","3":"0.00000000"},{"1":"Mortgage Lifter","2":"2020-10-11","3":"0.44092400"},{"1":"Mortgage Lifter","2":"2020-10-14","3":"1.89376858"},{"1":"Old German","2":"2020-07-11","3":"0.00000000"},{"1":"Old German","2":"2020-07-21","3":"0.00000000"},{"1":"Old German","2":"2020-07-24","3":"0.00000000"},{"1":"Old German","2":"2020-07-25","3":"0.00000000"},{"1":"Old German","2":"2020-07-26","3":"0.00000000"},{"1":"Old German","2":"2020-07-27","3":"0.00000000"},{"1":"Old German","2":"2020-07-28","3":"1.34702282"},{"1":"Old German","2":"2020-07-29","3":"0.00000000"},{"1":"Old German","2":"2020-07-30","3":"0.00000000"},{"1":"Old German","2":"2020-07-31","3":"1.39552446"},{"1":"Old German","2":"2020-08-01","3":"0.00000000"},{"1":"Old German","2":"2020-08-02","3":"0.74075232"},{"1":"Old German","2":"2020-08-03","3":"0.00000000"},{"1":"Old German","2":"2020-08-04","3":"0.00000000"},{"1":"Old German","2":"2020-08-05","3":"0.00000000"},{"1":"Old German","2":"2020-08-06","3":"0.00000000"},{"1":"Old German","2":"2020-08-07","3":"0.51367646"},{"1":"Old German","2":"2020-08-08","3":"0.00000000"},{"1":"Old German","2":"2020-08-09","3":"0.00000000"},{"1":"Old German","2":"2020-08-10","3":"0.00000000"},{"1":"Old German","2":"2020-08-11","3":"0.00000000"},{"1":"Old German","2":"2020-08-13","3":"0.00000000"},{"1":"Old German","2":"2020-08-14","3":"0.52469956"},{"1":"Old German","2":"2020-08-16","3":"1.32056738"},{"1":"Old German","2":"2020-08-17","3":"0.00000000"},{"1":"Old German","2":"2020-08-18","3":"0.23148510"},{"1":"Old German","2":"2020-08-19","3":"0.00000000"},{"1":"Old German","2":"2020-08-20","3":"0.00000000"},{"1":"Old German","2":"2020-08-21","3":"0.53572266"},{"1":"Old German","2":"2020-08-23","3":"1.76590062"},{"1":"Old German","2":"2020-08-24","3":"0.00000000"},{"1":"Old German","2":"2020-08-25","3":"0.25353130"},{"1":"Old German","2":"2020-08-26","3":"1.46827692"},{"1":"Old German","2":"2020-08-29","3":"0.00000000"},{"1":"Old German","2":"2020-08-30","3":"1.89817782"},{"1":"Old German","2":"2020-09-01","3":"1.77471910"},{"1":"Old German","2":"2020-09-03","3":"0.00000000"},{"1":"Old German","2":"2020-09-04","3":"0.00000000"},{"1":"Old German","2":"2020-09-06","3":"0.00000000"},{"1":"Old German","2":"2020-09-10","3":"1.48591388"},{"1":"Old German","2":"2020-09-15","3":"0.00000000"},{"1":"Old German","2":"2020-09-17","3":"0.00000000"},{"1":"Old German","2":"2020-09-18","3":"3.59573522"},{"1":"Old German","2":"2020-09-19","3":"0.00000000"},{"1":"Old German","2":"2020-09-21","3":"0.00000000"},{"1":"Old German","2":"2020-09-25","3":"4.01902226"},{"1":"Old German","2":"2020-09-30","3":"0.00000000"},{"1":"Old German","2":"2020-10-03","3":"0.00000000"},{"1":"Old German","2":"2020-10-07","3":"0.80027706"},{"1":"Old German","2":"2020-10-10","3":"0.00000000"},{"1":"Old German","2":"2020-10-11","3":"1.97974876"},{"1":"Old German","2":"2020-10-14","3":"1.06703608"},{"1":"volunteers","2":"2020-07-11","3":"0.00000000"},{"1":"volunteers","2":"2020-07-21","3":"0.00000000"},{"1":"volunteers","2":"2020-07-24","3":"0.00000000"},{"1":"volunteers","2":"2020-07-25","3":"0.00000000"},{"1":"volunteers","2":"2020-07-26","3":"0.00000000"},{"1":"volunteers","2":"2020-07-27","3":"0.00000000"},{"1":"volunteers","2":"2020-07-28","3":"0.00000000"},{"1":"volunteers","2":"2020-07-29","3":"0.00000000"},{"1":"volunteers","2":"2020-07-30","3":"0.00000000"},{"1":"volunteers","2":"2020-07-31","3":"0.00000000"},{"1":"volunteers","2":"2020-08-01","3":"0.00000000"},{"1":"volunteers","2":"2020-08-02","3":"0.00000000"},{"1":"volunteers","2":"2020-08-03","3":"0.00000000"},{"1":"volunteers","2":"2020-08-04","3":"0.16093726"},{"1":"volunteers","2":"2020-08-05","3":"0.14770954"},{"1":"volunteers","2":"2020-08-06","3":"0.00000000"},{"1":"volunteers","2":"2020-08-07","3":"0.00000000"},{"1":"volunteers","2":"2020-08-08","3":"0.00000000"},{"1":"volunteers","2":"2020-08-09","3":"0.11904948"},{"1":"volunteers","2":"2020-08-10","3":"0.00000000"},{"1":"volunteers","2":"2020-08-11","3":"0.35273920"},{"1":"volunteers","2":"2020-08-13","3":"0.00000000"},{"1":"volunteers","2":"2020-08-14","3":"1.08026380"},{"1":"volunteers","2":"2020-08-16","3":"0.72311536"},{"1":"volunteers","2":"2020-08-17","3":"0.67461372"},{"1":"volunteers","2":"2020-08-18","3":"0.32628376"},{"1":"volunteers","2":"2020-08-19","3":"0.67461372"},{"1":"volunteers","2":"2020-08-20","3":"0.73413846"},{"1":"volunteers","2":"2020-08-21","3":"1.23899644"},{"1":"volunteers","2":"2020-08-23","3":"0.00000000"},{"1":"volunteers","2":"2020-08-24","3":"0.00000000"},{"1":"volunteers","2":"2020-08-25","3":"1.07585456"},{"1":"volunteers","2":"2020-08-26","3":"0.57540582"},{"1":"volunteers","2":"2020-08-29","3":"2.87261986"},{"1":"volunteers","2":"2020-08-30","3":"1.81219764"},{"1":"volunteers","2":"2020-09-01","3":"4.30562286"},{"1":"volunteers","2":"2020-09-03","3":"1.34481820"},{"1":"volunteers","2":"2020-09-04","3":"2.72050108"},{"1":"volunteers","2":"2020-09-06","3":"5.24038174"},{"1":"volunteers","2":"2020-09-10","3":"0.91050806"},{"1":"volunteers","2":"2020-09-15","3":"1.59834950"},{"1":"volunteers","2":"2020-09-17","3":"0.46737944"},{"1":"volunteers","2":"2020-09-18","3":"0.00000000"},{"1":"volunteers","2":"2020-09-19","3":"6.46835508"},{"1":"volunteers","2":"2020-09-21","3":"0.20943890"},{"1":"volunteers","2":"2020-09-25","3":"4.36073836"},{"1":"volunteers","2":"2020-09-30","3":"0.15432340"},{"1":"volunteers","2":"2020-10-03","3":"0.00000000"},{"1":"volunteers","2":"2020-10-07","3":"0.14109568"},{"1":"volunteers","2":"2020-10-10","3":"4.35853374"},{"1":"volunteers","2":"2020-10-11","3":"0.50706260"},{"1":"volunteers","2":"2020-10-14","3":"6.25671156"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

  
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  
  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  



```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   state = col_character(),
##   est_pop_2018 = col_double()
## )
```

```r
states_map <- map_data("state")
```

## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
