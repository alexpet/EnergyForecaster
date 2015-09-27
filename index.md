---
title       : Energy Consumption Regression Modeller
subtitle    : Tool for predicting you energy consumption using temperature
author      : Alexander Petkovski
job         : Load Forecasting
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, quiz, bootstrap, shiny]    # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
ext_widgets : {rCharts: ["libraries/highcharts","libraries/nvd3", "libraries/morris", "libraries/leaflet", "libraries/rickshaw"]}

--- &radio
## How is your energy use affected by temperature?

Have you ever wanted an app that could answer the following questions?

1. How does temperature affect my consumption?
2. Are there any seasonal patterns in my usage?
3. Is it possible to know my energy use if I know the temperature?
4. Is there a simple formula that can be derived?
5. If predicatable, how accurate is that prediction?
6. _All of the above?_

*** .hint 

Go with the most optimistic answer

*** .explanation 

This app will do it all! Go to the next side to see it.

---

## How does the application work?

1. From the address you enter, the app locates the nearest weather station.
2. From the usage you enter, the app calculates average daily consumption and 
temperature.
3. An exploration area exists to show you interactive graphs between temperature 
consumption, along with a motion chart showing how the relationship works over time.
3. A regression model is generated over 5 possible models between temperature, 
season, Cooling Degree Days (CDD) and Heating Degree Days (HDD).
4. The best model is selected and various diagnostics such as residuals are provided.
5. The final model is a monthly forecast under normal temperatures with an option 
to increase or decrease temperatures.
6. The prediction model includes a 90% Confidence Interval and works with either 
gas or electricity and should be usable from any address world-wide.

--- 
## Here is what the regression model looks like

![plot of chunk unnamed-chunk-2](assets/fig/unnamed-chunk-2-1.png) 

#Prepare model data
motionModel <- subset(dModel,
                  select = c("chartDate",
                             "usageDays",
                             "avgUsage",
                             "avgTemp",
                             "CDD",
                             "HDD",
                             "season"
                             ))
motionModel$year <- format(motionModel$chartDate, "%Y")
names(motionModel) <- c("Date",
                    "Days",
                    "Consumption",
                    "Temperature",
                    "CDD",
                    "HDD",
                    "Season",
                    "Year"
                    )
#Return the model
M1 <- gvisMotionChart(motionModel,
                   idvar = "Year",
                   timevar = "Date",
                   colorvar = "Season",
                   sizevar = "Days",
                   xvar = "Temperature",
                   yvar = "Consumption"
   )
print(M1, tag = 'chart')
```


--- 
## Where to go next

So try out the app at the following page:   
[Energy Consumption Regression Modeller](https://alexpet.shinyapps.io/EnergyForecaster)
   
If you need a sample file, try the following:   
[Samples Gas Usage File](https://raw.githubusercontent.com/alexpet/DevelopingDataProducts/master/project/shiny/GasUsages.csv)
   
I'm sure you're going to love it!

