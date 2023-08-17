---
title: "Task 25"
author: "Gideon Miles"
date: "December 09, 2020"
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
cap<-read_csv("statecapitals.csv")
```

## Background

_Place Task Background Here_

## Data Wrangling


```r
# Use this R-Chunk to clean & wrangle your data!
library(maps)
library(USAboundaries)
library(tidyverse)
library(leaflet)

USALat<-world.cities %>% filter(country.etc=="USA")



USA2<-us_cities()

cities <- USA2 %>% filter(state_name!="Alaska", state_name!="Hawaii") %>% group_by(state_name) %>%  top_n(3, population) %>% mutate(top3=row_number(desc(population))) %>% mutate(long = map_dbl(geometry, ~st_centroid(.x)[[1]]),
         lat = map_dbl(geometry, ~st_centroid(.x)[[2]]))
```

## Data Visualization

#### Top Three Cities By Population in Each of the Continential 48 States


```r
# Use this R-Chunk to plot & visualize your data!
leaflet() %>% addTiles() %>% 
  addMarkers(data = cities,
             lng = ~long,
             lat = ~lat,
             label = ~paste(name_2010, "Population:", population),
             clusterOptions = markerClusterOptions())
```

<!--html_preserve--><div id="htmlwidget-f791339587ce8aa35e57" style="width:1152px;height:576px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-f791339587ce8aa35e57">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":1,"detectRetina":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap<\/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA<\/a>"}]},{"method":"addMarkers","args":[[33.5274441,30.668426,32.3462512,36.0715607,35.3492757,34.7254318,33.4019259,33.5721625,32.1542888,34.0193936,32.8152995,37.2968672,39.6880021,38.8672553,39.7618487,41.1873858,41.7660453,41.3108088,38.9041485,39.1606061,39.677569,39.7352263,30.3370193,25.775163,27.9700861,33.7629088,33.3655309,32.510197,41.9670481,41.5541036,41.5739461,43.5984881,43.617852,43.582381,41.763455,41.8375511,42.2633938,37.9877339,41.0881729,39.7766644,39.1225389,38.8890422,37.6906938,36.9709194,38.0401572,38.1780769,30.4484535,30.0686361,32.4670204,42.33196,42.115454,42.2694781,39.3002135,39.4330863,39.0836473,44.8306292,44.0895941,43.663811,42.3830375,42.961156,42.4929044,44.9633235,44.0154424,44.9488695,39.125212,37.194152,38.6356988,30.4160584,32.3158308,34.9508416,45.7895184,47.5014389,46.8693223,35.2087069,36.0964835,35.8302035,46.8110381,46.8652063,47.9127893,41.1542932,40.8089574,41.2646751,43.2324926,42.9846891,42.7490744,40.7114174,40.7242204,40.9147462,35.1055517,32.3264441,35.2850958,36.0122334,36.2277116,39.4744867,42.8924919,40.6642738,43.1699272,39.1399019,41.4781381,39.9847989,35.2405774,35.4670795,36.1279488,44.0567484,45.5369506,44.9236937,40.5939656,40.0093755,40.4397525,41.7697341,41.8230556,41.7007569,32.8179219,34.0297833,32.9173424,45.4646777,44.0710712,43.5383351,35.9708752,35.1035431,36.1718001,32.794176,29.7804724,29.4724026,40.2453301,40.7785197,40.6884927,36.6793761,36.9230149,36.7793219,44.4919905,43.6096702,44.4364933,47.6204993,47.6735545,47.2521991,44.5206763,43.0878055,43.0633484,38.3486917,38.4106509,39.2613533,42.8405322,41.1521947,41.3102405],[-86.799047,-88.1002261,-86.2685927,-94.1665396,-94.370883,-92.358556,-111.7173787,-112.0879662,-110.8710622,-118.4108248,-117.134993,-121.8193058,-104.68974,-104.760749,-104.8806251,-73.1957339,-72.6833394,-72.924953,-77.0170942,-75.5216585,-75.7573084,-75.5292892,-81.6613021,-80.2086152,-82.4796734,-84.4226745,-82.0734219,-84.874946,-91.6777599,-90.6039968,-93.616708,-116.2310843,-116.397129,-116.5638753,-88.290099,-87.6818441,-89.0628271,-87.534703,-85.14388,-86.1459355,-94.7417813,-94.6905839,-97.3426776,-86.4384623,-84.4584429,-85.6667077,-91.1258993,-89.9390074,-93.7926845,-71.0201725,-72.5399783,-71.8077831,-76.6105159,-77.4127579,-77.1556178,-68.7923966,-70.1721851,-70.255365,-83.1022365,-85.6555701,-83.0250007,-93.2682835,-92.4772105,-93.1038552,-94.5511362,-93.2913048,-90.2445816,-89.071845,-90.2128226,-89.977981,-108.5498909,-111.299975,-114.0103464,-80.8307389,-79.8271079,-78.6414394,-100.7701017,-96.8290052,-97.0750101,-95.9328384,-96.6803544,-96.0419269,-71.5612523,-71.4438932,-71.4905435,-74.0647599,-74.1725735,-74.1628255,-106.6473884,-106.7896951,-106.6988694,-115.0374619,-115.2640448,-119.7765384,-78.8596862,-73.9385004,-77.6168907,-84.5064465,-81.6794861,-82.9850438,-97.3453056,-97.5136565,-95.9023162,-123.1162068,-122.649971,-123.0231194,-75.4781595,-75.1333459,-79.9765919,-71.4850489,-71.4187795,-71.4203343,-79.9589267,-80.8965664,-80.0651497,-98.468104,-103.2179242,-96.7319985,-83.9464787,-89.9784984,-86.7850016,-96.7655033,-95.3863425,-98.5251419,-111.6448069,-111.9314142,-112.0117586,-76.3017884,-76.2446413,-76.0240202,-73.2393625,-72.9777884,-73.1826185,-122.3508761,-117.4165955,-122.4598318,-87.9841686,-89.4301208,-87.9666952,-81.632324,-82.4346886,-81.5433763,-106.3201684,-104.7832381,-105.6096249],null,null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},null,null,{"showCoverageOnHover":true,"zoomToBoundsOnClick":true,"spiderfyOnMaxZoom":true,"removeOutsideVisibleBounds":true,"spiderLegPolylineOptions":{"weight":1.5,"color":"#222","opacity":0.5},"freezeAtZoom":false},null,["Birmingham city Population: 212237","Mobile city Population: 195111","Montgomery city Population: 205764","Fayetteville city Population: 73580","Fort Smith city Population: 86209","Little Rock city Population: 193524","Mesa city Population: 439041","Phoenix city Population: 1445632","Tucson city Population: 520116","Los Angeles city Population: 3792621","San Diego city Population: 1307402","San Jose city Population: 945942","Aurora city Population: 325078","Colorado Springs city Population: 416427","Denver city Population: 600158","Bridgeport city Population: 144229","Hartford city Population: 124775","New Haven city Population: 129779","Washington city Population: 601723","Dover city Population: 36047","Newark city Population: 31454","Wilmington city Population: 70851","Jacksonville city Population: 821784","Miami city Population: 399457","Tampa city Population: 335709","Atlanta city Population: 420003","Augusta-Richmond County consolidated government Population: 195844","Columbus city Population: 189885","Cedar Rapids city Population: 126326","Davenport city Population: 99685","Des Moines city Population: 203433","Boise City city Population: 205671","Meridian city Population: 75092","Nampa city Population: 81557","Aurora city Population: 197899","Chicago city Population: 2695598","Rockford city Population: 152871","Evansville city Population: 117429","Fort Wayne city Population: 253691","Indianapolis city (balance) Population: 820445","Kansas City city Population: 145786","Overland Park city Population: 173372","Wichita city Population: 382368","Bowling Green city Population: 58067","Lexington-Fayette urban county Population: 295803","Louisville/Jefferson County metro government (balance) Population: 597337","Baton Rouge city Population: 229493","New Orleans city Population: 343829","Shreveport city Population: 199311","Boston city Population: 617594","Springfield city Population: 153060","Worcester city Population: 181045","Baltimore city Population: 620961","Frederick city Population: 65239","Rockville city Population: 61209","Bangor city Population: 33039","Lewiston city Population: 36592","Portland city Population: 66194","Detroit city Population: 713777","Grand Rapids city Population: 188040","Warren city Population: 134056","Minneapolis city Population: 382578","Rochester city Population: 106769","St. Paul city Population: 285068","Kansas City city Population: 459787","Springfield city Population: 159498","St. Louis city Population: 319294","Gulfport city Population: 67793","Jackson city Population: 173514","Southaven city Population: 48982","Billings city Population: 104170","Great Falls city Population: 58505","Missoula city Population: 66788","Charlotte city Population: 731424","Greensboro city Population: 269666","Raleigh city Population: 403892","Bismarck city Population: 61272","Fargo city Population: 105549","Grand Forks city Population: 52838","Bellevue city Population: 50137","Lincoln city Population: 258379","Omaha city Population: 408958","Concord city Population: 42695","Manchester city Population: 109565","Nashua city Population: 86494","Jersey City city Population: 247597","Newark city Population: 277140","Paterson city Population: 146199","Albuquerque city Population: 545852","Las Cruces city Population: 97618","Rio Rancho city Population: 87521","Henderson city Population: 257729","Las Vegas city Population: 583756","Reno city Population: 225221","Buffalo city Population: 261310","New York city Population: 8175133","Rochester city Population: 210565","Cincinnati city Population: 296943","Cleveland city Population: 396815","Columbus city Population: 787033","Norman city Population: 110925","Oklahoma City city Population: 579999","Tulsa city Population: 391906","Eugene city Population: 156185","Portland city Population: 583776","Salem city Population: 154637","Allentown city Population: 118032","Philadelphia city Population: 1526006","Pittsburgh city Population: 305704","Cranston city Population: 80387","Providence city Population: 178042","Warwick city Population: 82672","Charleston city Population: 120083","Columbia city Population: 129272","North Charleston city Population: 97471","Aberdeen city Population: 26091","Rapid City city Population: 67956","Sioux Falls city Population: 153888","Knoxville city Population: 178874","Memphis city Population: 646889","Nashville-Davidson metropolitan government (balance) Population: 601222","Dallas city Population: 1197816","Houston city Population: 2099451","San Antonio city Population: 1327407","Provo city Population: 112488","Salt Lake City city Population: 186440","West Valley City city Population: 129480","Chesapeake city Population: 222209","Norfolk city Population: 242803","Virginia Beach city Population: 437994","Burlington city Population: 42417","Rutland city Population: 16495","South Burlington city Population: 17904","Seattle city Population: 608660","Spokane city Population: 208916","Tacoma city Population: 198397","Green Bay city Population: 104057","Madison city Population: 233209","Milwaukee city Population: 594833","Charleston city Population: 51400","Huntington city Population: 49138","Parkersburg city Population: 31492","Casper city Population: 55316","Cheyenne city Population: 59466","Laramie city Population: 30816"],{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"limits":{"lat":[25.775163,47.9127893],"lng":[-123.1162068,-68.7923966]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

## Conclusions

I Love leafelt.  There is just something about an interactive graph that make sit feel like you've accomplsihed something more.  Something more insighful, intuitive, and feel like you have control over the sights you ar looking for.  It feels like you can play with and explore reality as you choose more fully rather than simiply being given a display, even if it is no different in the fact that the data given you is the same.  
