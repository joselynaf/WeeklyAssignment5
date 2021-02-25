---
title: 'Weekly Exercises #5'
author: "Joselyn Angeles Figueroa"
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
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
library(openintro)     # for the abbr2state() function
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
library(ggmap)         # for mapping points on maps
library(gplots)        # for col2hex() function
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
library(ggimage)
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 

# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)

# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")

panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")

panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
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
gardenharvestfreq<-garden_harvest %>%
  filter(vegetable == "lettuce") %>% 
  group_by(variety) %>% 
  summarize (cum_harvest= cumsum(weight)) %>% 
  ggplot(aes(y=fct_reorder(variety,cum_harvest)),
         text= variety) +
  geom_bar(fill="green3") + 
  ggtitle("Frequency of Lettuce Harvests by Variety") +
  theme(axis.title = element_blank())

ggplotly(gardenharvestfreq,
         tooltip = c("text", "x"))
```

```{=html}
<div id="htmlwidget-2322f73552ed662e3227" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-2322f73552ed662e3227">{"x":{"data":[{"orientation":"v","width":[1,3,9,27,29],"base":[0.55,1.55,2.55,3.55,4.55],"x":[0.5,1.5,4.5,13.5,14.5],"y":[0.9,0.9,0.9,0.9,0.9],"text":["count:  1","count:  3","count:  9","count: 27","count: 29"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(0,205,0,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":133.698630136986},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Frequency of Lettuce Harvests by Variety","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.45,30.45],"tickmode":"array","ticktext":["0","10","20","30"],"tickvals":[0,10,20,30],"categoryorder":"array","categoryarray":["0","10","20","30"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["mustard greens","reseed","Tatsoi","Farmer's Market Blend","Lettuce Mixture"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["mustard greens","reseed","Tatsoi","Farmer's Market Blend","Lettuce Mixture"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"52a072b68d3":{"y":{},"type":"bar"}},"cur_data":"52a072b68d3","visdat":{"52a072b68d3":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  

```r
library(babynames)

uniquebabynamesgraph<-babynames %>% 
  group_by(sex,year) %>% 
  summarize(unique_baby_name = n()) %>% 
  ggplot(aes(x=year, y=unique_baby_name, color=sex)) +
  geom_line ()+ ggtitle("Number of Distinct Baby Names between 1880-2017") + 
  theme(axis.title= element_blank())

ggplotly(uniquebabynamesgraph,
         tooltip = c("text", "x", "y"))
```

```{=html}
<div id="htmlwidget-8cc4c77008b2a480a1e7" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-8cc4c77008b2a480a1e7">{"x":{"data":[{"x":[1880,1881,1882,1883,1884,1885,1886,1887,1888,1889,1890,1891,1892,1893,1894,1895,1896,1897,1898,1899,1900,1901,1902,1903,1904,1905,1906,1907,1908,1909,1910,1911,1912,1913,1914,1915,1916,1917,1918,1919,1920,1921,1922,1923,1924,1925,1926,1927,1928,1929,1930,1931,1932,1933,1934,1935,1936,1937,1938,1939,1940,1941,1942,1943,1944,1945,1946,1947,1948,1949,1950,1951,1952,1953,1954,1955,1956,1957,1958,1959,1960,1961,1962,1963,1964,1965,1966,1967,1968,1969,1970,1971,1972,1973,1974,1975,1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],"y":[942,938,1028,1054,1172,1197,1282,1306,1474,1479,1534,1533,1661,1652,1702,1808,1825,1799,1975,1842,2224,1943,2042,2083,2165,2234,2220,2399,2434,2548,2790,2868,3445,3707,4206,4967,5162,5312,5586,5559,5765,5871,5789,5739,5899,5771,5621,5603,5436,5275,5248,4977,5100,4858,4973,4892,4856,4927,4994,4952,5025,5085,5380,5368,5245,5241,5686,6103,6040,6065,6111,6211,6391,6499,6616,6725,6885,7012,7022,7196,7331,7529,7583,7663,7803,7533,7616,7849,8194,8708,9350,9638,9661,9805,10239,10609,10900,11324,11470,11967,12157,12186,12327,12065,12171,12500,12823,13255,13877,14546,15235,15459,15611,15797,15751,15753,15891,16160,16598,16941,17653,17970,18081,18430,18826,19182,20050,20560,20457,20179,19811,19560,19498,19231,19181,19074,18817,18309],"text":["year: 1880<br />unique_baby_name:   942","year: 1881<br />unique_baby_name:   938","year: 1882<br />unique_baby_name:  1028","year: 1883<br />unique_baby_name:  1054","year: 1884<br />unique_baby_name:  1172","year: 1885<br />unique_baby_name:  1197","year: 1886<br />unique_baby_name:  1282","year: 1887<br />unique_baby_name:  1306","year: 1888<br />unique_baby_name:  1474","year: 1889<br />unique_baby_name:  1479","year: 1890<br />unique_baby_name:  1534","year: 1891<br />unique_baby_name:  1533","year: 1892<br />unique_baby_name:  1661","year: 1893<br />unique_baby_name:  1652","year: 1894<br />unique_baby_name:  1702","year: 1895<br />unique_baby_name:  1808","year: 1896<br />unique_baby_name:  1825","year: 1897<br />unique_baby_name:  1799","year: 1898<br />unique_baby_name:  1975","year: 1899<br />unique_baby_name:  1842","year: 1900<br />unique_baby_name:  2224","year: 1901<br />unique_baby_name:  1943","year: 1902<br />unique_baby_name:  2042","year: 1903<br />unique_baby_name:  2083","year: 1904<br />unique_baby_name:  2165","year: 1905<br />unique_baby_name:  2234","year: 1906<br />unique_baby_name:  2220","year: 1907<br />unique_baby_name:  2399","year: 1908<br />unique_baby_name:  2434","year: 1909<br />unique_baby_name:  2548","year: 1910<br />unique_baby_name:  2790","year: 1911<br />unique_baby_name:  2868","year: 1912<br />unique_baby_name:  3445","year: 1913<br />unique_baby_name:  3707","year: 1914<br />unique_baby_name:  4206","year: 1915<br />unique_baby_name:  4967","year: 1916<br />unique_baby_name:  5162","year: 1917<br />unique_baby_name:  5312","year: 1918<br />unique_baby_name:  5586","year: 1919<br />unique_baby_name:  5559","year: 1920<br />unique_baby_name:  5765","year: 1921<br />unique_baby_name:  5871","year: 1922<br />unique_baby_name:  5789","year: 1923<br />unique_baby_name:  5739","year: 1924<br />unique_baby_name:  5899","year: 1925<br />unique_baby_name:  5771","year: 1926<br />unique_baby_name:  5621","year: 1927<br />unique_baby_name:  5603","year: 1928<br />unique_baby_name:  5436","year: 1929<br />unique_baby_name:  5275","year: 1930<br />unique_baby_name:  5248","year: 1931<br />unique_baby_name:  4977","year: 1932<br />unique_baby_name:  5100","year: 1933<br />unique_baby_name:  4858","year: 1934<br />unique_baby_name:  4973","year: 1935<br />unique_baby_name:  4892","year: 1936<br />unique_baby_name:  4856","year: 1937<br />unique_baby_name:  4927","year: 1938<br />unique_baby_name:  4994","year: 1939<br />unique_baby_name:  4952","year: 1940<br />unique_baby_name:  5025","year: 1941<br />unique_baby_name:  5085","year: 1942<br />unique_baby_name:  5380","year: 1943<br />unique_baby_name:  5368","year: 1944<br />unique_baby_name:  5245","year: 1945<br />unique_baby_name:  5241","year: 1946<br />unique_baby_name:  5686","year: 1947<br />unique_baby_name:  6103","year: 1948<br />unique_baby_name:  6040","year: 1949<br />unique_baby_name:  6065","year: 1950<br />unique_baby_name:  6111","year: 1951<br />unique_baby_name:  6211","year: 1952<br />unique_baby_name:  6391","year: 1953<br />unique_baby_name:  6499","year: 1954<br />unique_baby_name:  6616","year: 1955<br />unique_baby_name:  6725","year: 1956<br />unique_baby_name:  6885","year: 1957<br />unique_baby_name:  7012","year: 1958<br />unique_baby_name:  7022","year: 1959<br />unique_baby_name:  7196","year: 1960<br />unique_baby_name:  7331","year: 1961<br />unique_baby_name:  7529","year: 1962<br />unique_baby_name:  7583","year: 1963<br />unique_baby_name:  7663","year: 1964<br />unique_baby_name:  7803","year: 1965<br />unique_baby_name:  7533","year: 1966<br />unique_baby_name:  7616","year: 1967<br />unique_baby_name:  7849","year: 1968<br />unique_baby_name:  8194","year: 1969<br />unique_baby_name:  8708","year: 1970<br />unique_baby_name:  9350","year: 1971<br />unique_baby_name:  9638","year: 1972<br />unique_baby_name:  9661","year: 1973<br />unique_baby_name:  9805","year: 1974<br />unique_baby_name: 10239","year: 1975<br />unique_baby_name: 10609","year: 1976<br />unique_baby_name: 10900","year: 1977<br />unique_baby_name: 11324","year: 1978<br />unique_baby_name: 11470","year: 1979<br />unique_baby_name: 11967","year: 1980<br />unique_baby_name: 12157","year: 1981<br />unique_baby_name: 12186","year: 1982<br />unique_baby_name: 12327","year: 1983<br />unique_baby_name: 12065","year: 1984<br />unique_baby_name: 12171","year: 1985<br />unique_baby_name: 12500","year: 1986<br />unique_baby_name: 12823","year: 1987<br />unique_baby_name: 13255","year: 1988<br />unique_baby_name: 13877","year: 1989<br />unique_baby_name: 14546","year: 1990<br />unique_baby_name: 15235","year: 1991<br />unique_baby_name: 15459","year: 1992<br />unique_baby_name: 15611","year: 1993<br />unique_baby_name: 15797","year: 1994<br />unique_baby_name: 15751","year: 1995<br />unique_baby_name: 15753","year: 1996<br />unique_baby_name: 15891","year: 1997<br />unique_baby_name: 16160","year: 1998<br />unique_baby_name: 16598","year: 1999<br />unique_baby_name: 16941","year: 2000<br />unique_baby_name: 17653","year: 2001<br />unique_baby_name: 17970","year: 2002<br />unique_baby_name: 18081","year: 2003<br />unique_baby_name: 18430","year: 2004<br />unique_baby_name: 18826","year: 2005<br />unique_baby_name: 19182","year: 2006<br />unique_baby_name: 20050","year: 2007<br />unique_baby_name: 20560","year: 2008<br />unique_baby_name: 20457","year: 2009<br />unique_baby_name: 20179","year: 2010<br />unique_baby_name: 19811","year: 2011<br />unique_baby_name: 19560","year: 2012<br />unique_baby_name: 19498","year: 2013<br />unique_baby_name: 19231","year: 2014<br />unique_baby_name: 19181","year: 2015<br />unique_baby_name: 19074","year: 2016<br />unique_baby_name: 18817","year: 2017<br />unique_baby_name: 18309"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)","dash":"solid"},"hoveron":"points","name":"F","legendgroup":"F","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1880,1881,1882,1883,1884,1885,1886,1887,1888,1889,1890,1891,1892,1893,1894,1895,1896,1897,1898,1899,1900,1901,1902,1903,1904,1905,1906,1907,1908,1909,1910,1911,1912,1913,1914,1915,1916,1917,1918,1919,1920,1921,1922,1923,1924,1925,1926,1927,1928,1929,1930,1931,1932,1933,1934,1935,1936,1937,1938,1939,1940,1941,1942,1943,1944,1945,1946,1947,1948,1949,1950,1951,1952,1953,1954,1955,1956,1957,1958,1959,1960,1961,1962,1963,1964,1965,1966,1967,1968,1969,1970,1971,1972,1973,1974,1975,1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],"y":[1058,997,1099,1030,1125,1097,1110,1067,1177,1111,1161,1127,1260,1179,1239,1241,1266,1229,1289,1200,1506,1210,1320,1306,1395,1421,1413,1549,1584,1679,1839,1999,2906,3261,3759,4390,4534,4602,4813,4810,4990,4986,4967,4904,4970,4867,4837,4803,4724,4543,4541,4320,4284,4154,4207,4145,4037,4019,4036,3967,3936,4000,4045,4040,3909,3783,4019,4268,4199,4203,4191,4251,4257,4339,4352,4388,4450,4552,4499,4573,4590,4652,4623,4619,4593,4420,4536,4550,4741,5040,5430,5655,5750,5876,6005,6335,6491,6851,6759,7071,7288,7286,7364,7338,7332,7581,7826,8148,8487,9227,9484,9646,9816,10169,10244,10327,10532,10811,11301,11609,12116,12299,12482,12753,13220,13364,14032,14390,14613,14523,14256,14343,14234,14038,14047,14024,14162,14160],"text":["year: 1880<br />unique_baby_name:  1058","year: 1881<br />unique_baby_name:   997","year: 1882<br />unique_baby_name:  1099","year: 1883<br />unique_baby_name:  1030","year: 1884<br />unique_baby_name:  1125","year: 1885<br />unique_baby_name:  1097","year: 1886<br />unique_baby_name:  1110","year: 1887<br />unique_baby_name:  1067","year: 1888<br />unique_baby_name:  1177","year: 1889<br />unique_baby_name:  1111","year: 1890<br />unique_baby_name:  1161","year: 1891<br />unique_baby_name:  1127","year: 1892<br />unique_baby_name:  1260","year: 1893<br />unique_baby_name:  1179","year: 1894<br />unique_baby_name:  1239","year: 1895<br />unique_baby_name:  1241","year: 1896<br />unique_baby_name:  1266","year: 1897<br />unique_baby_name:  1229","year: 1898<br />unique_baby_name:  1289","year: 1899<br />unique_baby_name:  1200","year: 1900<br />unique_baby_name:  1506","year: 1901<br />unique_baby_name:  1210","year: 1902<br />unique_baby_name:  1320","year: 1903<br />unique_baby_name:  1306","year: 1904<br />unique_baby_name:  1395","year: 1905<br />unique_baby_name:  1421","year: 1906<br />unique_baby_name:  1413","year: 1907<br />unique_baby_name:  1549","year: 1908<br />unique_baby_name:  1584","year: 1909<br />unique_baby_name:  1679","year: 1910<br />unique_baby_name:  1839","year: 1911<br />unique_baby_name:  1999","year: 1912<br />unique_baby_name:  2906","year: 1913<br />unique_baby_name:  3261","year: 1914<br />unique_baby_name:  3759","year: 1915<br />unique_baby_name:  4390","year: 1916<br />unique_baby_name:  4534","year: 1917<br />unique_baby_name:  4602","year: 1918<br />unique_baby_name:  4813","year: 1919<br />unique_baby_name:  4810","year: 1920<br />unique_baby_name:  4990","year: 1921<br />unique_baby_name:  4986","year: 1922<br />unique_baby_name:  4967","year: 1923<br />unique_baby_name:  4904","year: 1924<br />unique_baby_name:  4970","year: 1925<br />unique_baby_name:  4867","year: 1926<br />unique_baby_name:  4837","year: 1927<br />unique_baby_name:  4803","year: 1928<br />unique_baby_name:  4724","year: 1929<br />unique_baby_name:  4543","year: 1930<br />unique_baby_name:  4541","year: 1931<br />unique_baby_name:  4320","year: 1932<br />unique_baby_name:  4284","year: 1933<br />unique_baby_name:  4154","year: 1934<br />unique_baby_name:  4207","year: 1935<br />unique_baby_name:  4145","year: 1936<br />unique_baby_name:  4037","year: 1937<br />unique_baby_name:  4019","year: 1938<br />unique_baby_name:  4036","year: 1939<br />unique_baby_name:  3967","year: 1940<br />unique_baby_name:  3936","year: 1941<br />unique_baby_name:  4000","year: 1942<br />unique_baby_name:  4045","year: 1943<br />unique_baby_name:  4040","year: 1944<br />unique_baby_name:  3909","year: 1945<br />unique_baby_name:  3783","year: 1946<br />unique_baby_name:  4019","year: 1947<br />unique_baby_name:  4268","year: 1948<br />unique_baby_name:  4199","year: 1949<br />unique_baby_name:  4203","year: 1950<br />unique_baby_name:  4191","year: 1951<br />unique_baby_name:  4251","year: 1952<br />unique_baby_name:  4257","year: 1953<br />unique_baby_name:  4339","year: 1954<br />unique_baby_name:  4352","year: 1955<br />unique_baby_name:  4388","year: 1956<br />unique_baby_name:  4450","year: 1957<br />unique_baby_name:  4552","year: 1958<br />unique_baby_name:  4499","year: 1959<br />unique_baby_name:  4573","year: 1960<br />unique_baby_name:  4590","year: 1961<br />unique_baby_name:  4652","year: 1962<br />unique_baby_name:  4623","year: 1963<br />unique_baby_name:  4619","year: 1964<br />unique_baby_name:  4593","year: 1965<br />unique_baby_name:  4420","year: 1966<br />unique_baby_name:  4536","year: 1967<br />unique_baby_name:  4550","year: 1968<br />unique_baby_name:  4741","year: 1969<br />unique_baby_name:  5040","year: 1970<br />unique_baby_name:  5430","year: 1971<br />unique_baby_name:  5655","year: 1972<br />unique_baby_name:  5750","year: 1973<br />unique_baby_name:  5876","year: 1974<br />unique_baby_name:  6005","year: 1975<br />unique_baby_name:  6335","year: 1976<br />unique_baby_name:  6491","year: 1977<br />unique_baby_name:  6851","year: 1978<br />unique_baby_name:  6759","year: 1979<br />unique_baby_name:  7071","year: 1980<br />unique_baby_name:  7288","year: 1981<br />unique_baby_name:  7286","year: 1982<br />unique_baby_name:  7364","year: 1983<br />unique_baby_name:  7338","year: 1984<br />unique_baby_name:  7332","year: 1985<br />unique_baby_name:  7581","year: 1986<br />unique_baby_name:  7826","year: 1987<br />unique_baby_name:  8148","year: 1988<br />unique_baby_name:  8487","year: 1989<br />unique_baby_name:  9227","year: 1990<br />unique_baby_name:  9484","year: 1991<br />unique_baby_name:  9646","year: 1992<br />unique_baby_name:  9816","year: 1993<br />unique_baby_name: 10169","year: 1994<br />unique_baby_name: 10244","year: 1995<br />unique_baby_name: 10327","year: 1996<br />unique_baby_name: 10532","year: 1997<br />unique_baby_name: 10811","year: 1998<br />unique_baby_name: 11301","year: 1999<br />unique_baby_name: 11609","year: 2000<br />unique_baby_name: 12116","year: 2001<br />unique_baby_name: 12299","year: 2002<br />unique_baby_name: 12482","year: 2003<br />unique_baby_name: 12753","year: 2004<br />unique_baby_name: 13220","year: 2005<br />unique_baby_name: 13364","year: 2006<br />unique_baby_name: 14032","year: 2007<br />unique_baby_name: 14390","year: 2008<br />unique_baby_name: 14613","year: 2009<br />unique_baby_name: 14523","year: 2010<br />unique_baby_name: 14256","year: 2011<br />unique_baby_name: 14343","year: 2012<br />unique_baby_name: 14234","year: 2013<br />unique_baby_name: 14038","year: 2014<br />unique_baby_name: 14047","year: 2015<br />unique_baby_name: 14024","year: 2016<br />unique_baby_name: 14162","year: 2017<br />unique_baby_name: 14160"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)","dash":"solid"},"hoveron":"points","name":"M","legendgroup":"M","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":40.1826484018265},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Number of Distinct Baby Names between 1880-2017","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1873.15,2023.85],"tickmode":"array","ticktext":["1880","1920","1960","2000"],"tickvals":[1880,1920,1960,2000],"categoryorder":"array","categoryarray":["1880","1920","1960","2000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-43.1,21541.1],"tickmode":"array","ticktext":["0","5000","10000","15000","20000"],"tickvals":[-7.105427357601e-15,5000,10000,15000,20000],"categoryorder":"array","categoryarray":["0","5000","10000","15000","20000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":null,"family":null,"size":0}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.93503937007874},"annotations":[{"text":"sex","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"52a033cc6377":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"52a033cc6377","visdat":{"52a033cc6377":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
small_trains %>% 
  filter(departure_station %in% c("AIX EN PROVENCE TGV", "ANGERS sAINT LAUD","ANGOULEME","ANNENCY", "ARRAS","AVIGNON TGV")) %>% 
  ggplot(aes(x=year, y= total_num_trips,
             color= departure_station,
             size= total_num_trips,
             alpha= .5)) +
  geom_jitter() +
  labs(title = "Total trips from 'A' departure stations in France between 2015 to 2018",
       x = "",
       y = "",
       size = "Total Number of Trips",
       color = "Departure Station") +
  transition_time(year) +
  shadow_mark(past=TRUE)

anim_save("small_train.gif")
```

```r
knitr::include_graphics("small_train.gif")
```

![](small_train.gif)<!-- -->

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
  complete(variety, date, fill = list(daily_harvest_lb = 0))%>% 
  group_by(variety) %>% 
  mutate(cum_wtlbs = cumsum(daily_harvest_lb),
         variety = fct_reorder(variety, cum_wtlbs, sum, .desc = TRUE)) %>% 
  ggplot(aes(y =cum_wtlbs,
         x = date,
         fill = variety,
         group = variety)) +
  geom_area() +
  labs(title="Cumulative tomato harvests over time in pounds by variety",
       x="",
       y="") +
  transition_reveal(date) 


  anim_save("tomharvall.gif")
```

```r
knitr::include_graphics("tomharvall.gif")
```

![](tomharvall.gif)<!-- -->


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

```r
img<- "https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png"

mallorcamap<- get_stamenmap(
    bbox = c(left = 2.2393, bottom = 39.4624, right = 3.0536, top = 39.8151), 
    maptype = "terrain",
    zoom = 10) 

ggmap(mallorcamap) + 
  geom_path(data = mallorca_bike_day7,
             aes(x= lon, y=lat,
                 color= ele)) +
  geom_image(data= mallorca_bike_day7 %>%  mutate(image=img),
             aes(image=image, x= lon, y= lat), 
             size=.08)+
  labs(title = "Bike Route in Mallorca",
       subtitle= "Time: {frame_along}",
       x="",
       y= "")+
  transition_reveal(along = time) 

anim_save("mallorcabikerun.gif")
```

```r
knitr::include_graphics("mallorcabikerun.gif")
```

![](mallorcabikerun.gif)<!-- -->
  
 I think the animation is more exciting than the static plot because it shows the actual motion of a bike ride. 
  
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
panama_all<-panama_bike %>% 
  bind_rows(panama_run) %>% 
  bind_rows(panama_swim) %>% 
  arrange(hrminsec)

panama_map <- get_stamenmap(
    bbox = c(left = -79.5668, bottom = 8.8997, right = -79.4228, top = 8.9968), 
    maptype = "terrain",
    zoom = 13)

ggmap(panama_map) +
  geom_path(data = panama_all,
            aes (x=lon, y=lat),
            size = .5) +
  geom_point(data = panama_all,
             aes(x =lon, y = lat, color=event),
             size = .5) +
  labs(title = "Panama Ironman Route",
       subtitle = "Time:{frame_along}") +
  scale_color_manual (values = c("red","skyblue","green")) +
  theme_map () +
  theme(legend.background = element_blank()) +
  transition_reveal(time)

anim_save("panama_all.gif")
```

```r
knitr::include_graphics("panama_all.gif")
```

![](panama_all.gif)<!-- -->

## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  

```r
covidanimate<-covid19 %>% 
  mutate(new_cases_seven = cases - lag(cases, 7)/7,
         new_cases_seven = replace_na(new_cases_seven,0)) %>% 
  filter(cases>=20) %>% 
  ggplot(aes(x=cases, y=new_cases_seven)) +
  geom_path() +
  geom_point(aes(group=date))+
  geom_text(aes(label=state, color= state)) +
  scale_x_log10()+
  scale_y_log10()+
  theme(legend.position = "none") +
  labs(title = "Cumulative Cases by New COVID Cases in the past 7 days for the United States",
       subtitle = "Date: {frame_along}",
       x= "",
       y= "") +
  transition_reveal(date)

animate(covidanimate, duration = 30)
#Error: cannot allocate vector of size 1.2 Gb whenever changing fps

anim_save("covidcases.gif")
```

```r
knitr::include_graphics("covidcases.gif")
```

![](covidcases.gif)<!-- -->

In this animation, the amount of cases is increasing, with states that have higher populations such as California, New York and Texas leading the increase over time.

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

states_map <- map_data("state")

covid_10000data<-covid19 %>% 
  mutate(state_name=str_to_lower(state)) %>% 
  left_join(census_pop_est_2018,
            by = c("state_name" = "state")) %>%
  mutate(cases_per_10000 = (cases/est_pop_2018)*10000,
         weekday= wday( date, label = TRUE)) %>% 
  filter(weekday == "Fri")

covidanim<-covid_10000data %>% 
  ggplot() +
  geom_map(map = states_map,
           aes(map_id= state_name,
               fill = cases_per_10000,
               group = date)) +
  scale_fill_viridis_c()+
  labs(title = "Cumulative COVID cases per 10000 over time",
       x= "",
       y= "",
       fill= "Cases per 10000")+
  expand_limits(x = states_map$long, y = states_map$lat) +
  transition_states(date)

animate(covidanim,nframes=200,end_pause = 10)

anim_save("covidanim.gif")
```

```r
knitr::include_graphics("covidanim.gif")
```

![](covidanim.gif)<!-- -->

Over time the cases per 10000 increases throughout the United States, however it is concentrated in certain states such as North Dakota and South Dakota.

## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  


  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.

[Weekly Assignment 5 link](https://github.com/joselynaf/WeeklyAssignment5)

**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
