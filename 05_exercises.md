---
title: 'Weekly Exercises #5'
author: "Kennedy Kechely"
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
gardenplot <- garden_harvest %>% 
  group_by(date) %>% 
  summarize(total_weight_lbs = sum(weight) * 0.00220462) %>% 
  ggplot() +
  geom_line(aes(x=date, y = total_weight_lbs)) +
  ggtitle("Daily Weight (lbs) of All Produce Over Time")+
  xlab("") +
  ylab("") +
  theme(panel.grid.major.x = element_blank(), #removes vertical gridlines
        panel.grid.minor.x = element_blank()) +
  scale_y_continuous(breaks = seq(0,150,25))

gardenplot2 <- garden_harvest %>% 
  filter(vegetable=="lettuce") %>% 
  ggplot()+
  geom_bar(aes(y = variety))

ggplotly(gardenplot)
```

```{=html}
<div id="htmlwidget-30fe0931ada1a4975496" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-30fe0931ada1a4975496">{"x":{"data":[{"x":[18419,18421,18422,18424,18426,18430,18431,18432,18433,18434,18435,18436,18437,18438,18439,18440,18441,18442,18443,18444,18445,18446,18447,18449,18450,18451,18452,18453,18454,18455,18456,18457,18458,18459,18460,18461,18462,18463,18464,18465,18466,18467,18468,18469,18470,18471,18472,18473,18474,18475,18476,18477,18478,18479,18480,18481,18482,18483,18484,18485,18486,18487,18488,18489,18490,18491,18492,18493,18494,18495,18497,18498,18499,18500,18501,18502,18503,18504,18506,18507,18508,18509,18510,18511,18512,18513,18514,18515,18517,18520,18521,18522,18523,18524,18525,18526,18530,18531,18532,18535,18536,18537,18538,18539,18542,18543,18545,18546,18547,18549,18550,18551,18552,18553],"y":[0.12345872,0.0330693,0.0220462,0.21164352,0.21164352,0.53572266,0.37699002,0.32187452,0.7054784,0.88846186,0.4078547,0.55776886,0.34392072,0.11464024,0.97444204,1.17726708,2.21123386,3.04017098,0.24691744,0.1322772,3.75005862,1.1684486,1.95990718,2.41846814,0.45415172,2.15832298,1.05601298,0.46517482,2.3479203,1.75046828,2.20462,2.5683823,4.92071184,0.3086468,1.11112848,2.9652139,2.5683823,5.67469188,1.58953102,2.4361051,1.92242864,6.73290948,3.50755042,0.50485798,11.04294158,4.18657338,5.98113406,2.54413148,8.08875078,8.33125898,7.37665852,6.0296357,6.00979412,6.16852676,6.0957743,13.29606322,9.28806406,6.96880382,3.1746528,14.05886174,0.16093726,24.87472746,10.03543024,4.14909484,10.65051922,8.44810384,15.43234,11.13553562,13.8009212,19.68284736,21.44213412,0.97223742,18.10213482,17.40767952,0.03086468,7.40311396,16.80581826,18.51439876,71.57739754,2.80207202,6.85195896,19.7203259,4.09618396,14.70040616,7.23997208,2.866006,2.58601926,10.471945,0.23809896,2.16714146,1.88715472,1.61157722,9.77087584,158.38210542,0.35935306,1.78353758,26.86549932,0.55335962,4.43569544,7.04596552,0.27998674,4.06091004,1.78794682,0.08598018,4.08736548,1.78133296,8.0137937,13.65321166,62.1482378,23.2477179,37.28453344,3.57809826,8.80084304,19.26396956],"text":["date: 2020-06-06<br />total_weight_lbs:   0.12345872","date: 2020-06-08<br />total_weight_lbs:   0.03306930","date: 2020-06-09<br />total_weight_lbs:   0.02204620","date: 2020-06-11<br />total_weight_lbs:   0.21164352","date: 2020-06-13<br />total_weight_lbs:   0.21164352","date: 2020-06-17<br />total_weight_lbs:   0.53572266","date: 2020-06-18<br />total_weight_lbs:   0.37699002","date: 2020-06-19<br />total_weight_lbs:   0.32187452","date: 2020-06-20<br />total_weight_lbs:   0.70547840","date: 2020-06-21<br />total_weight_lbs:   0.88846186","date: 2020-06-22<br />total_weight_lbs:   0.40785470","date: 2020-06-23<br />total_weight_lbs:   0.55776886","date: 2020-06-24<br />total_weight_lbs:   0.34392072","date: 2020-06-25<br />total_weight_lbs:   0.11464024","date: 2020-06-26<br />total_weight_lbs:   0.97444204","date: 2020-06-27<br />total_weight_lbs:   1.17726708","date: 2020-06-28<br />total_weight_lbs:   2.21123386","date: 2020-06-29<br />total_weight_lbs:   3.04017098","date: 2020-06-30<br />total_weight_lbs:   0.24691744","date: 2020-07-01<br />total_weight_lbs:   0.13227720","date: 2020-07-02<br />total_weight_lbs:   3.75005862","date: 2020-07-03<br />total_weight_lbs:   1.16844860","date: 2020-07-04<br />total_weight_lbs:   1.95990718","date: 2020-07-06<br />total_weight_lbs:   2.41846814","date: 2020-07-07<br />total_weight_lbs:   0.45415172","date: 2020-07-08<br />total_weight_lbs:   2.15832298","date: 2020-07-09<br />total_weight_lbs:   1.05601298","date: 2020-07-10<br />total_weight_lbs:   0.46517482","date: 2020-07-11<br />total_weight_lbs:   2.34792030","date: 2020-07-12<br />total_weight_lbs:   1.75046828","date: 2020-07-13<br />total_weight_lbs:   2.20462000","date: 2020-07-14<br />total_weight_lbs:   2.56838230","date: 2020-07-15<br />total_weight_lbs:   4.92071184","date: 2020-07-16<br />total_weight_lbs:   0.30864680","date: 2020-07-17<br />total_weight_lbs:   1.11112848","date: 2020-07-18<br />total_weight_lbs:   2.96521390","date: 2020-07-19<br />total_weight_lbs:   2.56838230","date: 2020-07-20<br />total_weight_lbs:   5.67469188","date: 2020-07-21<br />total_weight_lbs:   1.58953102","date: 2020-07-22<br />total_weight_lbs:   2.43610510","date: 2020-07-23<br />total_weight_lbs:   1.92242864","date: 2020-07-24<br />total_weight_lbs:   6.73290948","date: 2020-07-25<br />total_weight_lbs:   3.50755042","date: 2020-07-26<br />total_weight_lbs:   0.50485798","date: 2020-07-27<br />total_weight_lbs:  11.04294158","date: 2020-07-28<br />total_weight_lbs:   4.18657338","date: 2020-07-29<br />total_weight_lbs:   5.98113406","date: 2020-07-30<br />total_weight_lbs:   2.54413148","date: 2020-07-31<br />total_weight_lbs:   8.08875078","date: 2020-08-01<br />total_weight_lbs:   8.33125898","date: 2020-08-02<br />total_weight_lbs:   7.37665852","date: 2020-08-03<br />total_weight_lbs:   6.02963570","date: 2020-08-04<br />total_weight_lbs:   6.00979412","date: 2020-08-05<br />total_weight_lbs:   6.16852676","date: 2020-08-06<br />total_weight_lbs:   6.09577430","date: 2020-08-07<br />total_weight_lbs:  13.29606322","date: 2020-08-08<br />total_weight_lbs:   9.28806406","date: 2020-08-09<br />total_weight_lbs:   6.96880382","date: 2020-08-10<br />total_weight_lbs:   3.17465280","date: 2020-08-11<br />total_weight_lbs:  14.05886174","date: 2020-08-12<br />total_weight_lbs:   0.16093726","date: 2020-08-13<br />total_weight_lbs:  24.87472746","date: 2020-08-14<br />total_weight_lbs:  10.03543024","date: 2020-08-15<br />total_weight_lbs:   4.14909484","date: 2020-08-16<br />total_weight_lbs:  10.65051922","date: 2020-08-17<br />total_weight_lbs:   8.44810384","date: 2020-08-18<br />total_weight_lbs:  15.43234000","date: 2020-08-19<br />total_weight_lbs:  11.13553562","date: 2020-08-20<br />total_weight_lbs:  13.80092120","date: 2020-08-21<br />total_weight_lbs:  19.68284736","date: 2020-08-23<br />total_weight_lbs:  21.44213412","date: 2020-08-24<br />total_weight_lbs:   0.97223742","date: 2020-08-25<br />total_weight_lbs:  18.10213482","date: 2020-08-26<br />total_weight_lbs:  17.40767952","date: 2020-08-27<br />total_weight_lbs:   0.03086468","date: 2020-08-28<br />total_weight_lbs:   7.40311396","date: 2020-08-29<br />total_weight_lbs:  16.80581826","date: 2020-08-30<br />total_weight_lbs:  18.51439876","date: 2020-09-01<br />total_weight_lbs:  71.57739754","date: 2020-09-02<br />total_weight_lbs:   2.80207202","date: 2020-09-03<br />total_weight_lbs:   6.85195896","date: 2020-09-04<br />total_weight_lbs:  19.72032590","date: 2020-09-05<br />total_weight_lbs:   4.09618396","date: 2020-09-06<br />total_weight_lbs:  14.70040616","date: 2020-09-07<br />total_weight_lbs:   7.23997208","date: 2020-09-08<br />total_weight_lbs:   2.86600600","date: 2020-09-09<br />total_weight_lbs:   2.58601926","date: 2020-09-10<br />total_weight_lbs:  10.47194500","date: 2020-09-12<br />total_weight_lbs:   0.23809896","date: 2020-09-15<br />total_weight_lbs:   2.16714146","date: 2020-09-16<br />total_weight_lbs:   1.88715472","date: 2020-09-17<br />total_weight_lbs:   1.61157722","date: 2020-09-18<br />total_weight_lbs:   9.77087584","date: 2020-09-19<br />total_weight_lbs: 158.38210542","date: 2020-09-20<br />total_weight_lbs:   0.35935306","date: 2020-09-21<br />total_weight_lbs:   1.78353758","date: 2020-09-25<br />total_weight_lbs:  26.86549932","date: 2020-09-26<br />total_weight_lbs:   0.55335962","date: 2020-09-27<br />total_weight_lbs:   4.43569544","date: 2020-09-30<br />total_weight_lbs:   7.04596552","date: 2020-10-01<br />total_weight_lbs:   0.27998674","date: 2020-10-02<br />total_weight_lbs:   4.06091004","date: 2020-10-03<br />total_weight_lbs:   1.78794682","date: 2020-10-04<br />total_weight_lbs:   0.08598018","date: 2020-10-07<br />total_weight_lbs:   4.08736548","date: 2020-10-08<br />total_weight_lbs:   1.78133296","date: 2020-10-10<br />total_weight_lbs:   8.01379370","date: 2020-10-11<br />total_weight_lbs:  13.65321166","date: 2020-10-12<br />total_weight_lbs:  62.14823780","date: 2020-10-14<br />total_weight_lbs:  23.24771790","date: 2020-10-15<br />total_weight_lbs:  37.28453344","date: 2020-10-16<br />total_weight_lbs:   3.57809826","date: 2020-10-17<br />total_weight_lbs:   8.80084304","date: 2020-10-18<br />total_weight_lbs:  19.26396956"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,0,0,1)","dash":"solid"},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":28.4931506849315},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Daily Weight (lbs) of All Produce Over Time","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18412.3,18559.7],"tickmode":"array","ticktext":["Jun","Jul","Aug","Sep","Oct"],"tickvals":[18414,18444,18475,18506,18536],"categoryorder":"array","categoryarray":["Jun","Jul","Aug","Sep","Oct"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-7.895956761,166.300108381],"tickmode":"array","ticktext":["0","25","50","75","100","125","150"],"tickvals":[0,25,50,75,100,125,150],"categoryorder":"array","categoryarray":["0","25","50","75","100","125","150"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"aed376fe1bc4":{"x":{},"y":{},"type":"scatter"}},"cur_data":"aed376fe1bc4","visdat":{"aed376fe1bc4":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

