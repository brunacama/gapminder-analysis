---
title: "Gapminder analysis"
output: 
  html_document:
    toc: true
    toc_float: true
    theme: default
    highlight: zenburn
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## R Markdown
###I'm testing headers here
####For example this is a level 4 header

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=TRUE}
plot(pressure)
```
Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
## Making a list
It's as simple as just writing the different points, markdown will turn them into bullet points

- Car 1
- Car 2
- Car 3

Alternatively, if you want a numbered bullet list, you don't need to actually write the correct numbers, you can just use the same number for all points and it will still number them correctly in the html

1. Car 1
1. Car 2
1. Car 3

## Evaluating code in-line
If you incorporate code in your text, putting it between backticks will incorporate a code explaination on that line
`r a<-c("red", "blue","yellow")`

##Incorporate image

![](http://tspa.000webhostapp.com/stockphoto/3.jpg)
<img src="http://tspa.000webhostapp.com/stockphoto/3.jpg" width="200px">"

## And now, Gapminder
### What Gapminder is
Gapminder is an independent Swedish foundation with no political, religious or economic affiliations. Gapminder is a fact tank, not a think tank. Gapminder fights devastating misconceptions about global development. Gapminder produces free teaching resources making the world understandable based on reliable statistics. Gapminder promotes a fact-based worldview everyone can understand.  Gapminder collaborates with universities, UN, public agencies and non-governmental organizations. All Gapminder activities are governed by the board. We do not award grants. Gapminder Foundation is registered at Stockholm County Administration Board. Our constitution can be found here.
### What Gapminder does

- Gapminder measures ignorance about the world
- Gapminder makes global data easy to use and understand
- Gapminder provides courses and certificates
- Gapminder promotes Factfulness, a new way of thinking
- Gapminder collaborates with educators across the world

![](https://s3-eu-west-1.amazonaws.com/static.gapminder.org/GapminderMedia/wp-uploads/20161019161829/screenshot2016.jpg)

## Insert an R chunk
You just need to go to the top right where it says insert > R, then write your setting for how you want to present the chunk in {}, then follow that up with the actual code. If you want the code to show up, use echo=TRUE, otherwise echo=FALSE. All of this goes in \```
```{r, chunk, echo=TRUE}
a<-c("red","blue","yellow")
print(a)

```

## Write an installation section
To install Gapminder, you can either access it the traditional way with install.packages
```{r, install-gapminder, eval=FALSE}
install.packages("gapminder")
```
Or, you can download it from GitHub if you wish.
```{r, github-gapminder, eval=FALSE}
devtools::install_github("jennybc/gapminder")
```
You may also need some additional packages, though they may be pre-installed. These are:
1. ggplot2
1. skimr
1. DT
```{r, install-additional, eval=FALSE}
install.packages(c("ggplot2","skimr","DT"))
```

##Displaying data
You just use the same code as R! If eval=FALSE, the code will actually be run as part of the report.
```{r data-display}
data(airquality)
head(airquality)
```

If you don't set eval (default eval=TRUE), only the code will show up, but not the outcome of it.
Same with tibbles!

```{r display-tibble}
library(tibble)
as_tibble(airquality)
```

You can display your data into a more orderly looking table using knitr.

```{r knitr-table}
library(knitr)
data(airquality)
kable(head(airquality), caption = "New York Air Quality Measurements")
```

These are pretty default, but you can also put your data into a nice looking, interactive table using DT. This will give you a table that can be scrolled horizontally, or ordered by a column's values, etc.

```{r interactive-table}
library(DT)
data(airquality)
datatable(airquality, caption = "New York Air Quality Measurements")
```

### Plotting

In markdown, you can make a plot normally (just make sure to call ggplot2 or other relevant packages within the same chunk)
```{r add-plot, echo=FALSE}
library(ggplot2)
library(gapminder)
gapminder
p <- ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent)) + 
    geom_point()
p
```

But, you can also make an interactive plot using plotly! It can be zoomed in/out, navigated, etc.
```{r plotly-plot, echo=FALSE}
library(plotly)
library(ggplot2)
library(gapminder)
library(dplyr)
gapminder
p <- ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent)) + 
    geom_point() +
    scale_x_log10()
ggplotly(p)
```
If needed, you can read a single chunk simply doing knitr::read_chunk(here:here("plotly-plot", "index.Rmd"))
