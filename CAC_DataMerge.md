CAC\_DataMerge
================
RPrice
2/11/2021

# Creating 1 file with all years of County Ag Commissioner’s Data

## Creating a list of files to read in

### (Note that the complete errata is used for 2018)

### Before proceeding: download the csv files

``` r
rm(list = ls()) #clear env
cac0 <- list.files(pattern="*.csv")
cac0 #list of all .csv files in the folder
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
    ## [40] "201908cropyear.csv"   "CountyAgComm_All.csv"

``` r
a <- c(41) #identifying files to remove CHECK PREVIOUS RESULTS FIRST
cac <- cac0[-a] #remove unwanted files
cac #list of desired files
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
    ## [40] "201908cropyear.csv"

## Reading in the data

``` r
cac_list <- lapply(cac,read.csv)
```

## Prepare to merge dataframes

### Confirm columns match/are mergable

``` r
for (i in 2:length(cac_list)) { #confirm column names match
  f <- colnames(cac_list[[1]]) == colnames(cac_list[[i]])
  print(f)
} #one does not match
```

    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
    ##  [1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE

``` r
i<-23
colnames(cac_list[[1]]) == colnames(cac_list[[i]]) #23 does not match
```

    ##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
colnames(cac_list[[1]]) #examine standard names
```

    ##  [1] "Year"            "Commodity.Code"  "Crop.Name"       "County.Code"    
    ##  [5] "County"          "Harvested.Acres" "Yield"           "Production"     
    ##  [9] "Price.P.U"       "Unit"            "Value"

``` r
colnames(cac_list[[23]]) #columns are the same, can just change names
```

    ##  [1] "year"       "commodity"  "cropname"   "countycode" "county"    
    ##  [6] "acres"      "yield"      "production" "price_per"  "unit"      
    ## [11] "value"

``` r
colnames(cac_list[[23]]) <- colnames(cac_list[[1]]) #change col names
colnames(cac_list[[23]]) 
```

    ##  [1] "Year"            "Commodity.Code"  "Crop.Name"       "County.Code"    
    ##  [5] "County"          "Harvested.Acres" "Yield"           "Production"     
    ##  [9] "Price.P.U"       "Unit"            "Value"

## Merge all years

``` r
cac_all <- data.frame(cac_list[[1]])
for (i in 2:length(cac_list)) {
  cac_all <- rbind(cac_all,data.frame(cac_list[[i]]))
}
dim(cac_all) #confirm length
```

    ## [1] 103754     11

## Save merged data

``` r
#setwd("~/2_School/3_Internship/Models/CountyAgCommData") #save to desktop if desired
#write.csv(cac_all,file = "CountyAgComm_All.csv",row.names = FALSE)
```

## How many unique crops?

``` r
length(unique(cac_all[,3]))
```

    ## [1] 722
