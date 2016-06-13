Introduction
============

TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT

### Required Packages

This RMD requires the following R packages to run: \* downloader \*
digest \* formattable

If you do not currently have installed any of these packages, please
uncomment the install.packages lines below before knitting this file.

    #install.packages("downloader")
    #install.packages("digest")
    #install.packages("formattable")

    library(downloader)
    library(digest)
    library(formattable)

Data Load
=========

TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT

### Products Data Load

### Load the Product Data File

The Gross Domestic Product data for the 190 ranked countries are are
found
[here](https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv).
Lets load this data from it's source if you do not already have this
data file in the DataLoad Directory.

    setwd(DataLoad)

    ##Only download the file fresh if the file does not exist
    if (file.exists("Products.csv") ==FALSE) {
      ## Download CSV File
      url <-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"
      download(url, destfile = "Products.csv")
    }  

    #Verify file exists in DataLoad Directory
    list.files()

    ## [1] "LoadEducation.RMD" "LoadProduct.RMD"   "Products.csv"

    ##Load Products.csv into ProductsRaw data.frame
    ProductsRaw <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    ## Ensure that the Products.csv file's data sha1 HASH value matches that of original research
    ## Define Data SHA1 HASH
    SHAHASHProduct <- digest(ProductsRaw, algo="sha1")
      
    ## If file's data does not match original research, download file fresh and check again
    if (SHAHASHProduct != "e6521fbc90c5a0991db48091c0d1967bbc856095") {
      url <-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"
      download(url, destfile = "Products.csv")
      
      ProductsRaw <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)
      
      ## Define new Data SHA1 HASH
      SHAHASHProduct <- digest(ProductsRaw, algo="sha1")
      
      ## If file's data still does not match, STOP BUILD WITH ERRORS
      if (SHAHASHProduct != "e6521fbc90c5a0991db48091c0d1967bbc856095") {

      stop("File SHA1 HASH Value does not match original research. Valid SHA1 HASH value of data = \"e6521fbc90c5a0991db48091c0d1967bbc856095\"")

      }
    }

    formattable(head(ProductsRaw,10))

<table style="width:122%;">
<colgroup>
<col width="6%" />
<col width="40%" />
<col width="5%" />
<col width="20%" />
<col width="19%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="6%" />
</colgroup>
<thead>
<tr class="header">
<th align="right">V1</th>
<th align="right">V2</th>
<th align="right">V3</th>
<th align="right">V4</th>
<th align="right">V5</th>
<th align="right">V6</th>
<th align="right">V7</th>
<th align="right">V8</th>
<th align="right">V9</th>
<th align="right">V10</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="right"></td>
<td align="right">Gross domestic product 2012</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="odd">
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right">(millions of</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="right"></td>
<td align="right">Ranking</td>
<td align="right">NA</td>
<td align="right">Economy</td>
<td align="right">US dollars)</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="odd">
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="right">USA</td>
<td align="right">1</td>
<td align="right">NA</td>
<td align="right">United States</td>
<td align="right">16,244,600</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="odd">
<td align="right">CHN</td>
<td align="right">2</td>
<td align="right">NA</td>
<td align="right">China</td>
<td align="right">8,227,103</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="right">JPN</td>
<td align="right">3</td>
<td align="right">NA</td>
<td align="right">Japan</td>
<td align="right">5,959,718</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="odd">
<td align="right">DEU</td>
<td align="right">4</td>
<td align="right">NA</td>
<td align="right">Germany</td>
<td align="right">3,428,131</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="right">FRA</td>
<td align="right">5</td>
<td align="right">NA</td>
<td align="right">France</td>
<td align="right">2,612,878</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
</tbody>
</table>

### Education Data Load

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

Data Cleanup
============

TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT

### Products Data Cleanup

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "CleanEducation.RMD" "CleanProduct.RMD"   "Products.csv"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

### Education Data Cleanup

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "CleanEducation.RMD" "CleanProduct.RMD"   "Products.csv"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

Data Analysis & Questions
=========================

TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT

### Question 1

#### Match the data based on the country shortcode. How many of the IDs match?

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "Products.csv"  "Question1.RMD" "Question2.RMD" "Question3.RMD"
    ## [5] "Question4.RMD" "Question5.RMD"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

### Question 2

#### Sort the data frame in ascending order by GDP rank (so United States is last). What is the 13th country in the resulting data frame?

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "Products.csv"  "Question1.RMD" "Question2.RMD" "Question3.RMD"
    ## [5] "Question4.RMD" "Question5.RMD"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

### Question 3

#### 3 What are the average GDP rankings for the "High income: OECD" and "High income: nonOECD" groups?

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "Products.csv"  "Question1.RMD" "Question2.RMD" "Question3.RMD"
    ## [5] "Question4.RMD" "Question5.RMD"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

### Question 4

#### 4 Plot the GDP for all of the countries. Use ggplot2 to color your plot by Income Group.

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "Products.csv"  "Question1.RMD" "Question2.RMD" "Question3.RMD"
    ## [5] "Question4.RMD" "Question5.RMD"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

### Question 5

#### 5 Cut the GDP ranking into 5 separate quantile groups. Make a table versus Income.Group. How many countries are Lower middle income but among the 38 nations with highest GDP?

    library("downloader")

    ## Load CSV File
    url<-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"

    download(url,destfile="Products.csv")

    list.files()

    ## [1] "Products.csv"  "Question1.RMD" "Question2.RMD" "Question3.RMD"
    ## [5] "Question4.RMD" "Question5.RMD"

    Products <- read.csv("Products.csv",stringsAsFactors = FALSE,header = FALSE)

    head(Products)

    ##    V1                          V2 V3            V4           V5 V6 V7 V8
    ## 1     Gross domestic product 2012 NA                               NA NA
    ## 2                                 NA                               NA NA
    ## 3                                 NA               (millions of    NA NA
    ## 4                         Ranking NA       Economy  US dollars)    NA NA
    ## 5                                 NA                               NA NA
    ## 6 USA                           1 NA United States  16,244,600     NA NA
    ##   V9 V10
    ## 1 NA  NA
    ## 2 NA  NA
    ## 3 NA  NA
    ## 4 NA  NA
    ## 5 NA  NA
    ## 6 NA  NA

Conclusion
==========

TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT TEXT
TEXT TEXT TEXT TEXT TEXT TEXT
