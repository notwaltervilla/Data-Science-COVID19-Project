Air Quality Data - Shawn Albertson, Jonas Kazlauskas, and Walter Villa
================
2020-10-26

*Purpose*: Is there a correlation between COVID-19 outcomes and air
quality?

*Background*:

Air pollution is a mixture of solid and gas particles present in the air
in small but persistent quantities. Changes in air pollution depending
on location are well documented, so we decided to investigate the
relationship between air pollution and COVID-19.

Long term exposure to pollutants has been linked to negative health,
being linked to irritation and damage throughout your respiratory
pathway. Additionally, this damage is exacerbated in people with
existing respiratory illnesses. COVID-19 is a novel coronavirus that
emerged in late 2019 and has spread throughout the US and the world
affecting millions. The virus and its effects are still being studied,
but it has been shown to attack the lungs and cause problems with
breathing. Due to the virus’ impact on the respiratory system, a study
was conducted by Harvard researchers to analyze the connection between
air pollution and COVID-19 mortality in the US.

<https://www.hsph.harvard.edu/news/hsph-in-the-news/air-pollution-linked-with-higher-covid-19-death-rates/>

They found that higher air pollution, specifically the pollution
category of PM2.5 (particulate diameter of \~2.5 micrometers), is linked
with higher COVID-19 death rates. The study suggested that counties that
have higher pollution will show “higher numbers of hospitalizations,
higher numbers of deaths”. We set out to explore this finding and to
test if it holds using our data sources.

<https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4776742/>

In addition to this Harvard paper, Stanford researcher Mary Prunicki
speaks about the potential damage that toxic air can have on peoples’
immune systems. Her findings include making statements on linking air
pollution to disease (diabetes, heart disease, stroke, cancer, etc), all
of which increase the risk of death in COVID19. She also comments that
air pollution causes a deregulated immune system, making it more likely
to cause damage and lay a foundation for potential chronic diseases.

Notes on PM 2.5

<https://scopeblog.stanford.edu/2020/07/17/why-air-pollution-is-linked-to-severe-cases-of-covid-19/#>:\~:text=Studies%20are%20coming%20out%20that,areas%20of%20high%20pollution%20exposure.\&text=This%20study%20and%20others%20have,the%20COVID%2D19%20death%20rate.

*Data*: Covid-19 data: New York Times data of cumulative counts of
Covid-19 cases and deaths by county in the US. This data is compiled
from state and local government as well as health departments.
<https://github.com/nytimes/covid-19-data>

EPA data: Annual data taken from EPA’s Air database that includes median
air quality index values for each year by county. Air quality index
(AQI) is a scale that takes into account many different forms of
pollution to give an overall rating. Numbers on the low end (0-50) are
considered “good” or healthy, whereas higher values (up to 500) are more
dangerous for public health. Data:
<https://aqs.epa.gov/aqsweb/airdata/download_files.html> AQI:
<https://www.airnow.gov/aqi/aqi-basics/>

PM 2.5 data: County-level PM2.5 exposure averaged from 2000-2016 taken
from the Harvard study exploring PM2.5’s link with Covid-19. Data is
originally from The Atmospheric Composition Analysis Group at Dalhouse
University. PM2.5 is specific pollution size of diameter of \~2.5
micrometers, which are considered fine and easily inhalable. These
particles have been shown to be a serious health risk in individuals who
are exposed in large amounts or over long periods of time.  
Study: <https://github.com/wxwx1993/PM_COVID> Data:
<http://fizz.phys.dal.ca/~atmos/martin/> PM2.5:
<https://www.epa.gov/pm-pollution/particulate-matter-pm-basics>

*EDA Observations*: We began by exploring the EPA dataset, to get an
idea of what patterns exist in the data. To more accurately represent
the long term health effects of air quality we calculated the 10 year
average of annual air quality. Taking a look at this data we found that
an overall average AQI of 36.51012, hawaii had the largest 10 year mean
AQI of 136.4, which is likely due to volcanic activity, and a minimum
AQI of 0.00 in a number of counties such as Brunswick, North Carolina.
While exploring this data we noticed that a large number of counties
were not included. This raised questions about the data, however it is
most likely that these counties simply did not have any places where air
quality is regularly measured.

