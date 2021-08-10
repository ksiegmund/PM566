---
title: 'Interactive Visualization'
subtitle: "PM 566: Introduction to Health Data Science"
author: "Abigail Horn"
output:
  # slidy_presentation
  xaringan::moon_reader:
    # css: ["theme.css"]
    lib_dir: libs
    nature:
      # beforeInit: "macros.js"
      ratio: "16:9"
      highlightStyle: github
      highlightLines: false
      countIncrementalSlides: false
      titleSlideClass: [center, middle]
    # code_download: true
editor_options: 
  chunk_output_type: console
---

<style type="text/css">
pre{
  font-size:20px;
}
code.r,code.cpp{
  font-size:large
}
</style>




# Introduction to interactive visualization

---

## What is interactive visualization?

- Interactive visualization involves the creation and sharing of graphical representations of data, model, or results that allow a user to directly manipulate and explore

- Some example products and packages in R:
--

  - Interactive plots (`Plotly`)
  
  - Interactive maps (`plotly`, `Leaflet`)
  
  - Interactive tables (`formattable`, `DT`)
  
  - Dashboards (`flexdashboard`)
  
  - Interactive applications (`shiny`)
  
  - Websites (Static using `R Markdown`, `blogdown`, `Hugo`, `Jeckyll`)

---

## What is interactive visualization (cont'd)

- Interactivity allows users to engage with data / models in a way that static visuals cannot

- Features of interactivity include: 
--
  
  - Identify, isolate, and visualize information for extended periods of time 

  - Zoom in and out

  - Highlight relevant information
    
  - Get more information
  
  - Filter
    
  - Animate
  
  - Change parameters

---

# Why use interactive visualization?

Interactive visualization helps with both the **exploration** and **communication** parts of the data science process

<div style="text-align: center;">
  <figure>
    <img style="width: 500px;vertical-align: middle;"  hspace="20px" src="img/data-science-2.png" alt="data_science_interactive_viz"
  </figure>
  <figcaption><b>Where interactive visualization fits in to the data science workflow</b></figcaption>
</div>

---

## Interactive Visualization for **exploratory data analysis** (EDA)

Interactive graphics are well suited to aid the exploration of high-dimensional or otherwise complex data. Interacting with information in a visual way helps to enable insights that wouldn’t be easy or even possible with static graphics, for reasons including:

--

1. **Investigate faster**: In a true exploratory setting, you have to make lots of visualizations, and investigate lots of follow-up questions, before stumbling across something truly valuable. Interactive visualization can aid in the sense-making process by searching for information quickly without fully specified questions (Unwin and Hofmann 1999)

--

2. **Identifying relationships or structure that would otherwise go missing** (J. W. Tukey and Fisherkeller 1973)

--

3. **Understand or diagnose problems with data, models, or algorithms** (Wickham, Cook, and Hofmann 2015)

---

## Interactive visualization for **communication**

Interactive graphics are well suited to communicating high-dimensional or otherwise complex data. Interacting with information in a visual way may help communicating data, models, and results for reasons including: 

(1) Engagement with information has been shown to improve the ability to retain information

<div style="text-align: center;">
  <figure>
    <img style="width: 550px;vertical-align: middle;"  hspace="20px" src="https://i0.wp.com/www.worklearning.com/wp-content/uploads/2015/01/Cone_of_learning_export_from_Wikipedia_11-11-2007.jpg?resize=705%2C518&amp;ssl=1" alt="Edgar Dale Cone of Experience"
  </figure>
  <figcaption><b>Edgar Dale's Cone of Learning</b></figcaption>
</div>

---

## Interactive visualization for **communication** (cont'd)

(2) Automate and efficiently share multiple dimensions of data/models/findings or complex analysis tasks

(3) Help users to better understand, and make decisions on, data/models/findings

<div style="text-align: center;">
  <a href="https://epimodel.shinyapps.io/covid-university/">
  <figure>
    <img style="width: 700px;vertical-align: middle;"  hspace="20px" src="img/COVID-uni-testing.png" alt="EpiModel University Testing"
  </figure>
  <figcaption><b>EpiModel Shiny app for COVID testing at universities</b></figcaption>
</div>

---

## Interactive visualization for **communication** (cont'd)

(4) Tell a more interesting or engaging story, presenting multiple viewpoints of data

(5) Allow users to focus on the aspects most important to them, making the user more likely to understand, learn from, remember and appreciate the data

<div style="text-align: center;">
  <a href="https://inequality.media.mit.edu/">
  <figure>
    <img style="width: 700px;vertical-align: middle;"  hspace="20px" src="img/atlas-of-inequality.png" alt="MIT-inequality"
  </figure>
  <figcaption><b>MIT Media Lab Atlas of Inequality</b></figcaption>
</div>

---

# Schedule: 3 Class Sessions on Interactive Visualization 

**10/28 (Today)**:
  - Creating interactive graphs with **plotly** for R package and tables with **DataTable**

**11/04**: 
  - Create a website using RStudio and GitHub Pages
  - Share your interactive graphics
  - Survey other options for sharing interactive graphics (Shiny apps, dashboards)

