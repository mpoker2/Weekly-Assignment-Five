---
title: 'Weekly Exercises #5'
author: "Michael Poker"
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
## ✓ ggplot2 3.3.3     ✓ purrr   0.3.4
## ✓ tibble  3.0.5     ✓ dplyr   1.0.3
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
## Linking to GEOS 3.8.1, GDAL 3.1.4, PROJ 6.3.1
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
vegetable_daily_harvests <- garden_harvest %>% 
  mutate(weight_in_lbs = weight*0.00220462) %>%
  ggplot() +
  theme(axis.text.x = element_text(angle = 90)) +
  geom_boxplot(aes(y = weight_in_lbs,
                   x = vegetable))+
  labs(x = "Vegetable",
       y = "Weight (lbs)")+
  ggtitle(label = "Daily Harvest for Each Vegetable")
ggplotly(vegetable_daily_harvests)
```

```{=html}
<div id="htmlwidget-8befd7f648b72845c22f" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-8befd7f648b72845c22f">{"x":{"data":[{"x":[17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,17,23,23,23,23,23,23,23,23,23,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,26,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,5,15,15,15,15,15,15,15,15,15,15,15,15,15,15,15,15,15,15,15,15,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,19,8,28,28,28,28,28,28,28,28,28,28,2,29,29,29,29,29,29,29,29,29,29,29,29,29,29,29,29,29,9,9,9,3,3,3,3,3,3,3,3,3,3,3,3,3,3,3,24,24,24,24,24,24,24,24,24,24,24,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,31,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,4,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,11,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,30,18,18,18,18,18,18,18,18,18,18,18,18,18,18,18,14,14,14,14,14,14,14,14,14,14,14,14,14,14,13,13,13,13,13,7,7,7,7,7,7,7,7,7,7,7,7,7,7,7,7,7,7,7,7,20,20,20,20,20,20,20,20,20,20,20,20,20,20,20,20,20,20,20,6,6,6,6,6,6,21,21,21,21,21,21,21,21,21,21,21,21,21,21,21,21,21,21,21,12,12,12,12,10,10,10,10,10,10,10,10,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,22,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,27,16,1,25,25,25,25,25,25,25,25,25,25,25,25,25,25,25,25,25],"y":[0.0440924,0.11464024,0.0330693,0.0220462,0.17857422,0.02645544,0.30203294,0.41667318,0.24471282,0.04188778,0.14770954,0.23589434,0.10582176,0.1873927,0.0661386,0.02866006,0.18077884,0.11464024,0.10361714,0.13448182,0.70988764,0.03747854,0.08598018,0.1763696,0.08377556,0.04850164,0.26896364,0.03968316,0.21605276,0.0992079,0.16093726,0.20282504,0.1322772,0.31746528,0.03527392,0.2094389,0.1433003,0.47840254,0.12345872,0.05070626,0.01763696,0.18298346,0.27116826,0.32407914,0.17416498,0.03968316,0.29541908,0.16093726,0.47619792,0.21825738,0.20062042,0.21825738,0.14770954,0.20723428,0.19621118,0.05070626,0.12786796,0.12345872,0.19180194,0.24471282,0.04188778,0.13448182,0.2866006,0.08598018,0.30644218,0.2094389,0.11684486,0.03086468,0.1653465,0.07936632,0.14770954,0.08598018,0.19400656,0.08157094,0.03527392,0.110231,0.11684486,0.09479866,0.04629702,0.21825738,0.1322772,0.1763696,0.08598018,0.12786796,0.11243562,0.09700328,0.09038942,0.12786796,0.01984158,0.08157094,0.03527392,0.0551155,0.06834322,0.15652802,0.04850164,0.03086468,0.08598018,0.13007258,0.04188778,0.0661386,0.37919464,0.23589434,0.10802638,0.19621118,0.12566334,0.0220462,0.32848838,5.45863912,0.18298346,0.22266662,0.43651476,0.15211878,0.13668644,4.87000558,0.01763696,0.0551155,0.67902296,0.02425082,0.6724091,0.08598018,0.28219136,0.25794054,0.23809896,0.13448182,0.26675902,0.30203294,0.1322772,0.3196699,0.35935306,0.06172936,0.6172936,0.38139926,0.84436946,0.15652802,0.0220462,0.27998674,0.28219136,0.24912206,0.04188778,0.26675902,0.6283167,0.74075232,0.95460046,0.15652802,1.00751134,1.15963012,0.55556424,0.1653465,0.10582176,1.3778875,0.32628376,1.74826366,0.0881848,1.23679182,0.3637623,0.9369635,0.0881848,0.3086468,0.45635634,0.73413846,0.07495708,0.0881848,1.63803266,1.75928676,0.01763696,0.01763696,0.16975574,0.1873927,0.20502966,0.04188778,0.05070626,0.03747854,0.08157094,0.19400656,0.24912206,0.0881848,0.0440924,0.05070626,0.56438272,1.02735292,0.50265336,0.6834322,0.21164352,0.39242236,1.13978854,0.66579524,0.04188778,0.06393398,0.19400656,0.07054784,0.05291088,0.68122758,0.51147184,0.02866006,0.07275246,0.00440924,0.03747854,0.01543234,0.03747854,0.30203294,0.02425082,0.0110231,0.330693,0.00661386,0.05952474,0.0551155,0.03527392,0.02645544,0.07495708,0.05291088,0.01984158,0.02866006,0.1322772,0.0661386,0.13448182,0.33510224,0.16975574,0.28880522,0.06393398,0.2314851,0.06393398,0.30203294,0.07054784,0.81791402,0.3858085,7.936632,0.16755112,3.39952404,1.61157722,0.17857422,1.4550492,2.91230302,0.3196699,0.75838928,2.866006,12.566334,0.2425082,2.68743178,8.377556,0.97664666,3.91099588,1.00751134,0.55556424,2.53751762,7.23997208,2.6786133,1.08467304,0.86641566,0.29541908,6.24127922,2.47358364,0.9810559,2.5904285,7.15178728,0.36155768,5.37045432,1.89376858,1.83865308,2.0282504,0.94137274,0.5180857,1.14419778,0.72311536,1.60496336,0.220462,0.6724091,0.04629702,0.20723428,0.771617,0.26896364,0.41005932,0.4960395,0.63272594,1.4550492,1.26104264,1.52780166,0.39242236,0.5401319,0.77382162,0.1433003,0.28439598,1.63803266,0.2314851,0.09038942,0.26896364,0.7054784,0.97664666,1.2015179,0.17196036,1.30513504,0.3527392,0.51588108,1.54543862,0.23809896,0.3086468,1.03176216,0.17857422,1.6644881,1.64685114,2.33028334,2.92553074,1.32056738,6.36694256,1.13317468,0.17196036,1.4440261,0.64815828,2.4912206,1.38009212,0.39462698,1.7306267,0.38360388,1.98636262,0.10361714,0.27998674,2.19800614,1.17065322,0.76500314,1.1574255,0.39462698,0.2866006,0.33510224,0.16755112,0.1543234,0.39903622,0.77382162,2.26855398,3.74124014,2.5463361,0.51367646,0.43431014,0.67902296,0.0881848,0.69886454,0.52469956,1.39552446,0.64154442,1.32056738,1.2345872,2.27737246,0.46517482,0.87523414,0.35714844,0.29982832,1.19710866,2.42949124,0.75838928,0.67902296,0.32628376,1.24340568,0.68784144,1.30293042,0.17857422,0.26014516,0.4850164,2.2266662,0.79145858,0.66579524,0.67681834,3.52959662,0.32628376,0.33730686,1.24120106,0.3527392,1.12215158,0.67681834,1.55205248,0.96121432,1.27647498,0.220462,0.86641566,0.98326052,0.6393398,0.74736618,1.60275874,0.78043548,0.9590097,0.5070626,1.36465978,0.21384814,0.11904948,1.34702282,0.14770954,0.40565008,1.23899644,0.48060716,2.18918766,4.35853374,0.52469956,1.1574255,0.46076558,0.74075232,0.34392072,0.27778212,0.22487124,1.09569614,1.08687766,0.6944553,1.56748482,2.64995324,1.23899644,1.02073906,0.50926722,0.16093726,0.74736618,0.8377556,1.62480494,2.19800614,2.41846814,0.58201968,1.4770954,2.3038279,0.30203294,0.6724091,0.73413846,1.29631656,1.68432968,0.7054784,0.6393398,1.72180822,0.49163026,0.84216484,0.47840254,1.11553772,0.18959732,1.83644846,4.42246772,0.67681834,0.3858085,0.06834322,0.5291088,0.54454114,1.48591388,1.85629004,3.39070556,0.2314851,0.79145858,0.86641566,0.80248168,0.05291088,0.56879196,1.76810524,0.64374904,0.23368972,1.92242864,2.49342522,1.3558413,0.46737944,0.7385477,0.59304278,4.7619792,0.67461372,0.80248168,0.73193384,6.46835508,1.06483146,1.39331984,0.96121432,0.55997348,0.80027706,1.5763033,5.24038174,0.14109568,1.29852118,3.63541838,1.3558413,0.28880522,3.086468,1.45284458,0.47619792,1.88935934,1.52559704,0.58642892,1.0802638,0.47619792,0.94357736,0.53572266,0.7275246,0.20062042,1.70417126,3.38850094,1.5983495,3.39952404,1.76590062,0.72311536,1.11553772,3.46786726,1.3448182,1.57409868,0.1543234,0.50265336,0.99428362,0.97444204,2.72050108,1.76590062,0.1653465,1.41536604,0.91050806,1.92022402,0.2535313,1.38670598,0.96121432,0.37037616,1.07585456,1.42418452,4.01902226,1.65787424,1.80558378,3.03576174,2.26194012,4.15791332,0.39903622,1.34040896,0.440924,3.06883104,0.68122758,1.7747191,0.57540582,1.80558378,0.5842243,0.5070626,0.92814502,0.85318794,1.05160374,0.76279852,1.89817782,3.19008514,6.46835508,2.7888443,1.49473236,1.81219764,0.72091074,2.31926024,3.59573522,0.44312862,0.5621781,1.24781492,0.66799986,0.3086468,0.67461372,2.29721404,1.32056738,0.3417161,1.66228348,0.52029032,2.90348454,6.25671156,0.39242236,0.85098332,4.30562286,0.9479866,2.33248796,5.46304836,1.89376858,1.30733966,0.69665992,0.59965664,0.59745202,0.78484472,0.51367646,6.03624956,1.15963012,2.59704236,1.74385442,2.73152418,0.39462698,1.46827692,0.44753786,1.08908228,0.8267325,1.5652802,1.27427036,6.39119338,0.67020448,0.14109568,0.69665992,0.7936632,2.5904285,0.97444204,0.46958406,0.91050806,1.12215158,1.57409868,1.97974876,4.36073836,0.53131342,1.0141252,0.92153116,1.06703608,0.48281178,0.55556424,0.2094389,1.05160374,0.27778212,0.24912206,0.30203294,0.22487124,0.16975574,0.40124084,0.04188778,0.20062042,0.4299009,0.63713518,0.07275246,0.28439598,0.26014516,0.40344546,0.110231,5.11912764,0.16314188,0.35714844,0.09479866,0.0440924,0.56879196,0.12786796,0.26234978,0.43431014,0.77602624,1.12215158,0.19180194,0.3858085,0.22487124,0.0881848,0.06834322,1.23238258,0.02645544,0.05291088,0.98987438,2.25532626,1.95770256,1.94667946,0.25573592,0.48722102,1.00751134,0.39242236,0.3527392,0.23589434,0.5621781,0.38360388,3.30693,0.1763696,0.37258078,0.97444204,0.37037616,0.3527392,0.12345872,0.36155768,0.2535313,0.8157094,0.24691744,1.38229674,0.1543234,0.72311536,0.31746528,0.14991416,0.42328704,0.55556424,0.5952474,0.1322772,0.18518808,0.20282504,2.27296322,0.17857422,0.37258078,0.18518808,0.19621118,0.82011864,0.96341894,0.29541908,0.1653465,0.48281178,0.22487124,3.78753716,0.59965664,1.57850792,0.6503629,0.22266662,1.38670598,3.51857352,0.59965664,0.61288436,0.96782818,3.36645474,0.69886454,0.71209226,0.37037616,0.57761044,0.82011864,0.96121432,1.85849466,0.64595366,1.06483146,0.24030358,1.16183474,3.62439528,0.7275246,1.45725382,3.54282434,3.44802568,0.47178868,1.75928676,0.75838928,0.84436946,15.542571,2.44492358,7.58609742,2.87041524,3.4612534,16.203957,3.54502896,5.01991974,3.84265266,6.46174122,6.35371484,2.66318096,5.92822318,2.54413148,2.26634936,2.49342522,13.778875,6.5918138,2.99607858,2.89025682,11.0231,10.48958196,5.16322004,2.866006,9.63859864,1.55646172,4.6737944,5.1257415,7.11430874,11.353793,1.56307558,4.72450066,4.299009,2.84616442,3.58691674,5.9745202,0.67681834,0.68784144,1.18388094,0.69225068,1.08908228,1.06703608,1.00089748,1.0582176,0.55556424,0.64815828,0.96341894,4.04327308,3.6486461,4.24830274,0.87523414,2.60806546,2.59704236,3.71698932,3.9352467,4.23948426,2.58381464,0.65256752,3.43479796,0.42108242,0.34392072,1.6314188,1.94667946,2.42728662,2.05470584,2.41626352,4.41144462,1.48370926,0.31746528,0.80689092,3.07103566,1.99077186,0.92373578,2.26194012,2.976237,0.65477214,0.11464024,0.25132668],"hoverinfo":"y","type":"box","fillcolor":"rgba(255,255,255,1)","marker":{"opacity":null,"outliercolor":"rgba(0,0,0,1)","line":{"width":1.88976377952756,"color":"rgba(0,0,0,1)"},"size":5.66929133858268},"line":{"color":"rgba(51,51,51,1)","width":1.88976377952756},"showlegend":false,"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":98.6301369863014,"l":37.2602739726027},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Daily Harvest for Each Vegetable","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,31.6],"tickmode":"array","ticktext":["apple","asparagus","basil","beans","beets","broccoli","carrots","chives","cilantro","corn","cucumbers","edamame","hot peppers","jalapeño","kale","kohlrabi","lettuce","onions","peas","peppers","potatoes","pumpkins","radish","raspberries","rutabaga","spinach","squash","strawberries","Swiss chard","tomatoes","zucchini"],"tickvals":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31],"categoryorder":"array","categoryarray":["apple","asparagus","basil","beans","beets","broccoli","carrots","chives","cilantro","corn","cucumbers","edamame","hot peppers","jalapeño","kale","kohlrabi","lettuce","onions","peas","peppers","potatoes","pumpkins","radish","raspberries","rutabaga","spinach","squash","strawberries","Swiss chard","tomatoes","zucchini"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-90,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Vegetable","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.805568148,17.013934388],"tickmode":"array","ticktext":["0","5","10","15"],"tickvals":[0,5,10,15],"categoryorder":"array","categoryarray":["0","5","10","15"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Weight (lbs)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"305d3a2f938a":{"x":{},"y":{},"type":"box"}},"cur_data":"305d3a2f938a","visdat":{"305d3a2f938a":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  

