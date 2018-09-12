---
title: 'R-package'
author: ''
date: '2018-09-11'
slug: r-package
categories: []
tags: []
weight: 10
---

{{% notice warning %}}
<i class="far fa-calendar-alt"></i> Competition from ... (included) to ... (included).   
<i class="fas fa-atlas"></i> Report due for ....   
<i class="far fa-clock"></i> Remember to forecast at least **one day before** the date 
for which the forecast is intended, **before 11pm at the latest**.   
<i class="far fa-comments"></i> Send your forecast before 8pm to receive 
feedback information.   
<i class='fa fa-fw fa-users'></i> Use our [discussion forum](https://piazza.com/unil.ch/fall2018/fc2018/home)
for questions related to methods, implementations and potential bugs.   
{{% /notice %}}

### Objectives

The goal of this competition is to forecast the number of times a R-package 
will be downloaded via [CRAN](https://cran.r-project.org/) (one of the major
repository for R packages). We are interested in particular with
the `fpp2` package.

The accuracy of the forecasts is measured by the mean squared error:
$$(x_t - \hat{x}_t)^2$$

The final points are attributed according to:
...

The objectives of this case study are the followings:   

- Learn to forecast with **exponential smoothing** and **ARIMA** models.   
- Experience forecasting situation dynamically on day-to-day data.   
- Deal with outliers and missing values.   
- Work and progress in groups.  
- Write a succint scientific report.   
- Have fun while learning.   

### Data
The number of downloads of packages on CRAN are easily obtained using the `cranlogs` package.
To install it, you simply need to install the package of the course,
the `cranlogs` package will be automatically installed.
Otherwise, you can follow this example:   

```{toml}
# if not installed, install the package of the course
devtools::install_github("SMAC-Group/fc2018")

# install the cranlogs package
devtools::install_github("metacran/cranlogs")
```

You can check the GitHub [page](https://github.com/metacran/cranlogs) of
this package for more information and examples. Here are some examples:

```{toml}
# the total number of downloads of all packages from last week
cran_downloads(when = "last-week")

# the total number of downloads of all packages for a specific window of time
cran_downloads(from = "2017-08-01", to = "2018-08-01")

# the total number of downloads of `ggplot2` for a specific window of time
cran_downloads(from = "2018-07-01", to = "2018-08-01", packages = "ggplot2")
```
### fpp2 package
Let's turn our attention to the `fpp2` package that we will forecast.

If you check the package's [archives](https://cran.r-project.org/src/contrib/Archive/fpp2/),
you can realize it was created on the 23rd of February 2017, so it is useless 
to retrieve data before. Let's obtain the data up to today (12th of September 2018)
and plot it:

```{toml}
fpp2 <- cran_downloads(packages = "fpp2", from = "2017-02-23", to = "2018-09-12")

# plot the time series
ggplot(fpp2, aes(x = date, y = count)) +
  geom_line() + xlab("Dates") + ylab("Number of downloads on CRAN") + 
  ggtitle("Number of downloads of 'fpp2'")
```
<img src="https://raw.githubusercontent.com/SMAC-Group/fc2018_website/master/data/fpp2_1.png" alt="fpp21" width="300px"/> 

You can notice peeks and zeros appearing. These questions will be addressed in a future
lecture.