**11/11**:  
  1. Guest speakers discussing interactive visualization in practice
    - [BioRealm.ai](https://www.biorealm.ai/) (data science statistical genetics company)
    - [NASA JPL](https://www.jpl.nasa.gov/)

  2. Project workshop

---

# Plotly

---

## What is Plotly?

<div style="text-align: center;">
  <figure>
    <img style="width: 200px;vertical-align: middle;"  hspace="20px" src="img/plotly.png" alt="Plotly"
  </figure>
</div>

  - Plotly is an open source interactive graphing library creating and sharing interactive graphics

  - It is powered by the JavaScript graphing library [plotly.js](https://github.com/plotly/plotly.js) and is designed on principles of adding layers

  - Plotly can work with several programming languages and applications including R, JavaScript,
Python, Matlab, and Excel. 

---

## `plot_ly()` vs. `ggplotly()`

- There are two main ways to create a plotly object:

--

  - Transforming a `ggplot2` object (via `ggplotly()`) into a plotly object 

--

  - Directly initializing a plotly object with `plot_ly()`/`plot_geo()`/`plot_mapbox()`. This provides a 'direct' interface to plotly.js with some additional abstractions to help reduce typing

--

- Both approaches are powered by plotly.js so many of the same concepts and tools that you learn for one interface can be reused in the other

---

## `plot_ly()`

- The `plot_ly()` function has numerous arguments that are unique to the R package (e.g., `color`, `stroke`, `span`, `symbol`, `linetype`, etc.) and make it easier to encode data variables as visual properties (e.g., color). By default, these arguments map values of a data variable to a visual range defined by the plural form of the argument

--

- (almost) every function anticipates a **plotly** object as input to its first argument and returns a modified version of that **plotly** object 

--

- The `layout()` function, which modifies layout components of the plotly object, anticipates a **plotly** object in its first argument and its other arguments add and/or modify various layout components of that object (e.g., the title)

--

- A family of `add_*()` functions (e.g., `add_histogram()`, `add_lines()`, `add_trace()`, etc.) define how to render data into geometric objects by adding a graphical layer to a plot. Layers can be included to add: 

--
  - data
  - aesthetic mappings (e.g., assigning `clarity` to `color`)
  - geometric representation (e.g., rectangles, circles, etc.)
  - statistical transformations (e.g., sum, mean, etc.)
  - positional adjustments (e.g., dodge, stack, etc.) 

---

## `ggplotly()`

- We also have the option of working with `ggplotly()` function from the **plotly** package, which can translate **ggplot2** to **plotly**. 

- The essence of this is very straightforward: 


```r
p <- ggplot(*) + geom_*()
ggplotly(p)
```

--

- This functionality can be really helpful for quickly adding interactivity to your existing **ggplot2** workflow.

--

- `ggplotly()` provides advantages to `plot_ly()` in particular when it comes to exploring statistical summaries across groups. The ability to quickly generate statistical summaries across groups and map to an interactive plot works for basically any geom (e.g., `geom_boxplot()`, `geom_histogram()`, `geom_density()`, etc.)

---

# Getting started

---

## Install Plotly


```r
if(!require(plotly)) install.packages("plotly", repos = "http://cran.us.r-project.org")
library(plotly)
```

---

## Load data for examples 

For examples today we will be using COVID data direct downloaded from the New York Times GitHub repository: https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv

This data source provides COVID cases (confirmed infections) and deaths by each US state and each date

We have preprocessed this data and added some additional variables in the file `"input_data/coronavirus_states.csv"`
  - `population` of each state
  - `new_cases`: daily change in cases
  - `new_deaths`: daily change in deaths
  - `per100k`: cases per 100,000 population
  - `deathsper100k`: deaths per 100,000 population
  - `naive_CFR`: naive[1] Case Fatality Rate (CFR) = deaths / cases, for each state on each date
  
In the lab we will preprocess this data together.

.footnote[[1]"naive" since calculation of CFR requires more sophisticated modeling to account for time delays between cases and deaths]

---

## Load data for examples


```r
# import data
cv_states = read.csv("input_data/coronavirus_states.csv")

# format the date
cv_states$date = as.Date(cv_states$date, format="%Y-%m-%d")

# create most recent day data frame
cv_states_today = subset(cv_states, date==max(cv_states$date))
```

---

## Load data for examples

Inspect the data


```r
str(cv_states)
```

```
## 'data.frame':	13104 obs. of  15 variables:
##  $ state             : Factor w/ 55 levels "Alabama","Alaska",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ date              : Date, format: "2020-03-13" "2020-03-14" ...
##  $ fips              : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ cases             : int  6 12 23 29 39 51 78 106 131 157 ...
##  $ deaths            : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ population        : int  4779736 4779736 4779736 4779736 4779736 4779736 4779736 4779736 4779736 4779736 ...
##  $ new_cases         : int  6 6 11 6 10 12 27 28 25 26 ...
##  $ new_deaths        : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ days_since_death10: int  0 0 0 0 0 0 0 0 0 0 ...
##  $ days_since_case100: int  0 0 0 0 0 0 0 0 1 2 ...
##  $ per100k           : num  0.1 0.3 0.5 0.6 0.8 1.1 1.6 2.2 2.7 3.3 ...
##  $ newper100k        : num  0.1 0.1 0.2 0.1 0.2 0.3 0.6 0.6 0.5 0.5 ...
##  $ deathsper100k     : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ newdeathsper100k  : num  0 0 0 0 0 0 0 0 0 0 ...
##  $ naive_CFR         : num  0 0 0 0 0 0 0 0 0 0 ...
```

---

## Load data for examples

Inspect the data


```r
#dim(cv_states)
summary(cv_states)
```

```
##            state            date                 fips           cases       
##  Washington   :  280   Min.   :2020-01-21   Min.   : 1.00   Min.   :     1  
##  Illinois     :  277   1st Qu.:2020-05-01   1st Qu.:17.00   1st Qu.:  2089  
##  California   :  276   Median :2020-06-29   Median :31.00   Median : 16764  
##  Arizona      :  275   Mean   :2020-06-28   Mean   :31.87   Mean   : 62365  
##  Massachusetts:  269   3rd Qu.:2020-08-28   3rd Qu.:46.00   3rd Qu.: 70786  
##  Wisconsin    :  265   Max.   :2020-10-26   Max.   :78.00   Max.   :916562  
##  (Other)      :11462                                                        
##      deaths           population         new_cases         new_deaths     
##  Min.   :    0.00   Min.   :   56882   Min.   :    0.0   Min.   :   0.00  
##  1st Qu.:   51.75   1st Qu.: 1360301   1st Qu.:   45.0   1st Qu.:   0.00  
##  Median :  453.50   Median : 3831074   Median :  264.0   Median :   4.00  
##  Mean   : 2158.38   Mean   : 5882962   Mean   :  670.6   Mean   :  17.26  
##  3rd Qu.: 2057.00   3rd Qu.: 6547629   3rd Qu.:  770.0   3rd Qu.:  15.00  
##  Max.   :33073.00   Max.   :37253956   Max.   :22276.0   Max.   :1877.00  
##                                                                           
##  days_since_death10 days_since_case100    per100k         newper100k    
##  Min.   :  0.00     Min.   :  0.00     Min.   :   0.0   Min.   :  0.00  
##  1st Qu.: 22.00     1st Qu.: 36.00     1st Qu.: 125.2   1st Qu.:  2.50  
##  Median : 83.00     Median : 96.00     Median : 623.4   Median :  7.10  
##  Mean   : 87.37     Mean   : 98.12     Mean   : 954.1   Mean   : 11.28  
##  3rd Qu.:146.00     3rd Qu.:158.00     3rd Qu.:1563.9   3rd Qu.: 15.30  
##  Max.   :237.00     Max.   :233.00     Max.   :5686.4   Max.   :220.40  
##                                                                         
##  deathsper100k    newdeathsper100k    naive_CFR     
##  Min.   :  0.00   Min.   : 0.0000   Min.   : 0.000  
##  1st Qu.:  3.60   1st Qu.: 0.0000   1st Qu.: 1.440  
##  Median : 14.90   Median : 0.1000   Median : 2.550  
##  Mean   : 29.39   Mean   : 0.2464   Mean   : 3.079  
##  3rd Qu.: 40.00   3rd Qu.: 0.3000   3rd Qu.: 4.330  
##  Max.   :185.30   Max.   :21.3000   Max.   :31.250  
## 
```

---

# Examples

---

## Basic Scatterplot

Let's start with a scatterplot of population-normalized (`per100k`) deaths vs. cases on the most recent date from dataframe `cv_states_today`

- Specify a scatterplot by `type = "scatter"` and `mode = 'markers'`
- Notice how the arguments for the `x` and `y` variables as specified as formulas, with the tilde operator (`~`)
- Use `color` to specify an additional data dimension (factor or continuous), each level of which is mapped to a different color (factor or continuous) 
- Use `colors` is used to specify the range of colors


```r
cv_states_today %>% 
           plot_ly(x = ~deathsper100k, y = ~per100k, 
                   type = 'scatter',
                   mode = 'markers',
                   color = ~state,
                   colors = "Blues")
```

---

## Basic Scatterplot

<!--html_preserve--><div id="htmlwidget-0ab09b219e2558482c5e" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-0ab09b219e2558482c5e">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-8.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

- Scatterplot of deaths vs. cases population-normalized (`per100k`)
- plotly allows us to hover and see the exact $(x,y)$ values of each point
- Notice the automatic `tooltip` that appears when your mouse hovers over each point
- Doubleclick any item in legend to isolate that point in the plot

---

## Scatterplot: size

- You can add an additional dimension by adjusting the `size` of each point (also with `~` operator)
  - Specify the limits of the size through `sizes`
  - `sizemode` specifies `'area'` or `'diameter'`
- Here we specify size as mapped to each state's `naive_CFR`


```r
cv_states_today %>% 
           plot_ly(x = ~deathsper100k, y = ~per100k, 
                   type = 'scatter',
                   mode = 'markers',
                   color = ~state,
                   size = ~naive_CFR,
                   sizes = c(5, 70),
                   marker = list(sizemode='diameter', opacity=0.5))
```

---

## Scatterplot: size

<!--html_preserve--><div id="htmlwidget-ff7b37cbc2a78c52625c" style="width:85%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-ff7b37cbc2a78c52625c">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-10.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

The closer to the bottom right corner of the plot, the higher the CFR, and the larger the point's circle.
---

## Specifying hover information

- You can specify what info will appear when hovering using `hoverinfo` through the `text` argument (also with `~` operator)
  - Multiple variables can be included upon hover
  - Create new lines between variables in `hoverinfo` using `sep = "<br>"`
- Let's add `per100k`, `deathsper100k`, and `naive_CFR` to the hover info:


```r
cv_states_today %>% 
  plot_ly(x = ~deathsper100k, y = ~per100k, 
          type = 'scatter', mode = 'markers', color = ~state,
          size = ~naive_CFR, sizes = c(5, 70), marker = list(sizemode='diameter', opacity=0.5),
          hoverinfo = 'text',
          text = ~paste( paste(state, ":", sep=""),
                         paste(" Cases per 100k: ", per100k, sep="") ,
                         paste(" Deaths per 100k: ", deathsper100k, sep=""),
                         paste(" CFR (%): ", naive_CFR,sep=""),
                         sep = "<br>")) 
```

---

## Specifying hover information

<!--html_preserve--><div id="htmlwidget-8fa3d94495582417687c" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-8fa3d94495582417687c">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-12.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

We can now clearly understand the information being shown in the `tooltip`

---

## Layout

- Specify chart labels through `layout()`
- `hovermode = "compare"` allows comparing multiple points (default is `"closest"`)


```r
cv_states_today %>% 
  plot_ly(x = ~deathsper100k, y = ~per100k, 
          type = 'scatter', mode = 'markers', color = ~state,
          size = ~naive_CFR, sizes = c(5, 70), marker = list(sizemode='diameter', opacity=0.5),
          hoverinfo = 'text',
          text = ~paste( paste(state, ":", sep=""), paste(" Cases per 100k: ", per100k, sep="") , paste(" Deaths per 100k: ", 
                        deathsper100k, sep=""), paste(" CFR (%): ", naive_CFR,sep=""), sep = "<br>")) %>% 
  layout(title = "Cases, Deaths, and Naive Case Fatality Rate for US States",
                  yaxis = list(title = "Cases"), xaxis = list(title = "Deaths"),
         hovermode = "compare")
```

---

## Layout

<!--html_preserve--><div id="htmlwidget-ec6fc30dc571494afab3" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-ec6fc30dc571494afab3">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-14.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---

## 3D Scatterplot

- Can add a 3rd dimension using `type = 'scatter3d'` (make sure to specify the dimension as `z`)


```r
cv_states_today %>% 
  plot_ly(x = ~deathsper100k, y = ~per100k, z = ~population,
          type = 'scatter3d', mode = 'markers', color = ~state,
          size = ~naive_CFR, sizes = c(5, 70), marker = list(sizemode='diameter', opacity=0.5),
          hoverinfo = 'text',
          text = ~paste( paste(state, ":", sep=""), paste(" Cases per 100k: ", per100k, sep="") , paste(" Deaths per 100k: ", 
                        deathsper100k, sep=""), paste(" CFR (%): ", naive_CFR,sep=""), sep = "<br>")) %>% 
  layout(title = "Cases, Deaths, and Naive Case Fatality Rate for US States",
                  yaxis = list(title = "Cases"), xaxis = list(title = "Deaths"),
         hovermode = "compare")
```

---

## 3D Scatterplot

<!--html_preserve--><div id="htmlwidget-acff94b8e9deacd414e7" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-acff94b8e9deacd414e7">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-16.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---

## Scatterplot with `ggplotly()`

- You can create a scatterplot with the `ggplotly()` function in 1 additional line of code
- The advantage of `ggplotly()` is that it allows taking advantage of the geom `geom_smooth()` to see the pattern in the scatter


```r
library(ggplot2)
p <- ggplot(cv_states_today, aes(x=deathsper100k, y=per100k, size=naive_CFR)) + geom_point() + geom_smooth()
ggplotly(p)
```

---

## Scatterplot with `ggplotly()`

<!--html_preserve--><div id="htmlwidget-c426146aa99caa47af5f" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-c426146aa99caa47af5f">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-18.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

The `geom_smooth()` helps us to see there is not a clear correlation between cases and deaths relative to population across the states.
Note that the `geom_smooth()` line also appears upon hover.

---

## Annotations

- You can add annotations to your interactive plot


```r
p <- ggplot(cv_states_today, aes(x=deathsper100k, y=per100k, size=naive_CFR)) + geom_point() + geom_smooth()
fig <- p %>%
  ggplotly(layerData = 2, originalData = F) %>%
  add_fun(function(fig) {
    fig %>% slice(which.max(se)) %>%
      add_segments(x = ~x, xend = ~x, y = ~ymin, yend = ~ymax) %>%
      add_annotations("Max uncertainty")
  })
fig <- fig %>% add_fun(function(p) {
    fig %>% slice(which.min(se)) %>%
      add_segments(x = ~x, xend = ~x, y = ~ymin, yend = ~ymax) %>%
      add_annotations("Min uncertainty")
  })
```

---

## Annotations

<!--html_preserve--><div id="htmlwidget-6df1dbb8610faf9b2ff4" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-6df1dbb8610faf9b2ff4">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-20.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---

## Line graph

- Specify a line plot using `type = "scatter"` and `mode = "lines"`
- Be sure to specify the feature (column in the data) that distinguishes the lines (normally through `color`)


```r
cv_states %>% filter(population>7500000) %>% 
plot_ly(x = ~date, y = ~deaths, color = ~state, type = "scatter", mode = "lines",
        hoverinfo = 'text',
        text = ~paste( paste("Date: ", date, sep=""), paste(state, ":", sep=""), paste(" Deaths (total): ", deaths, sep=""), 
                       paste(" Deaths per 100k: ", deathsper100k, sep=""), sep = "<br>"))
```

---

## Line graph

<!--html_preserve--><div id="htmlwidget-089f19095b8faa9dcbe7" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-089f19095b8faa9dcbe7">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-22.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

Deaths stabilized for New York and New Jersey around the time they started to rise for California, Texas, and Florida.
It helps to be able to see the exact values for each date upon hover.

---

## Line graph: `ggplotly()`

- Simply pass a `ggplot` object to `ggplotly()` to create an interactive version
- `subplot()` can be used to join arrange multiple plots -- works similarly to `grid.arrange()` function from the **gridExtra** package
  - Compare the automatic `tooltip` results for both plots


```r
g1 = plot_ly(cv_states, x = ~date, y = ~deaths, color = ~state, type = "scatter", mode = "lines")
g2 = ggplot(cv_states, aes(x = date, y = cases, color = state)) + geom_line() + geom_point(size = .5, alpha = 0.5)
g2_plotly <- ggplotly(g2)
subplot(g1, g2_plotly)
```

---

## Specifying text with `ggplotly()`

- You can specify the tooltip text in the `ggplot()` or `ggplotly()` prompt, but note that the `ggplotly()` prompt only accepts text in `" "`


```r
g1 = ggplot(cv_states, aes(x = date, y = cases, color = state, 
                           text=paste( paste("Date: ", date, sep=""), paste(state, ":", sep=""), paste(" Cases (total): ", cases, sep=""),sep = "<br>") )) + geom_line() + geom_point(size = .5, alpha = 0.5) 
g2<-ggplotly(g1, tooltip = "text")
widgetframe::frameWidget(g2, width = '75%')
```

---

## Histograms

- For `plot_ly()` use the `type = "histogram"` argument
- Note that `list()` is used to input keys with multiple values (e.g. `xbins`)


```r
g1 <- cv_states_today %>% 
  plot_ly(x = ~new_deaths, type = "histogram", xbins = list(size = 1, end=30 ))
g2 <- cv_states_today %>% ggplot( aes(x=new_deaths)) + geom_histogram(binwidth=1)
g2_plotly <- ggplotly(g2)
subplot(g1, g2_plotly)
```

---

## Histograms

             `plot_ly()`                        `ggplotly()`
             
<!--html_preserve--><div id="htmlwidget-236074f4b0aa7cb38514" style="width:700px;height:311.472px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-236074f4b0aa7cb38514">{"x":{"data":[{"x":[0,0,1,21,40,11,12,4,0,20,18,0,0,8,23,13,22,1,8,17,0,3,17,29,4,8,12,6,5,3,2,7,9,14,17,5,0,11,2,3,7,3,7,21,0,27,35,3,0,0,2,32,1,11,9],"xbins":{"size":1,"end":30},"type":"histogram","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null},{"orientation":"v","width":[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],"base":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"x":[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40],"y":[10,3,3,5,2,2,1,3,3,2,0,3,2,1,1,0,0,3,1,0,1,2,1,1,0,0,0,1,0,1,0,0,1,0,0,1,0,0,0,0,1],"text":["count: 10<br />new_deaths:  0","count:  3<br />new_deaths:  1","count:  3<br />new_deaths:  2","count:  5<br />new_deaths:  3","count:  2<br />new_deaths:  4","count:  2<br />new_deaths:  5","count:  1<br />new_deaths:  6","count:  3<br />new_deaths:  7","count:  3<br />new_deaths:  8","count:  2<br />new_deaths:  9","count:  0<br />new_deaths: 10","count:  3<br />new_deaths: 11","count:  2<br />new_deaths: 12","count:  1<br />new_deaths: 13","count:  1<br />new_deaths: 14","count:  0<br />new_deaths: 15","count:  0<br />new_deaths: 16","count:  3<br />new_deaths: 17","count:  1<br />new_deaths: 18","count:  0<br />new_deaths: 19","count:  1<br />new_deaths: 20","count:  2<br />new_deaths: 21","count:  1<br />new_deaths: 22","count:  1<br />new_deaths: 23","count:  0<br />new_deaths: 24","count:  0<br />new_deaths: 25","count:  0<br />new_deaths: 26","count:  1<br />new_deaths: 27","count:  0<br />new_deaths: 28","count:  1<br />new_deaths: 29","count:  0<br />new_deaths: 30","count:  0<br />new_deaths: 31","count:  1<br />new_deaths: 32","count:  0<br />new_deaths: 33","count:  0<br />new_deaths: 34","count:  1<br />new_deaths: 35","count:  0<br />new_deaths: 36","count:  0<br />new_deaths: 37","count:  0<br />new_deaths: 38","count:  0<br />new_deaths: 39","count:  1<br />new_deaths: 40"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(89,89,89,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x2","yaxis":"y2","hoverinfo":"text","frame":null}],"layout":{"xaxis":{"domain":[0,0.48],"automargin":true,"anchor":"y"},"xaxis2":{"domain":[0.52,1],"automargin":true,"type":"linear","autorange":false,"range":[-2.55,42.55],"tickmode":"array","ticktext":["0","10","20","30","40"],"tickvals":[0,10,20,30,40],"categoryorder":"array","categoryarray":["0","10","20","30","40"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y2","hoverformat":".2f"},"yaxis2":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-0.5,10.5],"tickmode":"array","ticktext":["0.0","2.5","5.0","7.5","10.0"],"tickvals":[0,2.5,5,7.5,10],"categoryorder":"array","categoryarray":["0.0","2.5","5.0","7.5","10.0"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.65296803652968,"tickwidth":0.66417600664176,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(255,255,255,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x2","hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"anchor":"x"},"annotations":[],"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0.52,"x1":1,"y0":0,"y1":1}],"images":[],"margin":{"b":41.7762409303838,"l":48.9497716894977,"t":27.8219030308404,"r":7.30593607305936},"hovermode":"closest","showlegend":false,"plot_bgcolor":"rgba(235,235,235,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.88976377952756,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"barmode":"relative"},"attrs":{"12ac7be0f751":{"x":{},"xbins":{"size":1,"end":30},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"histogram"},"12ac305d8c10":{"x":{},"type":"bar"}},"source":"A","config":{"doubleClick":"reset","showSendToCloud":false},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"subplot":true,"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---

## Heatmap

- Heatmaps are useful for displaying three dimensional data in two dimensions, using color for the third dimension. 
- To create a heatmap from a dataframe we first have to create a matrix out of the three dimensions we want to include. We can do this using the `pivot_wider()` function from **tidyr** (there are many other options)
  - Here we are choosing `date`, `state`, and `newdeathsper100k` to show in our heatmap


```r
library(tidyr)
cv_states_mat <- cv_states %>% select(state, date, newdeathsper100k) %>% filter(date>"2020-03-31") %>% filter(newdeathsper100k < 10)
cv_states_mat2 <- as.data.frame(pivot_wider(cv_states_mat, names_from = state, values_from = newdeathsper100k))
rownames(cv_states_mat2) <- cv_states_mat2$date
cv_states_mat2$date <- NULL
head(cv_states_mat2)
```

---

## Heatmap

- We can then create a heatmap from the matrix by using the `type = "heatmap"` argument
- If you want the x and y axes to show specify that with `x=colnames(data), y=rownames(data)` 
- You can hide or show scale using `showscale=T/F`


```r
library(tidyr)
cv_states_mat <- cv_states %>% select(state, date, newdeathsper100k) %>% filter(date>"2020-03-31") %>% filter(newdeathsper100k < 10)
cv_states_mat2 <- as.data.frame(pivot_wider(cv_states_mat, names_from = state, values_from = newdeathsper100k))
rownames(cv_states_mat2) <- cv_states_mat2$date
cv_states_mat2$date <- NULL
data <- as.matrix(cv_states_mat2)

plot_ly(x=colnames(data), y=rownames(data),
             z=~data,
             type="heatmap",
             showscale=T)
```

---

## Heatmap

<!--html_preserve--><div id="htmlwidget-0cd4c451e279c1280972" style="width:75%;height:311.472px;" class="widgetframe html-widget"></div>
<script type="application/json" data-for="htmlwidget-0cd4c451e279c1280972">{"x":{"url":"slides_files/figure-html//widgets/widget_unnamed-chunk-29.html","options":{"xdomain":"*","allowfullscreen":false,"lazyload":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

We can see when new deaths started to rise and fall for each state. No other state approached the values seen in NY. The hover info conveniently allows us to inspect the exact date and number of new deaths.

---

## 3D Surface

You can also create a 3D surface out of the matrix using `type = "surface"`


```r
plot_ly(x=colnames(cv_states_mat2), y=rownames(cv_states_mat2),
             z=~cv_states_mat2,
             type="surface",
             showscale=F)
```

---

## Choropleth Maps: Setup

Choropleth maps illustrate data across geographic areas by shading regions with different colors. Choropleth maps are easy to make with Plotly though they
require more setup compared to other Plotly graphics. 

Making choropleth maps requires two main types of input:

1. **Geometry information**: This can be supplied using:
  - **GeoJSON** file where each feature has either an id field or some identifying value in properties
  - or a **built-in geometry** within plot_ly: **US states** and **world countries**
2. **A list of values** indexed by feature identifier

The GeoJSON data is passed to the geojson argument, and the data is passed into the **z argument** of the choropleth `trace`

---

## Choropleth Maps: Setup

- Let's focus on interactively mapping the feature `naive_CFR` to each of the US states, including their boundaries
- To use the USA States geometry, set `locationmode='USA-states'` and provide locations as two-letter state abbreviations
- Our `cv_states` identifies states by their long names, so we need to transpose to their abbreviations first


```r
cv_CFR <- cv_states_today %>% select(state, naive_CFR) # select data

# Get state abbreviations and map to state names
library(dplyr)
st_crosswalk <- tibble(state = state.name) %>%
   bind_cols(tibble(abb = state.abb)) %>% 
   bind_rows(tibble(state = "District of Columbia", abb = "DC"))
cv_CFR2 <- left_join(cv_CFR, st_crosswalk, by = "state")
cv_CFR2$state.name <- cv_CFR2$state
cv_CFR2$state <- cv_CFR2$abb
cv_CFR2$abb <- NULL
```

---

## Choropleth Maps: Setup

- Hover text can be specified within the data frame (this is true for any `plot_ly()` object) 


```r
# Create hover text
cv_CFR2$hover <- with(cv_CFR, paste(state.name, '<br>', "CFR:", naive_CFR))

# Set up mapping details
set_map_details <- list(
  scope = 'usa',
  projection = list(type = 'albers usa'),
  showlakes = TRUE,
  lakecolor = toRGB('white')
)
```

---

## Choropleth Maps: Mapping

- Recall: To use the USA States geometry, set `locationmode='USA-states'`
- Specify the map projection details inside `layout()`


```r
# Create the map
fig <- plot_geo(cv_CFR2, locationmode = 'USA-states') %>% 
  add_trace(
    z = ~naive_CFR, text = ~hover, locations = ~state,
    color = ~naive_CFR, colors = 'Blues'
  )
fig <- fig %>% colorbar(title = "CFR")
fig <- fig %>% layout(
    title = paste('CFR by State as of', Sys.Date(), '<br>(Hover for value)'),
    geo = set_map_details
  )
```

---

## Choropleth Maps: Mapping

<!--html_preserve--><div id="htmlwidget-27023406d15be2871bc6" style="width:700px;height:311.472px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-27023406d15be2871bc6">{"x":{"visdat":{"12ac59c85282":["function () ","plotlyVisDat"]},"cur_data":"12ac59c85282","attrs":{"12ac59c85282":{"locationmode":"USA-states","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"z":{},"text":{},"locations":{},"color":{},"colors":"Blues","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"mapType":"geo","scene":{"zaxis":{"title":"naive_CFR"}},"geo":{"domain":{"x":[0,1],"y":[0,1]},"scope":"usa","projection":{"type":"albers usa"},"showlakes":true,"lakecolor":"rgba(255,255,255,1)"},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5},"title":"CFR by State as of 2020-10-29 <br>(Hover for value)"},"source":"A","config":{"showSendToCloud":false},"data":[{"colorbar":{"title":"CFR","ticklen":2,"len":0.5,"lenmode":"fraction","y":1,"yanchor":"top"},"colorscale":[["0","rgba(247,251,255,1)"],["0.0416666666666667","rgba(239,246,252,1)"],["0.0833333333333334","rgba(230,240,250,1)"],["0.125","rgba(222,235,247,1)"],["0.166666666666667","rgba(214,230,244,1)"],["0.208333333333333","rgba(206,224,242,1)"],["0.25","rgba(198,219,239,1)"],["0.291666666666667","rgba(185,213,234,1)"],["0.333333333333333","rgba(172,208,230,1)"],["0.375","rgba(158,202,225,1)"],["0.416666666666667","rgba(142,193,221,1)"],["0.458333333333333","rgba(125,183,218,1)"],["0.5","rgba(107,174,214,1)"],["0.541666666666667","rgba(94,165,209,1)"],["0.583333333333333","rgba(81,155,203,1)"],["0.625","rgba(66,146,198,1)"],["0.666666666666667","rgba(57,135,192,1)"],["0.708333333333333","rgba(46,124,187,1)"],["0.75","rgba(33,113,181,1)"],["0.791666666666667","rgba(27,102,173,1)"],["0.833333333333333","rgba(19,91,164,1)"],["0.875","rgba(8,81,156,1)"],["0.916666666666667","rgba(9,70,139,1)"],["0.958333333333333","rgba(9,59,123,1)"],["1","rgba(8,48,107,1)"]],"showscale":true,"locationmode":"USA-states","z":[1.55,0.45,2.46,1.72,1.9,2.31,6.74,2.83,3.82,2.1,2.1,1.37,1.42,0.96,2.55,2.48,1.41,1.21,1.48,3.18,2.33,2.9,6.51,4.2,1.78,2.82,1.61,1.06,0.94,1.82,4.57,7.04,2.29,6.6,1.6,1.22,2.17,2.61,1.07,1.55,4.34,1.27,3.82,2.23,0.94,1.27,1.97,0.54,2.78,1.56,2.05,2.24,1.91,0.86,0.67],"text":["Alabama <br> CFR: 1.55","Alaska <br> CFR: 0.45","Arizona <br> CFR: 2.46","Arkansas <br> CFR: 1.72","California <br> CFR: 1.9","Colorado <br> CFR: 2.31","Connecticut <br> CFR: 6.74","Delaware <br> CFR: 2.83","Florida <br> CFR: 3.82","Georgia <br> CFR: 2.1","Hawaii <br> CFR: 2.1","Idaho <br> CFR: 1.37","Illinois <br> CFR: 1.42","Indiana <br> CFR: 0.96","Iowa <br> CFR: 2.55","Kansas <br> CFR: 2.48","Kentucky <br> CFR: 1.41","Louisiana <br> CFR: 1.21","Maine <br> CFR: 1.48","Maryland <br> CFR: 3.18","Massachusetts <br> CFR: 2.33","Michigan <br> CFR: 2.9","Minnesota <br> CFR: 6.51","Mississippi <br> CFR: 4.2","Missouri <br> CFR: 1.78","Montana <br> CFR: 2.82","Nebraska <br> CFR: 1.61","Nevada <br> CFR: 1.06","New Hampshire <br> CFR: 0.94","New Jersey <br> CFR: 1.82","New Mexico <br> CFR: 4.57","New York <br> CFR: 7.04","North Carolina <br> CFR: 2.29","North Dakota <br> CFR: 6.6","Ohio <br> CFR: 1.6","Oklahoma <br> CFR: 1.22","Oregon <br> CFR: 2.17","Pennsylvania <br> CFR: 2.61","Rhode Island <br> CFR: 1.07","South Carolina <br> CFR: 1.55","South Dakota <br> CFR: 4.34","Tennessee <br> CFR: 1.27","Texas <br> CFR: 3.82","Utah <br> CFR: 2.23","Vermont <br> CFR: 0.94","Virginia <br> CFR: 1.27","Washington <br> CFR: 1.97","West Virginia <br> CFR: 0.54","Wisconsin <br> CFR: 2.78","Wyoming <br> CFR: 1.56","Alabama <br> CFR: 2.05","Alaska <br> CFR: 2.24","Arizona <br> CFR: 1.91","Arkansas <br> CFR: 0.86","California <br> CFR: 0.67"],"locations":["AL","AK","AZ","AR","CA","CO","CT","DE","DC","FL","GA",null,"HI","ID","IL","IN","IA","KS","KY","LA","ME","MD","MA","MI","MN","MS","MO","MT","NE","NV","NH","NJ","NM","NY","NC","ND",null,"OH","OK","OR","PA",null,"RI","SC","SD","TN","TX","UT","VT",null,"VA","WA","WV","WI","WY"],"type":"choropleth","marker":{"line":{"colorbar":{"title":"","ticklen":2},"cmin":0.45,"cmax":7.04,"colorscale":[["0","rgba(247,251,255,1)"],["0.0416666666666667","rgba(239,246,252,1)"],["0.0833333333333334","rgba(230,240,250,1)"],["0.125","rgba(222,235,247,1)"],["0.166666666666667","rgba(214,230,244,1)"],["0.208333333333333","rgba(206,224,242,1)"],["0.25","rgba(198,219,239,1)"],["0.291666666666667","rgba(185,213,234,1)"],["0.333333333333333","rgba(172,208,230,1)"],["0.375","rgba(158,202,225,1)"],["0.416666666666667","rgba(142,193,221,1)"],["0.458333333333333","rgba(125,183,218,1)"],["0.5","rgba(107,174,214,1)"],["0.541666666666667","rgba(94,165,209,1)"],["0.583333333333333","rgba(81,155,203,1)"],["0.625","rgba(66,146,198,1)"],["0.666666666666667","rgba(57,135,192,1)"],["0.708333333333333","rgba(46,124,187,1)"],["0.75","rgba(33,113,181,1)"],["0.791666666666667","rgba(27,102,173,1)"],["0.833333333333333","rgba(19,91,164,1)"],["0.875","rgba(8,81,156,1)"],["0.916666666666667","rgba(9,70,139,1)"],["0.958333333333333","rgba(9,59,123,1)"],["1","rgba(8,48,107,1)"]],"showscale":false,"color":[1.55,0.45,2.46,1.72,1.9,2.31,6.74,2.83,3.82,2.1,2.1,1.37,1.42,0.96,2.55,2.48,1.41,1.21,1.48,3.18,2.33,2.9,6.51,4.2,1.78,2.82,1.61,1.06,0.94,1.82,4.57,7.04,2.29,6.6,1.6,1.22,2.17,2.61,1.07,1.55,4.34,1.27,3.82,2.23,0.94,1.27,1.97,0.54,2.78,1.56,2.05,2.24,1.91,0.86,0.67]}},"geo":"geo","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

The northeast was hit hard with high CFRs. It would be interesting to see this map at different time points. 

---

## A note on interactive mapping

- There are in fact 4 different ways to render interactive maps with plotly: `plot_geo()`, `plot_ly()`, `plot_mapbox()`, and via **ggplot2**’s `geom_sf()`. 

- Plotly is a general purpose visualization library and doesn’t offer most fully featured geo-spatial visualization toolkit. If you run into limitations with plotly’s mapping functionality there are many other tools for interactive geospatial visualization in R, including: **leaflet**, **mapview**, **mapedit**, **tmap**, and **mapdeck**.


---

# Interactive tables

The `DT` package creates an interactive **DataTable** html widget out of a dataframe in 1 line of code


```r
library(DT)
cv_california <- cv_states %>% filter(state=="California") %>% select(date,cases,deaths,new_cases,new_deaths,naive_CFR)
datatable(cv_california)
```

Note that you can interactively reorder the values by clicking on the arrows at the top of each column, or search for specific values

---

## Interactive tables

<!--html_preserve--><div id="htmlwidget-85d8eae1c726f07166d3" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-85d8eae1c726f07166d3">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102","103","104","105","106","107","108","109","110","111","112","113","114","115","116","117","118","119","120","121","122","123","124","125","126","127","128","129","130","131","132","133","134","135","136","137","138","139","140","141","142","143","144","145","146","147","148","149","150","151","152","153","154","155","156","157","158","159","160","161","162","163","164","165","166","167","168","169","170","171","172","173","174","175","176","177","178","179","180","181","182","183","184","185","186","187","188","189","190","191","192","193","194","195","196","197","198","199","200","201","202","203","204","205","206","207","208","209","210","211","212","213","214","215","216","217","218","219","220","221","222","223","224","225","226","227","228","229","230","231","232","233","234","235","236","237","238","239","240","241","242","243","244","245","246","247","248","249","250","251","252","253","254","255","256","257","258","259","260","261","262","263","264","265","266","267","268","269","270","271","272","273","274","275","276"],["2020-01-25","2020-01-26","2020-01-27","2020-01-28","2020-01-29","2020-01-30","2020-01-31","2020-02-01","2020-02-02","2020-02-03","2020-02-04","2020-02-05","2020-02-06","2020-02-07","2020-02-08","2020-02-09","2020-02-10","2020-02-11","2020-02-12","2020-02-13","2020-02-14","2020-02-15","2020-02-16","2020-02-17","2020-02-18","2020-02-19","2020-02-20","2020-02-21","2020-02-22","2020-02-23","2020-02-24","2020-02-25","2020-02-26","2020-02-27","2020-02-28","2020-02-29","2020-03-01","2020-03-02","2020-03-03","2020-03-04","2020-03-05","2020-03-06","2020-03-07","2020-03-08","2020-03-09","2020-03-10","2020-03-11","2020-03-12","2020-03-13","2020-03-14","2020-03-15","2020-03-16","2020-03-17","2020-03-18","2020-03-19","2020-03-20","2020-03-21","2020-03-22","2020-03-23","2020-03-24","2020-03-25","2020-03-26","2020-03-27","2020-03-28","2020-03-29","2020-03-30","2020-03-31","2020-04-01","2020-04-02","2020-04-03","2020-04-04","2020-04-05","2020-04-06","2020-04-07","2020-04-08","2020-04-09","2020-04-10","2020-04-11","2020-04-12","2020-04-13","2020-04-14","2020-04-15","2020-04-16","2020-04-17","2020-04-18","2020-04-19","2020-04-20","2020-04-21","2020-04-22","2020-04-23","2020-04-24","2020-04-25","2020-04-26","2020-04-27","2020-04-28","2020-04-29","2020-04-30","2020-05-01","2020-05-02","2020-05-03","2020-05-04","2020-05-05","2020-05-06","2020-05-07","2020-05-08","2020-05-09","2020-05-10","2020-05-11","2020-05-12","2020-05-13","2020-05-14","2020-05-15","2020-05-16","2020-05-17","2020-05-18","2020-05-19","2020-05-20","2020-05-21","2020-05-22","2020-05-23","2020-05-24","2020-05-25","2020-05-26","2020-05-27","2020-05-28","2020-05-29","2020-05-30","2020-05-31","2020-06-01","2020-06-02","2020-06-03","2020-06-04","2020-06-05","2020-06-06","2020-06-07","2020-06-08","2020-06-09","2020-06-10","2020-06-11","2020-06-12","2020-06-13","2020-06-14","2020-06-15","2020-06-16","2020-06-17","2020-06-18","2020-06-19","2020-06-20","2020-06-21","2020-06-22","2020-06-23","2020-06-24","2020-06-25","2020-06-26","2020-06-27","2020-06-28","2020-06-29","2020-06-30","2020-07-01","2020-07-02","2020-07-03","2020-07-04","2020-07-05","2020-07-06","2020-07-07","2020-07-08","2020-07-09","2020-07-10","2020-07-11","2020-07-12","2020-07-13","2020-07-14","2020-07-15","2020-07-16","2020-07-17","2020-07-18","2020-07-19","2020-07-20","2020-07-21","2020-07-22","2020-07-23","2020-07-24","2020-07-25","2020-07-26","2020-07-27","2020-07-28","2020-07-29","2020-07-30","2020-07-31","2020-08-01","2020-08-02","2020-08-03","2020-08-04","2020-08-05","2020-08-06","2020-08-07","2020-08-08","2020-08-09","2020-08-10","2020-08-11","2020-08-12","2020-08-13","2020-08-14","2020-08-15","2020-08-16","2020-08-17","2020-08-18","2020-08-19","2020-08-20","2020-08-21","2020-08-22","2020-08-23","2020-08-24","2020-08-25","2020-08-26","2020-08-27","2020-08-28","2020-08-29","2020-08-30","2020-08-31","2020-09-01","2020-09-02","2020-09-03","2020-09-04","2020-09-05","2020-09-06","2020-09-07","2020-09-08","2020-09-09","2020-09-10","2020-09-11","2020-09-12","2020-09-13","2020-09-14","2020-09-15","2020-09-16","2020-09-17","2020-09-18","2020-09-19","2020-09-20","2020-09-21","2020-09-22","2020-09-23","2020-09-24","2020-09-25","2020-09-26","2020-09-27","2020-09-28","2020-09-29","2020-09-30","2020-10-01","2020-10-02","2020-10-03","2020-10-04","2020-10-05","2020-10-06","2020-10-07","2020-10-08","2020-10-09","2020-10-10","2020-10-11","2020-10-12","2020-10-13","2020-10-14","2020-10-15","2020-10-16","2020-10-17","2020-10-18","2020-10-19","2020-10-20","2020-10-21","2020-10-22","2020-10-23","2020-10-24","2020-10-25","2020-10-26"],[1,2,2,2,2,2,3,3,6,6,6,6,6,6,6,6,7,7,7,7,7,7,7,7,7,7,8,9,9,9,11,11,26,26,27,28,33,38,45,55,67,81,100,112,172,179,202,252,320,381,478,588,732,893,1067,1283,1544,1851,2240,2644,3183,4060,4915,5566,6321,7421,8583,9857,11190,12569,13796,15202,16361,17540,19043,20191,21366,22421,23323,24334,25758,27107,28142,29398,30829,31544,33862,35844,37573,39534,41368,42590,43691,45208,46570,48904,50470,52318,53753,55072,56333,58848,60787,62481,64616,66824,68051,69514,71150,73218,74947,77015,78933,80366,81943,83981,86125,88488,90801,92815,94743,97017,99924,101873,104071,107043,110100,113114,115643,118081,120407,122917,126510,129147,131997,134287,137245,140139,143709,147285,150434,152953,155662,159131,163381,167135,170843,174854,178807,184620,191039,195889,201413,207027,211453,216955,223995,232153,239764,248198,256298,265176,271587,277869,287766,296304,303516,311505,320030,327676,336206,346593,355497,364761,374922,383194,391460,400195,410366,422528,433175,443096,453327,459338,467103,474951,486039,494269,502273,509507,515937,522235,527258,532776,541013,548142,556158,563244,574267,586078,595097,603212,613243,621981,628508,634991,640499,646742,653401,659991,665325,669944,676236,682320,687612,692962,698389,702499,706589,712541,716628,722035,727398,732691,737073,740233,742689,746113,749196,753017,757125,760581,763389,767062,769917,773318,776944,781436,785076,788077,792217,795077,798350,801671,805733,809214,811698,814796,817939,821125,824306,828364,831494,834635,837720,840322,843732,847384,851228,854302,857076,859959,863614,867094,870380,874101,876257,878394,882665,887093,890153,896424,902325,906644,909344,913699],[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,2,3,4,4,5,5,6,11,14,17,19,24,28,35,39,52,68,83,104,122,132,147,184,212,247,282,323,351,386,447,506,548,594,632,676,725,778,885,971,1050,1146,1176,1223,1316,1425,1548,1619,1692,1716,1800,1884,1961,2057,2147,2213,2235,2297,2386,2478,2561,2650,2732,2769,2820,2902,3014,3039,3192,3254,3290,3322,3422,3514,3624,3690,3768,3790,3808,3859,3961,4042,4144,4214,4242,4287,4360,4422,4484,4550,4626,4653,4679,4775,4869,4941,4986,5059,5089,5120,5202,5283,5359,5425,5495,5517,5561,5637,5728,5810,5872,5902,5937,5979,6083,6168,6263,6315,6329,6369,6452,6563,6708,6825,6936,7012,7042,7086,7227,7368,7490,7607,7697,7710,7764,7883,8038,8190,8325,8428,8451,8544,8716,8884,9009,9222,9365,9399,9500,9696,9866,10014,10197,10299,10365,10460,10654,10808,10995,11146,11229,11245,11334,11523,11686,11801,11984,12137,12152,12250,12409,12547,12696,12836,12906,12939,13020,13149,13330,13497,13644,13708,13730,13763,13843,13990,14094,14265,14333,14386,14458,14606,14716,14807,14912,15023,15018,15069,15209,15313,15389,15533,15588,15608,15641,15791,15898,15989,16074,16122,16150,16179,16251,16358,16425,16502,16568,16581,16594,16650,16752,16839,16901,16940,16979,16987,17067,17189,17266,17316,17345,17358,17398],[1,1,0,0,0,0,1,0,3,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,1,1,0,0,2,0,15,0,1,1,5,5,7,10,12,14,19,12,60,7,23,50,68,61,97,110,144,161,174,216,261,307,389,404,539,877,855,651,755,1100,1162,1274,1333,1379,1227,1406,1159,1179,1503,1148,1175,1055,902,1011,1424,1349,1035,1256,1431,715,2318,1982,1729,1961,1834,1222,1101,1517,1362,2334,1566,1848,1435,1319,1261,2515,1939,1694,2135,2208,1227,1463,1636,2068,1729,2068,1918,1433,1577,2038,2144,2363,2313,2014,1928,2274,2907,1949,2198,2972,3057,3014,2529,2438,2326,2510,3593,2637,2850,2290,2958,2894,3570,3576,3149,2519,2709,3469,4250,3754,3708,4011,3953,5813,6419,4850,5524,5614,4426,5502,7040,8158,7611,8434,8100,8878,6411,6282,9897,8538,7212,7989,8525,7646,8530,10387,8904,9264,10161,8272,8266,8735,10171,12162,10647,9921,10231,6011,7765,7848,11088,8230,8004,7234,6430,6298,5023,5518,8237,7129,8016,7086,11023,11811,9019,8115,10031,8738,6527,6483,5508,6243,6659,6590,5334,4619,6292,6084,5292,5350,5427,4110,4090,5952,4087,5407,5363,5293,4382,3160,2456,3424,3083,3821,4108,3456,2808,3673,2855,3401,3626,4492,3640,3001,4140,2860,3273,3321,4062,3481,2484,3098,3143,3186,3181,4058,3130,3141,3085,2602,3410,3652,3844,3074,2774,2883,3655,3480,3286,3721,2156,2137,4271,4428,3060,6271,5901,4319,2700,4355],[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,1,1,1,0,1,0,1,5,3,3,2,5,4,7,4,13,16,15,21,18,10,15,37,28,35,35,41,28,35,61,59,42,46,38,44,49,53,107,86,79,96,30,47,93,109,123,71,73,24,84,84,77,96,90,66,22,62,89,92,83,89,82,37,51,82,112,25,153,62,36,32,100,92,110,66,78,22,18,51,102,81,102,70,28,45,73,62,62,66,76,27,26,96,94,72,45,73,30,31,82,81,76,66,70,22,44,76,91,82,62,30,35,42,104,85,95,52,14,40,83,111,145,117,111,76,30,44,141,141,122,117,90,13,54,119,155,152,135,103,23,93,172,168,125,213,143,34,101,196,170,148,183,102,66,95,194,154,187,151,83,16,89,189,163,115,183,153,15,98,159,138,149,140,70,33,81,129,181,167,147,64,22,33,80,147,104,171,68,53,72,148,110,91,105,111,0,51,140,104,76,144,55,20,33,150,107,91,85,48,28,29,72,107,67,77,66,13,13,56,102,87,62,39,39,8,80,122,77,50,29,13,40],[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1.82,1.49,1.23,1,0.89,1.16,1.68,1.98,1.59,1.56,1.31,1.26,1.87,1.91,1.9,1.78,1.87,1.81,1.89,1.74,1.97,2.14,2.04,2.12,2.19,2.09,1.98,2.14,2.15,2.21,2.24,2.34,2.31,2.36,2.55,2.66,2.71,2.78,2.82,2.9,2.98,3.02,3.26,3.45,3.57,3.72,3.73,3.61,3.67,3.79,3.92,3.91,3.97,3.93,3.98,4.05,4.01,4.08,4.1,4.12,4.06,4.08,4.05,4.08,4.1,4.1,4.09,4.07,4.06,4.08,4.12,4.05,4.14,4.12,4.09,4.05,4.07,4.08,4.1,4.06,4.06,4,3.93,3.86,3.89,3.88,3.87,3.83,3.75,3.71,3.69,3.67,3.65,3.6,3.58,3.53,3.48,3.48,3.47,3.44,3.39,3.36,3.33,3.29,3.27,3.23,3.21,3.18,3.14,3.09,3.01,2.95,2.92,2.88,2.84,2.79,2.74,2.67,2.62,2.57,2.52,2.46,2.39,2.35,2.32,2.28,2.26,2.25,2.23,2.19,2.15,2.11,2.09,2.07,2.05,2.03,2.01,1.97,1.94,1.92,1.9,1.89,1.88,1.86,1.84,1.83,1.84,1.83,1.82,1.84,1.84,1.82,1.82,1.84,1.85,1.85,1.86,1.85,1.84,1.82,1.82,1.82,1.82,1.82,1.81,1.79,1.78,1.8,1.81,1.81,1.82,1.82,1.81,1.81,1.82,1.82,1.83,1.84,1.84,1.83,1.83,1.83,1.85,1.86,1.86,1.86,1.85,1.85,1.86,1.87,1.87,1.88,1.88,1.88,1.88,1.9,1.9,1.91,1.91,1.91,1.91,1.9,1.91,1.92,1.92,1.93,1.93,1.92,1.92,1.93,1.94,1.94,1.94,1.94,1.93,1.93,1.93,1.94,1.94,1.94,1.94,1.93,1.93,1.93,1.93,1.93,1.93,1.93,1.93,1.92,1.92,1.93,1.93,1.92,1.91,1.91,1.9]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>date<\/th>\n      <th>cases<\/th>\n      <th>deaths<\/th>\n      <th>new_cases<\/th>\n      <th>new_deaths<\/th>\n      <th>naive_CFR<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[2,3,4,5,6]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

---

# Publishing views

Both `plot_ly()` and `ggplotly()` objects and be computed directly as part of an R Markdown file, which means they will show up on a website you create using R Markdown and GitHub pages.

You can also share your visualizations on https://plot.ly/ by making an account on their site

But you may want to save and embed the interactive HTML file, or save a static image based on the plot

---

## Saving and embedding HTML

Any widget made from any **htmlwidgets** package (e.g., **plotly**, **leaflet**, **DT**, etc.) can be saved as a standalone HTML file via the `htmlwidgets::saveWidget()` function. By default, it produces a completely self-contained HTML file, meaning that all the necessary JavaScript and CSS dependency files are bundled inside the HTML file. 

If you want to embed numerous widgets in a larger HTML document, save all the dependency files externally into a single directory. You can do this by setting `selfcontained = FALSE` and specifying a fixed `libdir` in `saveWidget()`:


```r
library(htmlwidgets)
p <- plot_ly(x = rnorm(100))
saveWidget(p, "p1.html", selfcontained = F, libdir = "lib")
saveWidget(p, "p2.html", selfcontained = F, libdir = "lib")
```

---

## Saving a static image

- With code (convenient if you need to output many static images): Any **plotly** object can be saved as a static image via the `orca()` function.

- From a browser (convenient if you want to manually post-process an image): By default, the 'download plot' icon in the modebar will download to PNG and use the `height` and `width` of the plot, but these defaults can be altered via the plot's configuration, e.g.


```r
plot_ly() %>%
  config(
    toImageButtonOptions = list(
      format = "svg",
      filename = "myplot",
      width = 600,
      height = 700
    )
  )
```

---

# Takeaways

Hopefully in this class you have learned: 

* How to create plots with **plotly** package using either `plot_ly()` calls or `ggplotly()` applied to a **ggplot2** workflow

* Other interactive options -- maps (multiple options), tables (**DataTable**)

* To appreciate how interactive visualization can help to explore data in ways static graphics cannot

* Get an idea of the multitude of options available to you

* Get inspired to create engaging, effective data visualizations and tell stories with your data and findings!

---

## Avoid pitfals 

* Don’t overcomplicate!

* Only use when adding value!

* Some examples of bad practices: [(link)](https://badvisualisations.tumblr.com/)

* And just hilariously bad examples: [(link)](https://viz.wtf/)

---

# More Resources

`Plotly`

- [Plolty R Reference](https://plotly.com/r/reference)
- [The Plotly R API](https://plot.ly/r/)
- [The Plotly R Package on GitHub](https://github.com/ropensci/plotly)
- [The Plotly R Cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf)
- ["Plotly for R" book by Carson Sievert](https://cpsievert.github.io/plotly_book/)

`shiny` and dashboards

- [The `Shiny` Website](http://shiny.rstudio.com)
- [R Markdown: The Definitive Guide, Chapter 5: Dashboards (Layout, Components, Shiny)](https://bookdown.org/yihui/rmarkdown/dashboards.html)

Website development in rmarkdown

- [Tutorial: Creating websites in R](https://www.emilyzabor.com/tutorials/rmarkdown_websites_tutorial.html), Emily C. Zabor   
- [Creating websites with R Markdown](https://bookdown.org/yihui/blogdown/): advanced website creation with `blogdown`, `Hugo`, `Jeckyll`

Data visualization best practices

- [Data Visualization: A Practical Introduction](https://kieranhealy.org/publications/dataviz/), Kieran Healy
- [Fundamentals of Data Visualization](https://serialmentor.com/dataviz/), Claus O. Wilke

---

# References

- ["Plotly for R" book by Carson Sievert](https://cpsievert.github.io/plotly_book/)

- Coursera course on Developing Data Products, Johns Hopkins Data Science Lab: [(GitHub repo for all course materials) materials)](https://github.com/DataScienceSpecialization/Developing_Data_Products)

- [Plolty R Reference](https://plotly.com/r/reference)