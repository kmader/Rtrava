Processing Geo-Data from Strava
=====
Reading, parsing, and playing around with Geographical Strava data in R
----------
Using the original Rtrava library (forked in this repository) which connect with the Strava API, the excellent R packages of ggplot2, plyr, knitr, rmarkdown, httr, maptools, maps, rjson, stringr, RCurl, and RMarkdown, we create a nice report of sports and with lots of little heatmpas and other simple analyses. As shown here: [https://rawgit.com/kmader/Rtrava/master/stravaResults.html](https://rawgit.com/kmader/Rtrava/master/stravaResults.html)
------

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