Next we explored the COVID-19 dataset building off of our work we had
done on the dataset in a previous challenge. We found that the data
included roughly 3000 counties, much more comprehensive than our EPA air
quality data. While exploring the dataset we noticed that the patient’s
location is being counted where they are treated rather than where they
live, which could have an effect on our final results. We noted this but
concluded more often that patients are treated in their home county.

Lastly, we looked into the PM2.5 dataset. This dataset included the
PM2.5 reading for each county across years 2000-2016. This offered a
long term time scale, which reflects the long term health effects of air
pollution well. This dataset also included information on over 3000
counties, meaning that nearly every county in the US is accounted for in
the data set.

*Conclusion*: We set out to explore the findings outlined in a Harvard
study that found a link between Covid-19 outcomes and a type of air
pollution called PM2.5. They argued that higher exposure to air
pollution could lead to more severe covid cases and higher death rates.
We found a weak correlation between 10 year averaged AQI and Covid-19
cases and deaths by county. The respective correlation between AQI and
cases and deaths are 0.125 and 0.099. Additionally, we found a weak
correlation between PM2.5 and Covid-19 cases and deaths. The respective
correlation between PM2.5 and cases and deaths are 0.244 and 0.150.
These findings are in agreement with the paper that found a relation to
COVID-19 outcomes and air pollution. However, the relationship we found
was much weaker. We believe this difference is because air pollution is
linked to many other factors that may be confounding our results. For
example, communities with higher levels of air pollution tend to be low
income communities. Additionally, across different counties there are
varying levels of testing availability, hospital availability, social
distancing, and public health information which can all impact the cases
and deaths resulting from COVID-19.

Air pollution linked to many other variables:
<https://www.niehs.nih.gov/research/programs/geh/geh_newsletter/2016/4/spotlight/poor_communities_exposed_to_elevated_air_pollution_levels.cfm>

*Questions and Future Exploration*: Because we wanted to carefully scope
our project, some questions that we have with regards to air quality are
geared towards how different air pollutants may expand or affect COVID19
cases within the US. While we investigated the median air quality index
through counties and confirmed cases/deaths within the United States,
our results intrigued us to look into certain subtopics that we found
within our research that may impact communities affected by air quality
and, more specifically, air pollution. Using average household income
data for every county may allow us to investigate and understand if air
pollution and income have a correlation, and plotting this data against
COVID19 deaths and cases may lead to insights on different income
communities and their reports on COVID19 activity. Additionally,
investigating the activity of wildfires may also lead to some insights
on how COVID19 is spreading throughout the states since air pollutants
worsen COVID19 symptoms and outcomes.

We load our libraries here:

``` r
library(tidyverse)
```

    ## -- Attaching packages -------------------------------------------------------------------------------------------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ----------------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(tidyr)
```

We load the our datasets here:

``` r
#Define our plotting theme
theme_common <- function() {
  theme_minimal() %+replace%
  theme(
    axis.text.x = element_text(size = 10),
    axis.text.y = element_text(size = 10),
    axis.title.x = element_text(margin = margin(4, 4, 4, 4), size = 10),
    axis.title.y = element_text(margin = margin(4, 4, 4, 4), size = 10, angle = 90),

    legend.title = element_text(size = 16),
    legend.text = element_text(size = 12),

    strip.text.x = element_text(size = 12),
    strip.text.y = element_text(size = 12),

    panel.grid.major = element_line(color = "grey90"),
    panel.grid.minor = element_line(color = "grey90"),

    aspect.ratio = 1.2 / 2,

    plot.margin = unit(c(t = +0.2, b = +0, r = +0.2, l = +0), "cm"),
    plot.title = element_text(size = 14),
    plot.title.position = "plot",
    plot.subtitle = element_text(size = 16),
    plot.caption = element_text(size = 12),
  )
}
```

``` r
# Load PM2.5 Data - run this once
# data originally from The Atmospheric Composition Analysis Group (ACAG) at Dalhouse University (http://fizz.phys.dal.ca/~atmos/martin/)
url_pm25 <- "https://raw.githubusercontent.com/wxwx1993/PM_COVID/master/Data/county_pm25.csv"
filename_pm25 <- "./data/pm25.csv"

# Download the data locally
curl::curl_download(
        url_pm25,
        destfile = filename_pm25
       )

#Load NYTimes Data - using code from c06
url_counties <- "https://raw.githubusercontent.com/nytimes/covid-19-data/master/live/us-counties.csv"
filename_nyt <- "./data/nyt_counties.csv"

