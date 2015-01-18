# Introduction to R
Ruhil  
January 14, 2015  

# Introduction to Basic Operations in R 

```r
x = 10 
x <- 10 # Note `=' is no different from `<-' 

x <- c(1,2,3,4,5,6)

y <- c(6,5,4,3,2,1)

z <- x * y

V <- cbind(x,y,z)

Vr <- rbind(x,y,z)

pi
```

```
## [1] 3.141593
```

```r
exp(1)
```

```
## [1] 2.718282
```

```r
log10(10)
```

```
## [1] 1
```

```r
s <- seq(10)
print(s)
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
s
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
s <- seq(20, 0, by=-2); s
```

```
##  [1] 20 18 16 14 12 10  8  6  4  2  0
```

```r
objects()
```

```
## [1] "s"  "V"  "Vr" "x"  "y"  "z"
```

```r
rm(s)
rm(x,y)
```

# Working Directory

getwd()
setwd("/Volumes/Storage/iClound Storage/Dropbox/Ruhil/PBIO 3150_5150/Data/Archive/")


# Importing data in Different Formats
ImportDataTAB <- read.table(file="ImportDataTab.txt", header=TRUE, sep="\t")

ImportDataCSV <- read.csv(file="ImportDataCSV.csv", header=TRUE, sep=",")

install.packages("xlsx")
library(xlsx)
ImportDataXLSX <- read.xlsx(file="ImportDataXLSX.xlsx", 1)

install.packages("sas7bdat")
library(sas7bdat)
ImportDataSAS <- read.sas7bdat(file="ImportDataSAS.sas7bdat")

install.packages("Hmisc")
library(Hmisc)
ImportDataSPSS <- spss.get(file="ImportDataSPSS.sav")

install.packages("foreign")
library(foreign)
ImportDataStata <- read.dta(file="ImportDataStata.dta")

# Checking Data Structure, etc.
data(trees)
str(trees)
summary(trees)
help(trees)

# An Example of Data Scraped from the Web ##
install.packages("XML")
library(XML)

theurl <- "http://elections.nytimes.com/2010/results/senate/big-board"
tables <- readHTMLTable(theurl)
n.rows <- unlist(lapply(tables, function(t) dim(t)[1]))
#This combines all but the first table
Elections <- do.call(rbind, tables[-1])
cleanElections <- cbind(Elections[1], sapply(Elections[-1], function(xx) as.numeric(gsub('[^0-9]', '', xx))))
rownames(cleanElections) <- 1:nrow(cleanElections)


# What else can R do? 
### Example 1 -- Simple yet Elegant Plots
hist(trees$Girth)
hist(trees$Girth, col="lightblue", xlab="Girth", main="Histogram of Girth")

### Better Graphics
library(ggplot2)
ggplot(trees, aes(Girth)) + geom_histogram(binwidth=2, fill="lightblue")


# Simple Random Sampling
 sample(trees$Height, 6, replace=TRUE)
 trees.sampled.1 = trees[sample(nrow(trees), 10, replace=TRUE), ] 
 trees.sampled.2 = trees[sample(nrow(trees), 10, replace=FALSE), ]


help.start() # Help on Basic R stuff
vignette() # Show available package vignettes
vignette("MatchIt") # Show vignette for ggplot2
data() # Show datasets preloaded in base R packages
data(package = .packages(all.available = TRUE)) # Show datasets preloaded in packages