```r
ggplotly(gardenplot2)
```

```{=html}
<div id="htmlwidget-c51e66b748a857bfe159" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-c51e66b748a857bfe159">{"x":{"data":[{"orientation":"v","width":[27,29,1,3,9],"base":[0.55,1.55,2.55,3.55,4.55],"x":[13.5,14.5,0.5,1.5,4.5],"y":[0.9,0.9,0.9,0.9,0.9],"text":["count: 27<br />variety: 0.9","count: 29<br />variety: 0.9","count:  1<br />variety: 0.9","count:  3<br />variety: 0.9","count:  9<br />variety: 0.9"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(89,89,89,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.2283105022831,"r":7.30593607305936,"b":40.1826484018265,"l":148.310502283105},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.45,30.45],"tickmode":"array","ticktext":["0","10","20","30"],"tickvals":[0,10,20,30],"categoryorder":"array","categoryarray":["0","10","20","30"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"count","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["Farmer's Market Blend","Lettuce Mixture","mustard greens","reseed","Tatsoi"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["Farmer's Market Blend","Lettuce Mixture","mustard greens","reseed","Tatsoi"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"variety","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"aed34b128df2":{"y":{},"type":"bar"}},"cur_data":"aed34b128df2","visdat":{"aed34b128df2":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
small_trains %>% 
  filter(year==2015,
         departure_station =="PARIS LYON",
         arrival_station == "GRENOBLE") %>% 
  distinct(month, .keep_all = TRUE) %>% 
  ggplot(aes(x = month,
             y = journey_time_avg)) +
  geom_line()+
  labs(title = "2015 Trip Time Avg from Paris Lyon to Grenoble",
       x = "Month",
       y = "Minutes")+
  transition_reveal(month)

anim_save("SmallTrains1.gif")
```


