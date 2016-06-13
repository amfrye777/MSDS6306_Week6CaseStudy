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

The Data utilized for this study is sourced from data.worldbank.org
(specific file download links to be provided below). The below sections
will walk through loading the data and verifying that the data values
match the original research files.

### Products Data Load

The Gross Domestic Product data for the 190 ranked countries are are
found
[here](https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv).

**Data Notes**

*"Year to year changes in the nominal level of output or income of an
economy are affected by a combination of forces: real growth, price
inflation, and exchange rates. Changes in any of the three can affect an
economy's relative size and, therefore, its ranking in comparison to
other economies. Of the rankings presented here, nominal GDP, perhaps
the most familiar measure of aggregate economic activity, is most
subject to price and exchange rate effects. Rankings are based on
available data only."*
[http://data.worldbank.org](http://data.worldbank.org/data-catalog/GDP-ranking-table)

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

    ## [1] "Education.csv"     "LoadEducation.RMD" "LoadProduct.RMD"  
    ## [4] "Products.csv"

If the File's Data SHA1 HASH value does not match original research,
lets re-load it.

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

Lets review the first 10 and last 100 records of this file:

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

    formattable(tail(ProductsRaw,100))

<table style="width:279%;">
<colgroup>
<col width="6%" />
<col width="6%" />
<col width="175%" />
<col width="5%" />
<col width="38%" />
<col width="16%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="5%" />
<col width="6%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
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
<td align="left">232</td>
<td align="right">MNA</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">Middle East &amp; North Africa</td>
<td align="right">1,540,807</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="left">233</td>
<td align="right">SAS</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">South Asia</td>
<td align="right">2,286,093</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="odd">
<td align="left">234</td>
<td align="right">SSA</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">1,289,813</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="left">235</td>
<td align="right">HIC</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">High income</td>
<td align="right">49,717,634</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="odd">
<td align="left">236</td>
<td align="right">EMU</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">Euro area</td>
<td align="right">12,192,344</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
</tr>
<tr class="even">
<td align="left">237</td>
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
<td align="left">238</td>
<td align="right"></td>
<td align="right">.. Not available.</td>
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
<td align="left">239</td>
<td align="right"></td>
<td align="right">Note: Rankings include only those economies with confirmed GDP estimates. Figures in italics are for 2011 or 2010.</td>
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
<td align="left">240</td>
<td align="right"></td>
<td align="right">a. Includes Former Spanish Sahara. b. Excludes South Sudan c. Covers mainland Tanzania only. d. Data are for the area</td>
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
<td align="left">241</td>
<td align="right"></td>
<td align="right">controlled by the government of the Republic of Cyprus. e. Excludes Abkhazia and South Ossetia. f. Excludes Transnistria.</td>
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
<td align="left">242</td>
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
<td align="left">243</td>
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
<td align="left">244</td>
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
<td align="left">245</td>
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
<td align="left">246</td>
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
<td align="left">247</td>
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
<td align="left">248</td>
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
<td align="left">249</td>
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
<td align="left">250</td>
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
<td align="left">251</td>
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
<td align="left">252</td>
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
<td align="left">253</td>
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
<td align="left">254</td>
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
<td align="left">255</td>
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
<td align="left">256</td>
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
<td align="left">257</td>
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
<td align="left">258</td>
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
<td align="left">259</td>
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
<td align="left">260</td>
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
<td align="left">261</td>
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
<td align="left">262</td>
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
<td align="left">263</td>
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
<td align="left">264</td>
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
<td align="left">265</td>
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
<td align="left">266</td>
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
<td align="left">267</td>
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
<td align="left">268</td>
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
<td align="left">269</td>
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
<td align="left">270</td>
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
<td align="left">271</td>
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
<td align="left">272</td>
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
<td align="left">273</td>
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
<td align="left">274</td>
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
<td align="left">275</td>
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
<td align="left">276</td>
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
<td align="left">277</td>
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
<td align="left">278</td>
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
<td align="left">279</td>
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
<td align="left">280</td>
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
<td align="left">281</td>
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
<td align="left">282</td>
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
<td align="left">283</td>
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
<td align="left">284</td>
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
<td align="left">285</td>
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
<td align="left">286</td>
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
<td align="left">287</td>
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
<td align="left">288</td>
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
<td align="left">289</td>
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
<td align="left">290</td>
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
<td align="left">291</td>
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
<td align="left">292</td>
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
<td align="left">293</td>
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
<td align="left">294</td>
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
<td align="left">295</td>
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
<td align="left">296</td>
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
<td align="left">297</td>
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
<td align="left">298</td>
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
<td align="left">299</td>
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
<td align="left">300</td>
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
<td align="left">301</td>
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
<td align="left">302</td>
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
<td align="left">303</td>
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
<td align="left">304</td>
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
<td align="left">305</td>
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
<td align="left">306</td>
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
<td align="left">307</td>
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
<td align="left">308</td>
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
<td align="left">309</td>
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
<td align="left">310</td>
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
<td align="left">311</td>
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
<td align="left">312</td>
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
<td align="left">313</td>
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
<td align="left">314</td>
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
<td align="left">315</td>
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
<td align="left">316</td>
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
<td align="left">317</td>
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
<td align="left">318</td>
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
<td align="left">319</td>
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
<td align="left">320</td>
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
<td align="left">321</td>
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
<td align="left">322</td>
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
<td align="left">323</td>
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
<td align="left">324</td>
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
<td align="left">325</td>
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
<td align="left">326</td>
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
<td align="left">327</td>
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
<td align="left">328</td>
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
<td align="left">329</td>
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
<td align="left">330</td>
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
<td align="left">331</td>
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
</tbody>
</table>

### Education Data Load

The Education data are are found
[here](https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv).

**Data Notes**

*"The World Bank EdStats All Indicator Query holds around 3,000
internationally comparable indicators that describe education access,
progression, completion, literacy, teachers, population, and
expenditures. The indicators cover the education cycle from pre-primary
to vocational and tertiary education."*
[Data.worldbank.org](http://data.worldbank.org/data-catalog/ed-stats)

Lets load this data from it's source if you do not already have this
data file in the DataLoad Directory.

    setwd(DataLoad)

    ##Only download the file fresh if the file does not exist
    if (file.exists("Education.csv") ==FALSE) {
      ## Download CSV File
      url <-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv"
      download(url, destfile = "Education.csv")
    }  

    #Verify file exists in DataLoad Directory
    list.files()

    ## [1] "Education.csv"     "LoadEducation.RMD" "LoadProduct.RMD"  
    ## [4] "Products.csv"

If the File's Data SHA1 HASH value does not match original research,
lets re-load it.

    ##Load Education.csv into EducationRaw data.frame
    EducationRaw <- read.csv("Education.csv",stringsAsFactors = FALSE,header = TRUE)

    ## Ensure that the Education.csv file's data sha1 HASH value matches that of original research
    ## Define Data SHA1 HASH
    SHAHASHEducation <- digest(EducationRaw, algo="sha1")
     
    ## If file's data does not match original research, download file fresh and check again
    if (SHAHASHEducation != "aa8a8e7da032757672d3522d645d89f128a98cb2") {
      url <-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv"
      download(url, destfile = "Education.csv")
      
      EducationRaw <- read.csv("Education.csv",stringsAsFactors = FALSE,header = TRUE)
      
      ## Define new Data SHA1 HASH
      SHAHASHEducation <- digest(EducationRaw, algo="sha1")
      
      ## If file's data still does not match, STOP BUILD WITH ERRORS
      if (SHAHASHEducation != "aa8a8e7da032757672d3522d645d89f128a98cb2") {

      stop("File SHA1 HASH Value does not match original research. Valid SHA1 HASH value of data = \"aa8a8e7da032757672d3522d645d89f128a98cb2\"")

      }
    }

Lets review the first and last 10 records of this file:

    formattable(head(EducationRaw,10))

<table style="width:1163%;">
<colgroup>
<col width="18%" />
<col width="41%" />
<col width="30%" />
<col width="38%" />
<col width="25%" />
<col width="19%" />
<col width="31%" />
<col width="36%" />
<col width="36%" />
<col width="106%" />
<col width="40%" />
<col width="47%" />
<col width="40%" />
<col width="29%" />
<col width="43%" />
<col width="23%" />
<col width="48%" />
<col width="44%" />
<col width="23%" />
<col width="43%" />
<col width="45%" />
<col width="70%" />
<col width="40%" />
<col width="38%" />
<col width="33%" />
<col width="26%" />
<col width="41%" />
<col width="20%" />
<col width="15%" />
<col width="30%" />
<col width="30%" />
</colgroup>
<thead>
<tr class="header">
<th align="right">CountryCode</th>
<th align="right">Long.Name</th>
<th align="right">Income.Group</th>
<th align="right">Region</th>
<th align="right">Lending.category</th>
<th align="right">Other.groups</th>
<th align="right">Currency.Unit</th>
<th align="right">Latest.population.census</th>
<th align="right">Latest.household.survey</th>
<th align="right">Special.Notes</th>
<th align="right">National.accounts.base.year</th>
<th align="right">National.accounts.reference.year</th>
<th align="right">System.of.National.Accounts</th>
<th align="right">SNA.price.valuation</th>
<th align="right">Alternative.conversion.factor</th>
<th align="right">PPP.survey.year</th>
<th align="right">Balance.of.Payments.Manual.in.use</th>
<th align="right">External.debt.Reporting.status</th>
<th align="right">System.of.trade</th>
<th align="right">Government.Accounting.concept</th>
<th align="right">IMF.data.dissemination.standard</th>
<th align="right">Source.of.most.recent.Income.and.expenditure.data</th>
<th align="right">Vital.registration.complete</th>
<th align="right">Latest.agricultural.census</th>
<th align="right">Latest.industrial.data</th>
<th align="right">Latest.trade.data</th>
<th align="right">Latest.water.withdrawal.data</th>
<th align="right">X2.alpha.code</th>
<th align="right">WB.2.code</th>
<th align="right">Table.Name</th>
<th align="right">Short.Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="right">ABW</td>
<td align="right">Aruba</td>
<td align="right">High income: nonOECD</td>
<td align="right">Latin America &amp; Caribbean</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Aruban florin</td>
<td align="right">2000</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1995</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Special</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">NA</td>
<td align="right">AW</td>
<td align="right">AW</td>
<td align="right">Aruba</td>
<td align="right">Aruba</td>
</tr>
<tr class="even">
<td align="right">ADO</td>
<td align="right">Principality of Andorra</td>
<td align="right">High income: nonOECD</td>
<td align="right">Europe &amp; Central Asia</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Euro</td>
<td align="right">Register based</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">General</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2006</td>
<td align="right">NA</td>
<td align="right">AD</td>
<td align="right">AD</td>
<td align="right">Andorra</td>
<td align="right">Andorra</td>
</tr>
<tr class="odd">
<td align="right">AFG</td>
<td align="right">Islamic State of Afghanistan</td>
<td align="right">Low income</td>
<td align="right">South Asia</td>
<td align="right">IDA</td>
<td align="right">HIPC</td>
<td align="right">Afghan afghani</td>
<td align="right">1979</td>
<td align="right">MICS, 2003</td>
<td align="right">Fiscal year end: March 20; reporting period for national accounts data: FY.</td>
<td align="right">2002/2003</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AF</td>
<td align="right">AF</td>
<td align="right">Afghanistan</td>
<td align="right">Afghanistan</td>
</tr>
<tr class="even">
<td align="right">AGO</td>
<td align="right">People's Republic of Angola</td>
<td align="right">Lower middle income</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">IDA</td>
<td align="right"></td>
<td align="right">Angolan kwanza</td>
<td align="right">1970</td>
<td align="right">MICS, 2001, MIS, 2006/07</td>
<td align="right"></td>
<td align="right">1997</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAP</td>
<td align="right">1991-96</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">Special</td>
<td align="right"></td>
<td align="right">GDDS</td>
<td align="right">IHS, 2000</td>
<td align="right"></td>
<td align="right">1964-65</td>
<td align="right">NA</td>
<td align="right">1991</td>
<td align="right">2000</td>
<td align="right">AO</td>
<td align="right">AO</td>
<td align="right">Angola</td>
<td align="right">Angola</td>
</tr>
<tr class="odd">
<td align="right">ALB</td>
<td align="right">Republic of Albania</td>
<td align="right">Upper middle income</td>
<td align="right">Europe &amp; Central Asia</td>
<td align="right">IBRD</td>
<td align="right"></td>
<td align="right">Albanian lek</td>
<td align="right">2001</td>
<td align="right">MICS, 2005</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1996</td>
<td align="right">1993</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right">LSMS, 2005</td>
<td align="right">Yes</td>
<td align="right">1998</td>
<td align="right">2005</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AL</td>
<td align="right">AL</td>
<td align="right">Albania</td>
<td align="right">Albania</td>
</tr>
<tr class="even">
<td align="right">ARE</td>
<td align="right">United Arab Emirates</td>
<td align="right">High income: nonOECD</td>
<td align="right">Middle East &amp; North Africa</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">U.A.E. dirham</td>
<td align="right">2005</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1995</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">BPM4</td>
<td align="right"></td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1998</td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">2005</td>
<td align="right">AE</td>
<td align="right">AE</td>
<td align="right">United Arab Emirates</td>
<td align="right">United Arab Emirates</td>
</tr>
<tr class="odd">
<td align="right">ARG</td>
<td align="right">Argentine Republic</td>
<td align="right">Upper middle income</td>
<td align="right">Latin America &amp; Caribbean</td>
<td align="right">IBRD</td>
<td align="right"></td>
<td align="right">Argentine peso</td>
<td align="right">2001</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1993</td>
<td align="right">NA</td>
<td align="right">1993</td>
<td align="right">VAB</td>
<td align="right">1971-84</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">Special</td>
<td align="right">Consolidated</td>
<td align="right">SDDS</td>
<td align="right">IHS, 2006</td>
<td align="right">Yes</td>
<td align="right">2002</td>
<td align="right">2001</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AR</td>
<td align="right">AR</td>
<td align="right">Argentina</td>
<td align="right">Argentina</td>
</tr>
<tr class="even">
<td align="right">ARM</td>
<td align="right">Republic of Armenia</td>
<td align="right">Lower middle income</td>
<td align="right">Europe &amp; Central Asia</td>
<td align="right">Blend</td>
<td align="right"></td>
<td align="right">Armenian dram</td>
<td align="right">2001</td>
<td align="right">DHS, 2005</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1996</td>
<td align="right">1993</td>
<td align="right">VAB</td>
<td align="right">1990-95</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">Special</td>
<td align="right">Consolidated</td>
<td align="right">SDDS</td>
<td align="right">IHS, 2007</td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AM</td>
<td align="right">AM</td>
<td align="right">Armenia</td>
<td align="right">Armenia</td>
</tr>
<tr class="odd">
<td align="right">ASM</td>
<td align="right">American Samoa</td>
<td align="right">Upper middle income</td>
<td align="right">East Asia &amp; Pacific</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">U.S. dollar</td>
<td align="right">2000</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">AS</td>
<td align="right">AS</td>
<td align="right">American Samoa</td>
<td align="right">American Samoa</td>
</tr>
<tr class="even">
<td align="right">ATG</td>
<td align="right">Antigua and Barbuda</td>
<td align="right">Upper middle income</td>
<td align="right">Latin America &amp; Caribbean</td>
<td align="right">IBRD</td>
<td align="right"></td>
<td align="right">East Caribbean dollar</td>
<td align="right">2001</td>
<td align="right"></td>
<td align="right">The government has revised national accounts data for 1998-2008.</td>
<td align="right">1990</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">BPM5</td>
<td align="right"></td>
<td align="right">General</td>
<td align="right"></td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2007</td>
<td align="right">1990</td>
<td align="right">AG</td>
<td align="right">AG</td>
<td align="right">Antigua and Barbuda</td>
<td align="right">Antigua and Barbuda</td>
</tr>
</tbody>
</table>

    formattable(tail(EducationRaw,10))

<table style="width:1163%;">
<colgroup>
<col width="6%" />
<col width="18%" />
<col width="47%" />
<col width="29%" />
<col width="38%" />
<col width="25%" />
<col width="19%" />
<col width="27%" />
<col width="36%" />
<col width="34%" />
<col width="106%" />
<col width="40%" />
<col width="47%" />
<col width="40%" />
<col width="29%" />
<col width="43%" />
<col width="23%" />
<col width="48%" />
<col width="44%" />
<col width="23%" />
<col width="43%" />
<col width="45%" />
<col width="70%" />
<col width="40%" />
<col width="38%" />
<col width="33%" />
<col width="26%" />
<col width="41%" />
<col width="20%" />
<col width="15%" />
<col width="27%" />
<col width="27%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="right">CountryCode</th>
<th align="right">Long.Name</th>
<th align="right">Income.Group</th>
<th align="right">Region</th>
<th align="right">Lending.category</th>
<th align="right">Other.groups</th>
<th align="right">Currency.Unit</th>
<th align="right">Latest.population.census</th>
<th align="right">Latest.household.survey</th>
<th align="right">Special.Notes</th>
<th align="right">National.accounts.base.year</th>
<th align="right">National.accounts.reference.year</th>
<th align="right">System.of.National.Accounts</th>
<th align="right">SNA.price.valuation</th>
<th align="right">Alternative.conversion.factor</th>
<th align="right">PPP.survey.year</th>
<th align="right">Balance.of.Payments.Manual.in.use</th>
<th align="right">External.debt.Reporting.status</th>
<th align="right">System.of.trade</th>
<th align="right">Government.Accounting.concept</th>
<th align="right">IMF.data.dissemination.standard</th>
<th align="right">Source.of.most.recent.Income.and.expenditure.data</th>
<th align="right">Vital.registration.complete</th>
<th align="right">Latest.agricultural.census</th>
<th align="right">Latest.industrial.data</th>
<th align="right">Latest.trade.data</th>
<th align="right">Latest.water.withdrawal.data</th>
<th align="right">X2.alpha.code</th>
<th align="right">WB.2.code</th>
<th align="right">Table.Name</th>
<th align="right">Short.Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">225</td>
<td align="right">VNM</td>
<td align="right">Socialist Republic of Vietnam</td>
<td align="right">Lower middle income</td>
<td align="right">East Asia &amp; Pacific</td>
<td align="right">Blend</td>
<td align="right"></td>
<td align="right">Vietnamese dong</td>
<td align="right">2009</td>
<td align="right">MICS, 2006</td>
<td align="right"></td>
<td align="right">1994</td>
<td align="right">NA</td>
<td align="right">1993</td>
<td align="right">VAP</td>
<td align="right">1991</td>
<td align="right">2005</td>
<td align="right">BPM4</td>
<td align="right">Estimate</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right">IHS, 2006</td>
<td align="right"></td>
<td align="right">2001</td>
<td align="right">1999</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">VN</td>
<td align="right">VN</td>
<td align="right">Vietnam</td>
<td align="right">Vietnam</td>
</tr>
<tr class="even">
<td align="left">226</td>
<td align="right">VUT</td>
<td align="right">Republic of Vanuatu</td>
<td align="right">Lower middle income</td>
<td align="right">East Asia &amp; Pacific</td>
<td align="right">IDA</td>
<td align="right"></td>
<td align="right">Vanuatu vatu</td>
<td align="right">2009</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1983</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAP</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">BPM5</td>
<td align="right">Estimate</td>
<td align="right"></td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2007</td>
<td align="right">NA</td>
<td align="right">VU</td>
<td align="right">VU</td>
<td align="right">Vanuatu</td>
<td align="right">Vanuatu</td>
</tr>
<tr class="odd">
<td align="left">227</td>
<td align="right">WBG</td>
<td align="right">West Bank and Gaza</td>
<td align="right">Lower middle income</td>
<td align="right">Middle East &amp; North Africa</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Israeli new shekel</td>
<td align="right">2007</td>
<td align="right">PAPFAM, 2006</td>
<td align="right"></td>
<td align="right">1997</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Budgetary</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1971</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">PS</td>
<td align="right">GZ</td>
<td align="right">West Bank and Gaza</td>
<td align="right">West Bank and Gaza</td>
</tr>
<tr class="even">
<td align="left">228</td>
<td align="right">WLD</td>
<td align="right">World</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">World aggregate.</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">World</td>
<td align="right">World</td>
</tr>
<tr class="odd">
<td align="left">229</td>
<td align="right">WSM</td>
<td align="right">Samoa</td>
<td align="right">Lower middle income</td>
<td align="right">East Asia &amp; Pacific</td>
<td align="right">IDA</td>
<td align="right"></td>
<td align="right">Samoan tala</td>
<td align="right">2006</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">2002</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">BPM5</td>
<td align="right">Preliminary</td>
<td align="right">General</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1999</td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">NA</td>
<td align="right">WS</td>
<td align="right">WS</td>
<td align="right">Samoa</td>
<td align="right">Samoa</td>
</tr>
<tr class="even">
<td align="left">230</td>
<td align="right">YEM</td>
<td align="right">Republic of Yemen</td>
<td align="right">Lower middle income</td>
<td align="right">Middle East &amp; North Africa</td>
<td align="right">IDA</td>
<td align="right"></td>
<td align="right">Yemeni rial</td>
<td align="right">2004</td>
<td align="right">MICS, 2006</td>
<td align="right"></td>
<td align="right">1990</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAP</td>
<td align="right">1990-96</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Budgetary</td>
<td align="right">GDDS</td>
<td align="right">ES/BS, 2005</td>
<td align="right"></td>
<td align="right">2002</td>
<td align="right">2005</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">YE</td>
<td align="right">RY</td>
<td align="right">Yemen, Rep.</td>
<td align="right">Yemen</td>
</tr>
<tr class="odd">
<td align="left">231</td>
<td align="right">ZAF</td>
<td align="right">Republic of South Africa</td>
<td align="right">Upper middle income</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">IBRD</td>
<td align="right"></td>
<td align="right">South African rand</td>
<td align="right">2001</td>
<td align="right">DHS, 2003</td>
<td align="right">Fiscal year end: March 31; reporting period for national accounts data: CY.</td>
<td align="right">2000</td>
<td align="right">NA</td>
<td align="right">1993</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Preliminary</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">SDDS</td>
<td align="right">ES/BS, 2000</td>
<td align="right"></td>
<td align="right">2000</td>
<td align="right">2005</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">ZA</td>
<td align="right">ZA</td>
<td align="right">South Africa</td>
<td align="right">South Africa</td>
</tr>
<tr class="even">
<td align="left">232</td>
<td align="right">ZAR</td>
<td align="right">Democratic Republic of the Congo</td>
<td align="right">Low income</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">IDA</td>
<td align="right">HIPC</td>
<td align="right">Congolese franc</td>
<td align="right">1984</td>
<td align="right">DHS 2007</td>
<td align="right"></td>
<td align="right">1987</td>
<td align="right">NA</td>
<td align="right">1993</td>
<td align="right">VAB</td>
<td align="right">1999-01</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Estimate</td>
<td align="right">Special</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right">1-2-3, 2005-06</td>
<td align="right"></td>
<td align="right">1990</td>
<td align="right">NA</td>
<td align="right">1986</td>
<td align="right">2000</td>
<td align="right">CD</td>
<td align="right">ZR</td>
<td align="right">Congo, Dem. Rep.</td>
<td align="right">Dem. Rep. Congo</td>
</tr>
<tr class="odd">
<td align="left">233</td>
<td align="right">ZMB</td>
<td align="right">Republic of Zambia</td>
<td align="right">Low income</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">IDA</td>
<td align="right">HIPC</td>
<td align="right">Zambian kwacha</td>
<td align="right">2000</td>
<td align="right">DHS, 2007</td>
<td align="right"></td>
<td align="right">1994</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right">1990-92</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Preliminary</td>
<td align="right">General</td>
<td align="right">Budgetary</td>
<td align="right">GDDS</td>
<td align="right">IHS, 2004-05</td>
<td align="right"></td>
<td align="right">1990</td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">ZM</td>
<td align="right">ZM</td>
<td align="right">Zambia</td>
<td align="right">Zambia</td>
</tr>
<tr class="even">
<td align="left">234</td>
<td align="right">ZWE</td>
<td align="right">Republic of Zimbabwe</td>
<td align="right">Low income</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">Blend</td>
<td align="right"></td>
<td align="right">Zimbabwe dollar</td>
<td align="right">2002</td>
<td align="right">DHS, 2005/06</td>
<td align="right">Fiscal year end: June 30; reporting period for national accounts data: CY.</td>
<td align="right">1990</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right">1991, 1998</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1960</td>
<td align="right">1995</td>
<td align="right">2008</td>
<td align="right">2002</td>
<td align="right">ZW</td>
<td align="right">ZW</td>
<td align="right">Zimbabwe</td>
<td align="right">Zimbabwe</td>
</tr>
</tbody>
</table>

Data Cleanup
============

Data cleanup is imperative to any data analysis. In our precursory view
into header/footer records, we can tell there are several items needing
to be cleaned across the two datasets. The following sections will walk
through cleaning the data to prep for analysis.

### Products Data Cleanup

When reviewing the Head/Tail records of the Raw product dataset, we see
that the first 5 records are not relevant for analysis, and there are
several NA or Blank values for CountryCode/Rankings and other NA
columns. Lets remove all invalid records, invalid columns, and declare
our column headers.

    ## Find and remove records with blank values for countrycode or Ranking (V1,V2)
    sum(!complete.cases(ProductsRaw))

    ## [1] 331

    nrow(ProductsRaw[ProductsRaw$V1=='' | ProductsRaw$V2=='' ,c(1,2,4,5,6)])

    ## [1] 141

    Products<-ProductsRaw[ProductsRaw$V1!='' & ProductsRaw$V2!='' ,c(1,2,4,5,6)]
    sum(!complete.cases(Products))

    ## [1] 0

    ## Define Variable Names
    names(Products)<-c("CountryCode", "Ranking", "Economy","USDollars", "Note")
    str(Products)

    ## 'data.frame':    190 obs. of  5 variables:
    ##  $ CountryCode: chr  "USA" "CHN" "JPN" "DEU" ...
    ##  $ Ranking    : chr  "1" "2" "3" "4" ...
    ##  $ Economy    : chr  "United States" "China" "Japan" "Germany" ...
    ##  $ USDollars  : chr  " 16,244,600 " " 8,227,103 " " 5,959,718 " " 3,428,131 " ...
    ##  $ Note       : chr  "" "" "" "" ...

With our blanks removed and columns trimmed, it is apparent that Note
values are simply letters. When looking at the tail of the original file
we see these Notes defined in the footer notes. Lets clean our dataset
to append these notes to the appropriate records.

    ##Append Notes
    Products$Note[Products$Note=="a"]<-"Includes Former Spanish Sahara."
    Products$Note[Products$Note=="b"]<-"Excludes South Sudan"
    Products$Note[Products$Note=="c"]<-"Covers mainland Tanzania only."
    Products$Note[Products$Note=="d"]<-"Data are for the area controlled by the government of the Republic of Cyprus."
    Products$Note[Products$Note=="e"]<-"Excludes Abkhazia and South Ossetia."
    Products$Note[Products$Note=="f"]<-"Excludes Transnistria."
    formattable(Products[Products$Note!="",])

<table style="width:176%;">
<colgroup>
<col width="6%" />
<col width="18%" />
<col width="12%" />
<col width="13%" />
<col width="15%" />
<col width="109%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="right">CountryCode</th>
<th align="right">Ranking</th>
<th align="right">Economy</th>
<th align="right">USDollars</th>
<th align="right">Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">67</td>
<td align="right">MAR</td>
<td align="right">62</td>
<td align="right">Morocco</td>
<td align="right">95,982</td>
<td align="right">Includes Former Spanish Sahara.</td>
</tr>
<tr class="even">
<td align="left">78</td>
<td align="right">SDN</td>
<td align="right">73</td>
<td align="right">Sudan</td>
<td align="right">58,769</td>
<td align="right">Excludes South Sudan</td>
</tr>
<tr class="odd">
<td align="left">100</td>
<td align="right">TZA</td>
<td align="right">95</td>
<td align="right">Tanzania</td>
<td align="right">28,242</td>
<td align="right">Covers mainland Tanzania only.</td>
</tr>
<tr class="even">
<td align="left">107</td>
<td align="right">CYP</td>
<td align="right">102</td>
<td align="right">Cyprus</td>
<td align="right">22,767</td>
<td align="right">Data are for the area controlled by the government of the Republic of Cyprus.</td>
</tr>
<tr class="odd">
<td align="left">119</td>
<td align="right">GEO</td>
<td align="right">114</td>
<td align="right">Georgia</td>
<td align="right">15,747</td>
<td align="right">Excludes Abkhazia and South Ossetia.</td>
</tr>
<tr class="even">
<td align="left">146</td>
<td align="right">MDA</td>
<td align="right">141</td>
<td align="right">Moldova</td>
<td align="right">7,253</td>
<td align="right">Excludes Transnistria.</td>
</tr>
</tbody>
</table>

Our USDollars and Ranking variables should be classified as an integer.
Lets remove the comma's and convert to a numberic value.

    #Remove commas and convert USDollars to Numeric
    Products$USDollars<-as.numeric(gsub(",","",Products$USDollars))

    #Convert Ranking to Numeric
    Products$Ranking<-as.numeric(Products$Ranking)

    str(Products)

    ## 'data.frame':    190 obs. of  5 variables:
    ##  $ CountryCode: chr  "USA" "CHN" "JPN" "DEU" ...
    ##  $ Ranking    : num  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Economy    : chr  "United States" "China" "Japan" "Germany" ...
    ##  $ USDollars  : num  16244600 8227103 5959718 3428131 2612878 ...
    ##  $ Note       : chr  "" "" "" "" ...

### Education Data Cleanup

Similar to our cleanup in the Product Data, lets search for and remove
any NA or Blank values found in CountryCode or Income.Group.

    ## Find and remove records with blank values for CountryCode or Income.Group
    nrow(EducationRaw[EducationRaw$CountryCode=='' | EducationRaw$Income.Group=='',])

    ## [1] 24

    Education<-EducationRaw[EducationRaw$CountryCode!='' & EducationRaw$Income.Group!='',]

Data Analysis & Questions
=========================

Now that we have Cleaned and Merged our data, we may begin our analysis.
Stakeholders have requested answers to 5 core questions:

### Question 1

#### Match the data based on the country shortcode. How many of the IDs match?

    ##Merge the Data
    Products_M_Education<-merge(Products,Education,by="CountryCode", all=TRUE)
    formattable(head(Products_M_Education))

<table style="width:1219%;">
<colgroup>
<col width="18%" />
<col width="12%" />
<col width="30%" />
<col width="15%" />
<col width="8%" />
<col width="41%" />
<col width="30%" />
<col width="38%" />
<col width="25%" />
<col width="19%" />
<col width="22%" />
<col width="36%" />
<col width="36%" />
<col width="106%" />
<col width="40%" />
<col width="47%" />
<col width="40%" />
<col width="29%" />
<col width="43%" />
<col width="23%" />
<col width="48%" />
<col width="44%" />
<col width="23%" />
<col width="43%" />
<col width="45%" />
<col width="70%" />
<col width="40%" />
<col width="38%" />
<col width="33%" />
<col width="26%" />
<col width="41%" />
<col width="20%" />
<col width="15%" />
<col width="30%" />
<col width="30%" />
</colgroup>
<thead>
<tr class="header">
<th align="right">CountryCode</th>
<th align="right">Ranking</th>
<th align="right">Economy</th>
<th align="right">USDollars</th>
<th align="right">Note</th>
<th align="right">Long.Name</th>
<th align="right">Income.Group</th>
<th align="right">Region</th>
<th align="right">Lending.category</th>
<th align="right">Other.groups</th>
<th align="right">Currency.Unit</th>
<th align="right">Latest.population.census</th>
<th align="right">Latest.household.survey</th>
<th align="right">Special.Notes</th>
<th align="right">National.accounts.base.year</th>
<th align="right">National.accounts.reference.year</th>
<th align="right">System.of.National.Accounts</th>
<th align="right">SNA.price.valuation</th>
<th align="right">Alternative.conversion.factor</th>
<th align="right">PPP.survey.year</th>
<th align="right">Balance.of.Payments.Manual.in.use</th>
<th align="right">External.debt.Reporting.status</th>
<th align="right">System.of.trade</th>
<th align="right">Government.Accounting.concept</th>
<th align="right">IMF.data.dissemination.standard</th>
<th align="right">Source.of.most.recent.Income.and.expenditure.data</th>
<th align="right">Vital.registration.complete</th>
<th align="right">Latest.agricultural.census</th>
<th align="right">Latest.industrial.data</th>
<th align="right">Latest.trade.data</th>
<th align="right">Latest.water.withdrawal.data</th>
<th align="right">X2.alpha.code</th>
<th align="right">WB.2.code</th>
<th align="right">Table.Name</th>
<th align="right">Short.Name</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="right">ABW</td>
<td align="right">161</td>
<td align="right">Aruba</td>
<td align="right">2584</td>
<td align="right"></td>
<td align="right">Aruba</td>
<td align="right">High income: nonOECD</td>
<td align="right">Latin America &amp; Caribbean</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Aruban florin</td>
<td align="right">2000</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1995</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Special</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">NA</td>
<td align="right">AW</td>
<td align="right">AW</td>
<td align="right">Aruba</td>
<td align="right">Aruba</td>
</tr>
<tr class="even">
<td align="right">ADO</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">Principality of Andorra</td>
<td align="right">High income: nonOECD</td>
<td align="right">Europe &amp; Central Asia</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Euro</td>
<td align="right">Register based</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">General</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2006</td>
<td align="right">NA</td>
<td align="right">AD</td>
<td align="right">AD</td>
<td align="right">Andorra</td>
<td align="right">Andorra</td>
</tr>
<tr class="odd">
<td align="right">AFG</td>
<td align="right">105</td>
<td align="right">Afghanistan</td>
<td align="right">20497</td>
<td align="right"></td>
<td align="right">Islamic State of Afghanistan</td>
<td align="right">Low income</td>
<td align="right">South Asia</td>
<td align="right">IDA</td>
<td align="right">HIPC</td>
<td align="right">Afghan afghani</td>
<td align="right">1979</td>
<td align="right">MICS, 2003</td>
<td align="right">Fiscal year end: March 20; reporting period for national accounts data: FY.</td>
<td align="right">2002/2003</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right"></td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AF</td>
<td align="right">AF</td>
<td align="right">Afghanistan</td>
<td align="right">Afghanistan</td>
</tr>
<tr class="even">
<td align="right">AGO</td>
<td align="right">60</td>
<td align="right">Angola</td>
<td align="right">114147</td>
<td align="right"></td>
<td align="right">People's Republic of Angola</td>
<td align="right">Lower middle income</td>
<td align="right">Sub-Saharan Africa</td>
<td align="right">IDA</td>
<td align="right"></td>
<td align="right">Angolan kwanza</td>
<td align="right">1970</td>
<td align="right">MICS, 2001, MIS, 2006/07</td>
<td align="right"></td>
<td align="right">1997</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAP</td>
<td align="right">1991-96</td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">Special</td>
<td align="right"></td>
<td align="right">GDDS</td>
<td align="right">IHS, 2000</td>
<td align="right"></td>
<td align="right">1964-65</td>
<td align="right">NA</td>
<td align="right">1991</td>
<td align="right">2000</td>
<td align="right">AO</td>
<td align="right">AO</td>
<td align="right">Angola</td>
<td align="right">Angola</td>
</tr>
<tr class="odd">
<td align="right">ALB</td>
<td align="right">125</td>
<td align="right">Albania</td>
<td align="right">12648</td>
<td align="right"></td>
<td align="right">Republic of Albania</td>
<td align="right">Upper middle income</td>
<td align="right">Europe &amp; Central Asia</td>
<td align="right">IBRD</td>
<td align="right"></td>
<td align="right">Albanian lek</td>
<td align="right">2001</td>
<td align="right">MICS, 2005</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1996</td>
<td align="right">1993</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">2005</td>
<td align="right">BPM5</td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right">LSMS, 2005</td>
<td align="right">Yes</td>
<td align="right">1998</td>
<td align="right">2005</td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AL</td>
<td align="right">AL</td>
<td align="right">Albania</td>
<td align="right">Albania</td>
</tr>
<tr class="even">
<td align="right">ARE</td>
<td align="right">32</td>
<td align="right">United Arab Emirates</td>
<td align="right">348595</td>
<td align="right"></td>
<td align="right">United Arab Emirates</td>
<td align="right">High income: nonOECD</td>
<td align="right">Middle East &amp; North Africa</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">U.A.E. dirham</td>
<td align="right">2005</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1995</td>
<td align="right">NA</td>
<td align="right">NA</td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right">NA</td>
<td align="right">BPM4</td>
<td align="right"></td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1998</td>
<td align="right">NA</td>
<td align="right">2008</td>
<td align="right">2005</td>
<td align="right">AE</td>
<td align="right">AE</td>
<td align="right">United Arab Emirates</td>
<td align="right">United Arab Emirates</td>
</tr>
</tbody>
</table>

    ##How Many Records Did Not Match?
    nrow(Products_M_Education[Products_M_Education$Ranking=='' | Products_M_Education$Income.Group=='' | is.na(Products_M_Education$Ranking)==TRUE | is.na(Products_M_Education$Income.Group)==TRUE,])

    ## [1] 22

    ##How Many Records Do Match?
    nrow(Products_M_Education[Products_M_Education$Ranking!='' & Products_M_Education$Income.Group!='' & is.na(Products_M_Education$Ranking)==FALSE & is.na(Products_M_Education$Income.Group)==FALSE,])

    ## [1] 189

    ##Remove non-Matches from Dataset
    Products_M_Education<-Products_M_Education[Products_M_Education$Ranking!='' & Products_M_Education$Income.Group!='' & is.na(Products_M_Education$Ranking)==FALSE & is.na(Products_M_Education$Income.Group)==FALSE,]

After Merging the data, we find 22 records which did not match on
CountryCode. If we remove the non-matches from the dataset, we are left
with 189 records which Merged successfully.

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
