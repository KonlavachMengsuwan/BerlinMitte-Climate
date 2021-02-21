---
title: "BerlinMitte-Climate"
output: html_notebook
---

# Berlin Mitte Daily Precipitation and Mean Temperature
## Data source: <https://www.ecad.eu/dailydata/index.php>

## Load ggplot2 package for visualization
```{r}
library(ggplot2)
```

## Read text file
```{r}
## Make first line as header of table
## Separate by ,
## Skip first 18 lines
## Clean missing value
temperature <- read.csv("Mean-Temperature/TG_STAID004563.txt", header = TRUE, sep = ",", skip = 18, na.strings = c("NA", " ", "-9999"))
```

## Display structure of the object
```{r}
str(temperature)
```

## Check the first few lines of dataframe
```{r}
head(temperature)
```

## Date Conversion from interger
```{r}
temperature$DATE = as.Date(as.character(temperature$DATE), format='%Y%m%d')

class(temperature$DATE)
# "Date"

head(temperature)
```
## Quick plot
```{r}
qplot(x = temperature$DATE,
      y = temperature$TG)
```

## Mean temperature from data = 0.1 * TG
```{r}
temperature$TG = temperature$TG * 0.1

# From "integer" to "numeric" class
class(temperature$TG)
# "numberic"

qplot(x = temperature$DATE,
      y = temperature$TG)

```
## Data start from
```{r}
min(temperature$DATE)
```
## Data end on
```{r}
max(temperature$DATE)
```

# Replicate data from year 2020
```{r}
temperature_2020 = temperature[temperature$DATE >= "2020-01-01" & temperature$DATE <= "2020-12-31",]

qplot(x = temperature_2020$DATE,
      y = temperature_2020$TG)

```