## Download the data locally
curl::curl_download(
        url_counties,
        destfile = filename_nyt
      )
```

``` r
#Loading EPA Air Quality Data
df_airquality2020 <- read.csv("./data/annual_aqi_by_county_2020.csv")
df_airquality2019 <- read.csv("./data/annual_aqi_by_county_2019.csv")
df_airquality2018 <- read.csv("./data/annual_aqi_by_county_2018.csv")
df_airquality2017 <- read.csv("./data/annual_aqi_by_county_2017.csv")
df_airquality2016 <- read.csv("./data/annual_aqi_by_county_2016.csv")
df_airquality2015 <- read.csv("./data/annual_aqi_by_county_2015.csv")
df_airquality2014 <- read.csv("./data/annual_aqi_by_county_2014.csv")
df_airquality2013 <- read.csv("./data/annual_aqi_by_county_2013.csv")
df_airquality2012 <- read.csv("./data/annual_aqi_by_county_2012.csv")
df_airquality2011 <- read.csv("./data/annual_aqi_by_county_2011.csv")
df_airquality2010 <- read.csv("./data/annual_aqi_by_county_2010.csv")
df_airquality2009 <- read.csv("./data/annual_aqi_by_county_2009.csv")

#Combine data from 2019 to 2009 into df_aqi_19_09
df_aqi_19_18 <- rbind(df_airquality2019, df_airquality2018)
df_aqi_19_17 <- rbind(df_aqi_19_18, df_airquality2017)
df_aqi_19_16 <- rbind(df_aqi_19_17, df_airquality2016)
df_aqi_19_15 <- rbind(df_aqi_19_16, df_airquality2015)
df_aqi_19_14 <- rbind(df_aqi_19_15, df_airquality2014)
df_aqi_19_13 <- rbind(df_aqi_19_14, df_airquality2013)
df_aqi_19_12 <- rbind(df_aqi_19_13, df_airquality2012)
df_aqi_19_11 <- rbind(df_aqi_19_12, df_airquality2011)
df_aqi_19_10 <- rbind(df_aqi_19_11, df_airquality2010)
df_aqi_19_09 <- rbind(df_aqi_19_10, df_airquality2009)

# Import Census data
df_pop <- 
  read_csv(
    "data/ACSDT5Y2018.B01003_data_with_overlays_2020-10-07T204051.csv", 
    c("id", "Geographic Area Name", "Estimate!!Total", "Margin of Error!!Total"),
  skip = 2
  ) %>% 
  mutate(fips = str_sub(id, -5, -1))
```

    ## Parsed with column specification:
    ## cols(
    ##   id = col_character(),
    ##   `Geographic Area Name` = col_character(),
    ##   `Estimate!!Total` = col_double(),
    ##   `Margin of Error!!Total` = col_character()
    ## )

``` r
df_pop
```

    ## # A tibble: 3,220 x 5
    ##    id          `Geographic Area Nam~ `Estimate!!Tota~ `Margin of Error!!T~ fips 
    ##    <chr>       <chr>                            <dbl> <chr>                <chr>
    ##  1 0500000US0~ Autauga County, Alab~            55200 *****                01001
    ##  2 0500000US0~ Baldwin County, Alab~           208107 *****                01003
    ##  3 0500000US0~ Barbour County, Alab~            25782 *****                01005
    ##  4 0500000US0~ Bibb County, Alabama             22527 *****                01007
    ##  5 0500000US0~ Blount County, Alaba~            57645 *****                01009
    ##  6 0500000US0~ Bullock County, Alab~            10352 *****                01011
    ##  7 0500000US0~ Butler County, Alaba~            20025 *****                01013
    ##  8 0500000US0~ Calhoun County, Alab~           115098 *****                01015
    ##  9 0500000US0~ Chambers County, Ala~            33826 *****                01017
    ## 10 0500000US0~ Cherokee County, Ala~            25853 *****                01019
    ## # ... with 3,210 more rows

``` r
# Import NYT-covid data
df_covid <- read_csv(filename_nyt)
```

    ## Parsed with column specification:
    ## cols(
    ##   date = col_date(format = ""),
    ##   county = col_character(),
    ##   state = col_character(),
    ##   fips = col_character(),
    ##   cases = col_double(),
    ##   deaths = col_double(),
    ##   confirmed_cases = col_double(),
    ##   confirmed_deaths = col_double(),
    ##   probable_cases = col_double(),
    ##   probable_deaths = col_double()
    ## )

