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
(specific file download links to be provided below). The below secions
will walk through loading the data and verifying that the data values
match the original research files.

### Products Data Load

The Gross Domestic Product data for the 190 ranked countries are are
found
[here](https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv).

\*\*Data <Notes:**>

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

Lets review the first 10 records of this file:

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

The Education data are are found
[here](https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv).

\*\*Data <Notes:**>

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
    EducationRaw <- read.csv("Education.csv",stringsAsFactors = FALSE,header = FALSE)

    ## Ensure that the Education.csv file's data sha1 HASH value matches that of original research
    ## Define Data SHA1 HASH
    SHAHASHEducation <- digest(EducationRaw, algo="sha1")
      
    ## If file's data does not match original research, download file fresh and check again
    if (SHAHASHEducation != "e62cde0a23e00d5882be1f5d9e76504f68b0efc8") {
      url <-"https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv"
      download(url, destfile = "Education.csv")
      
      EducationRaw <- read.csv("Education.csv",stringsAsFactors = FALSE,header = FALSE)
      
      ## Define new Data SHA1 HASH
      SHAHASHEducation <- digest(EducationRaw, algo="sha1")
      SHAHASHEducation
      ## If file's data still does not match, STOP BUILD WITH ERRORS
      if (SHAHASHEducation != "e62cde0a23e00d5882be1f5d9e76504f68b0efc8") {

      stop("File SHA1 HASH Value does not match original research. Valid SHA1 HASH value of data = \"e62cde0a23e00d5882be1f5d9e76504f68b0efc8\"")

      }
    }

Lets review the first 10 records of this file:

    formattable(head(EducationRaw,10))

<table style="width:1151%;">
<colgroup>
<col width="18%" />
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
<col width="19%" />
<col width="15%" />
<col width="30%" />
<col width="30%" />
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
<th align="right">V11</th>
<th align="right">V12</th>
<th align="right">V13</th>
<th align="right">V14</th>
<th align="right">V15</th>
<th align="right">V16</th>
<th align="right">V17</th>
<th align="right">V18</th>
<th align="right">V19</th>
<th align="right">V20</th>
<th align="right">V21</th>
<th align="right">V22</th>
<th align="right">V23</th>
<th align="right">V24</th>
<th align="right">V25</th>
<th align="right">V26</th>
<th align="right">V27</th>
<th align="right">V28</th>
<th align="right">V29</th>
<th align="right">V30</th>
<th align="right">V31</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="right">CountryCode</td>
<td align="right">Long Name</td>
<td align="right">Income Group</td>
<td align="right">Region</td>
<td align="right">Lending category</td>
<td align="right">Other groups</td>
<td align="right">Currency Unit</td>
<td align="right">Latest population census</td>
<td align="right">Latest household survey</td>
<td align="right">Special Notes</td>
<td align="right">National accounts base year</td>
<td align="right">National accounts reference year</td>
<td align="right">System of National Accounts</td>
<td align="right">SNA price valuation</td>
<td align="right">Alternative conversion factor</td>
<td align="right">PPP survey year</td>
<td align="right">Balance of Payments Manual in use</td>
<td align="right">External debt Reporting status</td>
<td align="right">System of trade</td>
<td align="right">Government Accounting concept</td>
<td align="right">IMF data dissemination standard</td>
<td align="right">Source of most recent Income and expenditure data</td>
<td align="right">Vital registration complete</td>
<td align="right">Latest agricultural census</td>
<td align="right">Latest industrial data</td>
<td align="right">Latest trade data</td>
<td align="right">Latest water withdrawal data</td>
<td align="right">2-alpha code</td>
<td align="right">WB-2 code</td>
<td align="right">Table Name</td>
<td align="right">Short Name</td>
</tr>
<tr class="even">
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
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Special</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">2008</td>
<td align="right"></td>
<td align="right">AW</td>
<td align="right">AW</td>
<td align="right">Aruba</td>
<td align="right">Aruba</td>
</tr>
<tr class="odd">
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
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">General</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">2006</td>
<td align="right"></td>
<td align="right">AD</td>
<td align="right">AD</td>
<td align="right">Andorra</td>
<td align="right">Andorra</td>
</tr>
<tr class="even">
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
<td align="right"></td>
<td align="right"></td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Actual</td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AF</td>
<td align="right">AF</td>
<td align="right">Afghanistan</td>
<td align="right">Afghanistan</td>
</tr>
<tr class="odd">
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
<td align="right"></td>
<td align="right"></td>
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
<td align="right"></td>
<td align="right">1991</td>
<td align="right">2000</td>
<td align="right">AO</td>
<td align="right">AO</td>
<td align="right">Angola</td>
<td align="right">Angola</td>
</tr>
<tr class="even">
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
<tr class="odd">
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
<td align="right"></td>
<td align="right"></td>
<td align="right">VAB</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">BPM4</td>
<td align="right"></td>
<td align="right">General</td>
<td align="right">Consolidated</td>
<td align="right">GDDS</td>
<td align="right"></td>
<td align="right"></td>
<td align="right">1998</td>
<td align="right"></td>
<td align="right">2008</td>
<td align="right">2005</td>
<td align="right">AE</td>
<td align="right">AE</td>
<td align="right">United Arab Emirates</td>
<td align="right">United Arab Emirates</td>
</tr>
<tr class="even">
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
<td align="right"></td>
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
<tr class="odd">
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
<td align="right"></td>
<td align="right">2008</td>
<td align="right">2000</td>
<td align="right">AM</td>
<td align="right">AM</td>
<td align="right">Armenia</td>
<td align="right">Armenia</td>
</tr>
<tr class="even">
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
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">Yes</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right">AS</td>
<td align="right">AS</td>
<td align="right">American Samoa</td>
<td align="right">American Samoa</td>
</tr>
</tbody>
</table>

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
