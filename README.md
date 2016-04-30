# NHL scritchy scratchy
RotBlauer LLC  
`r format(Sys.Date())`  
Going to look at some things using the nhl data ala 

Load up dat core data and setup

```r
library(ggplot2)
theme_set(theme_bw(24))
load("source-data/nhlscrapr-core.RData")
```

Checkin number of unique players by positions, for example:


```r
 theme_set(theme_bw(24))
 c <- ggplot(subset(roster.unique,pos!=''), aes(x=pos))
 c + geom_bar() +xlab("Player Position")
```

![](README_files/figure-html/numPos-1.png)<!-- -->


Lets load up 2014 - 2015

```r
load('source-data//nhlscrapr-20142015.RData')
```
Check out event types

```r
table(grand.data$etype)
```

```
## 
##  BLOCK CHANGE  EGPID    EGT  EIEND  EISTR    FAC   GIVE   GOAL    HIT 
##  38545 132296      1      1      4      4  81082  22193   7377  67418 
##   MISS   PEND   PENL   SHOT    SOC   TAKE 
##  30887   4459  10563  72659    173  18004
```

Neat events, plot time

```r
plot(grand.data$xcoord,grand.data$ycoord)
```

![](README_files/figure-html/p1-1.png)<!-- -->
It's a rink!

Look at density of events

```r
ggplot(grand.data, aes(x = xcoord, y = ycoord)) +  geom_point() + geom_density2d()
```

![](README_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

And just the goals

```r
ggplot(grand.data[grand.data$etype %in% "GOAL",], aes(x = xcoord, y = ycoord)) +  geom_point() + geom_density2d()
```

![](README_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

And just the shots

```r
ggplot(grand.data[grand.data$etype %in% "SHOT",], aes(x = xcoord, y = ycoord)) +  geom_point() + geom_density2d()
```

![](README_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

And our favorite, hits!

```r
ggplot(grand.data[grand.data$etype %in% "HIT",], aes(x = xcoord, y = ycoord)) +  geom_point() + geom_density2d()
```

![](README_files/figure-html/unnamed-chunk-4-1.png)<!-- -->