```r
knitr::include_graphics("SmallTrains1.gif")
```

![](SmallTrains1.gif)<!-- -->

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
  complete(variety, date, fill = list(daily_harvest_lb = 0)) %>% 
  group_by(variety) %>% 
  mutate(cum_weight_var = cumsum(daily_harvest_lb)) %>% 
  ggplot(aes(x = date)) +
  geom_area(aes(y = cum_weight_var, fill = variety)) +
  labs(title = "Cumulative Weight (lbs) of Tomatoes by Variety",
       x = "",
       y= "")+
  transition_reveal(date)

anim_save("CumGardenWeight.gif")
```


```r
knitr::include_graphics("CumGardenWeight.gif")
```

![](CumGardenWeight.gif)<!-- -->



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
  
  I prefer this to the static map because I can see the direction of the path. Since the path starts and ends at the same spot, it just looks like a circle on the static map. 
  

```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.2, bottom = 39.2, right = 3.7, top = 40), 
    maptype = "toner",
    zoom = 8
)

ggmap(mallorca_map) +
  geom_point(data = mallorca_bike_day7, 
            aes(x = lon, y = lat, color = "red"),
            size = .4) +
  geom_path(data= mallorca_bike_day7, 
            aes(x = lon, y = lat, color = as.factor(ele)))+
  transition_reveal(time)+
  labs(title = "Lisa's Mallorca Bike Ride", 
       subtitle = "Time: {frame_along}",
       x = "",
       y = "") +
  theme_map()

anim_save("LisaMallorcaRide.gif")
```

```r
knitr::include_graphics("LisaMallorcaRide.gif")
```

![](LisaMallorcaRide.gif)<!-- -->

  
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