``` r
df_covid
```

    ## # A tibble: 3,243 x 10
    ##    date       county state fips  cases deaths confirmed_cases confirmed_deaths
    ##    <date>     <chr>  <chr> <chr> <dbl>  <dbl>           <dbl>            <dbl>
    ##  1 2020-10-26 Autau~ Alab~ 01001  2074     31            1845               29
    ##  2 2020-10-26 Baldw~ Alab~ 01003  6694     69            5663               65
    ##  3 2020-10-26 Barbo~ Alab~ 01005  1033      9             731                9
    ##  4 2020-10-26 Bibb   Alab~ 01007   843     14             773               10
    ##  5 2020-10-26 Blount Alab~ 01009  1942     25            1507               25
    ##  6 2020-10-26 Bullo~ Alab~ 01011   649     17             611               14
    ##  7 2020-10-26 Butler Alab~ 01013  1013     40             965               39
    ##  8 2020-10-26 Calho~ Alab~ 01015  4621     61            3885               53
    ##  9 2020-10-26 Chamb~ Alab~ 01017  1352     44             951               41
    ## 10 2020-10-26 Chero~ Alab~ 01019   745     14             553               12
    ## # ... with 3,233 more rows, and 2 more variables: probable_cases <dbl>,
    ## #   probable_deaths <dbl>

``` r
# Import EPA Air Quality Data
df_airquality2020 <- read_csv("./data/annual_aqi_by_county_2020.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   State = col_character(),
    ##   County = col_character(),
    ##   Year = col_double(),
    ##   `Days with AQI` = col_double(),
    ##   `Good Days` = col_double(),
    ##   `Moderate Days` = col_double(),
    ##   `Unhealthy for Sensitive Groups Days` = col_double(),
    ##   `Unhealthy Days` = col_double(),
    ##   `Very Unhealthy Days` = col_double(),
    ##   `Hazardous Days` = col_double(),
    ##   `Max AQI` = col_double(),
    ##   `90th Percentile AQI` = col_double(),
    ##   `Median AQI` = col_double(),
    ##   `Days CO` = col_double(),
    ##   `Days NO2` = col_double(),
    ##   `Days Ozone` = col_double(),
    ##   `Days SO2` = col_double(),
    ##   `Days PM2.5` = col_double(),
    ##   `Days PM10` = col_double()
    ## )

``` r
df_airquality2020
```

    ## # A tibble: 627 x 19
    ##    State County  Year `Days with AQI` `Good Days` `Moderate Days`
    ##    <chr> <chr>  <dbl>           <dbl>       <dbl>           <dbl>
    ##  1 Alab~ Baldw~  2020              11          11               0
    ##  2 Alab~ Clay    2020               5           5               0
    ##  3 Alab~ DeKalb  2020              59          59               0
    ##  4 Alab~ Etowah  2020               8           8               0
    ##  5 Alab~ Jeffe~  2020              32          26               6
    ##  6 Alab~ Mobile  2020              30          27               3
    ##  7 Alab~ Montg~  2020              29          21               8
    ##  8 Alab~ Morgan  2020              31          31               0
    ##  9 Alab~ Russe~  2020              31          28               3
    ## 10 Alab~ Shelby  2020              31          28               3
    ## # ... with 617 more rows, and 13 more variables: `Unhealthy for Sensitive
    ## #   Groups Days` <dbl>, `Unhealthy Days` <dbl>, `Very Unhealthy Days` <dbl>,
    ## #   `Hazardous Days` <dbl>, `Max AQI` <dbl>, `90th Percentile AQI` <dbl>,
    ## #   `Median AQI` <dbl>, `Days CO` <dbl>, `Days NO2` <dbl>, `Days Ozone` <dbl>,
    ## #   `Days SO2` <dbl>, `Days PM2.5` <dbl>, `Days PM10` <dbl>

``` r
# Loads the downloaded csv
df_pm25 <- read_csv(filename_pm25)
```

    ## Parsed with column specification:
    ## cols(
    ##   fips = col_double(),
    ##   year = col_double(),
    ##   pm25 = col_double()
    ## )

