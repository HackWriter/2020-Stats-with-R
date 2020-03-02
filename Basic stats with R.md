First, set your working directory. 
setwd("FILE PATH HERE")

```setwd("~/IRE_NICAR/NOLA_2020")```

Or you can use the drop-down menu: Session -> Set Working Directory -> Choose Directory

Make sure these four packages are installed and loaded: dplyr, tidyverse, ggplot2 and psych
install.packages("package_name")
library(package_name)

```
library(dplyr)
library(tidyverse)
library(ggplot2)
library(psych)
```

We'll work with three data sets:
nba.csv -- NBA player stats
nfl.csv -- NFL team stats
txmiddle.csv -- Test scores for Texas middle schools 
Bring the .csv files into R. They all have field names, so we include this: col_names = TRUE
newfilename <- read_csv('csv file name', col_names = TRUE)

nba <- read_csv('nba.csv', col_names = TRUE)
nfl <- read_csv('nfl.csv', col_names = TRUE)
txschools <- read_csv('txmiddle.csv', col_names = TRUE)

Tip: Avoid column names that contain spaces. Go with 'field_name' not 'field name'

Let's start with the NBA file. To see how a file is structured, type
str(filename)
```
str(nba)
```
We have 509 cases and six variables.
The first two fields - player and team - are characters, while the other four are numeric.

Let's get some basic statistics from our data - averages, standard deviations, etc. 
The 'psych' package we loaded has a handy function called 'describe'. 
describe(filename)
```
describe(nba)
```
The first two fields are strings, so R can't run statistics on them.

But check out the last four. The average age of NBA players, for instance, is 25-1/2. They range from 19 to 43 years old.
The sd (standard deviation) of 4 means about two-thirds of players fall within 4 years of the average age.
That is, about two-third of players range from 21-1/2 to 29-1/2 years old.

You can also get a single statistic for a single variable.
measure(filename$fieldname)
```
mean(nba$height)
```
The average height for players is 78.3 inches. What about the heaviest player?
```
max(nba$weight)
```
Uh oh, we get "NA" because a couple of players have missing values. In that case, we tell R to remove the NAs by adding 'na.rm = TRUE'
```
max(nba$weight, na.rm = TRUE)
```
The heaviest player weights 311 pounds.

