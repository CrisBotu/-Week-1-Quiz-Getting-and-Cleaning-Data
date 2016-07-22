# -Week-1-Quiz-Getting-and-Cleaning-Data

1. 
The American Community Survey distributes downloadable data about United States communities. Download the 2006 microdata survey about housing for the state of Idaho using download.file() from here:

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv

and load the data into R. The code book, describing the variable names is here:

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FPUMSDataDict06.pdf

How many properties are worth $1,000,000 or more?

164

31

53

47

Code:
##In the directory create a folder with the data container
setwd("D:/Documentos/Coursera/Data Science/3.Getting and Cleaning Data/Week1")
> if (!file.exists("data")) {
        dir.create("data")
}
> URL<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv"
> download.file(URL,destfile = "./data/06hid.csv")
> sum(!is.na(dataQuestion1$VAL) & dataQuestion1$VAL==24)
##[1] 53
---
2. 
Use the data you loaded from Question 1. Consider the variable FES in the code book. Which of the "tidy data" principles does this variable violate?

Tidy data has one observation per row.
Each variable in a tidy data set has been transformed to be interpretable.
Each tidy data table contains information about only one type of observation.
Tidy data has one variable per column.

·The answer is: Tidy data has one variable per column… FES has: gender, marital status and empoloyement status.
---
3. 
Download the Excel spreadsheet on Natural Gas Aquisition Program here:

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FDATA.gov_NGAP.xlsx

Read rows 18-23 and columns 7-15 into R and assign the result to a variable called:



1| dat

What is the value of:


1|sum(dat$Zip*dat$Ext,na.rm=T)
(original data source: http://catalog.data.gov/dataset/natural-gas-acquisition-program)

NA
36534720
154339
0

> fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FDATA.gov_NGAP.xlsx"
> library(xlsx)
Loading required package: rJava
Loading required package: xlsxjars
> rowIndex = 18 : 23
> colIndex = 7 : 15
> download.file(URL,destfile = "./data/gas.xlsx", mode="wb")
> dat <- read.xlsx("./data/gas.xlsx",sheetIndex = 1, rowIndex = rowIndex,colIndex = colIndex, header = TRUE)
> sum(dat$Zip * dat$Ext, na.rm=T)
##[1] 36534720
---
4. 
Read the XML data on Baltimore restaurants from here:

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml

How many restaurants have zipcode 21231?

28
130
127
100

> URL <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml"
> library(XML)
> doc <- xmlTreeParse("./data/restaurants.xml", useInternal = TRUE)
> rootNode <- xmlRoot(doc)
> sum(xpathSApply(rootNode, "//zipcode", xmlValue) == "21231")
##[1] 127
---
5. 
The American Community Survey distributes downloadable data about United States communities. Download the 2006 microdata survey about housing for the state of Idaho using download.file() from here:

https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06pid.csv

using the fread() command load the data into an R object


1|DT
The following are ways to calculate the average value of the variable


1|pwgtp15
broken down by sex. Using the data.table package, which will deliver the fastest user time?

tapply(DT$pwgtp15,DT$SEX,mean)
mean(DT[DT$SEX==1,]$pwgtp15); mean(DT[DT$SEX==2,]$pwgtp15)
mean(DT$pwgtp15,by=DT$SEX)
rowMeans(DT)[DT$SEX==1]; rowMeans(DT)[DT$SEX==2]
DT[,mean(pwgtp15),by=SEX]
sapply(split(DT$pwgtp15,DT$SEX),mean)

> URL <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06pid.csv"
> download.file(URL,destfile = "./data/06pid.csv")