``` r
df_pm25
```

    ## # A tibble: 53,497 x 3
    ##     fips  year  pm25
    ##    <dbl> <dbl> <dbl>
    ##  1 36103  2000 13.7 
    ##  2 36103  2001 13.7 
    ##  3 36103  2002 12.5 
    ##  4 36103  2003 12.4 
    ##  5 36103  2004 11.7 
    ##  6 36103  2005 12.5 
    ##  7 36103  2006 11.0 
    ##  8 36103  2007 11.7 
    ##  9 36103  2008 10.8 
    ## 10 36103  2009  9.20
    ## # ... with 53,487 more rows

``` r
names(df_covid)[2] <- "County"
names(df_covid)[3] <- "State"

# Get the average aqi for years 2009-2019
df_avg_aqi <- df_aqi_19_09 %>%
  group_by(County, State) %>%
  summarise_at(vars("Median.AQI"),
                list(Avg_aqi = mean))

# Join with COVID data, add normalized data
df_covid_air_mean <- 
  inner_join(df_covid, df_avg_aqi, by = c("County", "State"))

df_covid_air_mean_pop <- 
  df_covid_air_mean %>% 
  full_join(df_pop, by = "fips") %>%  
  select(
  date,
  County,
  State,
  fips,
  cases,
  deaths,
  population = `Estimate!!Total`,
  Avg_aqi
  ) %>%
  mutate(deaths_per_100k = deaths * 100000 / population) %>%
  mutate(cases_per_100k = cases * 100000 / population)

df_covid_air_mean_pop #This is the joined version of COVID-19 and 10 year mean EPA data
```

    ## # A tibble: 3,220 x 10
    ##    date       County State fips  cases deaths population Avg_aqi deaths_per_100k
    ##    <date>     <chr>  <chr> <chr> <dbl>  <dbl>      <dbl>   <dbl>           <dbl>
    ##  1 2020-10-26 Baldw~ Alab~ 01003  6694     69     208107    37.8            33.2
    ##  2 2020-10-26 Clay   Alab~ 01027   749     12      13378    33.3            89.7
    ##  3 2020-10-26 Colbe~ Alab~ 01033  2041     32      54495    39.1            58.7
    ##  4 2020-10-26 DeKalb Alab~ 01049  3461     29      71200    38.6            40.7
    ##  5 2020-10-26 Elmore Alab~ 01051  3227     53      81212    37.9            65.3
    ##  6 2020-10-26 Etowah Alab~ 01055  4312     51     102939    43.7            49.5
    ##  7 2020-10-26 Houst~ Alab~ 01069  4180     34     104352    37.7            32.6
    ##  8 2020-10-26 Jeffe~ Alab~ 01073 23443    377     659892    53.2            57.1
    ##  9 2020-10-26 Lawre~ Alab~ 01079   861     32      33171    27.2            96.5
    ## 10 2020-10-26 Madis~ Alab~ 01089  9394     96     357560    41              26.8
    ## # ... with 3,210 more rows, and 1 more variable: cases_per_100k <dbl>

``` r
df_correlation_aqi <- 
  df_covid_air_mean_pop %>%
  drop_na(cases_per_100k) %>% 
  drop_na(deaths_per_100k) %>% 
  drop_na(Avg_aqi) %>% 
  summarise(correlation_deaths = cor(Avg_aqi, deaths_per_100k),
            correlation_cases = cor(Avg_aqi, cases_per_100k))
df_correlation_aqi
```

    ## # A tibble: 1 x 2
    ##   correlation_deaths correlation_cases
    ##                <dbl>             <dbl>
    ## 1              0.124            0.0972

``` r
df_aqi_deaths <- data.frame( x = 75,
                  y = 30,
                  cor = c( "r = 0.125") )

df_aqi_cases <- data.frame( x = 75,
                  y = 1500,
                  cor = c( "r = 0.099") )
df_aqi_deaths
```

    ##    x  y       cor
    ## 1 75 30 r = 0.125

``` r
df_aqi_cases
```

    ##    x    y       cor
    ## 1 75 1500 r = 0.099

