CAC\_DataMerge
================
RPrice
2/11/2021

# Creating 1 file with all years of County Ag Commissioner’s Data

## Creating a list of files to read in

### (Note that the complete errata is used for 2018)

### Before proceeding: download the csv files

``` r
cac0 <- list.files(path = "./CAC_DataMerge_files", full.names = FALSE)
cac0 #list of all files in the folder
```

    ##  [1] "198008cactb00.csv"    "198108cactb00.csv"    "198208cactb00.csv"   
    ##  [4] "198308cactb00.csv"    "198408cactb00.csv"    "198508cactb00.csv"   
    ##  [7] "198608cactb00.csv"    "198708cactb00.csv"    "198808cactb00.csv"   
    ## [10] "198908cactb00.csv"    "199008cactb00.csv"    "199108cactb00.csv"   
    ## [13] "199208cactb00.csv"    "199308cactb00.csv"    "199408cactb00.csv"   
    ## [16] "199508cactb00.csv"    "199608cactb00.csv"    "199708cactb00.csv"   
    ## [19] "199808cactb00.csv"    "199908cactb00.csv"    "200008cactb00.csv"   
    ## [22] "200108cactb00.csv"    "200208cactb00.csv"    "200308cactb00.csv"   
    ## [25] "200410cactb00.csv"    "200508cactb00.csv"    "200608cactb00.csv"   
    ## [28] "200708cactb00.csv"    "200810cactb00.csv"    "200910cactb00.csv"   
    ## [31] "201010cactb00.csv"    "201112cactb00.csv"    "201212cactb00.csv"   
    ## [34] "2013cropyear.csv"     "2014cropyear.csv"     "2015cropyear.csv"    
    ## [37] "2016cropyear.csv"     "201708cactb00.csv"    "2018cactbsErrata.csv"
    ## [40] "201908cropyear.csv"   "figure-gfm"
