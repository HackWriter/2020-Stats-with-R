### GETTING STARTED

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
- nba.csv -- NBA player stats
- nfl.csv -- NFL team stats
- txmiddle.csv -- Test scores for Texas middle schools 

Bring the .csv files into R. They all have field names, so we include this: col_names = TRUE
newfilename <- read_csv('csv file name', col_names = TRUE)
```
nba <- read_csv('nba.csv', col_names = TRUE)
nfl <- read_csv('nfl.csv', col_names = TRUE)
txschools <- read_csv('txmiddle.csv', col_names = TRUE)
```
Tip: Avoid column names that contain spaces. Go with 'field_name' not 'field name'

Let's start with the NBA file. To see how a file is structured, type
str(filename)
```
str(nba)
```
We have 509 cases and six variables.
The first two fields - player and team - are characters, while the other four are numeric.

### DESCRIPTIVES: MIN, MAX, AVERAGE, ETC.
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

### MAKE COMPARISONS: Z-scores

Sometimes we want to compare things on the same scale. 
For instance, Tacko Fall is the tallest AND heaviest player in our data.
But is he taller than he is heavy? 

That's where Z-scores come in. Z-scores tell you how far from the average a certain data point - or NBA player - is.
It's expressed as a standard deviation.

Calculate the Z-score for one variable
scale(filename$fieldname)
```
scale(nba$height)
```
Tacko Fall is row 445 in our data. His Z-score, or standardized score, is 3.02. 
That means his height is 3.02 standard deviations above the average height of 78.3 inches. 
Now get his standardized weight.
```
scale(nba$weight)
```
Tacko's weight is 3.88 standard deviations above the average weight of 217.3 pounds.
So he's heavier (3.88) than he is tall (3.02)

What if you want Z-scores for all variables? scale() works only on numeric data.

In our files, that's columns 3 through 6. Put that range in brackets, like so:
```
scale(nba[3:6])
```
This time we don't see all cases. Let's save this as a new file (or dataframe in R speak)
```
znba <- scale(nba[3:6])
```
Let's combine those Z-scores with our original file so we have everything together.
Use a function called cbind, for column bind.

newfile <- cbind(file1, file2)
```
nba_joined <- cbind(nba, znba)

View(nba_joined)
```
