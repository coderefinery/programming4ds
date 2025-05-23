# Plotting with [ggplot2](https://ggplot2.tidyverse.org/)

:::{objectives}
- Be able to create simple plots with ggplot2 and tweak them
- Know how to look for help
- Reading data into R from disk or web
- Know how to tweak example plots from a gallery for your own purpose
- We will build up an equivalent notebook to the original Python notebook
:::


## Repeatability/reproducibility

From [Claus O. Wilke: "Fundamentals of Data Visualization"](https://clauswilke.com/dataviz/):

> *One thing I have learned over the years is that automation is your friend. I
> think figures should be autogenerated as part of the data analysis pipeline
> (which should also be automated), and they should come out of the pipeline
> ready to be sent to the printer, no manual post-processing needed.*

- **Try to minimize manual post-processing**. Automated visualization prevents last-minute regeneration panic.
- No single library or language is perfect for every use-case.
- In R, common visualization libraries include:
  - [ggplot2](https://ggplot2.tidyverse.org/): grammar of graphics
  - [lattice](https://lattice.r-forge.r-project.org/): grid-based graphics
  - [plotly](https://plotly.com/r/): interactive visualizations
  - [highcharter](https://jkunst.com/highcharter/): interactive visualizations based on Highcharts
  - [leaflet](https://rstudio.github.io/leaflet/): interactive maps
  - [shiny](https://shiny.rstudio.com/): interactive web apps
  - [base R](https://www.rdocumentation.org/packages/graphics): traditional graphics system
- Two main visualization paradigms: procedural (base R) and declarative (ggplot2).


## Why are we starting with [ggplot2](https://ggplot2.tidyverse.org/)?

- Concise, powerful, and consistent grammar of graphics
- Intuitive mapping of visual aesthetics to data
- Easily integrates with data manipulation libraries like dplyr
- Well-documented, widely adopted, and open source
- Simple to export to multiple formats (png, svg, pdf)


## Example data: Weather data from two Norwegian cities

We will use weather data from [Norsk KlimaServiceSenter](https://seklima.met.no/observations/), Meteorologisk institutt (MET) (CC BY 4.0). The data is in CSV format for Oslo and Tromsø:

- [View data repository](https://github.com/coderefinery/data-visualization-python/tree/main/data)

We'll load CSV files using `read.csv()` or directly from the web with `read.csv(url)`.

Dataframes in R are excellent for tabular data and are directly usable with ggplot2.


## Reading data into a dataframe

Let's combine monthly data from two CSV files:

```r
url_prefix <- "https://raw.githubusercontent.com/coderefinery/data-visualization-python/main/data/"

data_tromso <- read.csv(paste0(url_prefix, "tromso-monthly.csv"))
data_oslo <- read.csv(paste0(url_prefix, "oslo-monthly.csv"))

data_monthly <- rbind(data_tromso, data_oslo)

# view combined data
data_monthly
```

Fixing date format:
```r
data_monthly$date <- as.Date(paste0("01.", data_monthly$date), format="%d.%m.%Y")
```


## What is in a dataframe?

Dataframes contain rows and columns:

Explore interactively in R:
```r
head(data_monthly)
tail(data_monthly)
names(data_monthly)
str(data_monthly)
dim(data_monthly)
data_monthly$max.temperature
summary(data_monthly$max.temperature)
max(data_monthly$max.temperature)
subset(data_monthly, max.temperature > 20)
```


## Where to learn more about dataframes in R

- [R for Data Science](https://r4ds.hadley.nz/)
- [Quick-R](https://www.statmethods.net/management/index.html)
- [Data Carpentry R lessons](https://datacarpentry.org/R-ecology-lesson/)


## Plotting the data

Simple plot:
```r
library(ggplot2)

ggplot(data_monthly, aes(x = date, y = precipitation, fill = name)) +
  geom_bar(stat = "identity", position = "dodge")
```

Improve temporal axis:
```r
ggplot(data_monthly, aes(x = date, y = precipitation, fill = name)) +
  geom_bar(stat = "identity", position = "dodge") +
  scale_x_date(date_labels = "%Y-%m")
```

Plot side-by-side panels:
```r
ggplot(data_monthly, aes(x = date, y = precipitation, fill = name)) +
  geom_bar(stat = "identity") +
  facet_wrap(~name)
```

Stacked bars:
```r
ggplot(data_monthly, aes(x = date, y = precipitation, fill = name)) +
  geom_bar(stat = "identity")
```

Temperature range area plot:
```r
ggplot(data_monthly, aes(x = date, ymin = min.temperature, ymax = max.temperature, fill = name)) +
  geom_ribbon(alpha = 0.5)
```

## Exercise: Using visual channels to re-arrange plots

- Switch axes:
```r
ggplot(data_monthly, aes(y = date, x = precipitation, fill = name)) +
  geom_bar(stat = "identity") + facet_wrap(~name)
```

- Change axis title:
```r
ggplot(data_monthly, aes(y = date, x = precipitation, fill = name)) +
  geom_bar(stat = "identity") + facet_wrap(~name) +
  labs(x = "Precipitation (mm)")
```

- Side-by-side temperature plots:
```r
ggplot(data_monthly, aes(x = date, ymin = min.temperature, ymax = max.temperature)) +
  geom_ribbon(alpha = 0.5) + facet_wrap(~name)
```

## More fun with visual channels

Read daily data:
```r
data_tromso_daily <- read.csv(paste0(url_prefix, "tromso-daily.csv"))
data_oslo_daily <- read.csv(paste0(url_prefix, "oslo-daily.csv"))
data_daily <- rbind(data_tromso_daily, data_oslo_daily)
data_daily$date <- as.Date(data_daily$date, format="%d.%m.%Y")
data_daily <- subset(data_daily, date > "2022-12-01" & date < "2023-05-01")
```

Snow depth plot:
```r
ggplot(data_daily, aes(x = date, y = snow.depth, fill = name)) +
  geom_bar(stat = "identity") + facet_wrap(~name)
```

Color by temperature:
```r
ggplot(data_daily, aes(x = date, y = snow.depth, color = max.temperature)) +
  geom_point() + facet_wrap(~name)
```

Change color scheme:
```r
ggplot(data_daily, aes(x = date, y = snow.depth, color = max.temperature)) +
  geom_point() + facet_wrap(~name) + scale_color_viridis_c(option="plasma")
```

## Themes

```r
# dark theme
theme_set(theme_dark())
```

Other themes:
- `theme_classic()`
- `theme_minimal()`
- `theme_bw()`

## Exercise: Anscombe's quartet

```r
data <- read.csv("example.csv")

ggplot(data, aes(x=x, y=y, color=dataset)) +
  geom_point() + facet_wrap(~dataset)
```

---

:::{keypoints}
- Browse example galleries for inspiration.
- Minimize manual post-processing.
- CSV files are good for storing data for visualization.
- Load data into R dataframes and plot using ggplot2.
::: 


