---
title       : Estimating MPG for Cars
subtitle    : Shiny Application 
author      : Yetik Serbest
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap, quiz, shiny, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## Tool Description

- It calculates MPG estimate for a car given the following information
  * Transmission type
  * Number of Cylinders in the engine
  * Weight of the car
  * Horse power of the car
- The calculation is done based on the linear model developed using mtcars data set in R
- User enters the parameters as well as the confidence interval
- The tool provides the estimated MPG, confidence interval, and the plot for the confidence interval
- The tool is hosted in this link [here] (https://yetikserbest.shinyapps.io/DevelopingDataProductsProject/)

--- .class #id 

## Tool Layout

* The tool has an input panel
* The tool has two output tabs: 1. Result, 2. Plot
* Result tab provide the estimated MPG and the confidence limits
* Plot tab provides the diagram for the confidence interval
* By default, the tool displays ui.R and server.R files on the right
* By default, the tool displays the tool readme file at the bottom

---

## MPG Calculation Detail

- Shiny application is a wrapper to make it easy for the user and the user does not need to know R
- This is the exact model used in the application


```r
data(mtcars)
fit <- lm(mpg ~ factor(am) + wt + factor(cyl) + hp, data=mtcars)
```

- The follwing is an example calculation


```r
predict(fit,newdata=list(am=factor(1),wt=3,cyl=factor(6),hp=280),interval=("confidence"), level=0.95)
```

```
##     fit   lwr   upr
## 1 16.01 11.68 20.33
```


--- &interactive

## Tool Interactive Console

<div class="row-fluid">
  <div id="transmission" class="control-group shiny-input-radiogroup">
    <label class="control-label" for="transmission">Transmission Type:</label>
    <label class="radio">
      <input type="radio" name="transmission" id="transmission1" value="0" checked="checked"/>
      <span>Automatic</span>
    </label>
    <label class="radio">
      <input type="radio" name="transmission" id="transmission2" value="1"/>
      <span>Manual</span>
    </label>
  </div>
  <div id="cylinder" class="control-group shiny-input-radiogroup">
    <label class="control-label" for="cylinder">Number of Cylinders:</label>
    <label class="radio">
      <input type="radio" name="cylinder" id="cylinder1" value="4" checked="checked"/>
      <span>4 Cylinders</span>
    </label>
    <label class="radio">
      <input type="radio" name="cylinder" id="cylinder2" value="6"/>
      <span>6 Cylinders</span>
    </label>
    <label class="radio">
      <input type="radio" name="cylinder" id="cylinder3" value="8"/>
      <span>8 Cylinders</span>
    </label>
  </div>
  <label for="weight">Weight of the car (in 1000lb)</label>
  <input id="weight" type="text" value=""/>
  <label for="horsepower">Horse Power of the car</label>
  <input id="horsepower" type="text" value=""/>
  <div>
    <label class="control-label" for="confint">Confidence Interval:</label>
    <input id="confint" type="slider" name="confint" value="0.05" class="jslider" data-from="0" data-to="1" data-step="0.004" data-skin="plastic" data-round="FALSE" data-locale="us" data-format="#,##0.#####" data-smooth="FALSE"/>
  </div>
  <div>
    <button type="submit" class="btn btn-primary">Submit</button>
  </div>
</div><div class="span8">
  <div id="nvd3plot" class="shiny-html-output nvd3 rChart"></div>
</div> 
