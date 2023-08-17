---
title: "CASE STUDY TITLE"
author: "YOUR NAME"
date: "October 14, 2020"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---






```r
# Use this R-Chunk to import all your datasets!
c1<-child_mortality

 
   ggplot(c1, aes(x=year, y=(deaths_per_woman), color = continent)) +
 geom_line(color="blue")+
  ylab("Number Of Surviving Children")+
  ggtitle("Child Survival Rate Increasing?")+
     facet_grid(~continent)
```

![](Miles_Task_9_files/figure-html/load_data-1.png)<!-- -->

```r
## Idea Geom point faceted by continet 
```

## Background

_Place Task Background Here_

## Data Wrangling


```r
# Use this R-Chunk to clean & wrangle your data!
```

## Data Visualization


```r
# Use this R-Chunk to plot & visualize your data!
```

## Conclusions