``` r
df_covid_air_mean_pop %>%
  ggplot() +
  geom_point(aes(Avg_aqi, deaths_per_100k), size = .2) +
  geom_smooth(aes(Avg_aqi, deaths_per_100k), method = "lm") +
  theme_common() +
  scale_y_log10() +
  geom_label(
    data = df_aqi_deaths,
    aes(x, y, label = cor)
  ) +
  labs(
      x = "2009-2019 Mean Air Quality Index (AQI)",
      y = "Deaths per 100k"
    ) +
  ggtitle("Correlation between deaths and 10 year mean aqi by county")
```

    ## Warning: Transformation introduced infinite values in continuous y-axis
    
    ## Warning: Transformation introduced infinite values in continuous y-axis

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 2149 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2087 rows containing missing values (geom_point).

![](COVID19Project_files/figure-gfm/plot%20EPA%20data-1.png)<!-- -->

``` r
df_covid_air_mean_pop %>%
  ggplot() +
  geom_point(aes(Avg_aqi, cases_per_100k), size = .2) +
  geom_smooth(aes(Avg_aqi, cases_per_100k), method = "lm") +
  theme_common() +
  scale_y_log10() +
  geom_label(
    data = df_aqi_cases,
    aes(x, y, label = cor)
  ) +
  labs(
      x = "2009-2019 Mean Air Quality Index (AQI)",
      y = "Cases per 100k"
    ) +
  ggtitle("Correlation between cases and 10 year mean aqi by county")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 2074 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 2074 rows containing missing values (geom_point).

![](COVID19Project_files/figure-gfm/plot%20EPA%20data-2.png)<!-- -->

``` r
df_data <- 
  df_covid %>% 
  full_join(df_pop, by = "fips") %>% 
  select(
  date,
  County,
  State,
  fips,
  cases,
  deaths,
  population = `Estimate!!Total`
  )
df_data
```

    ## # A tibble: 3,253 x 7
    ##    date       County   State   fips  cases deaths population
    ##    <date>     <chr>    <chr>   <chr> <dbl>  <dbl>      <dbl>
    ##  1 2020-10-26 Autauga  Alabama 01001  2074     31      55200
    ##  2 2020-10-26 Baldwin  Alabama 01003  6694     69     208107
    ##  3 2020-10-26 Barbour  Alabama 01005  1033      9      25782
    ##  4 2020-10-26 Bibb     Alabama 01007   843     14      22527
    ##  5 2020-10-26 Blount   Alabama 01009  1942     25      57645
    ##  6 2020-10-26 Bullock  Alabama 01011   649     17      10352
    ##  7 2020-10-26 Butler   Alabama 01013  1013     40      20025
    ##  8 2020-10-26 Calhoun  Alabama 01015  4621     61     115098
    ##  9 2020-10-26 Chambers Alabama 01017  1352     44      33826
    ## 10 2020-10-26 Cherokee Alabama 01019   745     14      25853
    ## # ... with 3,243 more rows

``` r
df_pm <- 
  group_by(df_pm25, fips) %>%
# Find mean pm2.5 concentration for available timeframe
  summarize(mean_pm25 = mean(pm25)) %>%
  
# Add "0" to zip codes that are missing it
  mutate(fips = ifelse(nchar(fips) == 4, paste("0", fips, sep = ""), fips)) %>% 
  mutate(fips = as.character(fips)) %>% 
  
# Join with NYT data
  full_join(df_data, by = "fips")
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
df_pm
```

    ## # A tibble: 3,254 x 8
    ##    fips  mean_pm25 date       County   State   cases deaths population
    ##    <chr>     <dbl> <date>     <chr>    <chr>   <dbl>  <dbl>      <dbl>
    ##  1 01001      11.7 2020-10-26 Autauga  Alabama  2074     31      55200
    ##  2 01003      10.1 2020-10-26 Baldwin  Alabama  6694     69     208107
    ##  3 01005      11.0 2020-10-26 Barbour  Alabama  1033      9      25782
    ##  4 01007      12.0 2020-10-26 Bibb     Alabama   843     14      22527
    ##  5 01009      11.8 2020-10-26 Blount   Alabama  1942     25      57645
    ##  6 01011      11.3 2020-10-26 Bullock  Alabama   649     17      10352
    ##  7 01013      10.8 2020-10-26 Butler   Alabama  1013     40      20025
    ##  8 01015      12.3 2020-10-26 Calhoun  Alabama  4621     61     115098
    ##  9 01017      11.4 2020-10-26 Chambers Alabama  1352     44      33826
    ## 10 01019      12.2 2020-10-26 Cherokee Alabama   745     14      25853
    ## # ... with 3,244 more rows

``` r
df_pm_norm <-
  df_pm %>% 
  mutate(deaths_per_100k = deaths * 100000 / population) %>%
  mutate(cases_per_100k = cases * 100000 / population)