```r
garden_harvest_graph <- garden_harvest %>%
  filter(vegetable %in% c("cucumbers", "beans", "zucchini"), date < mdy("10/1/2020")) %>%
  select(vegetable, weight, date) %>%
  group_by(vegetable, date) %>%
  mutate(weight_lb = weight*0.0022) %>% 
  summarise(total_weight = sum(weight_lb)) %>% 
  ggplot(aes(x = date, y = total_weight, color = vegetable, shape = vegetable))+
  geom_point()+
  geom_line()+
  labs(title = "Growth in Weight (lb) of Vegetables",
       x = "",
       y = "")+
  scale_y_continuous(n.breaks = 10)+
  scale_colour_viridis_d()+
  theme_minimal()+
  theme(legend.position="top",
        panel.grid.minor.x = element_blank(),
        panel.grid.major.x = element_blank())
```

```
## `summarise()` has grouped output by 'vegetable'. You can override using the `.groups` argument.
```

```r
ggplotly(garden_harvest_graph)
```

```{=html}
<div id="htmlwidget-966a9a088af27001a868" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-966a9a088af27001a868">{"x":{"data":[{"x":[18449,18451,18452,18454,18456,18458,18461,18463,18464,18465,18466,18467,18470,18472,18474,18477,18479,18482,18485,18487,18490,18491,18492,18494,18499,18506,18532],"y":[0.517,0.3916,0.308,1.5422,0.9746,1.6346,1.452,1.1418,0.0462,0.7722,0.2838,0.22,1.6016,0.671,1.3024,1.2584,0.605,1.705,2.3716,1.441,1.5246,1.001,0.495,1.353,1.1132,0.352,0.385],"text":["date: 2020-07-06<br />total_weight: 0.5170<br />vegetable: beans<br />vegetable: beans","date: 2020-07-08<br />total_weight: 0.3916<br />vegetable: beans<br />vegetable: beans","date: 2020-07-09<br />total_weight: 0.3080<br />vegetable: beans<br />vegetable: beans","date: 2020-07-11<br />total_weight: 1.5422<br />vegetable: beans<br />vegetable: beans","date: 2020-07-13<br />total_weight: 0.9746<br />vegetable: beans<br />vegetable: beans","date: 2020-07-15<br />total_weight: 1.6346<br />vegetable: beans<br />vegetable: beans","date: 2020-07-18<br />total_weight: 1.4520<br />vegetable: beans<br />vegetable: beans","date: 2020-07-20<br />total_weight: 1.1418<br />vegetable: beans<br />vegetable: beans","date: 2020-07-21<br />total_weight: 0.0462<br />vegetable: beans<br />vegetable: beans","date: 2020-07-22<br />total_weight: 0.7722<br />vegetable: beans<br />vegetable: beans","date: 2020-07-23<br />total_weight: 0.2838<br />vegetable: beans<br />vegetable: beans","date: 2020-07-24<br />total_weight: 0.2200<br />vegetable: beans<br />vegetable: beans","date: 2020-07-27<br />total_weight: 1.6016<br />vegetable: beans<br />vegetable: beans","date: 2020-07-29<br />total_weight: 0.6710<br />vegetable: beans<br />vegetable: beans","date: 2020-07-31<br />total_weight: 1.3024<br />vegetable: beans<br />vegetable: beans","date: 2020-08-03<br />total_weight: 1.2584<br />vegetable: beans<br />vegetable: beans","date: 2020-08-05<br />total_weight: 0.6050<br />vegetable: beans<br />vegetable: beans","date: 2020-08-08<br />total_weight: 1.7050<br />vegetable: beans<br />vegetable: beans","date: 2020-08-11<br />total_weight: 2.3716<br />vegetable: beans<br />vegetable: beans","date: 2020-08-13<br />total_weight: 1.4410<br />vegetable: beans<br />vegetable: beans","date: 2020-08-16<br />total_weight: 1.5246<br />vegetable: beans<br />vegetable: beans","date: 2020-08-17<br />total_weight: 1.0010<br />vegetable: beans<br />vegetable: beans","date: 2020-08-18<br />total_weight: 0.4950<br />vegetable: beans<br />vegetable: beans","date: 2020-08-20<br />total_weight: 1.3530<br />vegetable: beans<br />vegetable: beans","date: 2020-08-25<br />total_weight: 1.1132<br />vegetable: beans<br />vegetable: beans","date: 2020-09-01<br />total_weight: 0.3520<br />vegetable: beans<br />vegetable: beans","date: 2020-09-27<br />total_weight: 0.3850<br />vegetable: beans<br />vegetable: beans"],"type":"scatter","mode":"markers+lines","marker":{"autocolorscale":false,"color":"rgba(68,1,84,1)","opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(68,1,84,1)"}},"hoveron":"points","name":"beans","legendgroup":"beans","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","line":{"width":1.88976377952756,"color":"rgba(68,1,84,1)","dash":"solid"},"frame":null},{"x":[18451,18452,18455,18456,18457,18458,18460,18461,18462,18463,18465,18467,18468,18470,18471,18472,18473,18474,18475,18477,18480,18481,18482,18485,18487,18489,18492,18494,18495,18497,18499],"y":[0.3982,0.1716,0.286,0.1034,0.3344,2.3254,0.7634,0.6468,1.1682,0.3938,1.441,1.155,1.9822,1.727,0.1672,1.1308,1.3772,0.3828,2.486,2.541,0.2794,2.9194,3.7334,2.2638,1.3178,0.7722,6.8662,0.154,2.1934,1.6434,0.3938],"text":["date: 2020-07-08<br />total_weight: 0.3982<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-09<br />total_weight: 0.1716<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-12<br />total_weight: 0.2860<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-13<br />total_weight: 0.1034<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-14<br />total_weight: 0.3344<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-15<br />total_weight: 2.3254<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-17<br />total_weight: 0.7634<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-18<br />total_weight: 0.6468<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-19<br />total_weight: 1.1682<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-20<br />total_weight: 0.3938<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-22<br />total_weight: 1.4410<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-24<br />total_weight: 1.1550<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-25<br />total_weight: 1.9822<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-27<br />total_weight: 1.7270<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-28<br />total_weight: 0.1672<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-29<br />total_weight: 1.1308<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-30<br />total_weight: 1.3772<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-07-31<br />total_weight: 0.3828<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-01<br />total_weight: 2.4860<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-03<br />total_weight: 2.5410<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-06<br />total_weight: 0.2794<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-07<br />total_weight: 2.9194<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-08<br />total_weight: 3.7334<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-11<br />total_weight: 2.2638<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-13<br />total_weight: 1.3178<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-15<br />total_weight: 0.7722<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-18<br />total_weight: 6.8662<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-20<br />total_weight: 0.1540<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-21<br />total_weight: 2.1934<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-23<br />total_weight: 1.6434<br />vegetable: cucumbers<br />vegetable: cucumbers","date: 2020-08-25<br />total_weight: 0.3938<br />vegetable: cucumbers<br />vegetable: cucumbers"],"type":"scatter","mode":"markers+lines","marker":{"autocolorscale":false,"color":"rgba(33,144,140,1)","opacity":1,"size":5.66929133858268,"symbol":"triangle-up","line":{"width":1.88976377952756,"color":"rgba(33,144,140,1)"}},"hoveron":"points","name":"cucumbers","legendgroup":"cucumbers","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","line":{"width":1.88976377952756,"color":"rgba(33,144,140,1)","dash":"solid"},"frame":null},{"x":[18449,18455,18456,18458,18461,18462,18463,18464,18465,18467,18470,18472,18474,18475,18476,18477,18478,18481,18482,18483,18485,18487,18488,18489,18490,18492,18494,18495,18497,18499,18502,18506,18512,18513],"y":[0.385,1.0824,0.319,0.8646,0.1782,0.7568,0.2948,0.242,0.1672,2.9062,3.3924,1.0054,2.673,0.3608,2.585,0.5544,0.9394,2.6818,0.979,0.9746,1.6082,3.9028,0.8162,1.8898,1.452,2.5322,1.8348,2.4684,5.3592,2.024,7.1368,6.2282,7.2248,2.86],"text":["date: 2020-07-06<br />total_weight: 0.3850<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-12<br />total_weight: 1.0824<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-13<br />total_weight: 0.3190<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-15<br />total_weight: 0.8646<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-18<br />total_weight: 0.1782<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-19<br />total_weight: 0.7568<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-20<br />total_weight: 0.2948<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-21<br />total_weight: 0.2420<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-22<br />total_weight: 0.1672<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-24<br />total_weight: 2.9062<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-27<br />total_weight: 3.3924<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-29<br />total_weight: 1.0054<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-07-31<br />total_weight: 2.6730<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-01<br />total_weight: 0.3608<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-02<br />total_weight: 2.5850<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-03<br />total_weight: 0.5544<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-04<br />total_weight: 0.9394<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-07<br />total_weight: 2.6818<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-08<br />total_weight: 0.9790<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-09<br />total_weight: 0.9746<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-11<br />total_weight: 1.6082<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-13<br />total_weight: 3.9028<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-14<br />total_weight: 0.8162<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-15<br />total_weight: 1.8898<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-16<br />total_weight: 1.4520<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-18<br />total_weight: 2.5322<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-20<br />total_weight: 1.8348<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-21<br />total_weight: 2.4684<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-23<br />total_weight: 5.3592<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-25<br />total_weight: 2.0240<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-08-28<br />total_weight: 7.1368<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-09-01<br />total_weight: 6.2282<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-09-07<br />total_weight: 7.2248<br />vegetable: zucchini<br />vegetable: zucchini","date: 2020-09-08<br />total_weight: 2.8600<br />vegetable: zucchini<br />vegetable: zucchini"],"type":"scatter","mode":"markers+lines","marker":{"autocolorscale":false,"color":"rgba(253,231,37,1)","opacity":1,"size":5.66929133858268,"symbol":"square","line":{"width":1.88976377952756,"color":"rgba(253,231,37,1)"}},"hoveron":"points","name":"zucchini","legendgroup":"zucchini","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","line":{"width":1.88976377952756,"color":"rgba(253,231,37,1)","dash":"solid"},"frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":16.8036529680365},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Growth in Weight (lb) of Vegetables","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18444.85,18536.15],"tickmode":"array","ticktext":["Aug","Sep","Oct"],"tickvals":[18475,18506,18536],"categoryorder":"array","categoryarray":["Aug","Sep","Oct"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.31273,7.58373],"tickmode":"array","ticktext":["0","1","2","3","4","5","6","7"],"tickvals":[0,1,2,3,4,5,6,7],"categoryorder":"array","categoryarray":["0","1","2","3","4","5","6","7"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"vegetable","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"305d130a7217":{"x":{},"y":{},"colour":{},"shape":{},"type":"scatter"},"305d12c84dc5":{"x":{},"y":{},"colour":{},"shape":{}}},"cur_data":"305d130a7217","visdat":{"305d130a7217":["function (y) ","x"],"305d12c84dc5":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
train_anim <- small_trains %>%
  mutate(month = factor(month.abb[month], levels = month.abb)) %>% 
  ggplot(aes(x = month, y = num_arriving_late)) +
  geom_col() +
  transition_states(year)+
  labs(title = "Number of Late Arriving Trains by Month", 
       subtitle = "Year: {next_state}",
       x = "",
       y = "")
anim_save("train.gif", train_anim)
```

```
## Warning: Removed 54 rows containing missing values (position_stack).
```

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
## `summarise()` has grouped output by 'date'. You can override using the `.groups` argument.
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
