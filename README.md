Processing Geo-Data from Strava
=====
------
Reading, parsing, and playing around with Geographical Strava data in R
----------
As many people measure more and more of their lives with activity-trackers and GPS watches and upload the data to websites like Strava, there is a trove of interesting information to be found by harvesting these data. Being avid R users, we did not want to wait for the websites to roll out some of the more interesting analyses. Using the original Rtrava library (https://github.com/ptdrow/Rtrava) which connects with the Strava API, the R packages of ggplot2, plyr, knitr, rmarkdown, httr, maptools, maps, rjson, stringr, RCurl, and RMarkdown, it is possible to generate a report of sports and with lots of little heatmaps and other simple analyses. We can easily divide the data by sport type, speed, date, and any other parameter to begin to look at the correlations between speed and heart rate or elevation gain and duration.  As shown here: [https://kmader.github.io/stravaResults.html](stravaResults.html)

# Making your own

To make your own, you basically just have to copy the first portion of the stravaResults.Rmd file up until ```summary.data, pl.data``` are defined. These are the useful variables for plotting everything else. 

## Heatmap
A heat-map can be created using the following code which first pulls a black and white map at the scale 2 from the server and shows it with a 2d binning of the data on top. The bins are shown as hexagonal shapes (stat_binhex) and the filling is dictated by the ```log``` of the count (a count of 0 is not shown at all).
```{r}
map.data<-get_map(location=c(lon=8.22190,lat=47.53733),color="bw",scale=2)
ggmap(map.data)+
  stat_binhex(data=pl.data,aes(x=lng,y=lat),alpha=0.5,bins=200)+
  scale_fill_gradientn(colours=rainbow(6),trans = "log")+
  labs(y="Latitude",x="Longitude")+
  theme_bw(20)
```