df_pm_norm
```

    ## # A tibble: 3,254 x 10
    ##    fips  mean_pm25 date       County State cases deaths population
    ##    <chr>     <dbl> <date>     <chr>  <chr> <dbl>  <dbl>      <dbl>
    ##  1 01001      11.7 2020-10-26 Autau~ Alab~  2074     31      55200
    ##  2 01003      10.1 2020-10-26 Baldw~ Alab~  6694     69     208107
    ##  3 01005      11.0 2020-10-26 Barbo~ Alab~  1033      9      25782
    ##  4 01007      12.0 2020-10-26 Bibb   Alab~   843     14      22527
    ##  5 01009      11.8 2020-10-26 Blount Alab~  1942     25      57645
    ##  6 01011      11.3 2020-10-26 Bullo~ Alab~   649     17      10352
    ##  7 01013      10.8 2020-10-26 Butler Alab~  1013     40      20025
    ##  8 01015      12.3 2020-10-26 Calho~ Alab~  4621     61     115098
    ##  9 01017      11.4 2020-10-26 Chamb~ Alab~  1352     44      33826
    ## 10 01019      12.2 2020-10-26 Chero~ Alab~   745     14      25853
    ## # ... with 3,244 more rows, and 2 more variables: deaths_per_100k <dbl>,
    ## #   cases_per_100k <dbl>

``` r
df_correlation_pm <- 
  df_pm_norm %>%
  drop_na(cases_per_100k) %>% 
  drop_na(deaths_per_100k) %>% 
  drop_na(mean_pm25) %>% 
  summarise(correlation_deaths = cor(mean_pm25, deaths_per_100k),
            correlation_cases = cor(mean_pm25, cases_per_100k))



df_correlation_pm
```

    ## # A tibble: 1 x 2
    ##   correlation_deaths correlation_cases
    ##                <dbl>             <dbl>
    ## 1              0.243             0.149

``` r
df_pm_deaths <- data.frame( x = 14,
                  y = 200,
                  cor = c( "r = 0.244") )

df_pm_cases <- data.frame( x = 14,
                  y = 8000,
                  cor = c( "r = 0.150") )
df_pm_deaths
```

    ##    x   y       cor
    ## 1 14 200 r = 0.244

``` r
df_pm_cases
```

    ##    x    y       cor
    ## 1 14 8000 r = 0.150

``` r
df_pm_norm %>% 
  ggplot(aes(mean_pm25, deaths_per_100k)) + 
  geom_point(size = .1) + 
  scale_y_log10() + 
  geom_smooth(method = glm) +
  theme_common() + 
  geom_label(
    data = df_pm_deaths,
    aes(x, y, label = cor)
  ) +
  labs(
      x = "Mean PM2.5 concentration from 2000 - 2016 (μg/m³)",
      y = "Deaths per 100k"
    ) +
  ggtitle("Correlation between deaths and 16 year mean PM2.5 concentration by county\nR = .244")
```

    ## Warning: Transformation introduced infinite values in continuous y-axis
    
    ## Warning: Transformation introduced infinite values in continuous y-axis

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 490 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 165 rows containing missing values (geom_point).

![](COVID19Project_files/figure-gfm/graph%20of%20PM25%20with%20normalized%20death%20rate-1.png)<!-- -->

``` r
df_pm_norm %>% 
  ggplot(aes(mean_pm25, cases_per_100k)) + 
  geom_point(size = .1) + 
  scale_y_log10() + 
  geom_smooth(method = glm)+

  theme_common() + 
  labs(
      x = "Mean PM2.5 concentration from 2000 - 2016 (μg/m³)",
      y = "Cases per 100k"
    ) +
  geom_label(
    data = df_pm_cases,
    aes(x, y, label = cor)
  ) +
  ggtitle("Correlation between cases and year mean PM2.5 concentration by county")
```

    ## `geom_smooth()` using formula 'y ~ x'

    ## Warning: Removed 165 rows containing non-finite values (stat_smooth).
    
    ## Warning: Removed 165 rows containing missing values (geom_point).

![](COVID19Project_files/figure-gfm/graph%20of%20PM25%20with%20normalized%20death%20rate-2.png)<!-- -->
