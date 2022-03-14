---
title: "Lab 6 Homework"
author: "Eliza Mata"
date: "2022-03-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
## $ Country                   <chr> "Albania", "Albania", "Albania", "Albania", ~
## $ `Common name`             <chr> "Angelsharks, sand devils nei", "Atlantic bo~
## $ `ISSCAAP group#`          <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, ~
## $ `ISSCAAP taxonomic group` <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, ~
## $ `ASFIS species#`          <chr> "10903XXXXX", "1750100101", "17710001XX", "2~
## $ `ASFIS species name`      <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp~
## $ `FAO major fishing area`  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, ~
## $ Measure                   <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Q~
## $ `1950`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1951`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1952`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1953`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1954`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1955`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1956`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1957`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1958`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1959`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1960`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1961`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1962`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1963`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1964`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1965`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1966`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1967`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1968`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1969`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1970`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1971`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1972`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1973`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1974`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1975`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1976`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1977`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1978`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1979`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1980`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1981`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1982`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ~
## $ `1983`                    <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, N~
## $ `1984`                    <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, N~
## $ `1985`                    <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, N~
## $ `1986`                    <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, N~
## $ `1987`                    <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, N~
## $ `1988`                    <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, N~
## $ `1989`                    <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, N~
## $ `1990`                    <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, N~
## $ `1991`                    <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, N~
## $ `1992`                    <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, N~
## $ `1993`                    <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA,~
## $ `1994`                    <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA,~
## $ `1995`                    <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30"~
## $ `1996`                    <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA,~
## $ `1997`                    <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4"~
## $ `1998`                    <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA,~
## $ `1999`                    <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA,~
## $ `2000`                    <chr> "30", "25", "2", NA, NA, NA, "220", "20", NA~
## $ `2001`                    <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA,~
## $ `2002`                    <chr> "79", "24", NA, "34", "6", NA, "150", "84", ~
## $ `2003`                    <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA,~
## $ `2004`                    <chr> "4", "2", "2", "15", "1", "2", "76", "285", ~
## $ `2005`                    <chr> "68", "23", "4", "12", "5", "6", "68", "150"~
## $ `2006`                    <chr> "55", "30", "7", "18", "8", "9", "86", "102"~
## $ `2007`                    <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA,~
## $ `2008`                    <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA,~
## $ `2009`                    <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA,~
## $ `2010`                    <chr> "78", "23", "7", NA, NA, NA, "80", "228", NA~
## $ `2011`                    <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, "~
## $ `2012`                    <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA, ~
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries<-clean_names(fisheries)
```


```r
as.factor(fisheries$country) 
```

```
##     [1] Albania                   Albania                  
##     [3] Albania                   Albania                  
##     [5] Albania                   Albania                  
##     [7] Albania                   Albania                  
##     [9] Albania                   Albania                  
##    [11] Albania                   Albania                  
##    [13] Albania                   Albania                  
##    [15] Albania                   Albania                  
##    [17] Albania                   Albania                  
##    [19] Albania                   Albania                  
##    [21] Albania                   Albania                  
##    [23] Albania                   Albania                  
##    [25] Albania                   Albania                  
##    [27] Albania                   Albania                  
##    [29] Albania                   Albania                  
##    [31] Albania                   Albania                  
##    [33] Albania                   Albania                  
##    [35] Albania                   Albania                  
##    [37] Albania                   Albania                  
##    [39] Albania                   Albania                  
##    [41] Albania                   Albania                  
##    [43] Albania                   Albania                  
##    [45] Albania                   Albania                  
##    [47] Albania                   Albania                  
##    [49] Albania                   Albania                  
##    [51] Albania                   Albania                  
##    [53] Albania                   Albania                  
##    [55] Albania                   Albania                  
##    [57] Albania                   Albania                  
##    [59] Albania                   Albania                  
##    [61] Albania                   Albania                  
##    [63] Albania                   Albania                  
##    [65] Albania                   Albania                  
##    [67] Albania                   Algeria                  
##    [69] Algeria                   Algeria                  
##    [71] Algeria                   Algeria                  
##    [73] Algeria                   Algeria                  
##    [75] Algeria                   Algeria                  
##    [77] Algeria                   Algeria                  
##    [79] Algeria                   Algeria                  
##    [81] Algeria                   Algeria                  
##    [83] Algeria                   Algeria                  
##    [85] Algeria                   Algeria                  
##    [87] Algeria                   Algeria                  
##    [89] Algeria                   Algeria                  
##    [91] Algeria                   Algeria                  
##    [93] Algeria                   Algeria                  
##    [95] Algeria                   Algeria                  
##    [97] Algeria                   Algeria                  
##    [99] Algeria                   Algeria                  
##   [101] Algeria                   Algeria                  
##   [103] Algeria                   Algeria                  
##   [105] Algeria                   Algeria                  
##   [107] Algeria                   Algeria                  
##   [109] Algeria                   Algeria                  
##   [111] Algeria                   Algeria                  
##   [113] Algeria                   Algeria                  
##   [115] Algeria                   Algeria                  
##   [117] Algeria                   Algeria                  
##   [119] Algeria                   Algeria                  
##   [121] Algeria                   Algeria                  
##   [123] Algeria                   Algeria                  
##   [125] Algeria                   Algeria                  
##   [127] American Samoa            American Samoa           
##   [129] American Samoa            American Samoa           
##   [131] American Samoa            American Samoa           
##   [133] American Samoa            American Samoa           
##   [135] American Samoa            American Samoa           
##   [137] American Samoa            American Samoa           
##   [139] American Samoa            American Samoa           
##   [141] American Samoa            American Samoa           
##   [143] American Samoa            American Samoa           
##   [145] American Samoa            American Samoa           
##   [147] American Samoa            American Samoa           
##   [149] American Samoa            American Samoa           
##   [151] American Samoa            American Samoa           
##   [153] American Samoa            American Samoa           
##   [155] American Samoa            American Samoa           
##   [157] American Samoa            American Samoa           
##   [159] Angola                    Angola                   
##   [161] Angola                    Angola                   
##   [163] Angola                    Angola                   
##   [165] Angola                    Angola                   
##   [167] Angola                    Angola                   
##   [169] Angola                    Angola                   
##   [171] Angola                    Angola                   
##   [173] Angola                    Angola                   
##   [175] Angola                    Angola                   
##   [177] Angola                    Angola                   
##   [179] Angola                    Angola                   
##   [181] Angola                    Angola                   
##   [183] Angola                    Angola                   
##   [185] Angola                    Angola                   
##   [187] Angola                    Angola                   
##   [189] Angola                    Angola                   
##   [191] Angola                    Angola                   
##   [193] Angola                    Angola                   
##   [195] Angola                    Angola                   
##   [197] Angola                    Angola                   
##   [199] Angola                    Angola                   
##   [201] Angola                    Angola                   
##   [203] Angola                    Angola                   
##   [205] Angola                    Angola                   
##   [207] Angola                    Angola                   
##   [209] Angola                    Angola                   
##   [211] Angola                    Angola                   
##   [213] Angola                    Angola                   
##   [215] Angola                    Angola                   
##   [217] Angola                    Angola                   
##   [219] Angola                    Angola                   
##   [221] Angola                    Angola                   
##   [223] Angola                    Angola                   
##   [225] Angola                    Angola                   
##   [227] Angola                    Angola                   
##   [229] Angola                    Angola                   
##   [231] Angola                    Angola                   
##   [233] Angola                    Angola                   
##   [235] Angola                    Angola                   
##   [237] Angola                    Angola                   
##   [239] Angola                    Angola                   
##   [241] Angola                    Angola                   
##   [243] Angola                    Angola                   
##   [245] Angola                    Angola                   
##   [247] Anguilla                  Anguilla                 
##   [249] Anguilla                  Antigua and Barbuda      
##   [251] Antigua and Barbuda       Antigua and Barbuda      
##   [253] Antigua and Barbuda       Antigua and Barbuda      
##   [255] Antigua and Barbuda       Antigua and Barbuda      
##   [257] Antigua and Barbuda       Antigua and Barbuda      
##   [259] Antigua and Barbuda       Antigua and Barbuda      
##   [261] Antigua and Barbuda       Antigua and Barbuda      
##   [263] Antigua and Barbuda       Antigua and Barbuda      
##   [265] Antigua and Barbuda       Antigua and Barbuda      
##   [267] Antigua and Barbuda       Antigua and Barbuda      
##   [269] Antigua and Barbuda       Antigua and Barbuda      
##   [271] Antigua and Barbuda       Argentina                
##   [273] Argentina                 Argentina                
##   [275] Argentina                 Argentina                
##   [277] Argentina                 Argentina                
##   [279] Argentina                 Argentina                
##   [281] Argentina                 Argentina                
##   [283] Argentina                 Argentina                
##   [285] Argentina                 Argentina                
##   [287] Argentina                 Argentina                
##   [289] Argentina                 Argentina                
##   [291] Argentina                 Argentina                
##   [293] Argentina                 Argentina                
##   [295] Argentina                 Argentina                
##   [297] Argentina                 Argentina                
##   [299] Argentina                 Argentina                
##   [301] Argentina                 Argentina                
##   [303] Argentina                 Argentina                
##   [305] Argentina                 Argentina                
##   [307] Argentina                 Argentina                
##   [309] Argentina                 Argentina                
##   [311] Argentina                 Argentina                
##   [313] Argentina                 Argentina                
##   [315] Argentina                 Argentina                
##   [317] Argentina                 Argentina                
##   [319] Argentina                 Argentina                
##   [321] Argentina                 Argentina                
##   [323] Argentina                 Argentina                
##   [325] Argentina                 Argentina                
##   [327] Argentina                 Argentina                
##   [329] Argentina                 Argentina                
##   [331] Argentina                 Argentina                
##   [333] Argentina                 Argentina                
##   [335] Argentina                 Argentina                
##   [337] Argentina                 Argentina                
##   [339] Argentina                 Argentina                
##   [341] Argentina                 Argentina                
##   [343] Argentina                 Argentina                
##   [345] Argentina                 Argentina                
##   [347] Argentina                 Argentina                
##   [349] Argentina                 Argentina                
##   [351] Argentina                 Argentina                
##   [353] Argentina                 Argentina                
##   [355] Argentina                 Argentina                
##   [357] Argentina                 Argentina                
##   [359] Argentina                 Argentina                
##   [361] Argentina                 Argentina                
##   [363] Argentina                 Argentina                
##   [365] Argentina                 Argentina                
##   [367] Argentina                 Argentina                
##   [369] Argentina                 Argentina                
##   [371] Argentina                 Argentina                
##   [373] Argentina                 Argentina                
##   [375] Argentina                 Argentina                
##   [377] Argentina                 Argentina                
##   [379] Argentina                 Argentina                
##   [381] Argentina                 Argentina                
##   [383] Argentina                 Argentina                
##   [385] Argentina                 Argentina                
##   [387] Argentina                 Argentina                
##   [389] Argentina                 Argentina                
##   [391] Argentina                 Argentina                
##   [393] Argentina                 Argentina                
##   [395] Argentina                 Argentina                
##   [397] Argentina                 Argentina                
##   [399] Argentina                 Argentina                
##   [401] Argentina                 Argentina                
##   [403] Argentina                 Argentina                
##   [405] Argentina                 Argentina                
##   [407] Argentina                 Argentina                
##   [409] Argentina                 Argentina                
##   [411] Argentina                 Aruba                    
##   [413] Aruba                     Aruba                    
##   [415] Aruba                     Aruba                    
##   [417] Australia                 Australia                
##   [419] Australia                 Australia                
##   [421] Australia                 Australia                
##   [423] Australia                 Australia                
##   [425] Australia                 Australia                
##   [427] Australia                 Australia                
##   [429] Australia                 Australia                
##   [431] Australia                 Australia                
##   [433] Australia                 Australia                
##   [435] Australia                 Australia                
##   [437] Australia                 Australia                
##   [439] Australia                 Australia                
##   [441] Australia                 Australia                
##   [443] Australia                 Australia                
##   [445] Australia                 Australia                
##   [447] Australia                 Australia                
##   [449] Australia                 Australia                
##   [451] Australia                 Australia                
##   [453] Australia                 Australia                
##   [455] Australia                 Australia                
##   [457] Australia                 Australia                
##   [459] Australia                 Australia                
##   [461] Australia                 Australia                
##   [463] Australia                 Australia                
##   [465] Australia                 Australia                
##   [467] Australia                 Australia                
##   [469] Australia                 Australia                
##   [471] Australia                 Australia                
##   [473] Australia                 Australia                
##   [475] Australia                 Australia                
##   [477] Australia                 Australia                
##   [479] Australia                 Australia                
##   [481] Australia                 Australia                
##   [483] Australia                 Australia                
##   [485] Australia                 Australia                
##   [487] Australia                 Australia                
##   [489] Australia                 Australia                
##   [491] Australia                 Australia                
##   [493] Australia                 Australia                
##   [495] Australia                 Australia                
##   [497] Australia                 Australia                
##   [499] Australia                 Australia                
##   [501] Australia                 Australia                
##   [503] Australia                 Australia                
##   [505] Australia                 Australia                
##   [507] Australia                 Australia                
##   [509] Australia                 Australia                
##   [511] Australia                 Australia                
##   [513] Australia                 Australia                
##   [515] Australia                 Australia                
##   [517] Australia                 Australia                
##   [519] Australia                 Australia                
##   [521] Australia                 Australia                
##   [523] Australia                 Australia                
##   [525] Australia                 Australia                
##   [527] Australia                 Australia                
##   [529] Australia                 Australia                
##   [531] Australia                 Australia                
##   [533] Australia                 Australia                
##   [535] Australia                 Australia                
##   [537] Australia                 Australia                
##   [539] Australia                 Australia                
##   [541] Australia                 Australia                
##   [543] Australia                 Australia                
##   [545] Australia                 Australia                
##   [547] Australia                 Australia                
##   [549] Australia                 Australia                
##   [551] Australia                 Australia                
##   [553] Australia                 Australia                
##   [555] Australia                 Australia                
##   [557] Australia                 Australia                
##   [559] Australia                 Australia                
##   [561] Australia                 Australia                
##   [563] Australia                 Australia                
##   [565] Australia                 Australia                
##   [567] Australia                 Australia                
##   [569] Australia                 Australia                
##   [571] Australia                 Australia                
##   [573] Australia                 Australia                
##   [575] Australia                 Australia                
##   [577] Australia                 Australia                
##   [579] Australia                 Australia                
##   [581] Australia                 Australia                
##   [583] Australia                 Australia                
##   [585] Australia                 Australia                
##   [587] Australia                 Australia                
##   [589] Australia                 Australia                
##   [591] Australia                 Australia                
##   [593] Australia                 Australia                
##   [595] Australia                 Australia                
##   [597] Australia                 Australia                
##   [599] Australia                 Australia                
##   [601] Australia                 Australia                
##   [603] Australia                 Australia                
##   [605] Australia                 Australia                
##   [607] Australia                 Australia                
##   [609] Australia                 Australia                
##   [611] Australia                 Australia                
##   [613] Australia                 Australia                
##   [615] Australia                 Australia                
##   [617] Australia                 Australia                
##   [619] Australia                 Australia                
##   [621] Australia                 Australia                
##   [623] Australia                 Australia                
##   [625] Australia                 Australia                
##   [627] Australia                 Australia                
##   [629] Australia                 Australia                
##   [631] Australia                 Australia                
##   [633] Australia                 Australia                
##   [635] Australia                 Australia                
##   [637] Australia                 Australia                
##   [639] Australia                 Australia                
##   [641] Australia                 Australia                
##   [643] Australia                 Australia                
##   [645] Australia                 Australia                
##   [647] Australia                 Australia                
##   [649] Australia                 Australia                
##   [651] Australia                 Australia                
##   [653] Australia                 Australia                
##   [655] Australia                 Australia                
##   [657] Australia                 Australia                
##   [659] Australia                 Australia                
##   [661] Australia                 Australia                
##   [663] Australia                 Australia                
##   [665] Australia                 Australia                
##   [667] Australia                 Australia                
##   [669] Australia                 Australia                
##   [671] Australia                 Australia                
##   [673] Australia                 Australia                
##   [675] Australia                 Australia                
##   [677] Australia                 Australia                
##   [679] Australia                 Australia                
##   [681] Australia                 Australia                
##   [683] Australia                 Australia                
##   [685] Australia                 Australia                
##   [687] Australia                 Australia                
##   [689] Australia                 Australia                
##   [691] Australia                 Australia                
##   [693] Australia                 Australia                
##   [695] Australia                 Australia                
##   [697] Australia                 Australia                
##   [699] Australia                 Australia                
##   [701] Australia                 Australia                
##   [703] Australia                 Australia                
##   [705] Australia                 Australia                
##   [707] Australia                 Australia                
##   [709] Australia                 Australia                
##   [711] Australia                 Australia                
##   [713] Australia                 Australia                
##   [715] Australia                 Australia                
##   [717] Australia                 Bahamas                  
##   [719] Bahamas                   Bahamas                  
##   [721] Bahamas                   Bahamas                  
##   [723] Bahamas                   Bahamas                  
##   [725] Bahamas                   Bahamas                  
##   [727] Bahamas                   Bahamas                  
##   [729] Bahamas                   Bahamas                  
##   [731] Bahamas                   Bahrain                  
##   [733] Bahrain                   Bahrain                  
##   [735] Bahrain                   Bahrain                  
##   [737] Bahrain                   Bahrain                  
##   [739] Bahrain                   Bahrain                  
##   [741] Bahrain                   Bahrain                  
##   [743] Bahrain                   Bahrain                  
##   [745] Bahrain                   Bahrain                  
##   [747] Bahrain                   Bahrain                  
##   [749] Bahrain                   Bahrain                  
##   [751] Bahrain                   Bahrain                  
##   [753] Bahrain                   Bahrain                  
##   [755] Bahrain                   Bahrain                  
##   [757] Bahrain                   Bahrain                  
##   [759] Bahrain                   Bahrain                  
##   [761] Bahrain                   Bahrain                  
##   [763] Bahrain                   Bahrain                  
##   [765] Bahrain                   Bahrain                  
##   [767] Bahrain                   Bahrain                  
##   [769] Bahrain                   Bahrain                  
##   [771] Bahrain                   Bahrain                  
##   [773] Bahrain                   Bahrain                  
##   [775] Bahrain                   Bahrain                  
##   [777] Bahrain                   Bahrain                  
##   [779] Bahrain                   Bahrain                  
##   [781] Bahrain                   Bahrain                  
##   [783] Bahrain                   Bahrain                  
##   [785] Bahrain                   Bahrain                  
##   [787] Bahrain                   Bahrain                  
##   [789] Bahrain                   Bahrain                  
##   [791] Bahrain                   Bahrain                  
##   [793] Bahrain                   Bangladesh               
##   [795] Bangladesh                Bangladesh               
##   [797] Bangladesh                Bangladesh               
##   [799] Bangladesh                Bangladesh               
##   [801] Bangladesh                Barbados                 
##   [803] Barbados                  Barbados                 
##   [805] Barbados                  Barbados                 
##   [807] Barbados                  Barbados                 
##   [809] Barbados                  Barbados                 
##   [811] Barbados                  Barbados                 
##   [813] Barbados                  Barbados                 
##   [815] Barbados                  Barbados                 
##   [817] Barbados                  Barbados                 
##   [819] Barbados                  Barbados                 
##   [821] Barbados                  Barbados                 
##   [823] Belgium                   Belgium                  
##   [825] Belgium                   Belgium                  
##   [827] Belgium                   Belgium                  
##   [829] Belgium                   Belgium                  
##   [831] Belgium                   Belgium                  
##   [833] Belgium                   Belgium                  
##   [835] Belgium                   Belgium                  
##   [837] Belgium                   Belgium                  
##   [839] Belgium                   Belgium                  
##   [841] Belgium                   Belgium                  
##   [843] Belgium                   Belgium                  
##   [845] Belgium                   Belgium                  
##   [847] Belgium                   Belgium                  
##   [849] Belgium                   Belgium                  
##   [851] Belgium                   Belgium                  
##   [853] Belgium                   Belgium                  
##   [855] Belgium                   Belgium                  
##   [857] Belgium                   Belgium                  
##   [859] Belgium                   Belgium                  
##   [861] Belgium                   Belgium                  
##   [863] Belgium                   Belgium                  
##   [865] Belgium                   Belgium                  
##   [867] Belgium                   Belgium                  
##   [869] Belgium                   Belgium                  
##   [871] Belgium                   Belgium                  
##   [873] Belgium                   Belgium                  
##   [875] Belgium                   Belgium                  
##   [877] Belgium                   Belgium                  
##   [879] Belgium                   Belize                   
##   [881] Belize                    Belize                   
##   [883] Belize                    Belize                   
##   [885] Belize                    Belize                   
##   [887] Belize                    Belize                   
##   [889] Belize                    Belize                   
##   [891] Belize                    Belize                   
##   [893] Belize                    Belize                   
##   [895] Belize                    Belize                   
##   [897] Belize                    Belize                   
##   [899] Belize                    Belize                   
##   [901] Belize                    Belize                   
##   [903] Belize                    Belize                   
##   [905] Belize                    Belize                   
##   [907] Belize                    Belize                   
##   [909] Belize                    Belize                   
##   [911] Belize                    Belize                   
##   [913] Belize                    Belize                   
##   [915] Belize                    Belize                   
##   [917] Belize                    Belize                   
##   [919] Belize                    Belize                   
##   [921] Belize                    Belize                   
##   [923] Belize                    Belize                   
##   [925] Belize                    Belize                   
##   [927] Belize                    Belize                   
##   [929] Belize                    Belize                   
##   [931] Belize                    Belize                   
##   [933] Belize                    Belize                   
##   [935] Belize                    Belize                   
##   [937] Belize                    Belize                   
##   [939] Belize                    Belize                   
##   [941] Belize                    Belize                   
##   [943] Belize                    Belize                   
##   [945] Belize                    Belize                   
##   [947] Belize                    Belize                   
##   [949] Belize                    Belize                   
##   [951] Belize                    Belize                   
##   [953] Belize                    Belize                   
##   [955] Belize                    Belize                   
##   [957] Belize                    Belize                   
##   [959] Belize                    Belize                   
##   [961] Belize                    Belize                   
##   [963] Belize                    Belize                   
##   [965] Belize                    Belize                   
##   [967] Belize                    Belize                   
##   [969] Belize                    Belize                   
##   [971] Belize                    Belize                   
##   [973] Belize                    Belize                   
##   [975] Belize                    Belize                   
##   [977] Belize                    Belize                   
##   [979] Belize                    Belize                   
##   [981] Belize                    Belize                   
##   [983] Belize                    Belize                   
##   [985] Belize                    Belize                   
##   [987] Belize                    Belize                   
##   [989] Belize                    Belize                   
##   [991] Belize                    Belize                   
##   [993] Belize                    Belize                   
##   [995] Belize                    Belize                   
##   [997] Belize                    Belize                   
##   [999] Belize                    Belize                   
##  [1001] Belize                    Belize                   
##  [1003] Belize                    Belize                   
##  [1005] Belize                    Belize                   
##  [1007] Belize                    Belize                   
##  [1009] Belize                    Belize                   
##  [1011] Belize                    Belize                   
##  [1013] Benin                     Benin                    
##  [1015] Benin                     Benin                    
##  [1017] Benin                     Benin                    
##  [1019] Benin                     Benin                    
##  [1021] Benin                     Benin                    
##  [1023] Benin                     Benin                    
##  [1025] Benin                     Benin                    
##  [1027] Benin                     Benin                    
##  [1029] Benin                     Benin                    
##  [1031] Benin                     Benin                    
##  [1033] Benin                     Benin                    
##  [1035] Benin                     Benin                    
##  [1037] Benin                     Benin                    
##  [1039] Benin                     Benin                    
##  [1041] Benin                     Benin                    
##  [1043] Benin                     Benin                    
##  [1045] Benin                     Benin                    
##  [1047] Benin                     Benin                    
##  [1049] Benin                     Benin                    
##  [1051] Benin                     Benin                    
##  [1053] Benin                     Benin                    
##  [1055] Benin                     Benin                    
##  [1057] Benin                     Benin                    
##  [1059] Benin                     Benin                    
##  [1061] Benin                     Benin                    
##  [1063] Benin                     Benin                    
##  [1065] Benin                     Benin                    
##  [1067] Benin                     Benin                    
##  [1069] Benin                     Benin                    
##  [1071] Benin                     Benin                    
##  [1073] Benin                     Benin                    
##  [1075] Benin                     Benin                    
##  [1077] Benin                     Benin                    
##  [1079] Benin                     Benin                    
##  [1081] Bermuda                   Bermuda                  
##  [1083] Bermuda                   Bermuda                  
##  [1085] Bermuda                   Bermuda                  
##  [1087] Bermuda                   Bermuda                  
##  [1089] Bermuda                   Bermuda                  
##  [1091] Bermuda                   Bermuda                  
##  [1093] Bermuda                   Bermuda                  
##  [1095] Bermuda                   Bermuda                  
##  [1097] Bermuda                   Bermuda                  
##  [1099] Bermuda                   Bermuda                  
##  [1101] Bermuda                   Bermuda                  
##  [1103] Bermuda                   Bermuda                  
##  [1105] Bermuda                   Bermuda                  
##  [1107] Bermuda                   Bermuda                  
##  [1109] Bermuda                   Bermuda                  
##  [1111] Bermuda                   Bermuda                  
##  [1113] Bermuda                   Bermuda                  
##  [1115] Bermuda                   Bermuda                  
##  [1117] Bermuda                   Bermuda                  
##  [1119] Bermuda                   Bermuda                  
##  [1121] Bermuda                   Bermuda                  
##  [1123] Bermuda                   Bermuda                  
##  [1125] Bermuda                   Bermuda                  
##  [1127] Bermuda                   Bonaire/S.Eustatius/Saba 
##  [1129] Bonaire/S.Eustatius/Saba  Bosnia and Herzegovina   
##  [1131] Brazil                    Brazil                   
##  [1133] Brazil                    Brazil                   
##  [1135] Brazil                    Brazil                   
##  [1137] Brazil                    Brazil                   
##  [1139] Brazil                    Brazil                   
##  [1141] Brazil                    Brazil                   
##  [1143] Brazil                    Brazil                   
##  [1145] Brazil                    Brazil                   
##  [1147] Brazil                    Brazil                   
##  [1149] Brazil                    Brazil                   
##  [1151] Brazil                    Brazil                   
##  [1153] Brazil                    Brazil                   
##  [1155] Brazil                    Brazil                   
##  [1157] Brazil                    Brazil                   
##  [1159] Brazil                    Brazil                   
##  [1161] Brazil                    Brazil                   
##  [1163] Brazil                    Brazil                   
##  [1165] Brazil                    Brazil                   
##  [1167] Brazil                    Brazil                   
##  [1169] Brazil                    Brazil                   
##  [1171] Brazil                    Brazil                   
##  [1173] Brazil                    Brazil                   
##  [1175] Brazil                    Brazil                   
##  [1177] Brazil                    Brazil                   
##  [1179] Brazil                    Brazil                   
##  [1181] Brazil                    Brazil                   
##  [1183] Brazil                    Brazil                   
##  [1185] Brazil                    Brazil                   
##  [1187] Brazil                    Brazil                   
##  [1189] Brazil                    Brazil                   
##  [1191] Brazil                    Brazil                   
##  [1193] Brazil                    Brazil                   
##  [1195] Brazil                    Brazil                   
##  [1197] Brazil                    Brazil                   
##  [1199] Brazil                    Brazil                   
##  [1201] Brazil                    Brazil                   
##  [1203] Brazil                    Brazil                   
##  [1205] Brazil                    Brazil                   
##  [1207] Brazil                    Brazil                   
##  [1209] Brazil                    Brazil                   
##  [1211] Brazil                    Brazil                   
##  [1213] Brazil                    Brazil                   
##  [1215] Brazil                    Brazil                   
##  [1217] Brazil                    Brazil                   
##  [1219] Brazil                    Brazil                   
##  [1221] Brazil                    Brazil                   
##  [1223] Brazil                    Brazil                   
##  [1225] Brazil                    Brazil                   
##  [1227] Brazil                    Brazil                   
##  [1229] Brazil                    Brazil                   
##  [1231] Brazil                    Brazil                   
##  [1233] Brazil                    Brazil                   
##  [1235] Brazil                    Brazil                   
##  [1237] Brazil                    Brazil                   
##  [1239] Brazil                    Brazil                   
##  [1241] Brazil                    Brazil                   
##  [1243] Brazil                    Brazil                   
##  [1245] Brazil                    Brazil                   
##  [1247] Brazil                    Brazil                   
##  [1249] Brazil                    Brazil                   
##  [1251] Brazil                    Brazil                   
##  [1253] Brazil                    Brazil                   
##  [1255] Brazil                    Brazil                   
##  [1257] Brazil                    Brazil                   
##  [1259] Brazil                    Brazil                   
##  [1261] Brazil                    Brazil                   
##  [1263] Brazil                    Brazil                   
##  [1265] Brazil                    Brazil                   
##  [1267] British Indian Ocean Ter  British Indian Ocean Ter 
##  [1269] British Indian Ocean Ter  British Indian Ocean Ter 
##  [1271] British Indian Ocean Ter  British Indian Ocean Ter 
##  [1273] British Indian Ocean Ter  British Virgin Islands   
##  [1275] British Virgin Islands    British Virgin Islands   
##  [1277] British Virgin Islands    British Virgin Islands   
##  [1279] British Virgin Islands    British Virgin Islands   
##  [1281] British Virgin Islands    British Virgin Islands   
##  [1283] British Virgin Islands    British Virgin Islands   
##  [1285] British Virgin Islands    British Virgin Islands   
##  [1287] British Virgin Islands    British Virgin Islands   
##  [1289] British Virgin Islands    British Virgin Islands   
##  [1291] British Virgin Islands    Brunei Darussalam        
##  [1293] Brunei Darussalam         Brunei Darussalam        
##  [1295] Brunei Darussalam         Brunei Darussalam        
##  [1297] Brunei Darussalam         Brunei Darussalam        
##  [1299] Brunei Darussalam         Bulgaria                 
##  [1301] Bulgaria                  Bulgaria                 
##  [1303] Bulgaria                  Bulgaria                 
##  [1305] Bulgaria                  Bulgaria                 
##  [1307] Bulgaria                  Bulgaria                 
##  [1309] Bulgaria                  Bulgaria                 
##  [1311] Bulgaria                  Bulgaria                 
##  [1313] Bulgaria                  Bulgaria                 
##  [1315] Bulgaria                  Bulgaria                 
##  [1317] Bulgaria                  Bulgaria                 
##  [1319] Bulgaria                  Bulgaria                 
##  [1321] Bulgaria                  Bulgaria                 
##  [1323] Bulgaria                  Bulgaria                 
##  [1325] Bulgaria                  Bulgaria                 
##  [1327] Bulgaria                  Bulgaria                 
##  [1329] Bulgaria                  Bulgaria                 
##  [1331] Bulgaria                  Bulgaria                 
##  [1333] Bulgaria                  Bulgaria                 
##  [1335] Bulgaria                  Bulgaria                 
##  [1337] Bulgaria                  Bulgaria                 
##  [1339] Bulgaria                  Bulgaria                 
##  [1341] Bulgaria                  Bulgaria                 
##  [1343] Bulgaria                  Bulgaria                 
##  [1345] Bulgaria                  Bulgaria                 
##  [1347] Bulgaria                  Bulgaria                 
##  [1349] Bulgaria                  Bulgaria                 
##  [1351] Bulgaria                  Bulgaria                 
##  [1353] Bulgaria                  Bulgaria                 
##  [1355] Bulgaria                  Bulgaria                 
##  [1357] Bulgaria                  Bulgaria                 
##  [1359] Bulgaria                  Bulgaria                 
##  [1361] Bulgaria                  Bulgaria                 
##  [1363] Bulgaria                  Bulgaria                 
##  [1365] Bulgaria                  Bulgaria                 
##  [1367] Bulgaria                  Bulgaria                 
##  [1369] Bulgaria                  Bulgaria                 
##  [1371] Bulgaria                  Bulgaria                 
##  [1373] Bulgaria                  Bulgaria                 
##  [1375] Bulgaria                  Bulgaria                 
##  [1377] Bulgaria                  Bulgaria                 
##  [1379] Bulgaria                  Bulgaria                 
##  [1381] Bulgaria                  Bulgaria                 
##  [1383] Bulgaria                  Bulgaria                 
##  [1385] Bulgaria                  Bulgaria                 
##  [1387] Bulgaria                  Bulgaria                 
##  [1389] Bulgaria                  Bulgaria                 
##  [1391] Bulgaria                  Bulgaria                 
##  [1393] Bulgaria                  Bulgaria                 
##  [1395] Bulgaria                  Bulgaria                 
##  [1397] Bulgaria                  Bulgaria                 
##  [1399] Bulgaria                  Bulgaria                 
##  [1401] Bulgaria                  Bulgaria                 
##  [1403] Bulgaria                  Bulgaria                 
##  [1405] Bulgaria                  Bulgaria                 
##  [1407] Bulgaria                  Bulgaria                 
##  [1409] Bulgaria                  Bulgaria                 
##  [1411] Bulgaria                  Bulgaria                 
##  [1413] Bulgaria                  Bulgaria                 
##  [1415] Bulgaria                  Bulgaria                 
##  [1417] Bulgaria                  Bulgaria                 
##  [1419] Bulgaria                  Bulgaria                 
##  [1421] Bulgaria                  Bulgaria                 
##  [1423] Bulgaria                  Bulgaria                 
##  [1425] Bulgaria                  Bulgaria                 
##  [1427] Bulgaria                  Bulgaria                 
##  [1429] Bulgaria                  Bulgaria                 
##  [1431] Bulgaria                  Bulgaria                 
##  [1433] Bulgaria                  Bulgaria                 
##  [1435] Bulgaria                  Bulgaria                 
##  [1437] Bulgaria                  Bulgaria                 
##  [1439] Bulgaria                  Bulgaria                 
##  [1441] Bulgaria                  Bulgaria                 
##  [1443] Bulgaria                  Bulgaria                 
##  [1445] Bulgaria                  Bulgaria                 
##  [1447] Bulgaria                  Bulgaria                 
##  [1449] Bulgaria                  Bulgaria                 
##  [1451] Bulgaria                  Bulgaria                 
##  [1453] Bulgaria                  Bulgaria                 
##  [1455] Bulgaria                  Bulgaria                 
##  [1457] Bulgaria                  Bulgaria                 
##  [1459] Bulgaria                  Bulgaria                 
##  [1461] Bulgaria                  Bulgaria                 
##  [1463] Bulgaria                  Bulgaria                 
##  [1465] Bulgaria                  Bulgaria                 
##  [1467] Bulgaria                  Bulgaria                 
##  [1469] Bulgaria                  Bulgaria                 
##  [1471] Bulgaria                  Bulgaria                 
##  [1473] Bulgaria                  Bulgaria                 
##  [1475] Bulgaria                  Bulgaria                 
##  [1477] Bulgaria                  Bulgaria                 
##  [1479] Bulgaria                  Bulgaria                 
##  [1481] Bulgaria                  Bulgaria                 
##  [1483] Bulgaria                  Bulgaria                 
##  [1485] Bulgaria                  Bulgaria                 
##  [1487] Bulgaria                  Bulgaria                 
##  [1489] Bulgaria                  Bulgaria                 
##  [1491] Bulgaria                  Bulgaria                 
##  [1493] Bulgaria                  Bulgaria                 
##  [1495] Bulgaria                  Bulgaria                 
##  [1497] Cabo Verde                Cabo Verde               
##  [1499] Cabo Verde                Cabo Verde               
##  [1501] Cabo Verde                Cabo Verde               
##  [1503] Cabo Verde                Cabo Verde               
##  [1505] Cabo Verde                Cabo Verde               
##  [1507] Cabo Verde                Cabo Verde               
##  [1509] Cabo Verde                Cabo Verde               
##  [1511] Cabo Verde                Cabo Verde               
##  [1513] Cabo Verde                Cabo Verde               
##  [1515] Cabo Verde                Cabo Verde               
##  [1517] Cabo Verde                Cabo Verde               
##  [1519] Cabo Verde                Cabo Verde               
##  [1521] Cabo Verde                Cabo Verde               
##  [1523] Cambodia                  Cambodia                 
##  [1525] Cambodia                  Cambodia                 
##  [1527] Cambodia                  Cambodia                 
##  [1529] Cambodia                  Cambodia                 
##  [1531] Cameroon                  Cameroon                 
##  [1533] Cameroon                  Cameroon                 
##  [1535] Cameroon                  Cameroon                 
##  [1537] Cameroon                  Cameroon                 
##  [1539] Cameroon                  Cameroon                 
##  [1541] Cameroon                  Cameroon                 
##  [1543] Cameroon                  Cameroon                 
##  [1545] Cameroon                  Cameroon                 
##  [1547] Cameroon                  Cameroon                 
##  [1549] Cameroon                  Cameroon                 
##  [1551] Cameroon                  Cameroon                 
##  [1553] Cameroon                  Cameroon                 
##  [1555] Cameroon                  Cameroon                 
##  [1557] Cameroon                  Cameroon                 
##  [1559] Cameroon                  Cameroon                 
##  [1561] Cameroon                  Cameroon                 
##  [1563] Cameroon                  Cameroon                 
##  [1565] Cameroon                  Cameroon                 
##  [1567] Canada                    Canada                   
##  [1569] Canada                    Canada                   
##  [1571] Canada                    Canada                   
##  [1573] Canada                    Canada                   
##  [1575] Canada                    Canada                   
##  [1577] Canada                    Canada                   
##  [1579] Canada                    Canada                   
##  [1581] Canada                    Canada                   
##  [1583] Canada                    Canada                   
##  [1585] Canada                    Canada                   
##  [1587] Canada                    Canada                   
##  [1589] Canada                    Canada                   
##  [1591] Canada                    Canada                   
##  [1593] Canada                    Canada                   
##  [1595] Canada                    Canada                   
##  [1597] Canada                    Canada                   
##  [1599] Canada                    Canada                   
##  [1601] Canada                    Canada                   
##  [1603] Canada                    Canada                   
##  [1605] Canada                    Canada                   
##  [1607] Canada                    Canada                   
##  [1609] Canada                    Canada                   
##  [1611] Canada                    Canada                   
##  [1613] Canada                    Canada                   
##  [1615] Canada                    Canada                   
##  [1617] Canada                    Canada                   
##  [1619] Canada                    Canada                   
##  [1621] Canada                    Canada                   
##  [1623] Canada                    Canada                   
##  [1625] Canada                    Canada                   
##  [1627] Canada                    Canada                   
##  [1629] Canada                    Canada                   
##  [1631] Canada                    Canada                   
##  [1633] Canada                    Canada                   
##  [1635] Canada                    Canada                   
##  [1637] Canada                    Canada                   
##  [1639] Canada                    Canada                   
##  [1641] Canada                    Canada                   
##  [1643] Canada                    Canada                   
##  [1645] Canada                    Canada                   
##  [1647] Canada                    Canada                   
##  [1649] Canada                    Canada                   
##  [1651] Canada                    Canada                   
##  [1653] Canada                    Canada                   
##  [1655] Canada                    Canada                   
##  [1657] Canada                    Canada                   
##  [1659] Canada                    Canada                   
##  [1661] Canada                    Canada                   
##  [1663] Canada                    Canada                   
##  [1665] Canada                    Canada                   
##  [1667] Canada                    Canada                   
##  [1669] Canada                    Canada                   
##  [1671] Canada                    Canada                   
##  [1673] Canada                    Canada                   
##  [1675] Canada                    Canada                   
##  [1677] Canada                    Canada                   
##  [1679] Canada                    Canada                   
##  [1681] Canada                    Canada                   
##  [1683] Canada                    Canada                   
##  [1685] Canada                    Canada                   
##  [1687] Canada                    Canada                   
##  [1689] Canada                    Canada                   
##  [1691] Canada                    Cayman Islands           
##  [1693] Cayman Islands            Cayman Islands           
##  [1695] Cayman Islands            Channel Islands          
##  [1697] Channel Islands           Channel Islands          
##  [1699] Channel Islands           Channel Islands          
##  [1701] Channel Islands           Channel Islands          
##  [1703] Channel Islands           Channel Islands          
##  [1705] Channel Islands           Channel Islands          
##  [1707] Channel Islands           Channel Islands          
##  [1709] Channel Islands           Channel Islands          
##  [1711] Channel Islands           Channel Islands          
##  [1713] Channel Islands           Channel Islands          
##  [1715] Channel Islands           Channel Islands          
##  [1717] Channel Islands           Channel Islands          
##  [1719] Channel Islands           Channel Islands          
##  [1721] Channel Islands           Channel Islands          
##  [1723] Channel Islands           Channel Islands          
##  [1725] Channel Islands           Channel Islands          
##  [1727] Channel Islands           Channel Islands          
##  [1729] Channel Islands           Channel Islands          
##  [1731] Channel Islands           Channel Islands          
##  [1733] Channel Islands           Channel Islands          
##  [1735] Channel Islands           Channel Islands          
##  [1737] Channel Islands           Channel Islands          
##  [1739] Channel Islands           Channel Islands          
##  [1741] Channel Islands           Channel Islands          
##  [1743] Channel Islands           Channel Islands          
##  [1745] Channel Islands           Channel Islands          
##  [1747] Channel Islands           Channel Islands          
##  [1749] Channel Islands           Channel Islands          
##  [1751] Channel Islands           Channel Islands          
##  [1753] Channel Islands           Channel Islands          
##  [1755] Channel Islands           Channel Islands          
##  [1757] Channel Islands           Channel Islands          
##  [1759] Channel Islands           Channel Islands          
##  [1761] Chile                     Chile                    
##  [1763] Chile                     Chile                    
##  [1765] Chile                     Chile                    
##  [1767] Chile                     Chile                    
##  [1769] Chile                     Chile                    
##  [1771] Chile                     Chile                    
##  [1773] Chile                     Chile                    
##  [1775] Chile                     Chile                    
##  [1777] Chile                     Chile                    
##  [1779] Chile                     Chile                    
##  [1781] Chile                     Chile                    
##  [1783] Chile                     Chile                    
##  [1785] Chile                     Chile                    
##  [1787] Chile                     Chile                    
##  [1789] Chile                     Chile                    
##  [1791] Chile                     Chile                    
##  [1793] Chile                     Chile                    
##  [1795] Chile                     Chile                    
##  [1797] Chile                     Chile                    
##  [1799] Chile                     Chile                    
##  [1801] Chile                     Chile                    
##  [1803] Chile                     Chile                    
##  [1805] Chile                     Chile                    
##  [1807] Chile                     Chile                    
##  [1809] Chile                     Chile                    
##  [1811] Chile                     Chile                    
##  [1813] Chile                     Chile                    
##  [1815] Chile                     Chile                    
##  [1817] Chile                     Chile                    
##  [1819] Chile                     Chile                    
##  [1821] Chile                     Chile                    
##  [1823] Chile                     Chile                    
##  [1825] Chile                     Chile                    
##  [1827] Chile                     Chile                    
##  [1829] Chile                     Chile                    
##  [1831] Chile                     Chile                    
##  [1833] Chile                     Chile                    
##  [1835] Chile                     Chile                    
##  [1837] Chile                     Chile                    
##  [1839] Chile                     Chile                    
##  [1841] Chile                     Chile                    
##  [1843] Chile                     Chile                    
##  [1845] Chile                     Chile                    
##  [1847] Chile                     Chile                    
##  [1849] Chile                     Chile                    
##  [1851] Chile                     Chile                    
##  [1853] Chile                     Chile                    
##  [1855] Chile                     Chile                    
##  [1857] Chile                     Chile                    
##  [1859] Chile                     Chile                    
##  [1861] Chile                     Chile                    
##  [1863] Chile                     Chile                    
##  [1865] Chile                     Chile                    
##  [1867] Chile                     Chile                    
##  [1869] Chile                     Chile                    
##  [1871] Chile                     Chile                    
##  [1873] Chile                     Chile                    
##  [1875] Chile                     Chile                    
##  [1877] Chile                     Chile                    
##  [1879] Chile                     Chile                    
##  [1881] Chile                     Chile                    
##  [1883] Chile                     Chile                    
##  [1885] Chile                     Chile                    
##  [1887] Chile                     Chile                    
##  [1889] Chile                     Chile                    
##  [1891] Chile                     Chile                    
##  [1893] Chile                     Chile                    
##  [1895] Chile                     Chile                    
##  [1897] Chile                     Chile                    
##  [1899] Chile                     Chile                    
##  [1901] Chile                     China                    
##  [1903] China                     China                    
##  [1905] China                     China                    
##  [1907] China                     China                    
##  [1909] China                     China                    
##  [1911] China                     China                    
##  [1913] China                     China                    
##  [1915] China                     China                    
##  [1917] China                     China                    
##  [1919] China                     China                    
##  [1921] China                     China                    
##  [1923] China                     China                    
##  [1925] China                     China                    
##  [1927] China                     China                    
##  [1929] China                     China                    
##  [1931] China                     China                    
##  [1933] China                     China                    
##  [1935] China                     China                    
##  [1937] China                     China                    
##  [1939] China                     China                    
##  [1941] China                     China                    
##  [1943] China                     China                    
##  [1945] China                     China                    
##  [1947] China                     China                    
##  [1949] China                     China                    
##  [1951] China                     China                    
##  [1953] China                     China                    
##  [1955] China                     China                    
##  [1957] China                     China                    
##  [1959] China                     China                    
##  [1961] China                     China                    
##  [1963] China                     China                    
##  [1965] China                     China                    
##  [1967] China                     China                    
##  [1969] China                     China                    
##  [1971] China                     China                    
##  [1973] China                     China                    
##  [1975] China                     China                    
##  [1977] China                     China                    
##  [1979] China                     China                    
##  [1981] China                     China                    
##  [1983] China                     China                    
##  [1985] China                     China                    
##  [1987] China                     China                    
##  [1989] China                     China                    
##  [1991] China                     China                    
##  [1993] China                     China                    
##  [1995] China                     China                    
##  [1997] China                     China                    
##  [1999] China                     China                    
##  [2001] China                     China                    
##  [2003] China                     China                    
##  [2005] China                     China                    
##  [2007] China                     China                    
##  [2009] China                     China                    
##  [2011] China                     China                    
##  [2013] China                     China                    
##  [2015] China                     China                    
##  [2017] China                     China                    
##  [2019] China                     China                    
##  [2021] China                     China                    
##  [2023] China                     China                    
##  [2025] China                     China                    
##  [2027] China                     China                    
##  [2029] China                     China                    
##  [2031] China                     China                    
##  [2033] China                     China                    
##  [2035] China                     China                    
##  [2037] China                     China                    
##  [2039] China                     China                    
##  [2041] China                     China                    
##  [2043] China                     China                    
##  [2045] China                     China                    
##  [2047] China                     China                    
##  [2049] China                     China                    
##  [2051] China                     China                    
##  [2053] China                     China                    
##  [2055] China                     China                    
##  [2057] China                     China                    
##  [2059] China                     China                    
##  [2061] China                     China                    
##  [2063] China                     China                    
##  [2065] China                     China                    
##  [2067] China                     China                    
##  [2069] China                     China                    
##  [2071] China                     China                    
##  [2073] China                     China                    
##  [2075] China                     China                    
##  [2077] China                     China                    
##  [2079] China                     China                    
##  [2081] China                     China                    
##  [2083] China                     China                    
##  [2085] China                     China                    
##  [2087] China                     China                    
##  [2089] China                     China                    
##  [2091] China                     China                    
##  [2093] China                     China                    
##  [2095] China                     China                    
##  [2097] China                     China                    
##  [2099] China                     China                    
##  [2101] China                     China                    
##  [2103] China                     China                    
##  [2105] China                     China                    
##  [2107] China                     China                    
##  [2109] China                     China                    
##  [2111] China                     China                    
##  [2113] China                     China                    
##  [2115] China                     China                    
##  [2117] China                     China                    
##  [2119] China                     China                    
##  [2121] China                     China                    
##  [2123] China                     China                    
##  [2125] China                     China                    
##  [2127] China                     China                    
##  [2129] China                     China                    
##  [2131] China                     China                    
##  [2133] China                     China                    
##  [2135] China                     China                    
##  [2137] China                     China, Hong Kong SAR     
##  [2139] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2141] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2143] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2145] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2147] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2149] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2151] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2153] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2155] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2157] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2159] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2161] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2163] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2165] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2167] China, Hong Kong SAR      China, Hong Kong SAR     
##  [2169] China, Hong Kong SAR      China, Macao SAR         
##  [2171] China, Macao SAR          China, Macao SAR         
##  [2173] China, Macao SAR          Colombia                 
##  [2175] Colombia                  Colombia                 
##  [2177] Colombia                  Colombia                 
##  [2179] Colombia                  Colombia                 
##  [2181] Colombia                  Colombia                 
##  [2183] Colombia                  Colombia                 
##  [2185] Colombia                  Colombia                 
##  [2187] Colombia                  Colombia                 
##  [2189] Colombia                  Colombia                 
##  [2191] Colombia                  Colombia                 
##  [2193] Colombia                  Colombia                 
##  [2195] Colombia                  Colombia                 
##  [2197] Colombia                  Colombia                 
##  [2199] Colombia                  Colombia                 
##  [2201] Colombia                  Colombia                 
##  [2203] Colombia                  Colombia                 
##  [2205] Colombia                  Colombia                 
##  [2207] Colombia                  Colombia                 
##  [2209] Colombia                  Colombia                 
##  [2211] Colombia                  Colombia                 
##  [2213] Colombia                  Colombia                 
##  [2215] Colombia                  Colombia                 
##  [2217] Colombia                  Colombia                 
##  [2219] Colombia                  Colombia                 
##  [2221] Colombia                  Colombia                 
##  [2223] Colombia                  Colombia                 
##  [2225] Colombia                  Colombia                 
##  [2227] Colombia                  Colombia                 
##  [2229] Colombia                  Colombia                 
##  [2231] Colombia                  Colombia                 
##  [2233] Colombia                  Colombia                 
##  [2235] Colombia                  Colombia                 
##  [2237] Colombia                  Colombia                 
##  [2239] Colombia                  Colombia                 
##  [2241] Colombia                  Colombia                 
##  [2243] Colombia                  Colombia                 
##  [2245] Colombia                  Colombia                 
##  [2247] Colombia                  Colombia                 
##  [2249] Colombia                  Colombia                 
##  [2251] Colombia                  Colombia                 
##  [2253] Colombia                  Colombia                 
##  [2255] Comoros                   Comoros                  
##  [2257] Comoros                   Comoros                  
##  [2259] Comoros                   Comoros                  
##  [2261] Comoros                   Comoros                  
##  [2263] Comoros                   Comoros                  
##  [2265] Comoros                   Comoros                  
##  [2267] Comoros                   Comoros                  
##  [2269] Comoros                   Comoros                  
##  [2271] Comoros                   Comoros                  
##  [2273] Comoros                   Comoros                  
##  [2275] Comoros                   Comoros                  
##  [2277] Comoros                   Comoros                  
##  [2279] Comoros                   Comoros                  
##  [2281] Comoros                   Comoros                  
##  [2283] Comoros                   Comoros                  
##  [2285] Comoros                   Comoros                  
##  [2287] Comoros                   Comoros                  
##  [2289] Comoros                   Comoros                  
##  [2291] Comoros                   Comoros                  
##  [2293] Comoros                   Comoros                  
##  [2295] Comoros                   Comoros                  
##  [2297] Comoros                   Congo, Dem. Rep. of the  
##  [2299] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2301] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2303] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2305] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2307] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2309] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2311] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2313] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2315] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2317] Congo, Dem. Rep. of the   Congo, Dem. Rep. of the  
##  [2319] Congo, Republic of        Congo, Republic of       
##  [2321] Congo, Republic of        Congo, Republic of       
##  [2323] Congo, Republic of        Congo, Republic of       
##  [2325] Congo, Republic of        Congo, Republic of       
##  [2327] Congo, Republic of        Congo, Republic of       
##  [2329] Congo, Republic of        Congo, Republic of       
##  [2331] Congo, Republic of        Congo, Republic of       
##  [2333] Congo, Republic of        Congo, Republic of       
##  [2335] Congo, Republic of        Congo, Republic of       
##  [2337] Congo, Republic of        Congo, Republic of       
##  [2339] Congo, Republic of        Congo, Republic of       
##  [2341] Congo, Republic of        Congo, Republic of       
##  [2343] Congo, Republic of        Congo, Republic of       
##  [2345] Congo, Republic of        Congo, Republic of       
##  [2347] Congo, Republic of        Congo, Republic of       
##  [2349] Congo, Republic of        Congo, Republic of       
##  [2351] Congo, Republic of        Congo, Republic of       
##  [2353] Congo, Republic of        Congo, Republic of       
##  [2355] Congo, Republic of        Congo, Republic of       
##  [2357] Congo, Republic of        Congo, Republic of       
##  [2359] Congo, Republic of        Congo, Republic of       
##  [2361] Congo, Republic of        Congo, Republic of       
##  [2363] Congo, Republic of        Congo, Republic of       
##  [2365] Congo, Republic of        Congo, Republic of       
##  [2367] Congo, Republic of        Congo, Republic of       
##  [2369] Congo, Republic of        Congo, Republic of       
##  [2371] Congo, Republic of        Cook Islands             
##  [2373] Cook Islands              Cook Islands             
##  [2375] Cook Islands              Cook Islands             
##  [2377] Cook Islands              Cook Islands             
##  [2379] Cook Islands              Cook Islands             
##  [2381] Cook Islands              Cook Islands             
##  [2383] Cook Islands              Cook Islands             
##  [2385] Cook Islands              Cook Islands             
##  [2387] Cook Islands              Cook Islands             
##  [2389] Cook Islands              Cook Islands             
##  [2391] Cook Islands              Cook Islands             
##  [2393] Cook Islands              Cook Islands             
##  [2395] Cook Islands              Cook Islands             
##  [2397] Cook Islands              Cook Islands             
##  [2399] Cook Islands              Cook Islands             
##  [2401] Cook Islands              Cook Islands             
##  [2403] Cook Islands              Cook Islands             
##  [2405] Cook Islands              Cook Islands             
##  [2407] Cook Islands              Cook Islands             
##  [2409] Cook Islands              Cook Islands             
##  [2411] Cook Islands              Cook Islands             
##  [2413] Cook Islands              Cook Islands             
##  [2415] Cook Islands              Cook Islands             
##  [2417] Cook Islands              Cook Islands             
##  [2419] Cook Islands              Cook Islands             
##  [2421] Cook Islands              Cook Islands             
##  [2423] Cook Islands              Cook Islands             
##  [2425] Cook Islands              Cook Islands             
##  [2427] Costa Rica                Costa Rica               
##  [2429] Costa Rica                Costa Rica               
##  [2431] Costa Rica                Costa Rica               
##  [2433] Costa Rica                Costa Rica               
##  [2435] Costa Rica                Costa Rica               
##  [2437] Costa Rica                Costa Rica               
##  [2439] Costa Rica                Costa Rica               
##  [2441] Costa Rica                Costa Rica               
##  [2443] Costa Rica                Costa Rica               
##  [2445] Costa Rica                Costa Rica               
##  [2447] Costa Rica                Costa Rica               
##  [2449] Costa Rica                Costa Rica               
##  [2451] Costa Rica                Costa Rica               
##  [2453] Costa Rica                Costa Rica               
##  [2455] Costa Rica                Costa Rica               
##  [2457] Costa Rica                Costa Rica               
##  [2459] Costa Rica                Costa Rica               
##  [2461] Costa Rica                Costa Rica               
##  [2463] Costa Rica                Costa Rica               
##  [2465] Costa Rica                Costa Rica               
##  [2467] Costa Rica                Costa Rica               
##  [2469] Costa Rica                Costa Rica               
##  [2471] Costa Rica                Croatia                  
##  [2473] Croatia                   Croatia                  
##  [2475] Croatia                   Croatia                  
##  [2477] Croatia                   Croatia                  
##  [2479] Croatia                   Croatia                  
##  [2481] Croatia                   Croatia                  
##  [2483] Croatia                   Croatia                  
##  [2485] Croatia                   Croatia                  
##  [2487] Croatia                   Croatia                  
##  [2489] Croatia                   Croatia                  
##  [2491] Croatia                   Croatia                  
##  [2493] Croatia                   Croatia                  
##  [2495] Croatia                   Croatia                  
##  [2497] Croatia                   Croatia                  
##  [2499] Croatia                   Croatia                  
##  [2501] Croatia                   Croatia                  
##  [2503] Croatia                   Croatia                  
##  [2505] Croatia                   Croatia                  
##  [2507] Croatia                   Croatia                  
##  [2509] Croatia                   Croatia                  
##  [2511] Croatia                   Croatia                  
##  [2513] Croatia                   Croatia                  
##  [2515] Croatia                   Croatia                  
##  [2517] Croatia                   Croatia                  
##  [2519] Croatia                   Croatia                  
##  [2521] Croatia                   Croatia                  
##  [2523] Croatia                   Croatia                  
##  [2525] Croatia                   Croatia                  
##  [2527] Croatia                   Croatia                  
##  [2529] Croatia                   Croatia                  
##  [2531] Croatia                   Croatia                  
##  [2533] Croatia                   Croatia                  
##  [2535] Croatia                   Croatia                  
##  [2537] Croatia                   Croatia                  
##  [2539] Croatia                   Croatia                  
##  [2541] Croatia                   Croatia                  
##  [2543] Croatia                   Croatia                  
##  [2545] Croatia                   Croatia                  
##  [2547] Croatia                   Croatia                  
##  [2549] Croatia                   Croatia                  
##  [2551] Croatia                   Croatia                  
##  [2553] Croatia                   Croatia                  
##  [2555] Croatia                   Croatia                  
##  [2557] Croatia                   Croatia                  
##  [2559] Croatia                   Croatia                  
##  [2561] Croatia                   Croatia                  
##  [2563] Croatia                   Croatia                  
##  [2565] Croatia                   Croatia                  
##  [2567] Croatia                   Croatia                  
##  [2569] Croatia                   Croatia                  
##  [2571] Croatia                   Croatia                  
##  [2573] Croatia                   Croatia                  
##  [2575] Cuba                      Cuba                     
##  [2577] Cuba                      Cuba                     
##  [2579] Cuba                      Cuba                     
##  [2581] Cuba                      Cuba                     
##  [2583] Cuba                      Cuba                     
##  [2585] Cuba                      Cuba                     
##  [2587] Cuba                      Cuba                     
##  [2589] Cuba                      Cuba                     
##  [2591] Cuba                      Cuba                     
##  [2593] Cuba                      Cuba                     
##  [2595] Cuba                      Cuba                     
##  [2597] Cuba                      Cuba                     
##  [2599] Cuba                      Cuba                     
##  [2601] Cuba                      Cuba                     
##  [2603] Cuba                      Cuba                     
##  [2605] Cuba                      Cuba                     
##  [2607] Cuba                      Cuba                     
##  [2609] Cuba                      Cuba                     
##  [2611] Cuba                      Cuba                     
##  [2613] Cuba                      Cuba                     
##  [2615] Cuba                      Cuba                     
##  [2617] Cuba                      Cuba                     
##  [2619] Cuba                      Cuba                     
##  [2621] Cuba                      Cuba                     
##  [2623] Cuba                      Cuba                     
##  [2625] Cuba                      Cuba                     
##  [2627] Cuba                      Cuba                     
##  [2629] Cuba                      Cuba                     
##  [2631] Cuba                      Cuba                     
##  [2633] Cuba                      Cuba                     
##  [2635] Cuba                      Cuba                     
##  [2637] Cuba                      Cuba                     
##  [2639] Cuba                      Cuba                     
##  [2641] Cuba                      Cuba                     
##  [2643] Cuba                      Cuba                     
##  [2645] Cuba                      Cuba                     
##  [2647] Cuba                      Cuba                     
##  [2649] Cuba                      Cuba                     
##  [2651] Cuba                      Cuba                     
##  [2653] Cuba                      Cuba                     
##  [2655] Cuba                      Cuba                     
##  [2657] Cuba                      Cuba                     
##  [2659] Cuba                      Cuba                     
##  [2661] Cuba                      Cuba                     
##  [2663] Cuba                      Cuba                     
##  [2665] Cuba                      Cuba                     
##  [2667] Cuba                      Cuba                     
##  [2669] Cuba                      Cuba                     
##  [2671] Cuba                      Cuba                     
##  [2673] Cuba                      Cuba                     
##  [2675] Cuba                      Cuba                     
##  [2677] Cuba                      Cuba                     
##  [2679] Cuba                      Cuba                     
##  [2681] Cuba                      Cuba                     
##  [2683] Cuba                      Cuba                     
##  [2685] Cuba                      Cuba                     
##  [2687] Cuba                      Cuba                     
##  [2689] Cuba                      Cuba                     
##  [2691] Cuba                      Cuba                     
##  [2693] Cuba                      Cuba                     
##  [2695] Cuba                      Cuba                     
##  [2697] Cuba                      Cuba                     
##  [2699] Cuba                      Cuba                     
##  [2701] Cuba                      Cuba                     
##  [2703] Cuba                      Cuba                     
##  [2705] Cuba                      Cuba                     
##  [2707] Cuba                      Cuba                     
##  [2709] Cuba                      Cuba                     
##  [2711] Cuba                      Cuba                     
##  [2713] Cuba                      Cuba                     
##  [2715] Cuba                      Cuba                     
##  [2717] Cuba                      Cuba                     
##  [2719] Cuba                      Cuba                     
##  [2721] Cuba                      Cuba                     
##  [2723] Cuba                      Cuba                     
##  [2725] Cuba                      Cuba                     
##  [2727] Cuba                      Cuba                     
##  [2729] Cuba                      Cuba                     
##  [2731] Cuba                      Cuba                     
##  [2733] Cuba                      Cuba                     
##  [2735] Cuba                      Cuba                     
##  [2737] Cura<e7>ao                Cura<e7>ao               
##  [2739] Cura<e7>ao                Cura<e7>ao               
##  [2741] Cura<e7>ao                Cura<e7>ao               
##  [2743] Cura<e7>ao                Cura<e7>ao               
##  [2745] Cura<e7>ao                Cyprus                   
##  [2747] Cyprus                    Cyprus                   
##  [2749] Cyprus                    Cyprus                   
##  [2751] Cyprus                    Cyprus                   
##  [2753] Cyprus                    Cyprus                   
##  [2755] Cyprus                    Cyprus                   
##  [2757] Cyprus                    Cyprus                   
##  [2759] Cyprus                    Cyprus                   
##  [2761] Cyprus                    Cyprus                   
##  [2763] Cyprus                    Cyprus                   
##  [2765] Cyprus                    Cyprus                   
##  [2767] Cyprus                    Cyprus                   
##  [2769] Cyprus                    Cyprus                   
##  [2771] Cyprus                    Cyprus                   
##  [2773] Cyprus                    Cyprus                   
##  [2775] Cyprus                    Cyprus                   
##  [2777] Cyprus                    Cyprus                   
##  [2779] Cyprus                    Cyprus                   
##  [2781] Cyprus                    Cyprus                   
##  [2783] Cyprus                    Cyprus                   
##  [2785] Cyprus                    Cyprus                   
##  [2787] Cyprus                    Cyprus                   
##  [2789] Cyprus                    Cyprus                   
##  [2791] Cyprus                    Cyprus                   
##  [2793] Cyprus                    Cyprus                   
##  [2795] Cyprus                    Cyprus                   
##  [2797] Cyprus                    Cyprus                   
##  [2799] Cyprus                    Cyprus                   
##  [2801] Cyprus                    Cyprus                   
##  [2803] Cyprus                    Cyprus                   
##  [2805] Cyprus                    Cyprus                   
##  [2807] Cyprus                    Cyprus                   
##  [2809] Cyprus                    Cyprus                   
##  [2811] Cyprus                    Cyprus                   
##  [2813] Cyprus                    Cyprus                   
##  [2815] Cyprus                    Cyprus                   
##  [2817] Cyprus                    Cyprus                   
##  [2819] Cyprus                    Cyprus                   
##  [2821] Cyprus                    Cyprus                   
##  [2823] Cyprus                    Cyprus                   
##  [2825] Cyprus                    Cyprus                   
##  [2827] Cyprus                    Cyprus                   
##  [2829] Cyprus                    Cyprus                   
##  [2831] Cyprus                    Cyprus                   
##  [2833] Cyprus                    Cyprus                   
##  [2835] Cyprus                    Cyprus                   
##  [2837] Cyprus                    Cyprus                   
##  [2839] Cyprus                    Cyprus                   
##  [2841] Cyprus                    C<f4>te d'Ivoire         
##  [2843] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2845] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2847] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2849] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2851] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2853] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2855] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2857] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2859] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2861] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2863] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2865] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2867] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2869] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2871] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2873] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2875] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2877] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2879] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2881] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2883] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2885] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2887] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2889] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2891] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2893] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2895] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2897] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2899] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2901] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2903] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2905] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2907] C<f4>te d'Ivoire          C<f4>te d'Ivoire         
##  [2909] Denmark                   Denmark                  
##  [2911] Denmark                   Denmark                  
##  [2913] Denmark                   Denmark                  
##  [2915] Denmark                   Denmark                  
##  [2917] Denmark                   Denmark                  
##  [2919] Denmark                   Denmark                  
##  [2921] Denmark                   Denmark                  
##  [2923] Denmark                   Denmark                  
##  [2925] Denmark                   Denmark                  
##  [2927] Denmark                   Denmark                  
##  [2929] Denmark                   Denmark                  
##  [2931] Denmark                   Denmark                  
##  [2933] Denmark                   Denmark                  
##  [2935] Denmark                   Denmark                  
##  [2937] Denmark                   Denmark                  
##  [2939] Denmark                   Denmark                  
##  [2941] Denmark                   Denmark                  
##  [2943] Denmark                   Denmark                  
##  [2945] Denmark                   Denmark                  
##  [2947] Denmark                   Denmark                  
##  [2949] Denmark                   Denmark                  
##  [2951] Denmark                   Denmark                  
##  [2953] Denmark                   Denmark                  
##  [2955] Denmark                   Denmark                  
##  [2957] Denmark                   Denmark                  
##  [2959] Denmark                   Denmark                  
##  [2961] Denmark                   Denmark                  
##  [2963] Denmark                   Denmark                  
##  [2965] Denmark                   Denmark                  
##  [2967] Denmark                   Denmark                  
##  [2969] Denmark                   Denmark                  
##  [2971] Denmark                   Denmark                  
##  [2973] Denmark                   Denmark                  
##  [2975] Denmark                   Denmark                  
##  [2977] Denmark                   Denmark                  
##  [2979] Denmark                   Denmark                  
##  [2981] Denmark                   Denmark                  
##  [2983] Denmark                   Denmark                  
##  [2985] Denmark                   Denmark                  
##  [2987] Denmark                   Denmark                  
##  [2989] Denmark                   Denmark                  
##  [2991] Denmark                   Denmark                  
##  [2993] Denmark                   Denmark                  
##  [2995] Denmark                   Denmark                  
##  [2997] Denmark                   Denmark                  
##  [2999] Denmark                   Denmark                  
##  [3001] Denmark                   Denmark                  
##  [3003] Denmark                   Denmark                  
##  [3005] Denmark                   Denmark                  
##  [3007] Denmark                   Denmark                  
##  [3009] Denmark                   Denmark                  
##  [3011] Denmark                   Djibouti                 
##  [3013] Djibouti                  Djibouti                 
##  [3015] Djibouti                  Djibouti                 
##  [3017] Djibouti                  Djibouti                 
##  [3019] Djibouti                  Djibouti                 
##  [3021] Djibouti                  Djibouti                 
##  [3023] Djibouti                  Djibouti                 
##  [3025] Djibouti                  Dominica                 
##  [3027] Dominica                  Dominica                 
##  [3029] Dominica                  Dominica                 
##  [3031] Dominica                  Dominica                 
##  [3033] Dominica                  Dominica                 
##  [3035] Dominica                  Dominica                 
##  [3037] Dominica                  Dominica                 
##  [3039] Dominican Republic        Dominican Republic       
##  [3041] Dominican Republic        Dominican Republic       
##  [3043] Dominican Republic        Dominican Republic       
##  [3045] Dominican Republic        Dominican Republic       
##  [3047] Dominican Republic        Dominican Republic       
##  [3049] Dominican Republic        Dominican Republic       
##  [3051] Dominican Republic        Dominican Republic       
##  [3053] Dominican Republic        Dominican Republic       
##  [3055] Dominican Republic        Dominican Republic       
##  [3057] Dominican Republic        Dominican Republic       
##  [3059] Dominican Republic        Dominican Republic       
##  [3061] Dominican Republic        Dominican Republic       
##  [3063] Dominican Republic        Dominican Republic       
##  [3065] Dominican Republic        Dominican Republic       
##  [3067] Dominican Republic        Dominican Republic       
##  [3069] Dominican Republic        Dominican Republic       
##  [3071] Dominican Republic        Dominican Republic       
##  [3073] Dominican Republic        Dominican Republic       
##  [3075] Dominican Republic        Dominican Republic       
##  [3077] Dominican Republic        Dominican Republic       
##  [3079] Dominican Republic        Dominican Republic       
##  [3081] Dominican Republic        Dominican Republic       
##  [3083] Dominican Republic        Dominican Republic       
##  [3085] Dominican Republic        Dominican Republic       
##  [3087] Dominican Republic        Dominican Republic       
##  [3089] Ecuador                   Ecuador                  
##  [3091] Ecuador                   Ecuador                  
##  [3093] Ecuador                   Ecuador                  
##  [3095] Ecuador                   Ecuador                  
##  [3097] Ecuador                   Ecuador                  
##  [3099] Ecuador                   Ecuador                  
##  [3101] Ecuador                   Ecuador                  
##  [3103] Ecuador                   Ecuador                  
##  [3105] Ecuador                   Ecuador                  
##  [3107] Ecuador                   Ecuador                  
##  [3109] Ecuador                   Ecuador                  
##  [3111] Ecuador                   Ecuador                  
##  [3113] Ecuador                   Ecuador                  
##  [3115] Ecuador                   Ecuador                  
##  [3117] Ecuador                   Ecuador                  
##  [3119] Ecuador                   Ecuador                  
##  [3121] Ecuador                   Ecuador                  
##  [3123] Ecuador                   Ecuador                  
##  [3125] Ecuador                   Ecuador                  
##  [3127] Ecuador                   Ecuador                  
##  [3129] Ecuador                   Ecuador                  
##  [3131] Ecuador                   Ecuador                  
##  [3133] Ecuador                   Ecuador                  
##  [3135] Ecuador                   Ecuador                  
##  [3137] Ecuador                   Ecuador                  
##  [3139] Ecuador                   Ecuador                  
##  [3141] Ecuador                   Ecuador                  
##  [3143] Ecuador                   Ecuador                  
##  [3145] Ecuador                   Ecuador                  
##  [3147] Ecuador                   Ecuador                  
##  [3149] Ecuador                   Ecuador                  
##  [3151] Ecuador                   Ecuador                  
##  [3153] Ecuador                   Ecuador                  
##  [3155] Ecuador                   Ecuador                  
##  [3157] Ecuador                   Ecuador                  
##  [3159] Ecuador                   Ecuador                  
##  [3161] Ecuador                   Ecuador                  
##  [3163] Ecuador                   Ecuador                  
##  [3165] Ecuador                   Ecuador                  
##  [3167] Ecuador                   Ecuador                  
##  [3169] Ecuador                   Ecuador                  
##  [3171] Ecuador                   Ecuador                  
##  [3173] Ecuador                   Ecuador                  
##  [3175] Ecuador                   Ecuador                  
##  [3177] Ecuador                   Ecuador                  
##  [3179] Ecuador                   Ecuador                  
##  [3181] Ecuador                   Ecuador                  
##  [3183] Ecuador                   Ecuador                  
##  [3185] Ecuador                   Ecuador                  
##  [3187] Ecuador                   Ecuador                  
##  [3189] Egypt                     Egypt                    
##  [3191] Egypt                     Egypt                    
##  [3193] Egypt                     Egypt                    
##  [3195] Egypt                     Egypt                    
##  [3197] Egypt                     Egypt                    
##  [3199] Egypt                     Egypt                    
##  [3201] Egypt                     Egypt                    
##  [3203] Egypt                     Egypt                    
##  [3205] Egypt                     Egypt                    
##  [3207] Egypt                     Egypt                    
##  [3209] Egypt                     Egypt                    
##  [3211] Egypt                     Egypt                    
##  [3213] Egypt                     Egypt                    
##  [3215] Egypt                     Egypt                    
##  [3217] Egypt                     Egypt                    
##  [3219] Egypt                     Egypt                    
##  [3221] Egypt                     Egypt                    
##  [3223] Egypt                     Egypt                    
##  [3225] Egypt                     Egypt                    
##  [3227] Egypt                     Egypt                    
##  [3229] Egypt                     Egypt                    
##  [3231] Egypt                     Egypt                    
##  [3233] Egypt                     Egypt                    
##  [3235] Egypt                     Egypt                    
##  [3237] Egypt                     Egypt                    
##  [3239] Egypt                     Egypt                    
##  [3241] Egypt                     Egypt                    
##  [3243] Egypt                     Egypt                    
##  [3245] Egypt                     Egypt                    
##  [3247] Egypt                     Egypt                    
##  [3249] Egypt                     Egypt                    
##  [3251] Egypt                     Egypt                    
##  [3253] Egypt                     Egypt                    
##  [3255] Egypt                     Egypt                    
##  [3257] Egypt                     Egypt                    
##  [3259] Egypt                     Egypt                    
##  [3261] Egypt                     Egypt                    
##  [3263] Egypt                     Egypt                    
##  [3265] Egypt                     Egypt                    
##  [3267] Egypt                     Egypt                    
##  [3269] Egypt                     Egypt                    
##  [3271] Egypt                     Egypt                    
##  [3273] Egypt                     Egypt                    
##  [3275] Egypt                     El Salvador              
##  [3277] El Salvador               El Salvador              
##  [3279] El Salvador               El Salvador              
##  [3281] El Salvador               El Salvador              
##  [3283] El Salvador               El Salvador              
##  [3285] El Salvador               El Salvador              
##  [3287] El Salvador               El Salvador              
##  [3289] El Salvador               El Salvador              
##  [3291] El Salvador               El Salvador              
##  [3293] El Salvador               El Salvador              
##  [3295] El Salvador               El Salvador              
##  [3297] El Salvador               El Salvador              
##  [3299] El Salvador               El Salvador              
##  [3301] Equatorial Guinea         Equatorial Guinea        
##  [3303] Equatorial Guinea         Equatorial Guinea        
##  [3305] Equatorial Guinea         Equatorial Guinea        
##  [3307] Equatorial Guinea         Equatorial Guinea        
##  [3309] Equatorial Guinea         Equatorial Guinea        
##  [3311] Equatorial Guinea         Equatorial Guinea        
##  [3313] Equatorial Guinea         Equatorial Guinea        
##  [3315] Equatorial Guinea         Eritrea                  
##  [3317] Eritrea                   Eritrea                  
##  [3319] Eritrea                   Eritrea                  
##  [3321] Eritrea                   Eritrea                  
##  [3323] Eritrea                   Eritrea                  
##  [3325] Eritrea                   Eritrea                  
##  [3327] Eritrea                   Eritrea                  
##  [3329] Eritrea                   Eritrea                  
##  [3331] Eritrea                   Eritrea                  
##  [3333] Eritrea                   Eritrea                  
##  [3335] Eritrea                   Eritrea                  
##  [3337] Eritrea                   Eritrea                  
##  [3339] Eritrea                   Eritrea                  
##  [3341] Eritrea                   Eritrea                  
##  [3343] Eritrea                   Eritrea                  
##  [3345] Eritrea                   Eritrea                  
##  [3347] Eritrea                   Eritrea                  
##  [3349] Eritrea                   Eritrea                  
##  [3351] Eritrea                   Eritrea                  
##  [3353] Eritrea                   Eritrea                  
##  [3355] Eritrea                   Eritrea                  
##  [3357] Eritrea                   Eritrea                  
##  [3359] Eritrea                   Eritrea                  
##  [3361] Eritrea                   Eritrea                  
##  [3363] Eritrea                   Eritrea                  
##  [3365] Estonia                   Estonia                  
##  [3367] Estonia                   Estonia                  
##  [3369] Estonia                   Estonia                  
##  [3371] Estonia                   Estonia                  
##  [3373] Estonia                   Estonia                  
##  [3375] Estonia                   Estonia                  
##  [3377] Estonia                   Estonia                  
##  [3379] Estonia                   Estonia                  
##  [3381] Estonia                   Estonia                  
##  [3383] Estonia                   Estonia                  
##  [3385] Estonia                   Estonia                  
##  [3387] Estonia                   Estonia                  
##  [3389] Estonia                   Estonia                  
##  [3391] Estonia                   Estonia                  
##  [3393] Estonia                   Estonia                  
##  [3395] Estonia                   Estonia                  
##  [3397] Estonia                   Estonia                  
##  [3399] Estonia                   Estonia                  
##  [3401] Estonia                   Estonia                  
##  [3403] Estonia                   Estonia                  
##  [3405] Estonia                   Estonia                  
##  [3407] Estonia                   Estonia                  
##  [3409] Estonia                   Estonia                  
##  [3411] Estonia                   Estonia                  
##  [3413] Estonia                   Estonia                  
##  [3415] Estonia                   Estonia                  
##  [3417] Estonia                   Estonia                  
##  [3419] Estonia                   Estonia                  
##  [3421] Estonia                   Estonia                  
##  [3423] Estonia                   Estonia                  
##  [3425] Estonia                   Estonia                  
##  [3427] Estonia                   Estonia                  
##  [3429] Estonia                   Estonia                  
##  [3431] Estonia                   Estonia                  
##  [3433] Estonia                   Estonia                  
##  [3435] Estonia                   Estonia                  
##  [3437] Estonia                   Estonia                  
##  [3439] Estonia                   Estonia                  
##  [3441] Estonia                   Estonia                  
##  [3443] Estonia                   Estonia                  
##  [3445] Estonia                   Estonia                  
##  [3447] Estonia                   Estonia                  
##  [3449] Estonia                   Estonia                  
##  [3451] Estonia                   Estonia                  
##  [3453] Estonia                   Estonia                  
##  [3455] Estonia                   Estonia                  
##  [3457] Estonia                   Estonia                  
##  [3459] Estonia                   Estonia                  
##  [3461] Estonia                   Estonia                  
##  [3463] Estonia                   Estonia                  
##  [3465] Estonia                   Estonia                  
##  [3467] Estonia                   Estonia                  
##  [3469] Estonia                   Estonia                  
##  [3471] Estonia                   Estonia                  
##  [3473] Estonia                   Estonia                  
##  [3475] Estonia                   Estonia                  
##  [3477] Estonia                   Estonia                  
##  [3479] Estonia                   Estonia                  
##  [3481] Estonia                   Estonia                  
##  [3483] Estonia                   Estonia                  
##  [3485] Estonia                   Estonia                  
##  [3487] Estonia                   Estonia                  
##  [3489] Estonia                   Estonia                  
##  [3491] Estonia                   Estonia                  
##  [3493] Estonia                   Estonia                  
##  [3495] Estonia                   Estonia                  
##  [3497] Estonia                   Estonia                  
##  [3499] Estonia                   Estonia                  
##  [3501] Estonia                   Estonia                  
##  [3503] Estonia                   Estonia                  
##  [3505] Estonia                   Estonia                  
##  [3507] Estonia                   Estonia                  
##  [3509] Estonia                   Estonia                  
##  [3511] Estonia                   Estonia                  
##  [3513] Estonia                   Estonia                  
##  [3515] Estonia                   Estonia                  
##  [3517] Estonia                   Estonia                  
##  [3519] Estonia                   Estonia                  
##  [3521] Estonia                   Estonia                  
##  [3523] Estonia                   Estonia                  
##  [3525] Estonia                   Estonia                  
##  [3527] Estonia                   Estonia                  
##  [3529] Estonia                   Estonia                  
##  [3531] Estonia                   Estonia                  
##  [3533] Estonia                   Estonia                  
##  [3535] Estonia                   Estonia                  
##  [3537] Estonia                   Estonia                  
##  [3539] Estonia                   Estonia                  
##  [3541] Estonia                   Estonia                  
##  [3543] Estonia                   Estonia                  
##  [3545] Estonia                   Estonia                  
##  [3547] Estonia                   Estonia                  
##  [3549] Ethiopia                  Ethiopia                 
##  [3551] Ethiopia                  Ethiopia                 
##  [3553] Ethiopia                  Falkland Is.(Malvinas)   
##  [3555] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3557] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3559] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3561] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3563] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3565] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3567] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3569] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3571] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3573] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3575] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3577] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3579] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3581] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3583] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3585] Falkland Is.(Malvinas)    Falkland Is.(Malvinas)   
##  [3587] Faroe Islands             Faroe Islands            
##  [3589] Faroe Islands             Faroe Islands            
##  [3591] Faroe Islands             Faroe Islands            
##  [3593] Faroe Islands             Faroe Islands            
##  [3595] Faroe Islands             Faroe Islands            
##  [3597] Faroe Islands             Faroe Islands            
##  [3599] Faroe Islands             Faroe Islands            
##  [3601] Faroe Islands             Faroe Islands            
##  [3603] Faroe Islands             Faroe Islands            
##  [3605] Faroe Islands             Faroe Islands            
##  [3607] Faroe Islands             Faroe Islands            
##  [3609] Faroe Islands             Faroe Islands            
##  [3611] Faroe Islands             Faroe Islands            
##  [3613] Faroe Islands             Faroe Islands            
##  [3615] Faroe Islands             Faroe Islands            
##  [3617] Faroe Islands             Faroe Islands            
##  [3619] Faroe Islands             Faroe Islands            
##  [3621] Faroe Islands             Faroe Islands            
##  [3623] Faroe Islands             Faroe Islands            
##  [3625] Faroe Islands             Faroe Islands            
##  [3627] Faroe Islands             Faroe Islands            
##  [3629] Faroe Islands             Faroe Islands            
##  [3631] Faroe Islands             Faroe Islands            
##  [3633] Faroe Islands             Faroe Islands            
##  [3635] Faroe Islands             Faroe Islands            
##  [3637] Faroe Islands             Faroe Islands            
##  [3639] Faroe Islands             Faroe Islands            
##  [3641] Faroe Islands             Faroe Islands            
##  [3643] Faroe Islands             Faroe Islands            
##  [3645] Faroe Islands             Faroe Islands            
##  [3647] Faroe Islands             Faroe Islands            
##  [3649] Faroe Islands             Faroe Islands            
##  [3651] Faroe Islands             Faroe Islands            
##  [3653] Faroe Islands             Faroe Islands            
##  [3655] Faroe Islands             Faroe Islands            
##  [3657] Faroe Islands             Faroe Islands            
##  [3659] Faroe Islands             Faroe Islands            
##  [3661] Faroe Islands             Faroe Islands            
##  [3663] Faroe Islands             Faroe Islands            
##  [3665] Faroe Islands             Faroe Islands            
##  [3667] Faroe Islands             Faroe Islands            
##  [3669] Faroe Islands             Faroe Islands            
##  [3671] Faroe Islands             Faroe Islands            
##  [3673] Faroe Islands             Faroe Islands            
##  [3675] Faroe Islands             Faroe Islands            
##  [3677] Faroe Islands             Faroe Islands            
##  [3679] Faroe Islands             Faroe Islands            
##  [3681] Faroe Islands             Faroe Islands            
##  [3683] Fiji, Republic of         Fiji, Republic of        
##  [3685] Fiji, Republic of         Fiji, Republic of        
##  [3687] Fiji, Republic of         Fiji, Republic of        
##  [3689] Fiji, Republic of         Fiji, Republic of        
##  [3691] Fiji, Republic of         Fiji, Republic of        
##  [3693] Fiji, Republic of         Fiji, Republic of        
##  [3695] Fiji, Republic of         Fiji, Republic of        
##  [3697] Fiji, Republic of         Fiji, Republic of        
##  [3699] Fiji, Republic of         Fiji, Republic of        
##  [3701] Fiji, Republic of         Fiji, Republic of        
##  [3703] Fiji, Republic of         Fiji, Republic of        
##  [3705] Fiji, Republic of         Fiji, Republic of        
##  [3707] Fiji, Republic of         Fiji, Republic of        
##  [3709] Fiji, Republic of         Fiji, Republic of        
##  [3711] Fiji, Republic of         Fiji, Republic of        
##  [3713] Fiji, Republic of         Fiji, Republic of        
##  [3715] Fiji, Republic of         Fiji, Republic of        
##  [3717] Fiji, Republic of         Fiji, Republic of        
##  [3719] Fiji, Republic of         Fiji, Republic of        
##  [3721] Fiji, Republic of         Fiji, Republic of        
##  [3723] Fiji, Republic of         Fiji, Republic of        
##  [3725] Fiji, Republic of         Fiji, Republic of        
##  [3727] Fiji, Republic of         Fiji, Republic of        
##  [3729] Fiji, Republic of         Fiji, Republic of        
##  [3731] Fiji, Republic of         Fiji, Republic of        
##  [3733] Finland                   Finland                  
##  [3735] Finland                   Finland                  
##  [3737] Finland                   Finland                  
##  [3739] Finland                   Finland                  
##  [3741] Finland                   Finland                  
##  [3743] Finland                   Finland                  
##  [3745] Finland                   Finland                  
##  [3747] Finland                   Finland                  
##  [3749] France                    France                   
##  [3751] France                    France                   
##  [3753] France                    France                   
##  [3755] France                    France                   
##  [3757] France                    France                   
##  [3759] France                    France                   
##  [3761] France                    France                   
##  [3763] France                    France                   
##  [3765] France                    France                   
##  [3767] France                    France                   
##  [3769] France                    France                   
##  [3771] France                    France                   
##  [3773] France                    France                   
##  [3775] France                    France                   
##  [3777] France                    France                   
##  [3779] France                    France                   
##  [3781] France                    France                   
##  [3783] France                    France                   
##  [3785] France                    France                   
##  [3787] France                    France                   
##  [3789] France                    France                   
##  [3791] France                    France                   
##  [3793] France                    France                   
##  [3795] France                    France                   
##  [3797] France                    France                   
##  [3799] France                    France                   
##  [3801] France                    France                   
##  [3803] France                    France                   
##  [3805] France                    France                   
##  [3807] France                    France                   
##  [3809] France                    France                   
##  [3811] France                    France                   
##  [3813] France                    France                   
##  [3815] France                    France                   
##  [3817] France                    France                   
##  [3819] France                    France                   
##  [3821] France                    France                   
##  [3823] France                    France                   
##  [3825] France                    France                   
##  [3827] France                    France                   
##  [3829] France                    France                   
##  [3831] France                    France                   
##  [3833] France                    France                   
##  [3835] France                    France                   
##  [3837] France                    France                   
##  [3839] France                    France                   
##  [3841] France                    France                   
##  [3843] France                    France                   
##  [3845] France                    France                   
##  [3847] France                    France                   
##  [3849] France                    France                   
##  [3851] France                    France                   
##  [3853] France                    France                   
##  [3855] France                    France                   
##  [3857] France                    France                   
##  [3859] France                    France                   
##  [3861] France                    France                   
##  [3863] France                    France                   
##  [3865] France                    France                   
##  [3867] France                    France                   
##  [3869] France                    France                   
##  [3871] France                    France                   
##  [3873] France                    France                   
##  [3875] France                    France                   
##  [3877] France                    France                   
##  [3879] France                    France                   
##  [3881] France                    France                   
##  [3883] France                    France                   
##  [3885] France                    France                   
##  [3887] France                    France                   
##  [3889] France                    France                   
##  [3891] France                    France                   
##  [3893] France                    France                   
##  [3895] France                    France                   
##  [3897] France                    France                   
##  [3899] France                    France                   
##  [3901] France                    France                   
##  [3903] France                    France                   
##  [3905] France                    France                   
##  [3907] France                    France                   
##  [3909] France                    France                   
##  [3911] France                    France                   
##  [3913] France                    France                   
##  [3915] France                    France                   
##  [3917] France                    France                   
##  [3919] France                    France                   
##  [3921] France                    France                   
##  [3923] France                    France                   
##  [3925] France                    France                   
##  [3927] France                    France                   
##  [3929] France                    France                   
##  [3931] France                    France                   
##  [3933] France                    France                   
##  [3935] France                    France                   
##  [3937] France                    France                   
##  [3939] France                    France                   
##  [3941] France                    France                   
##  [3943] France                    France                   
##  [3945] France                    France                   
##  [3947] France                    France                   
##  [3949] France                    France                   
##  [3951] France                    France                   
##  [3953] France                    France                   
##  [3955] France                    France                   
##  [3957] France                    France                   
##  [3959] France                    France                   
##  [3961] France                    France                   
##  [3963] France                    France                   
##  [3965] France                    France                   
##  [3967] France                    France                   
##  [3969] France                    France                   
##  [3971] France                    France                   
##  [3973] France                    France                   
##  [3975] France                    France                   
##  [3977] France                    France                   
##  [3979] France                    France                   
##  [3981] France                    France                   
##  [3983] France                    France                   
##  [3985] France                    France                   
##  [3987] France                    France                   
##  [3989] France                    France                   
##  [3991] France                    France                   
##  [3993] France                    France                   
##  [3995] France                    France                   
##  [3997] France                    France                   
##  [3999] France                    France                   
##  [4001] France                    France                   
##  [4003] France                    France                   
##  [4005] France                    France                   
##  [4007] France                    France                   
##  [4009] France                    France                   
##  [4011] France                    France                   
##  [4013] France                    France                   
##  [4015] France                    France                   
##  [4017] France                    France                   
##  [4019] France                    France                   
##  [4021] France                    France                   
##  [4023] France                    France                   
##  [4025] France                    France                   
##  [4027] France                    France                   
##  [4029] France                    France                   
##  [4031] France                    France                   
##  [4033] France                    France                   
##  [4035] France                    France                   
##  [4037] France                    France                   
##  [4039] France                    France                   
##  [4041] France                    France                   
##  [4043] France                    France                   
##  [4045] France                    France                   
##  [4047] France                    France                   
##  [4049] France                    France                   
##  [4051] France                    France                   
##  [4053] France                    France                   
##  [4055] France                    France                   
##  [4057] France                    France                   
##  [4059] France                    France                   
##  [4061] France                    France                   
##  [4063] France                    France                   
##  [4065] France                    France                   
##  [4067] France                    France                   
##  [4069] France                    France                   
##  [4071] France                    France                   
##  [4073] France                    France                   
##  [4075] France                    France                   
##  [4077] France                    France                   
##  [4079] France                    France                   
##  [4081] France                    France                   
##  [4083] France                    France                   
##  [4085] France                    France                   
##  [4087] France                    France                   
##  [4089] France                    France                   
##  [4091] France                    France                   
##  [4093] France                    France                   
##  [4095] France                    France                   
##  [4097] France                    France                   
##  [4099] France                    France                   
##  [4101] France                    France                   
##  [4103] France                    France                   
##  [4105] France                    France                   
##  [4107] France                    France                   
##  [4109] France                    France                   
##  [4111] France                    France                   
##  [4113] France                    France                   
##  [4115] France                    France                   
##  [4117] France                    France                   
##  [4119] France                    France                   
##  [4121] France                    France                   
##  [4123] France                    France                   
##  [4125] France                    France                   
##  [4127] France                    France                   
##  [4129] France                    France                   
##  [4131] France                    France                   
##  [4133] France                    France                   
##  [4135] France                    France                   
##  [4137] France                    France                   
##  [4139] France                    France                   
##  [4141] France                    France                   
##  [4143] France                    France                   
##  [4145] France                    France                   
##  [4147] France                    France                   
##  [4149] France                    France                   
##  [4151] France                    France                   
##  [4153] France                    France                   
##  [4155] France                    France                   
##  [4157] France                    France                   
##  [4159] France                    France                   
##  [4161] France                    France                   
##  [4163] France                    France                   
##  [4165] France                    France                   
##  [4167] France                    France                   
##  [4169] France                    France                   
##  [4171] France                    France                   
##  [4173] France                    France                   
##  [4175] France                    France                   
##  [4177] France                    France                   
##  [4179] France                    France                   
##  [4181] France                    France                   
##  [4183] France                    France                   
##  [4185] France                    France                   
##  [4187] France                    France                   
##  [4189] France                    France                   
##  [4191] France                    France                   
##  [4193] France                    France                   
##  [4195] France                    France                   
##  [4197] France                    France                   
##  [4199] France                    France                   
##  [4201] France                    France                   
##  [4203] France                    France                   
##  [4205] France                    France                   
##  [4207] France                    France                   
##  [4209] France                    France                   
##  [4211] France                    France                   
##  [4213] France                    France                   
##  [4215] France                    France                   
##  [4217] France                    France                   
##  [4219] France                    France                   
##  [4221] France                    France                   
##  [4223] France                    France                   
##  [4225] France                    France                   
##  [4227] France                    France                   
##  [4229] France                    France                   
##  [4231] France                    France                   
##  [4233] France                    France                   
##  [4235] France                    France                   
##  [4237] France                    French Guiana            
##  [4239] French Guiana             French Guiana            
##  [4241] French Guiana             French Guiana            
##  [4243] French Guiana             French Guiana            
##  [4245] French Guiana             French Guiana            
##  [4247] French Guiana             French Guiana            
##  [4249] French Guiana             French Guiana            
##  [4251] French Guiana             French Guiana            
##  [4253] French Guiana             French Guiana            
##  [4255] French Guiana             French Polynesia         
##  [4257] French Polynesia          French Polynesia         
##  [4259] French Polynesia          French Polynesia         
##  [4261] French Polynesia          French Polynesia         
##  [4263] French Polynesia          French Polynesia         
##  [4265] French Polynesia          French Polynesia         
##  [4267] French Polynesia          French Polynesia         
##  [4269] French Polynesia          French Polynesia         
##  [4271] French Polynesia          French Polynesia         
##  [4273] French Polynesia          French Polynesia         
##  [4275] French Polynesia          French Polynesia         
##  [4277] French Polynesia          French Polynesia         
##  [4279] French Polynesia          French Polynesia         
##  [4281] French Polynesia          French Polynesia         
##  [4283] French Polynesia          French Polynesia         
##  [4285] French Polynesia          French Polynesia         
##  [4287] French Southern Terr      French Southern Terr     
##  [4289] French Southern Terr      Gabon                    
##  [4291] Gabon                     Gabon                    
##  [4293] Gabon                     Gabon                    
##  [4295] Gabon                     Gabon                    
##  [4297] Gabon                     Gabon                    
##  [4299] Gabon                     Gabon                    
##  [4301] Gabon                     Gabon                    
##  [4303] Gabon                     Gabon                    
##  [4305] Gabon                     Gabon                    
##  [4307] Gabon                     Gabon                    
##  [4309] Gabon                     Gabon                    
##  [4311] Gabon                     Gabon                    
##  [4313] Gabon                     Gabon                    
##  [4315] Gabon                     Gabon                    
##  [4317] Gabon                     Gabon                    
##  [4319] Gabon                     Gabon                    
##  [4321] Gabon                     Gabon                    
##  [4323] Gabon                     Gabon                    
##  [4325] Gabon                     Gabon                    
##  [4327] Gabon                     Gabon                    
##  [4329] Gabon                     Gabon                    
##  [4331] Gabon                     Gabon                    
##  [4333] Gabon                     Gabon                    
##  [4335] Gambia                    Gambia                   
##  [4337] Gambia                    Gambia                   
##  [4339] Gambia                    Gambia                   
##  [4341] Gambia                    Gambia                   
##  [4343] Gambia                    Gambia                   
##  [4345] Gambia                    Gambia                   
##  [4347] Gambia                    Gambia                   
##  [4349] Gambia                    Gambia                   
##  [4351] Gambia                    Gambia                   
##  [4353] Gambia                    Gambia                   
##  [4355] Gambia                    Gambia                   
##  [4357] Gambia                    Gambia                   
##  [4359] Gambia                    Gambia                   
##  [4361] Gambia                    Gambia                   
##  [4363] Gambia                    Gambia                   
##  [4365] Gambia                    Gambia                   
##  [4367] Gambia                    Gambia                   
##  [4369] Gambia                    Gambia                   
##  [4371] Gambia                    Gambia                   
##  [4373] Gambia                    Gambia                   
##  [4375] Gambia                    Gambia                   
##  [4377] Gambia                    Gambia                   
##  [4379] Gambia                    Gambia                   
##  [4381] Gambia                    Gambia                   
##  [4383] Gambia                    Georgia                  
##  [4385] Georgia                   Georgia                  
##  [4387] Georgia                   Georgia                  
##  [4389] Georgia                   Georgia                  
##  [4391] Georgia                   Georgia                  
##  [4393] Georgia                   Georgia                  
##  [4395] Georgia                   Georgia                  
##  [4397] Georgia                   Georgia                  
##  [4399] Georgia                   Georgia                  
##  [4401] Georgia                   Georgia                  
##  [4403] Georgia                   Georgia                  
##  [4405] Georgia                   Georgia                  
##  [4407] Georgia                   Georgia                  
##  [4409] Georgia                   Georgia                  
##  [4411] Georgia                   Georgia                  
##  [4413] Georgia                   Georgia                  
##  [4415] Georgia                   Georgia                  
##  [4417] Georgia                   Georgia                  
##  [4419] Georgia                   Georgia                  
##  [4421] Georgia                   Georgia                  
##  [4423] Georgia                   Georgia                  
##  [4425] Georgia                   Georgia                  
##  [4427] Georgia                   Georgia                  
##  [4429] Georgia                   Georgia                  
##  [4431] Georgia                   Georgia                  
##  [4433] Georgia                   Georgia                  
##  [4435] Georgia                   Georgia                  
##  [4437] Georgia                   Georgia                  
##  [4439] Georgia                   Georgia                  
##  [4441] Georgia                   Georgia                  
##  [4443] Georgia                   Georgia                  
##  [4445] Georgia                   Georgia                  
##  [4447] Georgia                   Georgia                  
##  [4449] Georgia                   Georgia                  
##  [4451] Georgia                   Georgia                  
##  [4453] Georgia                   Georgia                  
##  [4455] Georgia                   Georgia                  
##  [4457] Georgia                   Georgia                  
##  [4459] Georgia                   Georgia                  
##  [4461] Georgia                   Georgia                  
##  [4463] Georgia                   Georgia                  
##  [4465] Georgia                   Georgia                  
##  [4467] Georgia                   Georgia                  
##  [4469] Georgia                   Germany                  
##  [4471] Germany                   Germany                  
##  [4473] Germany                   Germany                  
##  [4475] Germany                   Germany                  
##  [4477] Germany                   Germany                  
##  [4479] Germany                   Germany                  
##  [4481] Germany                   Germany                  
##  [4483] Germany                   Germany                  
##  [4485] Germany                   Germany                  
##  [4487] Germany                   Germany                  
##  [4489] Germany                   Germany                  
##  [4491] Germany                   Germany                  
##  [4493] Germany                   Germany                  
##  [4495] Germany                   Germany                  
##  [4497] Germany                   Germany                  
##  [4499] Germany                   Germany                  
##  [4501] Germany                   Germany                  
##  [4503] Germany                   Germany                  
##  [4505] Germany                   Germany                  
##  [4507] Germany                   Germany                  
##  [4509] Germany                   Germany                  
##  [4511] Germany                   Germany                  
##  [4513] Germany                   Germany                  
##  [4515] Germany                   Germany                  
##  [4517] Germany                   Germany                  
##  [4519] Germany                   Germany                  
##  [4521] Germany                   Germany                  
##  [4523] Germany                   Germany                  
##  [4525] Germany                   Germany                  
##  [4527] Germany                   Germany                  
##  [4529] Germany                   Germany                  
##  [4531] Germany                   Germany                  
##  [4533] Germany                   Germany                  
##  [4535] Germany                   Germany                  
##  [4537] Germany                   Germany                  
##  [4539] Germany                   Germany                  
##  [4541] Germany                   Germany                  
##  [4543] Germany                   Germany                  
##  [4545] Germany                   Germany                  
##  [4547] Germany                   Germany                  
##  [4549] Germany                   Germany                  
##  [4551] Germany                   Germany                  
##  [4553] Germany                   Germany                  
##  [4555] Germany                   Germany                  
##  [4557] Germany                   Germany                  
##  [4559] Germany                   Germany                  
##  [4561] Germany                   Germany                  
##  [4563] Germany                   Germany                  
##  [4565] Germany                   Germany                  
##  [4567] Germany                   Germany                  
##  [4569] Germany                   Germany                  
##  [4571] Germany                   Germany                  
##  [4573] Germany                   Germany                  
##  [4575] Germany                   Germany                  
##  [4577] Germany                   Germany                  
##  [4579] Germany                   Germany                  
##  [4581] Germany                   Germany                  
##  [4583] Germany                   Germany                  
##  [4585] Germany                   Germany                  
##  [4587] Germany                   Germany                  
##  [4589] Germany                   Germany                  
##  [4591] Germany                   Germany                  
##  [4593] Germany                   Germany                  
##  [4595] Germany                   Germany                  
##  [4597] Germany                   Germany                  
##  [4599] Germany                   Germany                  
##  [4601] Germany                   Germany                  
##  [4603] Germany                   Germany                  
##  [4605] Germany                   Germany                  
##  [4607] Germany                   Germany                  
##  [4609] Germany                   Germany                  
##  [4611] Germany                   Germany                  
##  [4613] Germany                   Germany                  
##  [4615] Germany                   Germany                  
##  [4617] Germany                   Germany                  
##  [4619] Germany                   Germany                  
##  [4621] Germany                   Germany                  
##  [4623] Germany                   Germany                  
##  [4625] Germany                   Germany                  
##  [4627] Germany                   Germany                  
##  [4629] Germany                   Germany                  
##  [4631] Germany                   Germany                  
##  [4633] Germany                   Germany                  
##  [4635] Germany                   Germany                  
##  [4637] Germany                   Germany                  
##  [4639] Germany                   Germany                  
##  [4641] Germany                   Germany                  
##  [4643] Germany                   Germany                  
##  [4645] Germany                   Germany                  
##  [4647] Germany                   Germany                  
##  [4649] Germany                   Germany                  
##  [4651] Germany                   Germany                  
##  [4653] Germany                   Germany                  
##  [4655] Germany                   Germany                  
##  [4657] Germany                   Germany                  
##  [4659] Germany                   Germany                  
##  [4661] Germany                   Germany                  
##  [4663] Germany                   Germany                  
##  [4665] Germany                   Germany                  
##  [4667] Germany                   Germany                  
##  [4669] Germany                   Germany                  
##  [4671] Germany                   Germany                  
##  [4673] Germany                   Germany                  
##  [4675] Germany                   Germany                  
##  [4677] Germany                   Germany                  
##  [4679] Germany                   Germany                  
##  [4681] Germany                   Germany                  
##  [4683] Germany                   Germany                  
##  [4685] Germany                   Germany                  
##  [4687] Germany                   Germany                  
##  [4689] Germany                   Germany                  
##  [4691] Germany                   Germany                  
##  [4693] Germany                   Germany                  
##  [4695] Germany                   Germany                  
##  [4697] Germany                   Germany                  
##  [4699] Germany                   Germany                  
##  [4701] Germany                   Germany                  
##  [4703] Germany                   Germany                  
##  [4705] Germany                   Germany                  
##  [4707] Germany                   Germany                  
##  [4709] Germany                   Germany                  
##  [4711] Germany                   Germany                  
##  [4713] Germany                   Germany                  
##  [4715] Germany                   Germany                  
##  [4717] Germany                   Germany                  
##  [4719] Germany                   Germany                  
##  [4721] Germany                   Germany                  
##  [4723] Germany                   Germany                  
##  [4725] Germany                   Germany                  
##  [4727] Germany                   Germany                  
##  [4729] Germany                   Germany                  
##  [4731] Germany                   Germany                  
##  [4733] Germany                   Germany                  
##  [4735] Germany                   Germany                  
##  [4737] Germany                   Germany                  
##  [4739] Germany                   Germany                  
##  [4741] Germany                   Germany                  
##  [4743] Germany                   Germany                  
##  [4745] Germany                   Germany                  
##  [4747] Germany                   Germany                  
##  [4749] Germany                   Germany                  
##  [4751] Germany                   Germany                  
##  [4753] Germany                   Germany                  
##  [4755] Germany                   Germany                  
##  [4757] Germany                   Germany                  
##  [4759] Germany                   Germany                  
##  [4761] Germany                   Germany                  
##  [4763] Germany                   Germany                  
##  [4765] Germany                   Germany                  
##  [4767] Germany                   Germany                  
##  [4769] Germany                   Germany                  
##  [4771] Germany                   Germany                  
##  [4773] Germany                   Germany                  
##  [4775] Germany                   Ghana                    
##  [4777] Ghana                     Ghana                    
##  [4779] Ghana                     Ghana                    
##  [4781] Ghana                     Ghana                    
##  [4783] Ghana                     Ghana                    
##  [4785] Ghana                     Ghana                    
##  [4787] Ghana                     Ghana                    
##  [4789] Ghana                     Ghana                    
##  [4791] Ghana                     Ghana                    
##  [4793] Ghana                     Ghana                    
##  [4795] Ghana                     Ghana                    
##  [4797] Ghana                     Ghana                    
##  [4799] Ghana                     Ghana                    
##  [4801] Ghana                     Ghana                    
##  [4803] Ghana                     Ghana                    
##  [4805] Ghana                     Ghana                    
##  [4807] Ghana                     Ghana                    
##  [4809] Ghana                     Ghana                    
##  [4811] Ghana                     Ghana                    
##  [4813] Ghana                     Ghana                    
##  [4815] Ghana                     Ghana                    
##  [4817] Ghana                     Ghana                    
##  [4819] Ghana                     Ghana                    
##  [4821] Ghana                     Ghana                    
##  [4823] Ghana                     Ghana                    
##  [4825] Ghana                     Ghana                    
##  [4827] Ghana                     Ghana                    
##  [4829] Ghana                     Ghana                    
##  [4831] Ghana                     Ghana                    
##  [4833] Ghana                     Ghana                    
##  [4835] Ghana                     Ghana                    
##  [4837] Ghana                     Ghana                    
##  [4839] Ghana                     Ghana                    
##  [4841] Ghana                     Ghana                    
##  [4843] Ghana                     Ghana                    
##  [4845] Ghana                     Ghana                    
##  [4847] Ghana                     Ghana                    
##  [4849] Ghana                     Ghana                    
##  [4851] Ghana                     Ghana                    
##  [4853] Ghana                     Ghana                    
##  [4855] Ghana                     Ghana                    
##  [4857] Ghana                     Ghana                    
##  [4859] Ghana                     Ghana                    
##  [4861] Ghana                     Ghana                    
##  [4863] Ghana                     Ghana                    
##  [4865] Ghana                     Ghana                    
##  [4867] Ghana                     Ghana                    
##  [4869] Ghana                     Gibraltar                
##  [4871] Greece                    Greece                   
##  [4873] Greece                    Greece                   
##  [4875] Greece                    Greece                   
##  [4877] Greece                    Greece                   
##  [4879] Greece                    Greece                   
##  [4881] Greece                    Greece                   
##  [4883] Greece                    Greece                   
##  [4885] Greece                    Greece                   
##  [4887] Greece                    Greece                   
##  [4889] Greece                    Greece                   
##  [4891] Greece                    Greece                   
##  [4893] Greece                    Greece                   
##  [4895] Greece                    Greece                   
##  [4897] Greece                    Greece                   
##  [4899] Greece                    Greece                   
##  [4901] Greece                    Greece                   
##  [4903] Greece                    Greece                   
##  [4905] Greece                    Greece                   
##  [4907] Greece                    Greece                   
##  [4909] Greece                    Greece                   
##  [4911] Greece                    Greece                   
##  [4913] Greece                    Greece                   
##  [4915] Greece                    Greece                   
##  [4917] Greece                    Greece                   
##  [4919] Greece                    Greece                   
##  [4921] Greece                    Greece                   
##  [4923] Greece                    Greece                   
##  [4925] Greece                    Greece                   
##  [4927] Greece                    Greece                   
##  [4929] Greece                    Greece                   
##  [4931] Greece                    Greece                   
##  [4933] Greece                    Greece                   
##  [4935] Greece                    Greece                   
##  [4937] Greece                    Greece                   
##  [4939] Greece                    Greece                   
##  [4941] Greece                    Greece                   
##  [4943] Greece                    Greece                   
##  [4945] Greece                    Greece                   
##  [4947] Greece                    Greece                   
##  [4949] Greece                    Greece                   
##  [4951] Greece                    Greece                   
##  [4953] Greece                    Greece                   
##  [4955] Greece                    Greece                   
##  [4957] Greece                    Greece                   
##  [4959] Greece                    Greece                   
##  [4961] Greece                    Greece                   
##  [4963] Greece                    Greece                   
##  [4965] Greece                    Greece                   
##  [4967] Greece                    Greece                   
##  [4969] Greece                    Greece                   
##  [4971] Greece                    Greece                   
##  [4973] Greece                    Greece                   
##  [4975] Greece                    Greece                   
##  [4977] Greece                    Greece                   
##  [4979] Greece                    Greece                   
##  [4981] Greece                    Greece                   
##  [4983] Greece                    Greece                   
##  [4985] Greece                    Greece                   
##  [4987] Greece                    Greece                   
##  [4989] Greece                    Greece                   
##  [4991] Greece                    Greece                   
##  [4993] Greece                    Greece                   
##  [4995] Greece                    Greenland                
##  [4997] Greenland                 Greenland                
##  [4999] Greenland                 Greenland                
##  [5001] Greenland                 Greenland                
##  [5003] Greenland                 Greenland                
##  [5005] Greenland                 Greenland                
##  [5007] Greenland                 Greenland                
##  [5009] Greenland                 Greenland                
##  [5011] Greenland                 Greenland                
##  [5013] Greenland                 Greenland                
##  [5015] Greenland                 Greenland                
##  [5017] Greenland                 Greenland                
##  [5019] Greenland                 Greenland                
##  [5021] Greenland                 Greenland                
##  [5023] Greenland                 Greenland                
##  [5025] Greenland                 Greenland                
##  [5027] Greenland                 Greenland                
##  [5029] Greenland                 Greenland                
##  [5031] Greenland                 Greenland                
##  [5033] Greenland                 Greenland                
##  [5035] Greenland                 Greenland                
##  [5037] Greenland                 Greenland                
##  [5039] Greenland                 Greenland                
##  [5041] Greenland                 Greenland                
##  [5043] Greenland                 Greenland                
##  [5045] Greenland                 Greenland                
##  [5047] Greenland                 Greenland                
##  [5049] Greenland                 Greenland                
##  [5051] Greenland                 Greenland                
##  [5053] Greenland                 Greenland                
##  [5055] Greenland                 Grenada                  
##  [5057] Grenada                   Grenada                  
##  [5059] Grenada                   Grenada                  
##  [5061] Grenada                   Grenada                  
##  [5063] Grenada                   Grenada                  
##  [5065] Grenada                   Grenada                  
##  [5067] Grenada                   Grenada                  
##  [5069] Grenada                   Grenada                  
##  [5071] Grenada                   Grenada                  
##  [5073] Grenada                   Grenada                  
##  [5075] Grenada                   Grenada                  
##  [5077] Grenada                   Grenada                  
##  [5079] Grenada                   Grenada                  
##  [5081] Grenada                   Grenada                  
##  [5083] Grenada                   Grenada                  
##  [5085] Grenada                   Grenada                  
##  [5087] Grenada                   Grenada                  
##  [5089] Grenada                   Grenada                  
##  [5091] Grenada                   Grenada                  
##  [5093] Grenada                   Grenada                  
##  [5095] Grenada                   Grenada                  
##  [5097] Grenada                   Grenada                  
##  [5099] Grenada                   Grenada                  
##  [5101] Grenada                   Grenada                  
##  [5103] Guadeloupe                Guadeloupe               
##  [5105] Guadeloupe                Guadeloupe               
##  [5107] Guadeloupe                Guadeloupe               
##  [5109] Guadeloupe                Guadeloupe               
##  [5111] Guam                      Guam                     
##  [5113] Guam                      Guam                     
##  [5115] Guam                      Guam                     
##  [5117] Guam                      Guam                     
##  [5119] Guam                      Guam                     
##  [5121] Guam                      Guam                     
##  [5123] Guam                      Guam                     
##  [5125] Guam                      Guam                     
##  [5127] Guam                      Guam                     
##  [5129] Guam                      Guam                     
##  [5131] Guam                      Guam                     
##  [5133] Guam                      Guatemala                
##  [5135] Guatemala                 Guatemala                
##  [5137] Guatemala                 Guatemala                
##  [5139] Guatemala                 Guatemala                
##  [5141] Guatemala                 Guatemala                
##  [5143] Guatemala                 Guatemala                
##  [5145] Guatemala                 Guatemala                
##  [5147] Guatemala                 Guatemala                
##  [5149] Guatemala                 Guatemala                
##  [5151] Guatemala                 Guatemala                
##  [5153] Guatemala                 Guatemala                
##  [5155] Guatemala                 Guatemala                
##  [5157] Guatemala                 Guatemala                
##  [5159] Guatemala                 Guatemala                
##  [5161] Guatemala                 Guatemala                
##  [5163] Guatemala                 Guatemala                
##  [5165] Guatemala                 Guatemala                
##  [5167] Guatemala                 Guatemala                
##  [5169] Guatemala                 Guatemala                
##  [5171] Guatemala                 Guinea                   
##  [5173] Guinea                    Guinea                   
##  [5175] Guinea                    Guinea                   
##  [5177] Guinea                    Guinea                   
##  [5179] Guinea                    Guinea                   
##  [5181] Guinea                    Guinea                   
##  [5183] Guinea                    Guinea                   
##  [5185] Guinea                    Guinea                   
##  [5187] Guinea                    Guinea                   
##  [5189] Guinea                    Guinea                   
##  [5191] Guinea                    Guinea                   
##  [5193] Guinea                    Guinea                   
##  [5195] Guinea                    Guinea                   
##  [5197] Guinea                    Guinea                   
##  [5199] Guinea                    Guinea                   
##  [5201] Guinea                    Guinea                   
##  [5203] Guinea                    Guinea                   
##  [5205] Guinea                    Guinea                   
##  [5207] Guinea                    Guinea                   
##  [5209] Guinea                    Guinea                   
##  [5211] Guinea                    Guinea                   
##  [5213] Guinea                    Guinea                   
##  [5215] Guinea                    Guinea                   
##  [5217] Guinea                    Guinea                   
##  [5219] Guinea                    Guinea                   
##  [5221] Guinea                    Guinea                   
##  [5223] Guinea                    Guinea                   
##  [5225] Guinea                    Guinea                   
##  [5227] Guinea                    GuineaBissau             
##  [5229] GuineaBissau              GuineaBissau             
##  [5231] GuineaBissau              GuineaBissau             
##  [5233] GuineaBissau              GuineaBissau             
##  [5235] GuineaBissau              GuineaBissau             
##  [5237] GuineaBissau              GuineaBissau             
##  [5239] GuineaBissau              GuineaBissau             
##  [5241] GuineaBissau              GuineaBissau             
##  [5243] GuineaBissau              GuineaBissau             
##  [5245] GuineaBissau              GuineaBissau             
##  [5247] GuineaBissau              GuineaBissau             
##  [5249] GuineaBissau              GuineaBissau             
##  [5251] GuineaBissau              GuineaBissau             
##  [5253] GuineaBissau              GuineaBissau             
##  [5255] GuineaBissau              GuineaBissau             
##  [5257] GuineaBissau              GuineaBissau             
##  [5259] GuineaBissau              Guyana                   
##  [5261] Guyana                    Guyana                   
##  [5263] Guyana                    Guyana                   
##  [5265] Guyana                    Guyana                   
##  [5267] Guyana                    Guyana                   
##  [5269] Guyana                    Guyana                   
##  [5271] Haiti                     Haiti                    
##  [5273] Haiti                     Haiti                    
##  [5275] Haiti                     Haiti                    
##  [5277] Honduras                  Honduras                 
##  [5279] Honduras                  Honduras                 
##  [5281] Honduras                  Honduras                 
##  [5283] Honduras                  Honduras                 
##  [5285] Honduras                  Honduras                 
##  [5287] Honduras                  Honduras                 
##  [5289] Honduras                  Honduras                 
##  [5291] Honduras                  Honduras                 
##  [5293] Honduras                  Honduras                 
##  [5295] Honduras                  Honduras                 
##  [5297] Honduras                  Honduras                 
##  [5299] Honduras                  Honduras                 
##  [5301] Honduras                  Honduras                 
##  [5303] Honduras                  Honduras                 
##  [5305] Honduras                  Honduras                 
##  [5307] Honduras                  Honduras                 
##  [5309] Honduras                  Honduras                 
##  [5311] Honduras                  Honduras                 
##  [5313] Honduras                  Honduras                 
##  [5315] Honduras                  Honduras                 
##  [5317] Honduras                  Honduras                 
##  [5319] Honduras                  Honduras                 
##  [5321] Honduras                  Honduras                 
##  [5323] Honduras                  Honduras                 
##  [5325] Honduras                  Honduras                 
##  [5327] Honduras                  Honduras                 
##  [5329] Honduras                  Honduras                 
##  [5331] Honduras                  Honduras                 
##  [5333] Honduras                  Honduras                 
##  [5335] Honduras                  Honduras                 
##  [5337] Honduras                  Honduras                 
##  [5339] Honduras                  Honduras                 
##  [5341] Honduras                  Honduras                 
##  [5343] Honduras                  Honduras                 
##  [5345] Iceland                   Iceland                  
##  [5347] Iceland                   Iceland                  
##  [5349] Iceland                   Iceland                  
##  [5351] Iceland                   Iceland                  
##  [5353] Iceland                   Iceland                  
##  [5355] Iceland                   Iceland                  
##  [5357] Iceland                   Iceland                  
##  [5359] Iceland                   Iceland                  
##  [5361] Iceland                   Iceland                  
##  [5363] Iceland                   Iceland                  
##  [5365] Iceland                   Iceland                  
##  [5367] Iceland                   Iceland                  
##  [5369] Iceland                   Iceland                  
##  [5371] Iceland                   Iceland                  
##  [5373] Iceland                   Iceland                  
##  [5375] Iceland                   Iceland                  
##  [5377] Iceland                   Iceland                  
##  [5379] Iceland                   Iceland                  
##  [5381] Iceland                   Iceland                  
##  [5383] Iceland                   Iceland                  
##  [5385] Iceland                   Iceland                  
##  [5387] Iceland                   Iceland                  
##  [5389] Iceland                   Iceland                  
##  [5391] Iceland                   Iceland                  
##  [5393] Iceland                   Iceland                  
##  [5395] Iceland                   Iceland                  
##  [5397] Iceland                   Iceland                  
##  [5399] Iceland                   Iceland                  
##  [5401] Iceland                   Iceland                  
##  [5403] Iceland                   Iceland                  
##  [5405] Iceland                   Iceland                  
##  [5407] Iceland                   Iceland                  
##  [5409] Iceland                   Iceland                  
##  [5411] Iceland                   Iceland                  
##  [5413] Iceland                   Iceland                  
##  [5415] Iceland                   Iceland                  
##  [5417] Iceland                   Iceland                  
##  [5419] Iceland                   Iceland                  
##  [5421] Iceland                   Iceland                  
##  [5423] Iceland                   Iceland                  
##  [5425] Iceland                   Iceland                  
##  [5427] Iceland                   Iceland                  
##  [5429] Iceland                   Iceland                  
##  [5431] Iceland                   Iceland                  
##  [5433] Iceland                   Iceland                  
##  [5435] Iceland                   Iceland                  
##  [5437] Iceland                   Iceland                  
##  [5439] Iceland                   Iceland                  
##  [5441] Iceland                   Iceland                  
##  [5443] Iceland                   Iceland                  
##  [5445] Iceland                   Iceland                  
##  [5447] Iceland                   Iceland                  
##  [5449] Iceland                   Iceland                  
##  [5451] Iceland                   India                    
##  [5453] India                     India                    
##  [5455] India                     India                    
##  [5457] India                     India                    
##  [5459] India                     India                    
##  [5461] India                     India                    
##  [5463] India                     India                    
##  [5465] India                     India                    
##  [5467] India                     India                    
##  [5469] India                     India                    
##  [5471] India                     India                    
##  [5473] India                     India                    
##  [5475] India                     India                    
##  [5477] India                     India                    
##  [5479] India                     India                    
##  [5481] India                     India                    
##  [5483] India                     India                    
##  [5485] India                     India                    
##  [5487] India                     India                    
##  [5489] India                     India                    
##  [5491] India                     India                    
##  [5493] India                     India                    
##  [5495] India                     India                    
##  [5497] India                     India                    
##  [5499] India                     India                    
##  [5501] India                     India                    
##  [5503] India                     India                    
##  [5505] India                     India                    
##  [5507] India                     India                    
##  [5509] India                     India                    
##  [5511] India                     India                    
##  [5513] India                     India                    
##  [5515] India                     India                    
##  [5517] India                     India                    
##  [5519] India                     India                    
##  [5521] India                     India                    
##  [5523] India                     India                    
##  [5525] India                     India                    
##  [5527] India                     India                    
##  [5529] India                     India                    
##  [5531] India                     India                    
##  [5533] India                     India                    
##  [5535] India                     India                    
##  [5537] India                     India                    
##  [5539] India                     India                    
##  [5541] India                     India                    
##  [5543] India                     India                    
##  [5545] India                     India                    
##  [5547] India                     India                    
##  [5549] India                     India                    
##  [5551] India                     India                    
##  [5553] India                     India                    
##  [5555] India                     India                    
##  [5557] India                     India                    
##  [5559] India                     Indonesia                
##  [5561] Indonesia                 Indonesia                
##  [5563] Indonesia                 Indonesia                
##  [5565] Indonesia                 Indonesia                
##  [5567] Indonesia                 Indonesia                
##  [5569] Indonesia                 Indonesia                
##  [5571] Indonesia                 Indonesia                
##  [5573] Indonesia                 Indonesia                
##  [5575] Indonesia                 Indonesia                
##  [5577] Indonesia                 Indonesia                
##  [5579] Indonesia                 Indonesia                
##  [5581] Indonesia                 Indonesia                
##  [5583] Indonesia                 Indonesia                
##  [5585] Indonesia                 Indonesia                
##  [5587] Indonesia                 Indonesia                
##  [5589] Indonesia                 Indonesia                
##  [5591] Indonesia                 Indonesia                
##  [5593] Indonesia                 Indonesia                
##  [5595] Indonesia                 Indonesia                
##  [5597] Indonesia                 Indonesia                
##  [5599] Indonesia                 Indonesia                
##  [5601] Indonesia                 Indonesia                
##  [5603] Indonesia                 Indonesia                
##  [5605] Indonesia                 Indonesia                
##  [5607] Indonesia                 Indonesia                
##  [5609] Indonesia                 Indonesia                
##  [5611] Indonesia                 Indonesia                
##  [5613] Indonesia                 Indonesia                
##  [5615] Indonesia                 Indonesia                
##  [5617] Indonesia                 Indonesia                
##  [5619] Indonesia                 Indonesia                
##  [5621] Indonesia                 Indonesia                
##  [5623] Indonesia                 Indonesia                
##  [5625] Indonesia                 Indonesia                
##  [5627] Indonesia                 Indonesia                
##  [5629] Indonesia                 Indonesia                
##  [5631] Indonesia                 Indonesia                
##  [5633] Indonesia                 Indonesia                
##  [5635] Indonesia                 Indonesia                
##  [5637] Indonesia                 Indonesia                
##  [5639] Indonesia                 Indonesia                
##  [5641] Indonesia                 Indonesia                
##  [5643] Indonesia                 Indonesia                
##  [5645] Indonesia                 Indonesia                
##  [5647] Indonesia                 Indonesia                
##  [5649] Indonesia                 Indonesia                
##  [5651] Indonesia                 Indonesia                
##  [5653] Indonesia                 Indonesia                
##  [5655] Indonesia                 Indonesia                
##  [5657] Indonesia                 Indonesia                
##  [5659] Indonesia                 Indonesia                
##  [5661] Indonesia                 Indonesia                
##  [5663] Indonesia                 Indonesia                
##  [5665] Indonesia                 Indonesia                
##  [5667] Indonesia                 Indonesia                
##  [5669] Indonesia                 Indonesia                
##  [5671] Indonesia                 Indonesia                
##  [5673] Indonesia                 Indonesia                
##  [5675] Indonesia                 Indonesia                
##  [5677] Indonesia                 Indonesia                
##  [5679] Indonesia                 Indonesia                
##  [5681] Indonesia                 Indonesia                
##  [5683] Indonesia                 Indonesia                
##  [5685] Indonesia                 Indonesia                
##  [5687] Indonesia                 Indonesia                
##  [5689] Indonesia                 Indonesia                
##  [5691] Indonesia                 Indonesia                
##  [5693] Indonesia                 Indonesia                
##  [5695] Indonesia                 Indonesia                
##  [5697] Indonesia                 Indonesia                
##  [5699] Indonesia                 Indonesia                
##  [5701] Indonesia                 Indonesia                
##  [5703] Indonesia                 Indonesia                
##  [5705] Indonesia                 Indonesia                
##  [5707] Indonesia                 Indonesia                
##  [5709] Indonesia                 Indonesia                
##  [5711] Indonesia                 Indonesia                
##  [5713] Indonesia                 Indonesia                
##  [5715] Indonesia                 Indonesia                
##  [5717] Indonesia                 Indonesia                
##  [5719] Indonesia                 Indonesia                
##  [5721] Indonesia                 Indonesia                
##  [5723] Indonesia                 Indonesia                
##  [5725] Indonesia                 Indonesia                
##  [5727] Indonesia                 Indonesia                
##  [5729] Indonesia                 Indonesia                
##  [5731] Indonesia                 Indonesia                
##  [5733] Indonesia                 Indonesia                
##  [5735] Indonesia                 Indonesia                
##  [5737] Indonesia                 Indonesia                
##  [5739] Indonesia                 Indonesia                
##  [5741] Indonesia                 Indonesia                
##  [5743] Indonesia                 Indonesia                
##  [5745] Indonesia                 Indonesia                
##  [5747] Indonesia                 Indonesia                
##  [5749] Indonesia                 Indonesia                
##  [5751] Indonesia                 Indonesia                
##  [5753] Indonesia                 Indonesia                
##  [5755] Indonesia                 Indonesia                
##  [5757] Indonesia                 Indonesia                
##  [5759] Indonesia                 Indonesia                
##  [5761] Indonesia                 Indonesia                
##  [5763] Indonesia                 Indonesia                
##  [5765] Indonesia                 Indonesia                
##  [5767] Indonesia                 Indonesia                
##  [5769] Indonesia                 Indonesia                
##  [5771] Indonesia                 Indonesia                
##  [5773] Indonesia                 Indonesia                
##  [5775] Indonesia                 Indonesia                
##  [5777] Indonesia                 Indonesia                
##  [5779] Indonesia                 Indonesia                
##  [5781] Indonesia                 Indonesia                
##  [5783] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5785] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5787] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5789] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5791] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5793] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5795] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5797] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5799] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5801] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5803] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5805] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5807] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5809] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5811] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5813] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5815] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5817] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5819] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5821] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5823] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5825] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5827] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5829] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5831] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5833] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5835] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5837] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5839] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5841] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5843] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5845] Iran (Islamic Rep. of)    Iran (Islamic Rep. of)   
##  [5847] Iraq                      Iraq                     
##  [5849] Iraq                      Iraq                     
##  [5851] Iraq                      Iraq                     
##  [5853] Iraq                      Iraq                     
##  [5855] Iraq                      Iraq                     
##  [5857] Iraq                      Iraq                     
##  [5859] Iraq                      Iraq                     
##  [5861] Iraq                      Iraq                     
##  [5863] Ireland                   Ireland                  
##  [5865] Ireland                   Ireland                  
##  [5867] Ireland                   Ireland                  
##  [5869] Ireland                   Ireland                  
##  [5871] Ireland                   Ireland                  
##  [5873] Ireland                   Ireland                  
##  [5875] Ireland                   Ireland                  
##  [5877] Ireland                   Ireland                  
##  [5879] Ireland                   Ireland                  
##  [5881] Ireland                   Ireland                  
##  [5883] Ireland                   Ireland                  
##  [5885] Ireland                   Ireland                  
##  [5887] Ireland                   Ireland                  
##  [5889] Ireland                   Ireland                  
##  [5891] Ireland                   Ireland                  
##  [5893] Ireland                   Ireland                  
##  [5895] Ireland                   Ireland                  
##  [5897] Ireland                   Ireland                  
##  [5899] Ireland                   Ireland                  
##  [5901] Ireland                   Ireland                  
##  [5903] Ireland                   Ireland                  
##  [5905] Ireland                   Ireland                  
##  [5907] Ireland                   Ireland                  
##  [5909] Ireland                   Ireland                  
##  [5911] Ireland                   Ireland                  
##  [5913] Ireland                   Ireland                  
##  [5915] Ireland                   Ireland                  
##  [5917] Ireland                   Ireland                  
##  [5919] Ireland                   Ireland                  
##  [5921] Ireland                   Ireland                  
##  [5923] Ireland                   Ireland                  
##  [5925] Ireland                   Ireland                  
##  [5927] Ireland                   Ireland                  
##  [5929] Ireland                   Ireland                  
##  [5931] Ireland                   Ireland                  
##  [5933] Ireland                   Ireland                  
##  [5935] Ireland                   Ireland                  
##  [5937] Ireland                   Ireland                  
##  [5939] Ireland                   Ireland                  
##  [5941] Ireland                   Ireland                  
##  [5943] Ireland                   Ireland                  
##  [5945] Ireland                   Ireland                  
##  [5947] Ireland                   Ireland                  
##  [5949] Ireland                   Ireland                  
##  [5951] Ireland                   Ireland                  
##  [5953] Ireland                   Ireland                  
##  [5955] Ireland                   Ireland                  
##  [5957] Ireland                   Ireland                  
##  [5959] Ireland                   Ireland                  
##  [5961] Ireland                   Ireland                  
##  [5963] Ireland                   Ireland                  
##  [5965] Ireland                   Ireland                  
##  [5967] Ireland                   Ireland                  
##  [5969] Ireland                   Ireland                  
##  [5971] Ireland                   Ireland                  
##  [5973] Ireland                   Ireland                  
##  [5975] Ireland                   Ireland                  
##  [5977] Ireland                   Ireland                  
##  [5979] Ireland                   Ireland                  
##  [5981] Ireland                   Ireland                  
##  [5983] Ireland                   Ireland                  
##  [5985] Ireland                   Ireland                  
##  [5987] Ireland                   Ireland                  
##  [5989] Ireland                   Ireland                  
##  [5991] Ireland                   Ireland                  
##  [5993] Ireland                   Ireland                  
##  [5995] Ireland                   Ireland                  
##  [5997] Ireland                   Ireland                  
##  [5999] Ireland                   Ireland                  
##  [6001] Ireland                   Ireland                  
##  [6003] Ireland                   Ireland                  
##  [6005] Ireland                   Ireland                  
##  [6007] Ireland                   Ireland                  
##  [6009] Ireland                   Ireland                  
##  [6011] Ireland                   Ireland                  
##  [6013] Ireland                   Ireland                  
##  [6015] Ireland                   Ireland                  
##  [6017] Ireland                   Ireland                  
##  [6019] Ireland                   Ireland                  
##  [6021] Ireland                   Ireland                  
##  [6023] Ireland                   Ireland                  
##  [6025] Ireland                   Ireland                  
##  [6027] Ireland                   Ireland                  
##  [6029] Ireland                   Ireland                  
##  [6031] Ireland                   Ireland                  
##  [6033] Ireland                   Ireland                  
##  [6035] Ireland                   Ireland                  
##  [6037] Ireland                   Ireland                  
##  [6039] Ireland                   Ireland                  
##  [6041] Ireland                   Ireland                  
##  [6043] Ireland                   Ireland                  
##  [6045] Ireland                   Ireland                  
##  [6047] Ireland                   Ireland                  
##  [6049] Ireland                   Ireland                  
##  [6051] Ireland                   Ireland                  
##  [6053] Ireland                   Isle of Man              
##  [6055] Isle of Man               Isle of Man              
##  [6057] Isle of Man               Isle of Man              
##  [6059] Isle of Man               Isle of Man              
##  [6061] Isle of Man               Isle of Man              
##  [6063] Isle of Man               Isle of Man              
##  [6065] Isle of Man               Isle of Man              
##  [6067] Isle of Man               Isle of Man              
##  [6069] Isle of Man               Isle of Man              
##  [6071] Isle of Man               Isle of Man              
##  [6073] Isle of Man               Isle of Man              
##  [6075] Isle of Man               Isle of Man              
##  [6077] Isle of Man               Isle of Man              
##  [6079] Isle of Man               Isle of Man              
##  [6081] Isle of Man               Isle of Man              
##  [6083] Isle of Man               Isle of Man              
##  [6085] Isle of Man               Isle of Man              
##  [6087] Isle of Man               Isle of Man              
##  [6089] Isle of Man               Isle of Man              
##  [6091] Isle of Man               Isle of Man              
##  [6093] Isle of Man               Isle of Man              
##  [6095] Israel                    Israel                   
##  [6097] Israel                    Israel                   
##  [6099] Israel                    Israel                   
##  [6101] Israel                    Israel                   
##  [6103] Israel                    Israel                   
##  [6105] Israel                    Israel                   
##  [6107] Israel                    Israel                   
##  [6109] Israel                    Israel                   
##  [6111] Israel                    Israel                   
##  [6113] Israel                    Israel                   
##  [6115] Israel                    Israel                   
##  [6117] Israel                    Israel                   
##  [6119] Israel                    Israel                   
##  [6121] Israel                    Israel                   
##  [6123] Israel                    Israel                   
##  [6125] Israel                    Israel                   
##  [6127] Israel                    Israel                   
##  [6129] Israel                    Israel                   
##  [6131] Israel                    Israel                   
##  [6133] Israel                    Israel                   
##  [6135] Israel                    Israel                   
##  [6137] Israel                    Israel                   
##  [6139] Israel                    Israel                   
##  [6141] Israel                    Israel                   
##  [6143] Israel                    Israel                   
##  [6145] Israel                    Israel                   
##  [6147] Israel                    Israel                   
##  [6149] Israel                    Israel                   
##  [6151] Israel                    Israel                   
##  [6153] Israel                    Israel                   
##  [6155] Israel                    Israel                   
##  [6157] Israel                    Israel                   
##  [6159] Israel                    Israel                   
##  [6161] Israel                    Israel                   
##  [6163] Israel                    Israel                   
##  [6165] Israel                    Israel                   
##  [6167] Israel                    Israel                   
##  [6169] Israel                    Israel                   
##  [6171] Israel                    Israel                   
##  [6173] Israel                    Italy                    
##  [6175] Italy                     Italy                    
##  [6177] Italy                     Italy                    
##  [6179] Italy                     Italy                    
##  [6181] Italy                     Italy                    
##  [6183] Italy                     Italy                    
##  [6185] Italy                     Italy                    
##  [6187] Italy                     Italy                    
##  [6189] Italy                     Italy                    
##  [6191] Italy                     Italy                    
##  [6193] Italy                     Italy                    
##  [6195] Italy                     Italy                    
##  [6197] Italy                     Italy                    
##  [6199] Italy                     Italy                    
##  [6201] Italy                     Italy                    
##  [6203] Italy                     Italy                    
##  [6205] Italy                     Italy                    
##  [6207] Italy                     Italy                    
##  [6209] Italy                     Italy                    
##  [6211] Italy                     Italy                    
##  [6213] Italy                     Italy                    
##  [6215] Italy                     Italy                    
##  [6217] Italy                     Italy                    
##  [6219] Italy                     Italy                    
##  [6221] Italy                     Italy                    
##  [6223] Italy                     Italy                    
##  [6225] Italy                     Italy                    
##  [6227] Italy                     Italy                    
##  [6229] Italy                     Italy                    
##  [6231] Italy                     Italy                    
##  [6233] Italy                     Italy                    
##  [6235] Italy                     Italy                    
##  [6237] Italy                     Italy                    
##  [6239] Italy                     Italy                    
##  [6241] Italy                     Italy                    
##  [6243] Italy                     Italy                    
##  [6245] Italy                     Italy                    
##  [6247] Italy                     Italy                    
##  [6249] Italy                     Italy                    
##  [6251] Italy                     Italy                    
##  [6253] Italy                     Italy                    
##  [6255] Italy                     Italy                    
##  [6257] Italy                     Italy                    
##  [6259] Italy                     Italy                    
##  [6261] Italy                     Italy                    
##  [6263] Italy                     Italy                    
##  [6265] Italy                     Italy                    
##  [6267] Italy                     Italy                    
##  [6269] Italy                     Italy                    
##  [6271] Italy                     Italy                    
##  [6273] Italy                     Italy                    
##  [6275] Italy                     Italy                    
##  [6277] Italy                     Italy                    
##  [6279] Italy                     Italy                    
##  [6281] Italy                     Italy                    
##  [6283] Italy                     Italy                    
##  [6285] Italy                     Italy                    
##  [6287] Italy                     Italy                    
##  [6289] Italy                     Italy                    
##  [6291] Italy                     Italy                    
##  [6293] Italy                     Italy                    
##  [6295] Italy                     Italy                    
##  [6297] Italy                     Italy                    
##  [6299] Italy                     Italy                    
##  [6301] Italy                     Italy                    
##  [6303] Italy                     Italy                    
##  [6305] Italy                     Italy                    
##  [6307] Italy                     Italy                    
##  [6309] Italy                     Italy                    
##  [6311] Italy                     Italy                    
##  [6313] Italy                     Italy                    
##  [6315] Italy                     Italy                    
##  [6317] Italy                     Italy                    
##  [6319] Italy                     Italy                    
##  [6321] Italy                     Italy                    
##  [6323] Italy                     Italy                    
##  [6325] Italy                     Italy                    
##  [6327] Italy                     Italy                    
##  [6329] Italy                     Italy                    
##  [6331] Italy                     Italy                    
##  [6333] Italy                     Italy                    
##  [6335] Italy                     Italy                    
##  [6337] Italy                     Italy                    
##  [6339] Italy                     Italy                    
##  [6341] Italy                     Italy                    
##  [6343] Italy                     Italy                    
##  [6345] Italy                     Italy                    
##  [6347] Italy                     Italy                    
##  [6349] Italy                     Italy                    
##  [6351] Italy                     Italy                    
##  [6353] Italy                     Italy                    
##  [6355] Italy                     Italy                    
##  [6357] Italy                     Italy                    
##  [6359] Italy                     Italy                    
##  [6361] Italy                     Italy                    
##  [6363] Italy                     Italy                    
##  [6365] Italy                     Italy                    
##  [6367] Italy                     Italy                    
##  [6369] Italy                     Italy                    
##  [6371] Italy                     Italy                    
##  [6373] Italy                     Italy                    
##  [6375] Italy                     Italy                    
##  [6377] Italy                     Italy                    
##  [6379] Italy                     Italy                    
##  [6381] Italy                     Italy                    
##  [6383] Italy                     Italy                    
##  [6385] Italy                     Italy                    
##  [6387] Italy                     Italy                    
##  [6389] Italy                     Italy                    
##  [6391] Italy                     Italy                    
##  [6393] Italy                     Italy                    
##  [6395] Italy                     Italy                    
##  [6397] Italy                     Italy                    
##  [6399] Italy                     Italy                    
##  [6401] Italy                     Italy                    
##  [6403] Italy                     Italy                    
##  [6405] Italy                     Italy                    
##  [6407] Italy                     Italy                    
##  [6409] Italy                     Italy                    
##  [6411] Italy                     Italy                    
##  [6413] Italy                     Italy                    
##  [6415] Italy                     Italy                    
##  [6417] Italy                     Italy                    
##  [6419] Italy                     Italy                    
##  [6421] Italy                     Italy                    
##  [6423] Italy                     Italy                    
##  [6425] Italy                     Italy                    
##  [6427] Italy                     Italy                    
##  [6429] Italy                     Italy                    
##  [6431] Italy                     Italy                    
##  [6433] Italy                     Italy                    
##  [6435] Jamaica                   Jamaica                  
##  [6437] Jamaica                   Jamaica                  
##  [6439] Jamaica                   Jamaica                  
##  [6441] Japan                     Japan                    
##  [6443] Japan                     Japan                    
##  [6445] Japan                     Japan                    
##  [6447] Japan                     Japan                    
##  [6449] Japan                     Japan                    
##  [6451] Japan                     Japan                    
##  [6453] Japan                     Japan                    
##  [6455] Japan                     Japan                    
##  [6457] Japan                     Japan                    
##  [6459] Japan                     Japan                    
##  [6461] Japan                     Japan                    
##  [6463] Japan                     Japan                    
##  [6465] Japan                     Japan                    
##  [6467] Japan                     Japan                    
##  [6469] Japan                     Japan                    
##  [6471] Japan                     Japan                    
##  [6473] Japan                     Japan                    
##  [6475] Japan                     Japan                    
##  [6477] Japan                     Japan                    
##  [6479] Japan                     Japan                    
##  [6481] Japan                     Japan                    
##  [6483] Japan                     Japan                    
##  [6485] Japan                     Japan                    
##  [6487] Japan                     Japan                    
##  [6489] Japan                     Japan                    
##  [6491] Japan                     Japan                    
##  [6493] Japan                     Japan                    
##  [6495] Japan                     Japan                    
##  [6497] Japan                     Japan                    
##  [6499] Japan                     Japan                    
##  [6501] Japan                     Japan                    
##  [6503] Japan                     Japan                    
##  [6505] Japan                     Japan                    
##  [6507] Japan                     Japan                    
##  [6509] Japan                     Japan                    
##  [6511] Japan                     Japan                    
##  [6513] Japan                     Japan                    
##  [6515] Japan                     Japan                    
##  [6517] Japan                     Japan                    
##  [6519] Japan                     Japan                    
##  [6521] Japan                     Japan                    
##  [6523] Japan                     Japan                    
##  [6525] Japan                     Japan                    
##  [6527] Japan                     Japan                    
##  [6529] Japan                     Japan                    
##  [6531] Japan                     Japan                    
##  [6533] Japan                     Japan                    
##  [6535] Japan                     Japan                    
##  [6537] Japan                     Japan                    
##  [6539] Japan                     Japan                    
##  [6541] Japan                     Japan                    
##  [6543] Japan                     Japan                    
##  [6545] Japan                     Japan                    
##  [6547] Japan                     Japan                    
##  [6549] Japan                     Japan                    
##  [6551] Japan                     Japan                    
##  [6553] Japan                     Japan                    
##  [6555] Japan                     Japan                    
##  [6557] Japan                     Japan                    
##  [6559] Japan                     Japan                    
##  [6561] Japan                     Japan                    
##  [6563] Japan                     Japan                    
##  [6565] Japan                     Japan                    
##  [6567] Japan                     Japan                    
##  [6569] Japan                     Japan                    
##  [6571] Japan                     Japan                    
##  [6573] Japan                     Japan                    
##  [6575] Japan                     Japan                    
##  [6577] Japan                     Japan                    
##  [6579] Japan                     Japan                    
##  [6581] Japan                     Japan                    
##  [6583] Japan                     Japan                    
##  [6585] Japan                     Japan                    
##  [6587] Japan                     Japan                    
##  [6589] Japan                     Japan                    
##  [6591] Japan                     Japan                    
##  [6593] Japan                     Japan                    
##  [6595] Japan                     Japan                    
##  [6597] Japan                     Japan                    
##  [6599] Japan                     Japan                    
##  [6601] Japan                     Japan                    
##  [6603] Japan                     Japan                    
##  [6605] Japan                     Japan                    
##  [6607] Japan                     Japan                    
##  [6609] Japan                     Japan                    
##  [6611] Japan                     Japan                    
##  [6613] Japan                     Japan                    
##  [6615] Japan                     Japan                    
##  [6617] Japan                     Japan                    
##  [6619] Japan                     Japan                    
##  [6621] Japan                     Japan                    
##  [6623] Japan                     Japan                    
##  [6625] Japan                     Japan                    
##  [6627] Japan                     Japan                    
##  [6629] Japan                     Japan                    
##  [6631] Japan                     Japan                    
##  [6633] Japan                     Japan                    
##  [6635] Japan                     Japan                    
##  [6637] Japan                     Japan                    
##  [6639] Japan                     Japan                    
##  [6641] Japan                     Japan                    
##  [6643] Japan                     Japan                    
##  [6645] Japan                     Japan                    
##  [6647] Japan                     Japan                    
##  [6649] Japan                     Japan                    
##  [6651] Japan                     Japan                    
##  [6653] Japan                     Japan                    
##  [6655] Japan                     Japan                    
##  [6657] Japan                     Japan                    
##  [6659] Japan                     Japan                    
##  [6661] Japan                     Japan                    
##  [6663] Japan                     Japan                    
##  [6665] Japan                     Japan                    
##  [6667] Japan                     Japan                    
##  [6669] Japan                     Japan                    
##  [6671] Japan                     Japan                    
##  [6673] Japan                     Japan                    
##  [6675] Japan                     Japan                    
##  [6677] Japan                     Japan                    
##  [6679] Japan                     Japan                    
##  [6681] Japan                     Japan                    
##  [6683] Japan                     Japan                    
##  [6685] Japan                     Japan                    
##  [6687] Japan                     Japan                    
##  [6689] Japan                     Japan                    
##  [6691] Japan                     Japan                    
##  [6693] Japan                     Japan                    
##  [6695] Japan                     Japan                    
##  [6697] Japan                     Japan                    
##  [6699] Japan                     Japan                    
##  [6701] Japan                     Japan                    
##  [6703] Japan                     Japan                    
##  [6705] Japan                     Japan                    
##  [6707] Japan                     Japan                    
##  [6709] Japan                     Japan                    
##  [6711] Japan                     Japan                    
##  [6713] Japan                     Japan                    
##  [6715] Japan                     Japan                    
##  [6717] Japan                     Japan                    
##  [6719] Japan                     Japan                    
##  [6721] Japan                     Japan                    
##  [6723] Japan                     Japan                    
##  [6725] Japan                     Japan                    
##  [6727] Japan                     Japan                    
##  [6729] Japan                     Japan                    
##  [6731] Japan                     Japan                    
##  [6733] Japan                     Japan                    
##  [6735] Japan                     Japan                    
##  [6737] Japan                     Japan                    
##  [6739] Japan                     Japan                    
##  [6741] Japan                     Japan                    
##  [6743] Japan                     Japan                    
##  [6745] Japan                     Japan                    
##  [6747] Japan                     Japan                    
##  [6749] Japan                     Japan                    
##  [6751] Japan                     Japan                    
##  [6753] Japan                     Japan                    
##  [6755] Japan                     Japan                    
##  [6757] Japan                     Japan                    
##  [6759] Japan                     Japan                    
##  [6761] Japan                     Japan                    
##  [6763] Japan                     Japan                    
##  [6765] Japan                     Japan                    
##  [6767] Japan                     Japan                    
##  [6769] Japan                     Japan                    
##  [6771] Japan                     Japan                    
##  [6773] Japan                     Japan                    
##  [6775] Japan                     Japan                    
##  [6777] Japan                     Japan                    
##  [6779] Japan                     Japan                    
##  [6781] Japan                     Japan                    
##  [6783] Japan                     Japan                    
##  [6785] Japan                     Japan                    
##  [6787] Japan                     Japan                    
##  [6789] Japan                     Japan                    
##  [6791] Japan                     Japan                    
##  [6793] Japan                     Japan                    
##  [6795] Japan                     Japan                    
##  [6797] Japan                     Japan                    
##  [6799] Japan                     Japan                    
##  [6801] Japan                     Japan                    
##  [6803] Japan                     Japan                    
##  [6805] Japan                     Japan                    
##  [6807] Japan                     Japan                    
##  [6809] Japan                     Japan                    
##  [6811] Japan                     Japan                    
##  [6813] Japan                     Japan                    
##  [6815] Japan                     Japan                    
##  [6817] Japan                     Japan                    
##  [6819] Japan                     Japan                    
##  [6821] Japan                     Japan                    
##  [6823] Japan                     Japan                    
##  [6825] Japan                     Japan                    
##  [6827] Japan                     Japan                    
##  [6829] Japan                     Japan                    
##  [6831] Japan                     Japan                    
##  [6833] Japan                     Japan                    
##  [6835] Japan                     Japan                    
##  [6837] Japan                     Japan                    
##  [6839] Japan                     Japan                    
##  [6841] Japan                     Japan                    
##  [6843] Japan                     Japan                    
##  [6845] Japan                     Japan                    
##  [6847] Japan                     Japan                    
##  [6849] Japan                     Japan                    
##  [6851] Japan                     Japan                    
##  [6853] Japan                     Japan                    
##  [6855] Japan                     Japan                    
##  [6857] Japan                     Japan                    
##  [6859] Japan                     Japan                    
##  [6861] Japan                     Japan                    
##  [6863] Japan                     Japan                    
##  [6865] Japan                     Japan                    
##  [6867] Japan                     Japan                    
##  [6869] Japan                     Japan                    
##  [6871] Japan                     Japan                    
##  [6873] Japan                     Japan                    
##  [6875] Japan                     Japan                    
##  [6877] Japan                     Japan                    
##  [6879] Japan                     Japan                    
##  [6881] Japan                     Japan                    
##  [6883] Japan                     Japan                    
##  [6885] Japan                     Japan                    
##  [6887] Japan                     Japan                    
##  [6889] Japan                     Japan                    
##  [6891] Japan                     Japan                    
##  [6893] Japan                     Japan                    
##  [6895] Japan                     Japan                    
##  [6897] Japan                     Japan                    
##  [6899] Japan                     Japan                    
##  [6901] Japan                     Japan                    
##  [6903] Japan                     Japan                    
##  [6905] Japan                     Japan                    
##  [6907] Japan                     Japan                    
##  [6909] Japan                     Japan                    
##  [6911] Japan                     Japan                    
##  [6913] Japan                     Japan                    
##  [6915] Japan                     Japan                    
##  [6917] Japan                     Japan                    
##  [6919] Japan                     Japan                    
##  [6921] Japan                     Japan                    
##  [6923] Japan                     Japan                    
##  [6925] Japan                     Japan                    
##  [6927] Japan                     Japan                    
##  [6929] Japan                     Japan                    
##  [6931] Japan                     Japan                    
##  [6933] Japan                     Japan                    
##  [6935] Japan                     Japan                    
##  [6937] Japan                     Japan                    
##  [6939] Japan                     Japan                    
##  [6941] Japan                     Japan                    
##  [6943] Japan                     Japan                    
##  [6945] Japan                     Japan                    
##  [6947] Japan                     Japan                    
##  [6949] Japan                     Japan                    
##  [6951] Japan                     Japan                    
##  [6953] Japan                     Japan                    
##  [6955] Japan                     Japan                    
##  [6957] Japan                     Japan                    
##  [6959] Japan                     Japan                    
##  [6961] Japan                     Japan                    
##  [6963] Japan                     Japan                    
##  [6965] Japan                     Japan                    
##  [6967] Japan                     Japan                    
##  [6969] Japan                     Japan                    
##  [6971] Japan                     Japan                    
##  [6973] Japan                     Japan                    
##  [6975] Japan                     Japan                    
##  [6977] Japan                     Japan                    
##  [6979] Japan                     Japan                    
##  [6981] Japan                     Japan                    
##  [6983] Japan                     Japan                    
##  [6985] Japan                     Japan                    
##  [6987] Japan                     Japan                    
##  [6989] Japan                     Japan                    
##  [6991] Japan                     Japan                    
##  [6993] Japan                     Japan                    
##  [6995] Japan                     Japan                    
##  [6997] Japan                     Japan                    
##  [6999] Japan                     Japan                    
##  [7001] Japan                     Japan                    
##  [7003] Japan                     Japan                    
##  [7005] Japan                     Japan                    
##  [7007] Japan                     Japan                    
##  [7009] Japan                     Japan                    
##  [7011] Japan                     Japan                    
##  [7013] Japan                     Japan                    
##  [7015] Japan                     Japan                    
##  [7017] Japan                     Japan                    
##  [7019] Japan                     Japan                    
##  [7021] Japan                     Japan                    
##  [7023] Japan                     Japan                    
##  [7025] Japan                     Japan                    
##  [7027] Japan                     Japan                    
##  [7029] Japan                     Japan                    
##  [7031] Japan                     Japan                    
##  [7033] Japan                     Japan                    
##  [7035] Japan                     Japan                    
##  [7037] Japan                     Japan                    
##  [7039] Japan                     Japan                    
##  [7041] Japan                     Japan                    
##  [7043] Japan                     Japan                    
##  [7045] Japan                     Japan                    
##  [7047] Japan                     Japan                    
##  [7049] Japan                     Japan                    
##  [7051] Japan                     Jordan                   
##  [7053] Jordan                    Jordan                   
##  [7055] Jordan                    Jordan                   
##  [7057] Jordan                    Jordan                   
##  [7059] Jordan                    Jordan                   
##  [7061] Jordan                    Jordan                   
##  [7063] Jordan                    Kenya                    
##  [7065] Kenya                     Kenya                    
##  [7067] Kenya                     Kenya                    
##  [7069] Kenya                     Kenya                    
##  [7071] Kenya                     Kenya                    
##  [7073] Kenya                     Kenya                    
##  [7075] Kenya                     Kenya                    
##  [7077] Kenya                     Kenya                    
##  [7079] Kenya                     Kenya                    
##  [7081] Kenya                     Kenya                    
##  [7083] Kenya                     Kenya                    
##  [7085] Kenya                     Kenya                    
##  [7087] Kenya                     Kenya                    
##  [7089] Kenya                     Kenya                    
##  [7091] Kenya                     Kenya                    
##  [7093] Kenya                     Kenya                    
##  [7095] Kiribati                  Kiribati                 
##  [7097] Kiribati                  Kiribati                 
##  [7099] Kiribati                  Kiribati                 
##  [7101] Kiribati                  Kiribati                 
##  [7103] Kiribati                  Kiribati                 
##  [7105] Kiribati                  Kiribati                 
##  [7107] Kiribati                  Kiribati                 
##  [7109] Kiribati                  Kiribati                 
##  [7111] Kiribati                  Kiribati                 
##  [7113] Kiribati                  Kiribati                 
##  [7115] Kiribati                  Kiribati                 
##  [7117] Kiribati                  Kiribati                 
##  [7119] Kiribati                  Kiribati                 
##  [7121] Kiribati                  Korea, Dem. People's Rep 
##  [7123] Korea, Dem. People's Rep  Korea, Dem. People's Rep 
##  [7125] Korea, Dem. People's Rep  Korea, Dem. People's Rep 
##  [7127] Korea, Dem. People's Rep  Korea, Dem. People's Rep 
##  [7129] Korea, Dem. People's Rep  Korea, Dem. People's Rep 
##  [7131] Korea, Dem. People's Rep  Korea, Dem. People's Rep 
##  [7133] Korea, Dem. People's Rep  Korea, Dem. People's Rep 
##  [7135] Korea, Dem. People's Rep  Korea, Republic of       
##  [7137] Korea, Republic of        Korea, Republic of       
##  [7139] Korea, Republic of        Korea, Republic of       
##  [7141] Korea, Republic of        Korea, Republic of       
##  [7143] Korea, Republic of        Korea, Republic of       
##  [7145] Korea, Republic of        Korea, Republic of       
##  [7147] Korea, Republic of        Korea, Republic of       
##  [7149] Korea, Republic of        Korea, Republic of       
##  [7151] Korea, Republic of        Korea, Republic of       
##  [7153] Korea, Republic of        Korea, Republic of       
##  [7155] Korea, Republic of        Korea, Republic of       
##  [7157] Korea, Republic of        Korea, Republic of       
##  [7159] Korea, Republic of        Korea, Republic of       
##  [7161] Korea, Republic of        Korea, Republic of       
##  [7163] Korea, Republic of        Korea, Republic of       
##  [7165] Korea, Republic of        Korea, Republic of       
##  [7167] Korea, Republic of        Korea, Republic of       
##  [7169] Korea, Republic of        Korea, Republic of       
##  [7171] Korea, Republic of        Korea, Republic of       
##  [7173] Korea, Republic of        Korea, Republic of       
##  [7175] Korea, Republic of        Korea, Republic of       
##  [7177] Korea, Republic of        Korea, Republic of       
##  [7179] Korea, Republic of        Korea, Republic of       
##  [7181] Korea, Republic of        Korea, Republic of       
##  [7183] Korea, Republic of        Korea, Republic of       
##  [7185] Korea, Republic of        Korea, Republic of       
##  [7187] Korea, Republic of        Korea, Republic of       
##  [7189] Korea, Republic of        Korea, Republic of       
##  [7191] Korea, Republic of        Korea, Republic of       
##  [7193] Korea, Republic of        Korea, Republic of       
##  [7195] Korea, Republic of        Korea, Republic of       
##  [7197] Korea, Republic of        Korea, Republic of       
##  [7199] Korea, Republic of        Korea, Republic of       
##  [7201] Korea, Republic of        Korea, Republic of       
##  [7203] Korea, Republic of        Korea, Republic of       
##  [7205] Korea, Republic of        Korea, Republic of       
##  [7207] Korea, Republic of        Korea, Republic of       
##  [7209] Korea, Republic of        Korea, Republic of       
##  [7211] Korea, Republic of        Korea, Republic of       
##  [7213] Korea, Republic of        Korea, Republic of       
##  [7215] Korea, Republic of        Korea, Republic of       
##  [7217] Korea, Republic of        Korea, Republic of       
##  [7219] Korea, Republic of        Korea, Republic of       
##  [7221] Korea, Republic of        Korea, Republic of       
##  [7223] Korea, Republic of        Korea, Republic of       
##  [7225] Korea, Republic of        Korea, Republic of       
##  [7227] Korea, Republic of        Korea, Republic of       
##  [7229] Korea, Republic of        Korea, Republic of       
##  [7231] Korea, Republic of        Korea, Republic of       
##  [7233] Korea, Republic of        Korea, Republic of       
##  [7235] Korea, Republic of        Korea, Republic of       
##  [7237] Korea, Republic of        Korea, Republic of       
##  [7239] Korea, Republic of        Korea, Republic of       
##  [7241] Korea, Republic of        Korea, Republic of       
##  [7243] Korea, Republic of        Korea, Republic of       
##  [7245] Korea, Republic of        Korea, Republic of       
##  [7247] Korea, Republic of        Korea, Republic of       
##  [7249] Korea, Republic of        Korea, Republic of       
##  [7251] Korea, Republic of        Korea, Republic of       
##  [7253] Korea, Republic of        Korea, Republic of       
##  [7255] Korea, Republic of        Korea, Republic of       
##  [7257] Korea, Republic of        Korea, Republic of       
##  [7259] Korea, Republic of        Korea, Republic of       
##  [7261] Korea, Republic of        Korea, Republic of       
##  [7263] Korea, Republic of        Korea, Republic of       
##  [7265] Korea, Republic of        Korea, Republic of       
##  [7267] Korea, Republic of        Korea, Republic of       
##  [7269] Korea, Republic of        Korea, Republic of       
##  [7271] Korea, Republic of        Korea, Republic of       
##  [7273] Korea, Republic of        Korea, Republic of       
##  [7275] Korea, Republic of        Korea, Republic of       
##  [7277] Korea, Republic of        Korea, Republic of       
##  [7279] Korea, Republic of        Korea, Republic of       
##  [7281] Korea, Republic of        Korea, Republic of       
##  [7283] Korea, Republic of        Korea, Republic of       
##  [7285] Korea, Republic of        Korea, Republic of       
##  [7287] Korea, Republic of        Korea, Republic of       
##  [7289] Korea, Republic of        Korea, Republic of       
##  [7291] Korea, Republic of        Korea, Republic of       
##  [7293] Korea, Republic of        Korea, Republic of       
##  [7295] Korea, Republic of        Korea, Republic of       
##  [7297] Korea, Republic of        Korea, Republic of       
##  [7299] Korea, Republic of        Korea, Republic of       
##  [7301] Korea, Republic of        Korea, Republic of       
##  [7303] Korea, Republic of        Korea, Republic of       
##  [7305] Korea, Republic of        Korea, Republic of       
##  [7307] Korea, Republic of        Korea, Republic of       
##  [7309] Korea, Republic of        Korea, Republic of       
##  [7311] Korea, Republic of        Korea, Republic of       
##  [7313] Korea, Republic of        Korea, Republic of       
##  [7315] Korea, Republic of        Korea, Republic of       
##  [7317] Korea, Republic of        Korea, Republic of       
##  [7319] Korea, Republic of        Korea, Republic of       
##  [7321] Korea, Republic of        Korea, Republic of       
##  [7323] Korea, Republic of        Korea, Republic of       
##  [7325] Korea, Republic of        Korea, Republic of       
##  [7327] Korea, Republic of        Korea, Republic of       
##  [7329] Korea, Republic of        Korea, Republic of       
##  [7331] Korea, Republic of        Korea, Republic of       
##  [7333] Korea, Republic of        Korea, Republic of       
##  [7335] Korea, Republic of        Korea, Republic of       
##  [7337] Korea, Republic of        Korea, Republic of       
##  [7339] Korea, Republic of        Korea, Republic of       
##  [7341] Korea, Republic of        Korea, Republic of       
##  [7343] Korea, Republic of        Korea, Republic of       
##  [7345] Korea, Republic of        Korea, Republic of       
##  [7347] Korea, Republic of        Korea, Republic of       
##  [7349] Korea, Republic of        Korea, Republic of       
##  [7351] Korea, Republic of        Korea, Republic of       
##  [7353] Korea, Republic of        Korea, Republic of       
##  [7355] Korea, Republic of        Korea, Republic of       
##  [7357] Korea, Republic of        Korea, Republic of       
##  [7359] Korea, Republic of        Korea, Republic of       
##  [7361] Korea, Republic of        Korea, Republic of       
##  [7363] Korea, Republic of        Korea, Republic of       
##  [7365] Korea, Republic of        Korea, Republic of       
##  [7367] Korea, Republic of        Korea, Republic of       
##  [7369] Korea, Republic of        Korea, Republic of       
##  [7371] Korea, Republic of        Korea, Republic of       
##  [7373] Korea, Republic of        Korea, Republic of       
##  [7375] Korea, Republic of        Korea, Republic of       
##  [7377] Korea, Republic of        Korea, Republic of       
##  [7379] Korea, Republic of        Korea, Republic of       
##  [7381] Korea, Republic of        Korea, Republic of       
##  [7383] Korea, Republic of        Korea, Republic of       
##  [7385] Korea, Republic of        Korea, Republic of       
##  [7387] Korea, Republic of        Korea, Republic of       
##  [7389] Korea, Republic of        Korea, Republic of       
##  [7391] Korea, Republic of        Korea, Republic of       
##  [7393] Korea, Republic of        Korea, Republic of       
##  [7395] Korea, Republic of        Korea, Republic of       
##  [7397] Korea, Republic of        Korea, Republic of       
##  [7399] Korea, Republic of        Korea, Republic of       
##  [7401] Korea, Republic of        Korea, Republic of       
##  [7403] Korea, Republic of        Korea, Republic of       
##  [7405] Korea, Republic of        Korea, Republic of       
##  [7407] Korea, Republic of        Korea, Republic of       
##  [7409] Korea, Republic of        Korea, Republic of       
##  [7411] Korea, Republic of        Korea, Republic of       
##  [7413] Korea, Republic of        Korea, Republic of       
##  [7415] Korea, Republic of        Korea, Republic of       
##  [7417] Korea, Republic of        Korea, Republic of       
##  [7419] Korea, Republic of        Korea, Republic of       
##  [7421] Korea, Republic of        Korea, Republic of       
##  [7423] Korea, Republic of        Korea, Republic of       
##  [7425] Korea, Republic of        Korea, Republic of       
##  [7427] Korea, Republic of        Korea, Republic of       
##  [7429] Korea, Republic of        Korea, Republic of       
##  [7431] Korea, Republic of        Korea, Republic of       
##  [7433] Korea, Republic of        Korea, Republic of       
##  [7435] Korea, Republic of        Korea, Republic of       
##  [7437] Korea, Republic of        Korea, Republic of       
##  [7439] Korea, Republic of        Korea, Republic of       
##  [7441] Korea, Republic of        Korea, Republic of       
##  [7443] Korea, Republic of        Korea, Republic of       
##  [7445] Korea, Republic of        Korea, Republic of       
##  [7447] Korea, Republic of        Korea, Republic of       
##  [7449] Korea, Republic of        Korea, Republic of       
##  [7451] Korea, Republic of        Korea, Republic of       
##  [7453] Korea, Republic of        Korea, Republic of       
##  [7455] Korea, Republic of        Korea, Republic of       
##  [7457] Korea, Republic of        Korea, Republic of       
##  [7459] Korea, Republic of        Korea, Republic of       
##  [7461] Korea, Republic of        Korea, Republic of       
##  [7463] Korea, Republic of        Korea, Republic of       
##  [7465] Korea, Republic of        Korea, Republic of       
##  [7467] Korea, Republic of        Korea, Republic of       
##  [7469] Korea, Republic of        Korea, Republic of       
##  [7471] Korea, Republic of        Korea, Republic of       
##  [7473] Korea, Republic of        Korea, Republic of       
##  [7475] Korea, Republic of        Korea, Republic of       
##  [7477] Korea, Republic of        Korea, Republic of       
##  [7479] Korea, Republic of        Korea, Republic of       
##  [7481] Korea, Republic of        Korea, Republic of       
##  [7483] Korea, Republic of        Korea, Republic of       
##  [7485] Korea, Republic of        Korea, Republic of       
##  [7487] Korea, Republic of        Korea, Republic of       
##  [7489] Korea, Republic of        Korea, Republic of       
##  [7491] Korea, Republic of        Korea, Republic of       
##  [7493] Korea, Republic of        Korea, Republic of       
##  [7495] Korea, Republic of        Korea, Republic of       
##  [7497] Korea, Republic of        Korea, Republic of       
##  [7499] Korea, Republic of        Korea, Republic of       
##  [7501] Korea, Republic of        Korea, Republic of       
##  [7503] Korea, Republic of        Korea, Republic of       
##  [7505] Korea, Republic of        Korea, Republic of       
##  [7507] Korea, Republic of        Korea, Republic of       
##  [7509] Korea, Republic of        Korea, Republic of       
##  [7511] Korea, Republic of        Korea, Republic of       
##  [7513] Korea, Republic of        Korea, Republic of       
##  [7515] Korea, Republic of        Korea, Republic of       
##  [7517] Korea, Republic of        Korea, Republic of       
##  [7519] Korea, Republic of        Korea, Republic of       
##  [7521] Korea, Republic of        Korea, Republic of       
##  [7523] Korea, Republic of        Korea, Republic of       
##  [7525] Korea, Republic of        Korea, Republic of       
##  [7527] Korea, Republic of        Korea, Republic of       
##  [7529] Korea, Republic of        Korea, Republic of       
##  [7531] Korea, Republic of        Korea, Republic of       
##  [7533] Korea, Republic of        Korea, Republic of       
##  [7535] Korea, Republic of        Korea, Republic of       
##  [7537] Korea, Republic of        Korea, Republic of       
##  [7539] Korea, Republic of        Korea, Republic of       
##  [7541] Korea, Republic of        Korea, Republic of       
##  [7543] Korea, Republic of        Korea, Republic of       
##  [7545] Korea, Republic of        Korea, Republic of       
##  [7547] Korea, Republic of        Korea, Republic of       
##  [7549] Korea, Republic of        Korea, Republic of       
##  [7551] Korea, Republic of        Korea, Republic of       
##  [7553] Korea, Republic of        Korea, Republic of       
##  [7555] Korea, Republic of        Korea, Republic of       
##  [7557] Korea, Republic of        Korea, Republic of       
##  [7559] Korea, Republic of        Korea, Republic of       
##  [7561] Korea, Republic of        Korea, Republic of       
##  [7563] Korea, Republic of        Korea, Republic of       
##  [7565] Korea, Republic of        Korea, Republic of       
##  [7567] Korea, Republic of        Korea, Republic of       
##  [7569] Korea, Republic of        Korea, Republic of       
##  [7571] Korea, Republic of        Korea, Republic of       
##  [7573] Korea, Republic of        Korea, Republic of       
##  [7575] Korea, Republic of        Korea, Republic of       
##  [7577] Korea, Republic of        Korea, Republic of       
##  [7579] Korea, Republic of        Korea, Republic of       
##  [7581] Korea, Republic of        Korea, Republic of       
##  [7583] Korea, Republic of        Korea, Republic of       
##  [7585] Korea, Republic of        Korea, Republic of       
##  [7587] Korea, Republic of        Korea, Republic of       
##  [7589] Korea, Republic of        Korea, Republic of       
##  [7591] Korea, Republic of        Korea, Republic of       
##  [7593] Korea, Republic of        Korea, Republic of       
##  [7595] Korea, Republic of        Korea, Republic of       
##  [7597] Korea, Republic of        Korea, Republic of       
##  [7599] Korea, Republic of        Korea, Republic of       
##  [7601] Korea, Republic of        Korea, Republic of       
##  [7603] Korea, Republic of        Korea, Republic of       
##  [7605] Korea, Republic of        Korea, Republic of       
##  [7607] Korea, Republic of        Korea, Republic of       
##  [7609] Korea, Republic of        Korea, Republic of       
##  [7611] Korea, Republic of        Korea, Republic of       
##  [7613] Korea, Republic of        Korea, Republic of       
##  [7615] Korea, Republic of        Korea, Republic of       
##  [7617] Korea, Republic of        Korea, Republic of       
##  [7619] Korea, Republic of        Korea, Republic of       
##  [7621] Korea, Republic of        Korea, Republic of       
##  [7623] Korea, Republic of        Korea, Republic of       
##  [7625] Korea, Republic of        Korea, Republic of       
##  [7627] Korea, Republic of        Korea, Republic of       
##  [7629] Korea, Republic of        Korea, Republic of       
##  [7631] Korea, Republic of        Korea, Republic of       
##  [7633] Korea, Republic of        Korea, Republic of       
##  [7635] Korea, Republic of        Korea, Republic of       
##  [7637] Korea, Republic of        Korea, Republic of       
##  [7639] Korea, Republic of        Korea, Republic of       
##  [7641] Korea, Republic of        Korea, Republic of       
##  [7643] Korea, Republic of        Korea, Republic of       
##  [7645] Korea, Republic of        Korea, Republic of       
##  [7647] Korea, Republic of        Korea, Republic of       
##  [7649] Korea, Republic of        Korea, Republic of       
##  [7651] Korea, Republic of        Korea, Republic of       
##  [7653] Korea, Republic of        Korea, Republic of       
##  [7655] Korea, Republic of        Korea, Republic of       
##  [7657] Korea, Republic of        Korea, Republic of       
##  [7659] Korea, Republic of        Korea, Republic of       
##  [7661] Korea, Republic of        Korea, Republic of       
##  [7663] Korea, Republic of        Korea, Republic of       
##  [7665] Korea, Republic of        Korea, Republic of       
##  [7667] Korea, Republic of        Korea, Republic of       
##  [7669] Korea, Republic of        Korea, Republic of       
##  [7671] Korea, Republic of        Korea, Republic of       
##  [7673] Korea, Republic of        Korea, Republic of       
##  [7675] Korea, Republic of        Korea, Republic of       
##  [7677] Korea, Republic of        Korea, Republic of       
##  [7679] Korea, Republic of        Korea, Republic of       
##  [7681] Korea, Republic of        Korea, Republic of       
##  [7683] Korea, Republic of        Korea, Republic of       
##  [7685] Korea, Republic of        Korea, Republic of       
##  [7687] Korea, Republic of        Korea, Republic of       
##  [7689] Korea, Republic of        Korea, Republic of       
##  [7691] Korea, Republic of        Korea, Republic of       
##  [7693] Korea, Republic of        Korea, Republic of       
##  [7695] Korea, Republic of        Korea, Republic of       
##  [7697] Korea, Republic of        Korea, Republic of       
##  [7699] Korea, Republic of        Korea, Republic of       
##  [7701] Korea, Republic of        Korea, Republic of       
##  [7703] Korea, Republic of        Korea, Republic of       
##  [7705] Korea, Republic of        Korea, Republic of       
##  [7707] Korea, Republic of        Korea, Republic of       
##  [7709] Korea, Republic of        Korea, Republic of       
##  [7711] Korea, Republic of        Korea, Republic of       
##  [7713] Korea, Republic of        Korea, Republic of       
##  [7715] Korea, Republic of        Korea, Republic of       
##  [7717] Korea, Republic of        Korea, Republic of       
##  [7719] Korea, Republic of        Korea, Republic of       
##  [7721] Korea, Republic of        Korea, Republic of       
##  [7723] Korea, Republic of        Korea, Republic of       
##  [7725] Korea, Republic of        Korea, Republic of       
##  [7727] Korea, Republic of        Korea, Republic of       
##  [7729] Korea, Republic of        Korea, Republic of       
##  [7731] Korea, Republic of        Korea, Republic of       
##  [7733] Korea, Republic of        Korea, Republic of       
##  [7735] Korea, Republic of        Korea, Republic of       
##  [7737] Korea, Republic of        Korea, Republic of       
##  [7739] Korea, Republic of        Korea, Republic of       
##  [7741] Korea, Republic of        Korea, Republic of       
##  [7743] Korea, Republic of        Korea, Republic of       
##  [7745] Korea, Republic of        Korea, Republic of       
##  [7747] Korea, Republic of        Korea, Republic of       
##  [7749] Korea, Republic of        Korea, Republic of       
##  [7751] Korea, Republic of        Korea, Republic of       
##  [7753] Korea, Republic of        Korea, Republic of       
##  [7755] Korea, Republic of        Kuwait                   
##  [7757] Kuwait                    Kuwait                   
##  [7759] Kuwait                    Kuwait                   
##  [7761] Kuwait                    Kuwait                   
##  [7763] Kuwait                    Kuwait                   
##  [7765] Kuwait                    Kuwait                   
##  [7767] Kuwait                    Kuwait                   
##  [7769] Kuwait                    Kuwait                   
##  [7771] Kuwait                    Kuwait                   
##  [7773] Kuwait                    Kuwait                   
##  [7775] Kuwait                    Kuwait                   
##  [7777] Kuwait                    Kuwait                   
##  [7779] Latvia                    Latvia                   
##  [7781] Latvia                    Latvia                   
##  [7783] Latvia                    Latvia                   
##  [7785] Latvia                    Latvia                   
##  [7787] Latvia                    Latvia                   
##  [7789] Latvia                    Latvia                   
##  [7791] Latvia                    Latvia                   
##  [7793] Latvia                    Latvia                   
##  [7795] Latvia                    Latvia                   
##  [7797] Latvia                    Latvia                   
##  [7799] Latvia                    Latvia                   
##  [7801] Latvia                    Latvia                   
##  [7803] Latvia                    Latvia                   
##  [7805] Latvia                    Latvia                   
##  [7807] Latvia                    Latvia                   
##  [7809] Latvia                    Latvia                   
##  [7811] Latvia                    Latvia                   
##  [7813] Latvia                    Latvia                   
##  [7815] Latvia                    Latvia                   
##  [7817] Latvia                    Latvia                   
##  [7819] Latvia                    Latvia                   
##  [7821] Latvia                    Latvia                   
##  [7823] Latvia                    Latvia                   
##  [7825] Latvia                    Latvia                   
##  [7827] Latvia                    Latvia                   
##  [7829] Latvia                    Latvia                   
##  [7831] Latvia                    Latvia                   
##  [7833] Latvia                    Latvia                   
##  [7835] Latvia                    Latvia                   
##  [7837] Latvia                    Latvia                   
##  [7839] Latvia                    Latvia                   
##  [7841] Latvia                    Latvia                   
##  [7843] Latvia                    Latvia                   
##  [7845] Latvia                    Latvia                   
##  [7847] Latvia                    Latvia                   
##  [7849] Latvia                    Latvia                   
##  [7851] Latvia                    Latvia                   
##  [7853] Latvia                    Latvia                   
##  [7855] Latvia                    Latvia                   
##  [7857] Latvia                    Latvia                   
##  [7859] Latvia                    Latvia                   
##  [7861] Latvia                    Latvia                   
##  [7863] Latvia                    Latvia                   
##  [7865] Latvia                    Latvia                   
##  [7867] Latvia                    Latvia                   
##  [7869] Latvia                    Latvia                   
##  [7871] Latvia                    Latvia                   
##  [7873] Latvia                    Latvia                   
##  [7875] Latvia                    Latvia                   
##  [7877] Latvia                    Latvia                   
##  [7879] Latvia                    Latvia                   
##  [7881] Latvia                    Latvia                   
##  [7883] Latvia                    Latvia                   
##  [7885] Latvia                    Latvia                   
##  [7887] Latvia                    Latvia                   
##  [7889] Latvia                    Latvia                   
##  [7891] Latvia                    Latvia                   
##  [7893] Latvia                    Latvia                   
##  [7895] Latvia                    Latvia                   
##  [7897] Latvia                    Latvia                   
##  [7899] Latvia                    Latvia                   
##  [7901] Latvia                    Latvia                   
##  [7903] Latvia                    Latvia                   
##  [7905] Latvia                    Latvia                   
##  [7907] Latvia                    Latvia                   
##  [7909] Latvia                    Latvia                   
##  [7911] Latvia                    Latvia                   
##  [7913] Latvia                    Latvia                   
##  [7915] Latvia                    Latvia                   
##  [7917] Latvia                    Latvia                   
##  [7919] Latvia                    Latvia                   
##  [7921] Latvia                    Latvia                   
##  [7923] Latvia                    Latvia                   
##  [7925] Latvia                    Latvia                   
##  [7927] Latvia                    Latvia                   
##  [7929] Latvia                    Latvia                   
##  [7931] Latvia                    Latvia                   
##  [7933] Latvia                    Latvia                   
##  [7935] Latvia                    Latvia                   
##  [7937] Latvia                    Latvia                   
##  [7939] Latvia                    Latvia                   
##  [7941] Lebanon                   Lebanon                  
##  [7943] Lebanon                   Lebanon                  
##  [7945] Lebanon                   Lebanon                  
##  [7947] Lebanon                   Lebanon                  
##  [7949] Lebanon                   Lebanon                  
##  [7951] Lebanon                   Lebanon                  
##  [7953] Lebanon                   Lebanon                  
##  [7955] Lebanon                   Lebanon                  
##  [7957] Lebanon                   Lebanon                  
##  [7959] Lebanon                   Lebanon                  
##  [7961] Liberia                   Liberia                  
##  [7963] Liberia                   Liberia                  
##  [7965] Liberia                   Liberia                  
##  [7967] Liberia                   Liberia                  
##  [7969] Liberia                   Liberia                  
##  [7971] Liberia                   Liberia                  
##  [7973] Liberia                   Liberia                  
##  [7975] Liberia                   Liberia                  
##  [7977] Liberia                   Liberia                  
##  [7979] Liberia                   Liberia                  
##  [7981] Liberia                   Liberia                  
##  [7983] Liberia                   Liberia                  
##  [7985] Liberia                   Liberia                  
##  [7987] Liberia                   Liberia                  
##  [7989] Liberia                   Liberia                  
##  [7991] Liberia                   Liberia                  
##  [7993] Liberia                   Liberia                  
##  [7995] Liberia                   Liberia                  
##  [7997] Liberia                   Liberia                  
##  [7999] Liberia                   Liberia                  
##  [8001] Liberia                   Liberia                  
##  [8003] Liberia                   Liberia                  
##  [8005] Liberia                   Liberia                  
##  [8007] Liberia                   Liberia                  
##  [8009] Liberia                   Liberia                  
##  [8011] Liberia                   Liberia                  
##  [8013] Liberia                   Liberia                  
##  [8015] Liberia                   Liberia                  
##  [8017] Liberia                   Liberia                  
##  [8019] Liberia                   Liberia                  
##  [8021] Liberia                   Liberia                  
##  [8023] Liberia                   Liberia                  
##  [8025] Liberia                   Liberia                  
##  [8027] Liberia                   Liberia                  
##  [8029] Liberia                   Liberia                  
##  [8031] Liberia                   Liberia                  
##  [8033] Liberia                   Liberia                  
##  [8035] Liberia                   Liberia                  
##  [8037] Libya                     Libya                    
##  [8039] Libya                     Libya                    
##  [8041] Libya                     Libya                    
##  [8043] Libya                     Libya                    
##  [8045] Libya                     Libya                    
##  [8047] Libya                     Libya                    
##  [8049] Libya                     Libya                    
##  [8051] Libya                     Libya                    
##  [8053] Libya                     Libya                    
##  [8055] Libya                     Libya                    
##  [8057] Libya                     Libya                    
##  [8059] Libya                     Libya                    
##  [8061] Libya                     Libya                    
##  [8063] Libya                     Libya                    
##  [8065] Libya                     Libya                    
##  [8067] Libya                     Libya                    
##  [8069] Libya                     Libya                    
##  [8071] Libya                     Libya                    
##  [8073] Libya                     Libya                    
##  [8075] Libya                     Libya                    
##  [8077] Libya                     Libya                    
##  [8079] Libya                     Libya                    
##  [8081] Libya                     Libya                    
##  [8083] Libya                     Libya                    
##  [8085] Libya                     Libya                    
##  [8087] Libya                     Libya                    
##  [8089] Libya                     Libya                    
##  [8091] Libya                     Libya                    
##  [8093] Lithuania                 Lithuania                
##  [8095] Lithuania                 Lithuania                
##  [8097] Lithuania                 Lithuania                
##  [8099] Lithuania                 Lithuania                
##  [8101] Lithuania                 Lithuania                
##  [8103] Lithuania                 Lithuania                
##  [8105] Lithuania                 Lithuania                
##  [8107] Lithuania                 Lithuania                
##  [8109] Lithuania                 Lithuania                
##  [8111] Lithuania                 Lithuania                
##  [8113] Lithuania                 Lithuania                
##  [8115] Lithuania                 Lithuania                
##  [8117] Lithuania                 Lithuania                
##  [8119] Lithuania                 Lithuania                
##  [8121] Lithuania                 Lithuania                
##  [8123] Lithuania                 Lithuania                
##  [8125] Lithuania                 Lithuania                
##  [8127] Lithuania                 Lithuania                
##  [8129] Lithuania                 Lithuania                
##  [8131] Lithuania                 Lithuania                
##  [8133] Lithuania                 Lithuania                
##  [8135] Lithuania                 Lithuania                
##  [8137] Lithuania                 Lithuania                
##  [8139] Lithuania                 Lithuania                
##  [8141] Lithuania                 Lithuania                
##  [8143] Lithuania                 Lithuania                
##  [8145] Lithuania                 Lithuania                
##  [8147] Lithuania                 Lithuania                
##  [8149] Lithuania                 Lithuania                
##  [8151] Lithuania                 Lithuania                
##  [8153] Lithuania                 Lithuania                
##  [8155] Lithuania                 Lithuania                
##  [8157] Lithuania                 Lithuania                
##  [8159] Lithuania                 Lithuania                
##  [8161] Lithuania                 Lithuania                
##  [8163] Lithuania                 Lithuania                
##  [8165] Lithuania                 Lithuania                
##  [8167] Lithuania                 Lithuania                
##  [8169] Lithuania                 Lithuania                
##  [8171] Lithuania                 Lithuania                
##  [8173] Lithuania                 Lithuania                
##  [8175] Lithuania                 Lithuania                
##  [8177] Lithuania                 Lithuania                
##  [8179] Lithuania                 Lithuania                
##  [8181] Lithuania                 Lithuania                
##  [8183] Lithuania                 Lithuania                
##  [8185] Lithuania                 Lithuania                
##  [8187] Lithuania                 Lithuania                
##  [8189] Lithuania                 Lithuania                
##  [8191] Lithuania                 Lithuania                
##  [8193] Lithuania                 Lithuania                
##  [8195] Lithuania                 Lithuania                
##  [8197] Lithuania                 Lithuania                
##  [8199] Lithuania                 Lithuania                
##  [8201] Lithuania                 Lithuania                
##  [8203] Lithuania                 Lithuania                
##  [8205] Lithuania                 Lithuania                
##  [8207] Lithuania                 Lithuania                
##  [8209] Lithuania                 Lithuania                
##  [8211] Lithuania                 Lithuania                
##  [8213] Lithuania                 Lithuania                
##  [8215] Lithuania                 Lithuania                
##  [8217] Lithuania                 Lithuania                
##  [8219] Lithuania                 Lithuania                
##  [8221] Lithuania                 Lithuania                
##  [8223] Lithuania                 Lithuania                
##  [8225] Lithuania                 Lithuania                
##  [8227] Lithuania                 Lithuania                
##  [8229] Lithuania                 Lithuania                
##  [8231] Lithuania                 Lithuania                
##  [8233] Lithuania                 Lithuania                
##  [8235] Lithuania                 Lithuania                
##  [8237] Lithuania                 Lithuania                
##  [8239] Lithuania                 Lithuania                
##  [8241] Lithuania                 Lithuania                
##  [8243] Lithuania                 Lithuania                
##  [8245] Lithuania                 Lithuania                
##  [8247] Lithuania                 Lithuania                
##  [8249] Lithuania                 Lithuania                
##  [8251] Lithuania                 Lithuania                
##  [8253] Lithuania                 Lithuania                
##  [8255] Lithuania                 Lithuania                
##  [8257] Lithuania                 Lithuania                
##  [8259] Lithuania                 Lithuania                
##  [8261] Lithuania                 Lithuania                
##  [8263] Lithuania                 Lithuania                
##  [8265] Lithuania                 Lithuania                
##  [8267] Lithuania                 Lithuania                
##  [8269] Lithuania                 Lithuania                
##  [8271] Lithuania                 Lithuania                
##  [8273] Lithuania                 Lithuania                
##  [8275] Lithuania                 Lithuania                
##  [8277] Lithuania                 Lithuania                
##  [8279] Lithuania                 Lithuania                
##  [8281] Lithuania                 Lithuania                
##  [8283] Lithuania                 Lithuania                
##  [8285] Lithuania                 Lithuania                
##  [8287] Lithuania                 Lithuania                
##  [8289] Lithuania                 Lithuania                
##  [8291] Lithuania                 Lithuania                
##  [8293] Lithuania                 Lithuania                
##  [8295] Lithuania                 Lithuania                
##  [8297] Lithuania                 Lithuania                
##  [8299] Lithuania                 Lithuania                
##  [8301] Lithuania                 Lithuania                
##  [8303] Lithuania                 Lithuania                
##  [8305] Lithuania                 Lithuania                
##  [8307] Lithuania                 Madagascar               
##  [8309] Madagascar                Madagascar               
##  [8311] Madagascar                Madagascar               
##  [8313] Madagascar                Madagascar               
##  [8315] Madagascar                Madagascar               
##  [8317] Madagascar                Madagascar               
##  [8319] Madagascar                Madagascar               
##  [8321] Madagascar                Madagascar               
##  [8323] Madagascar                Madagascar               
##  [8325] Madagascar                Madagascar               
##  [8327] Madagascar                Madagascar               
##  [8329] Madagascar                Madagascar               
##  [8331] Madagascar                Madagascar               
##  [8333] Madagascar                Madagascar               
##  [8335] Madagascar                Madagascar               
##  [8337] Madagascar                Madagascar               
##  [8339] Madagascar                Madagascar               
##  [8341] Madagascar                Madagascar               
##  [8343] Malaysia                  Malaysia                 
##  [8345] Malaysia                  Malaysia                 
##  [8347] Malaysia                  Malaysia                 
##  [8349] Malaysia                  Malaysia                 
##  [8351] Malaysia                  Malaysia                 
##  [8353] Malaysia                  Malaysia                 
##  [8355] Malaysia                  Malaysia                 
##  [8357] Malaysia                  Malaysia                 
##  [8359] Malaysia                  Malaysia                 
##  [8361] Malaysia                  Malaysia                 
##  [8363] Malaysia                  Malaysia                 
##  [8365] Malaysia                  Malaysia                 
##  [8367] Malaysia                  Malaysia                 
##  [8369] Malaysia                  Malaysia                 
##  [8371] Malaysia                  Malaysia                 
##  [8373] Malaysia                  Malaysia                 
##  [8375] Malaysia                  Malaysia                 
##  [8377] Malaysia                  Malaysia                 
##  [8379] Malaysia                  Malaysia                 
##  [8381] Malaysia                  Malaysia                 
##  [8383] Malaysia                  Malaysia                 
##  [8385] Malaysia                  Malaysia                 
##  [8387] Malaysia                  Malaysia                 
##  [8389] Malaysia                  Malaysia                 
##  [8391] Malaysia                  Malaysia                 
##  [8393] Malaysia                  Malaysia                 
##  [8395] Malaysia                  Malaysia                 
##  [8397] Malaysia                  Malaysia                 
##  [8399] Malaysia                  Malaysia                 
##  [8401] Malaysia                  Malaysia                 
##  [8403] Malaysia                  Malaysia                 
##  [8405] Malaysia                  Malaysia                 
##  [8407] Malaysia                  Malaysia                 
##  [8409] Malaysia                  Malaysia                 
##  [8411] Malaysia                  Malaysia                 
##  [8413] Malaysia                  Malaysia                 
##  [8415] Malaysia                  Malaysia                 
##  [8417] Malaysia                  Malaysia                 
##  [8419] Malaysia                  Malaysia                 
##  [8421] Malaysia                  Malaysia                 
##  [8423] Malaysia                  Malaysia                 
##  [8425] Malaysia                  Malaysia                 
##  [8427] Malaysia                  Malaysia                 
##  [8429] Malaysia                  Malaysia                 
##  [8431] Malaysia                  Malaysia                 
##  [8433] Malaysia                  Malaysia                 
##  [8435] Malaysia                  Malaysia                 
##  [8437] Malaysia                  Malaysia                 
##  [8439] Malaysia                  Malaysia                 
##  [8441] Malaysia                  Malaysia                 
##  [8443] Malaysia                  Malaysia                 
##  [8445] Malaysia                  Malaysia                 
##  [8447] Malaysia                  Malaysia                 
##  [8449] Malaysia                  Malaysia                 
##  [8451] Malaysia                  Malaysia                 
##  [8453] Malaysia                  Malaysia                 
##  [8455] Malaysia                  Malaysia                 
##  [8457] Malaysia                  Malaysia                 
##  [8459] Malaysia                  Malaysia                 
##  [8461] Malaysia                  Malaysia                 
##  [8463] Malaysia                  Malaysia                 
##  [8465] Malaysia                  Malaysia                 
##  [8467] Malaysia                  Malaysia                 
##  [8469] Malaysia                  Malaysia                 
##  [8471] Malaysia                  Malaysia                 
##  [8473] Malaysia                  Malaysia                 
##  [8475] Malaysia                  Malaysia                 
##  [8477] Malaysia                  Malaysia                 
##  [8479] Malaysia                  Malaysia                 
##  [8481] Malaysia                  Malaysia                 
##  [8483] Malaysia                  Malaysia                 
##  [8485] Malaysia                  Malaysia                 
##  [8487] Malaysia                  Malaysia                 
##  [8489] Malaysia                  Malaysia                 
##  [8491] Malaysia                  Malaysia                 
##  [8493] Malaysia                  Malaysia                 
##  [8495] Malaysia                  Malaysia                 
##  [8497] Malaysia                  Malaysia                 
##  [8499] Malaysia                  Malaysia                 
##  [8501] Malaysia                  Malaysia                 
##  [8503] Malaysia                  Malaysia                 
##  [8505] Malaysia                  Malaysia                 
##  [8507] Malaysia                  Malaysia                 
##  [8509] Maldives                  Maldives                 
##  [8511] Maldives                  Maldives                 
##  [8513] Maldives                  Maldives                 
##  [8515] Maldives                  Maldives                 
##  [8517] Maldives                  Maldives                 
##  [8519] Maldives                  Maldives                 
##  [8521] Malta                     Malta                    
##  [8523] Malta                     Malta                    
##  [8525] Malta                     Malta                    
##  [8527] Malta                     Malta                    
##  [8529] Malta                     Malta                    
##  [8531] Malta                     Malta                    
##  [8533] Malta                     Malta                    
##  [8535] Malta                     Malta                    
##  [8537] Malta                     Malta                    
##  [8539] Malta                     Malta                    
##  [8541] Malta                     Malta                    
##  [8543] Malta                     Malta                    
##  [8545] Malta                     Malta                    
##  [8547] Malta                     Malta                    
##  [8549] Malta                     Malta                    
##  [8551] Malta                     Malta                    
##  [8553] Malta                     Malta                    
##  [8555] Malta                     Malta                    
##  [8557] Malta                     Malta                    
##  [8559] Malta                     Malta                    
##  [8561] Malta                     Malta                    
##  [8563] Malta                     Malta                    
##  [8565] Malta                     Malta                    
##  [8567] Malta                     Malta                    
##  [8569] Malta                     Malta                    
##  [8571] Malta                     Malta                    
##  [8573] Malta                     Malta                    
##  [8575] Malta                     Malta                    
##  [8577] Malta                     Malta                    
##  [8579] Malta                     Malta                    
##  [8581] Malta                     Malta                    
##  [8583] Malta                     Malta                    
##  [8585] Malta                     Malta                    
##  [8587] Malta                     Malta                    
##  [8589] Malta                     Malta                    
##  [8591] Malta                     Malta                    
##  [8593] Malta                     Malta                    
##  [8595] Malta                     Malta                    
##  [8597] Malta                     Malta                    
##  [8599] Malta                     Malta                    
##  [8601] Malta                     Malta                    
##  [8603] Malta                     Malta                    
##  [8605] Malta                     Malta                    
##  [8607] Malta                     Malta                    
##  [8609] Malta                     Malta                    
##  [8611] Malta                     Malta                    
##  [8613] Malta                     Malta                    
##  [8615] Malta                     Malta                    
##  [8617] Malta                     Malta                    
##  [8619] Malta                     Malta                    
##  [8621] Malta                     Malta                    
##  [8623] Malta                     Malta                    
##  [8625] Marshall Islands          Marshall Islands         
##  [8627] Marshall Islands          Marshall Islands         
##  [8629] Marshall Islands          Marshall Islands         
##  [8631] Marshall Islands          Marshall Islands         
##  [8633] Marshall Islands          Marshall Islands         
##  [8635] Marshall Islands          Marshall Islands         
##  [8637] Marshall Islands          Martinique               
##  [8639] Martinique                Martinique               
##  [8641] Martinique                Martinique               
##  [8643] Martinique                Martinique               
##  [8645] Martinique                Martinique               
##  [8647] Martinique                Martinique               
##  [8649] Martinique                Martinique               
##  [8651] Martinique                Martinique               
##  [8653] Martinique                Mauritania               
##  [8655] Mauritania                Mauritania               
##  [8657] Mauritania                Mauritania               
##  [8659] Mauritania                Mauritania               
##  [8661] Mauritania                Mauritania               
##  [8663] Mauritania                Mauritania               
##  [8665] Mauritania                Mauritania               
##  [8667] Mauritania                Mauritania               
##  [8669] Mauritania                Mauritania               
##  [8671] Mauritania                Mauritania               
##  [8673] Mauritania                Mauritania               
##  [8675] Mauritania                Mauritania               
##  [8677] Mauritania                Mauritania               
##  [8679] Mauritania                Mauritania               
##  [8681] Mauritania                Mauritania               
##  [8683] Mauritania                Mauritania               
##  [8685] Mauritania                Mauritania               
##  [8687] Mauritania                Mauritania               
##  [8689] Mauritania                Mauritania               
##  [8691] Mauritania                Mauritania               
##  [8693] Mauritania                Mauritania               
##  [8695] Mauritania                Mauritania               
##  [8697] Mauritania                Mauritania               
##  [8699] Mauritania                Mauritania               
##  [8701] Mauritania                Mauritania               
##  [8703] Mauritania                Mauritania               
##  [8705] Mauritania                Mauritania               
##  [8707] Mauritania                Mauritania               
##  [8709] Mauritania                Mauritania               
##  [8711] Mauritania                Mauritania               
##  [8713] Mauritania                Mauritania               
##  [8715] Mauritania                Mauritania               
##  [8717] Mauritania                Mauritania               
##  [8719] Mauritania                Mauritania               
##  [8721] Mauritania                Mauritania               
##  [8723] Mauritania                Mauritania               
##  [8725] Mauritania                Mauritania               
##  [8727] Mauritania                Mauritania               
##  [8729] Mauritania                Mauritania               
##  [8731] Mauritania                Mauritania               
##  [8733] Mauritania                Mauritania               
##  [8735] Mauritania                Mauritania               
##  [8737] Mauritania                Mauritania               
##  [8739] Mauritania                Mauritania               
##  [8741] Mauritania                Mauritania               
##  [8743] Mauritania                Mauritania               
##  [8745] Mauritania                Mauritania               
##  [8747] Mauritius                 Mauritius                
##  [8749] Mauritius                 Mauritius                
##  [8751] Mauritius                 Mauritius                
##  [8753] Mauritius                 Mauritius                
##  [8755] Mauritius                 Mauritius                
##  [8757] Mauritius                 Mauritius                
##  [8759] Mauritius                 Mauritius                
##  [8761] Mauritius                 Mauritius                
##  [8763] Mauritius                 Mauritius                
##  [8765] Mauritius                 Mauritius                
##  [8767] Mauritius                 Mauritius                
##  [8769] Mauritius                 Mauritius                
##  [8771] Mauritius                 Mauritius                
##  [8773] Mauritius                 Mauritius                
##  [8775] Mauritius                 Mauritius                
##  [8777] Mayotte                   Mayotte                  
##  [8779] Mayotte                   Mayotte                  
##  [8781] Mayotte                   Mayotte                  
##  [8783] Mayotte                   Mayotte                  
##  [8785] Mayotte                   Mayotte                  
##  [8787] Mayotte                   Mayotte                  
##  [8789] Mayotte                   Mayotte                  
##  [8791] Mexico                    Mexico                   
##  [8793] Mexico                    Mexico                   
##  [8795] Mexico                    Mexico                   
##  [8797] Mexico                    Mexico                   
##  [8799] Mexico                    Mexico                   
##  [8801] Mexico                    Mexico                   
##  [8803] Mexico                    Mexico                   
##  [8805] Mexico                    Mexico                   
##  [8807] Mexico                    Mexico                   
##  [8809] Mexico                    Mexico                   
##  [8811] Mexico                    Mexico                   
##  [8813] Mexico                    Mexico                   
##  [8815] Mexico                    Mexico                   
##  [8817] Mexico                    Mexico                   
##  [8819] Mexico                    Mexico                   
##  [8821] Mexico                    Mexico                   
##  [8823] Mexico                    Mexico                   
##  [8825] Mexico                    Mexico                   
##  [8827] Mexico                    Mexico                   
##  [8829] Mexico                    Mexico                   
##  [8831] Mexico                    Mexico                   
##  [8833] Mexico                    Mexico                   
##  [8835] Mexico                    Mexico                   
##  [8837] Mexico                    Mexico                   
##  [8839] Mexico                    Mexico                   
##  [8841] Mexico                    Mexico                   
##  [8843] Mexico                    Mexico                   
##  [8845] Mexico                    Mexico                   
##  [8847] Mexico                    Mexico                   
##  [8849] Mexico                    Mexico                   
##  [8851] Mexico                    Mexico                   
##  [8853] Mexico                    Mexico                   
##  [8855] Mexico                    Mexico                   
##  [8857] Mexico                    Mexico                   
##  [8859] Mexico                    Mexico                   
##  [8861] Mexico                    Mexico                   
##  [8863] Mexico                    Mexico                   
##  [8865] Mexico                    Mexico                   
##  [8867] Mexico                    Mexico                   
##  [8869] Mexico                    Mexico                   
##  [8871] Mexico                    Mexico                   
##  [8873] Mexico                    Mexico                   
##  [8875] Mexico                    Mexico                   
##  [8877] Mexico                    Mexico                   
##  [8879] Mexico                    Mexico                   
##  [8881] Mexico                    Mexico                   
##  [8883] Mexico                    Mexico                   
##  [8885] Mexico                    Mexico                   
##  [8887] Mexico                    Mexico                   
##  [8889] Mexico                    Mexico                   
##  [8891] Mexico                    Mexico                   
##  [8893] Mexico                    Mexico                   
##  [8895] Mexico                    Mexico                   
##  [8897] Mexico                    Mexico                   
##  [8899] Mexico                    Mexico                   
##  [8901] Mexico                    Mexico                   
##  [8903] Mexico                    Mexico                   
##  [8905] Mexico                    Mexico                   
##  [8907] Mexico                    Mexico                   
##  [8909] Mexico                    Mexico                   
##  [8911] Mexico                    Mexico                   
##  [8913] Mexico                    Mexico                   
##  [8915] Mexico                    Mexico                   
##  [8917] Mexico                    Mexico                   
##  [8919] Mexico                    Mexico                   
##  [8921] Mexico                    Mexico                   
##  [8923] Mexico                    Mexico                   
##  [8925] Mexico                    Mexico                   
##  [8927] Mexico                    Mexico                   
##  [8929] Mexico                    Mexico                   
##  [8931] Mexico                    Mexico                   
##  [8933] Mexico                    Mexico                   
##  [8935] Mexico                    Mexico                   
##  [8937] Mexico                    Mexico                   
##  [8939] Mexico                    Mexico                   
##  [8941] Mexico                    Mexico                   
##  [8943] Mexico                    Mexico                   
##  [8945] Mexico                    Mexico                   
##  [8947] Mexico                    Mexico                   
##  [8949] Mexico                    Mexico                   
##  [8951] Mexico                    Mexico                   
##  [8953] Mexico                    Mexico                   
##  [8955] Mexico                    Mexico                   
##  [8957] Mexico                    Mexico                   
##  [8959] Mexico                    Mexico                   
##  [8961] Mexico                    Mexico                   
##  [8963] Mexico                    Mexico                   
##  [8965] Mexico                    Mexico                   
##  [8967] Mexico                    Mexico                   
##  [8969] Mexico                    Mexico                   
##  [8971] Mexico                    Mexico                   
##  [8973] Mexico                    Mexico                   
##  [8975] Mexico                    Mexico                   
##  [8977] Mexico                    Mexico                   
##  [8979] Mexico                    Mexico                   
##  [8981] Mexico                    Mexico                   
##  [8983] Mexico                    Mexico                   
##  [8985] Mexico                    Mexico                   
##  [8987] Mexico                    Mexico                   
##  [8989] Micronesia, Fed.States of Micronesia, Fed.States of
##  [8991] Micronesia, Fed.States of Micronesia, Fed.States of
##  [8993] Micronesia, Fed.States of Micronesia, Fed.States of
##  [8995] Micronesia, Fed.States of Micronesia, Fed.States of
##  [8997] Micronesia, Fed.States of Micronesia, Fed.States of
##  [8999] Micronesia, Fed.States of Micronesia, Fed.States of
##  [9001] Micronesia, Fed.States of Monaco                   
##  [9003] Montenegro                Montenegro               
##  [9005] Montenegro                Montenegro               
##  [9007] Montenegro                Montenegro               
##  [9009] Montenegro                Montenegro               
##  [9011] Montenegro                Montenegro               
##  [9013] Montenegro                Montenegro               
##  [9015] Montenegro                Montenegro               
##  [9017] Montenegro                Montenegro               
##  [9019] Montenegro                Montenegro               
##  [9021] Montenegro                Montenegro               
##  [9023] Montenegro                Montenegro               
##  [9025] Montenegro                Montenegro               
##  [9027] Montserrat                Morocco                  
##  [9029] Morocco                   Morocco                  
##  [9031] Morocco                   Morocco                  
##  [9033] Morocco                   Morocco                  
##  [9035] Morocco                   Morocco                  
##  [9037] Morocco                   Morocco                  
##  [9039] Morocco                   Morocco                  
##  [9041] Morocco                   Morocco                  
##  [9043] Morocco                   Morocco                  
##  [9045] Morocco                   Morocco                  
##  [9047] Morocco                   Morocco                  
##  [9049] Morocco                   Morocco                  
##  [9051] Morocco                   Morocco                  
##  [9053] Morocco                   Morocco                  
##  [9055] Morocco                   Morocco                  
##  [9057] Morocco                   Morocco                  
##  [9059] Morocco                   Morocco                  
##  [9061] Morocco                   Morocco                  
##  [9063] Morocco                   Morocco                  
##  [9065] Morocco                   Morocco                  
##  [9067] Morocco                   Morocco                  
##  [9069] Morocco                   Morocco                  
##  [9071] Morocco                   Morocco                  
##  [9073] Morocco                   Morocco                  
##  [9075] Morocco                   Morocco                  
##  [9077] Morocco                   Morocco                  
##  [9079] Morocco                   Morocco                  
##  [9081] Morocco                   Morocco                  
##  [9083] Morocco                   Morocco                  
##  [9085] Morocco                   Morocco                  
##  [9087] Morocco                   Morocco                  
##  [9089] Morocco                   Morocco                  
##  [9091] Morocco                   Morocco                  
##  [9093] Morocco                   Morocco                  
##  [9095] Morocco                   Morocco                  
##  [9097] Morocco                   Morocco                  
##  [9099] Morocco                   Morocco                  
##  [9101] Morocco                   Morocco                  
##  [9103] Morocco                   Morocco                  
##  [9105] Morocco                   Morocco                  
##  [9107] Morocco                   Morocco                  
##  [9109] Morocco                   Morocco                  
##  [9111] Morocco                   Morocco                  
##  [9113] Morocco                   Morocco                  
##  [9115] Morocco                   Morocco                  
##  [9117] Morocco                   Morocco                  
##  [9119] Morocco                   Morocco                  
##  [9121] Morocco                   Morocco                  
##  [9123] Morocco                   Morocco                  
##  [9125] Morocco                   Morocco                  
##  [9127] Morocco                   Morocco                  
##  [9129] Morocco                   Morocco                  
##  [9131] Morocco                   Morocco                  
##  [9133] Morocco                   Morocco                  
##  [9135] Morocco                   Morocco                  
##  [9137] Morocco                   Morocco                  
##  [9139] Morocco                   Morocco                  
##  [9141] Morocco                   Morocco                  
##  [9143] Morocco                   Morocco                  
##  [9145] Morocco                   Morocco                  
##  [9147] Morocco                   Morocco                  
##  [9149] Morocco                   Morocco                  
##  [9151] Morocco                   Morocco                  
##  [9153] Morocco                   Morocco                  
##  [9155] Morocco                   Morocco                  
##  [9157] Morocco                   Morocco                  
##  [9159] Morocco                   Morocco                  
##  [9161] Morocco                   Morocco                  
##  [9163] Morocco                   Morocco                  
##  [9165] Morocco                   Morocco                  
##  [9167] Morocco                   Morocco                  
##  [9169] Morocco                   Morocco                  
##  [9171] Morocco                   Morocco                  
##  [9173] Morocco                   Morocco                  
##  [9175] Morocco                   Morocco                  
##  [9177] Morocco                   Morocco                  
##  [9179] Morocco                   Morocco                  
##  [9181] Mozambique                Mozambique               
##  [9183] Mozambique                Mozambique               
##  [9185] Mozambique                Mozambique               
##  [9187] Mozambique                Mozambique               
##  [9189] Mozambique                Mozambique               
##  [9191] Mozambique                Mozambique               
##  [9193] Mozambique                Mozambique               
##  [9195] Mozambique                Mozambique               
##  [9197] Mozambique                Mozambique               
##  [9199] Mozambique                Mozambique               
##  [9201] Mozambique                Mozambique               
##  [9203] Mozambique                Mozambique               
##  [9205] Mozambique                Mozambique               
##  [9207] Mozambique                Mozambique               
##  [9209] Mozambique                Mozambique               
##  [9211] Myanmar                   Myanmar                  
##  [9213] Myanmar                   Myanmar                  
##  [9215] Myanmar                   Namibia                  
##  [9217] Namibia                   Namibia                  
##  [9219] Namibia                   Namibia                  
##  [9221] Namibia                   Namibia                  
##  [9223] Namibia                   Namibia                  
##  [9225] Namibia                   Namibia                  
##  [9227] Namibia                   Namibia                  
##  [9229] Namibia                   Namibia                  
##  [9231] Namibia                   Namibia                  
##  [9233] Namibia                   Namibia                  
##  [9235] Namibia                   Namibia                  
##  [9237] Namibia                   Namibia                  
##  [9239] Namibia                   Namibia                  
##  [9241] Namibia                   Namibia                  
##  [9243] Namibia                   Namibia                  
##  [9245] Namibia                   Namibia                  
##  [9247] Namibia                   Namibia                  
##  [9249] Namibia                   Namibia                  
##  [9251] Namibia                   Namibia                  
##  [9253] Namibia                   Namibia                  
##  [9255] Namibia                   Namibia                  
##  [9257] Namibia                   Namibia                  
##  [9259] Namibia                   Namibia                  
##  [9261] Namibia                   Namibia                  
##  [9263] Namibia                   Namibia                  
##  [9265] Namibia                   Namibia                  
##  [9267] Namibia                   Namibia                  
##  [9269] Namibia                   Namibia                  
##  [9271] Namibia                   Namibia                  
##  [9273] Namibia                   Namibia                  
##  [9275] Namibia                   Namibia                  
##  [9277] Namibia                   Namibia                  
##  [9279] Namibia                   Namibia                  
##  [9281] Namibia                   Namibia                  
##  [9283] Namibia                   Namibia                  
##  [9285] Namibia                   Namibia                  
##  [9287] Namibia                   Namibia                  
##  [9289] Namibia                   Namibia                  
##  [9291] Namibia                   Nauru                    
##  [9293] Nauru                     Nauru                    
##  [9295] Nauru                     Nauru                    
##  [9297] Nauru                     Nauru                    
##  [9299] Nauru                     Nauru                    
##  [9301] Netherlands               Netherlands              
##  [9303] Netherlands               Netherlands              
##  [9305] Netherlands               Netherlands              
##  [9307] Netherlands               Netherlands              
##  [9309] Netherlands               Netherlands              
##  [9311] Netherlands               Netherlands              
##  [9313] Netherlands               Netherlands              
##  [9315] Netherlands               Netherlands              
##  [9317] Netherlands               Netherlands              
##  [9319] Netherlands               Netherlands              
##  [9321] Netherlands               Netherlands              
##  [9323] Netherlands               Netherlands              
##  [9325] Netherlands               Netherlands              
##  [9327] Netherlands               Netherlands              
##  [9329] Netherlands               Netherlands              
##  [9331] Netherlands               Netherlands              
##  [9333] Netherlands               Netherlands              
##  [9335] Netherlands               Netherlands              
##  [9337] Netherlands               Netherlands              
##  [9339] Netherlands               Netherlands              
##  [9341] Netherlands               Netherlands              
##  [9343] Netherlands               Netherlands              
##  [9345] Netherlands               Netherlands              
##  [9347] Netherlands               Netherlands              
##  [9349] Netherlands               Netherlands              
##  [9351] Netherlands               Netherlands              
##  [9353] Netherlands               Netherlands              
##  [9355] Netherlands               Netherlands              
##  [9357] Netherlands               Netherlands              
##  [9359] Netherlands               Netherlands              
##  [9361] Netherlands               Netherlands              
##  [9363] Netherlands               Netherlands              
##  [9365] Netherlands               Netherlands              
##  [9367] Netherlands               Netherlands              
##  [9369] Netherlands               Netherlands              
##  [9371] Netherlands               Netherlands              
##  [9373] Netherlands               Netherlands              
##  [9375] Netherlands               Netherlands              
##  [9377] Netherlands               Netherlands              
##  [9379] Netherlands               Netherlands              
##  [9381] Netherlands               Netherlands              
##  [9383] Netherlands               Netherlands              
##  [9385] Netherlands               Netherlands              
##  [9387] Netherlands               Netherlands              
##  [9389] Netherlands               Netherlands              
##  [9391] Netherlands               Netherlands              
##  [9393] Netherlands               Netherlands              
##  [9395] Netherlands               Netherlands              
##  [9397] Netherlands               Netherlands              
##  [9399] Netherlands               Netherlands              
##  [9401] Netherlands               Netherlands              
##  [9403] Netherlands               Netherlands              
##  [9405] Netherlands               Netherlands              
##  [9407] Netherlands               Netherlands              
##  [9409] Netherlands               Netherlands              
##  [9411] Netherlands               Netherlands              
##  [9413] Netherlands               Netherlands              
##  [9415] Netherlands               Netherlands              
##  [9417] Netherlands               Netherlands              
##  [9419] Netherlands               Netherlands              
##  [9421] Netherlands               Netherlands              
##  [9423] Netherlands               Netherlands              
##  [9425] Netherlands               Netherlands              
##  [9427] Netherlands               Netherlands              
##  [9429] Netherlands               Netherlands              
##  [9431] Netherlands               Netherlands              
##  [9433] Netherlands               Netherlands              
##  [9435] Netherlands               Netherlands              
##  [9437] Netherlands               Netherlands              
##  [9439] Netherlands               Netherlands              
##  [9441] Netherlands               Netherlands              
##  [9443] Netherlands               Netherlands              
##  [9445] Netherlands               Netherlands              
##  [9447] Netherlands               Netherlands              
##  [9449] Netherlands               Netherlands              
##  [9451] Netherlands               Netherlands              
##  [9453] Netherlands               Netherlands              
##  [9455] Netherlands               Netherlands Antilles     
##  [9457] Netherlands Antilles      Netherlands Antilles     
##  [9459] Netherlands Antilles      Netherlands Antilles     
##  [9461] Netherlands Antilles      Netherlands Antilles     
##  [9463] Netherlands Antilles      Netherlands Antilles     
##  [9465] Netherlands Antilles      Netherlands Antilles     
##  [9467] Netherlands Antilles      Netherlands Antilles     
##  [9469] Netherlands Antilles      Netherlands Antilles     
##  [9471] Netherlands Antilles      Netherlands Antilles     
##  [9473] New Caledonia             New Caledonia            
##  [9475] New Caledonia             New Caledonia            
##  [9477] New Caledonia             New Caledonia            
##  [9479] New Caledonia             New Caledonia            
##  [9481] New Caledonia             New Caledonia            
##  [9483] New Caledonia             New Caledonia            
##  [9485] New Caledonia             New Caledonia            
##  [9487] New Caledonia             New Caledonia            
##  [9489] New Caledonia             New Caledonia            
##  [9491] New Caledonia             New Caledonia            
##  [9493] New Caledonia             New Caledonia            
##  [9495] New Caledonia             New Caledonia            
##  [9497] New Caledonia             New Caledonia            
##  [9499] New Zealand               New Zealand              
##  [9501] New Zealand               New Zealand              
##  [9503] New Zealand               New Zealand              
##  [9505] New Zealand               New Zealand              
##  [9507] New Zealand               New Zealand              
##  [9509] New Zealand               New Zealand              
##  [9511] New Zealand               New Zealand              
##  [9513] New Zealand               New Zealand              
##  [9515] New Zealand               New Zealand              
##  [9517] New Zealand               New Zealand              
##  [9519] New Zealand               New Zealand              
##  [9521] New Zealand               New Zealand              
##  [9523] New Zealand               New Zealand              
##  [9525] New Zealand               New Zealand              
##  [9527] New Zealand               New Zealand              
##  [9529] New Zealand               New Zealand              
##  [9531] New Zealand               New Zealand              
##  [9533] New Zealand               New Zealand              
##  [9535] New Zealand               New Zealand              
##  [9537] New Zealand               New Zealand              
##  [9539] New Zealand               New Zealand              
##  [9541] New Zealand               New Zealand              
##  [9543] New Zealand               New Zealand              
##  [9545] New Zealand               New Zealand              
##  [9547] New Zealand               New Zealand              
##  [9549] New Zealand               New Zealand              
##  [9551] New Zealand               New Zealand              
##  [9553] New Zealand               New Zealand              
##  [9555] New Zealand               New Zealand              
##  [9557] New Zealand               New Zealand              
##  [9559] New Zealand               New Zealand              
##  [9561] New Zealand               New Zealand              
##  [9563] New Zealand               New Zealand              
##  [9565] New Zealand               New Zealand              
##  [9567] New Zealand               New Zealand              
##  [9569] New Zealand               New Zealand              
##  [9571] New Zealand               New Zealand              
##  [9573] New Zealand               New Zealand              
##  [9575] New Zealand               New Zealand              
##  [9577] New Zealand               New Zealand              
##  [9579] New Zealand               New Zealand              
##  [9581] New Zealand               New Zealand              
##  [9583] New Zealand               New Zealand              
##  [9585] New Zealand               New Zealand              
##  [9587] New Zealand               New Zealand              
##  [9589] New Zealand               New Zealand              
##  [9591] New Zealand               New Zealand              
##  [9593] New Zealand               New Zealand              
##  [9595] New Zealand               New Zealand              
##  [9597] New Zealand               New Zealand              
##  [9599] New Zealand               New Zealand              
##  [9601] New Zealand               New Zealand              
##  [9603] New Zealand               New Zealand              
##  [9605] New Zealand               New Zealand              
##  [9607] New Zealand               New Zealand              
##  [9609] New Zealand               New Zealand              
##  [9611] New Zealand               New Zealand              
##  [9613] New Zealand               New Zealand              
##  [9615] New Zealand               New Zealand              
##  [9617] New Zealand               New Zealand              
##  [9619] New Zealand               New Zealand              
##  [9621] New Zealand               New Zealand              
##  [9623] New Zealand               New Zealand              
##  [9625] New Zealand               New Zealand              
##  [9627] New Zealand               New Zealand              
##  [9629] New Zealand               New Zealand              
##  [9631] New Zealand               New Zealand              
##  [9633] New Zealand               New Zealand              
##  [9635] New Zealand               New Zealand              
##  [9637] New Zealand               New Zealand              
##  [9639] New Zealand               New Zealand              
##  [9641] New Zealand               New Zealand              
##  [9643] New Zealand               New Zealand              
##  [9645] New Zealand               New Zealand              
##  [9647] New Zealand               New Zealand              
##  [9649] New Zealand               New Zealand              
##  [9651] New Zealand               New Zealand              
##  [9653] New Zealand               New Zealand              
##  [9655] New Zealand               New Zealand              
##  [9657] New Zealand               New Zealand              
##  [9659] New Zealand               New Zealand              
##  [9661] New Zealand               New Zealand              
##  [9663] New Zealand               New Zealand              
##  [9665] New Zealand               New Zealand              
##  [9667] New Zealand               New Zealand              
##  [9669] New Zealand               New Zealand              
##  [9671] New Zealand               New Zealand              
##  [9673] New Zealand               New Zealand              
##  [9675] New Zealand               New Zealand              
##  [9677] New Zealand               New Zealand              
##  [9679] New Zealand               New Zealand              
##  [9681] New Zealand               New Zealand              
##  [9683] New Zealand               New Zealand              
##  [9685] New Zealand               New Zealand              
##  [9687] New Zealand               New Zealand              
##  [9689] New Zealand               New Zealand              
##  [9691] New Zealand               New Zealand              
##  [9693] New Zealand               New Zealand              
##  [9695] New Zealand               New Zealand              
##  [9697] New Zealand               New Zealand              
##  [9699] New Zealand               New Zealand              
##  [9701] New Zealand               New Zealand              
##  [9703] New Zealand               New Zealand              
##  [9705] New Zealand               New Zealand              
##  [9707] Nicaragua                 Nicaragua                
##  [9709] Nicaragua                 Nicaragua                
##  [9711] Nicaragua                 Nicaragua                
##  [9713] Nicaragua                 Nicaragua                
##  [9715] Nicaragua                 Nicaragua                
##  [9717] Nicaragua                 Nicaragua                
##  [9719] Nicaragua                 Nicaragua                
##  [9721] Nicaragua                 Nicaragua                
##  [9723] Nicaragua                 Nicaragua                
##  [9725] Nicaragua                 Nicaragua                
##  [9727] Nicaragua                 Nicaragua                
##  [9729] Nicaragua                 Nicaragua                
##  [9731] Nicaragua                 Nicaragua                
##  [9733] Nicaragua                 Nicaragua                
##  [9735] Nicaragua                 Nicaragua                
##  [9737] Nicaragua                 Nicaragua                
##  [9739] Nicaragua                 Nicaragua                
##  [9741] Nicaragua                 Nicaragua                
##  [9743] Nicaragua                 Nicaragua                
##  [9745] Nicaragua                 Nicaragua                
##  [9747] Nicaragua                 Nicaragua                
##  [9749] Nicaragua                 Nicaragua                
##  [9751] Nicaragua                 Nicaragua                
##  [9753] Nicaragua                 Nicaragua                
##  [9755] Nicaragua                 Nicaragua                
##  [9757] Nicaragua                 Nicaragua                
##  [9759] Nicaragua                 Nicaragua                
##  [9761] Nicaragua                 Nicaragua                
##  [9763] Nicaragua                 Nicaragua                
##  [9765] Nicaragua                 Nigeria                  
##  [9767] Nigeria                   Nigeria                  
##  [9769] Nigeria                   Nigeria                  
##  [9771] Nigeria                   Nigeria                  
##  [9773] Nigeria                   Nigeria                  
##  [9775] Nigeria                   Nigeria                  
##  [9777] Nigeria                   Nigeria                  
##  [9779] Nigeria                   Nigeria                  
##  [9781] Nigeria                   Nigeria                  
##  [9783] Nigeria                   Nigeria                  
##  [9785] Nigeria                   Nigeria                  
##  [9787] Nigeria                   Nigeria                  
##  [9789] Nigeria                   Nigeria                  
##  [9791] Nigeria                   Nigeria                  
##  [9793] Nigeria                   Nigeria                  
##  [9795] Nigeria                   Nigeria                  
##  [9797] Nigeria                   Nigeria                  
##  [9799] Nigeria                   Nigeria                  
##  [9801] Nigeria                   Nigeria                  
##  [9803] Nigeria                   Nigeria                  
##  [9805] Nigeria                   Nigeria                  
##  [9807] Nigeria                   Nigeria                  
##  [9809] Nigeria                   Nigeria                  
##  [9811] Nigeria                   Nigeria                  
##  [9813] Nigeria                   Nigeria                  
##  [9815] Nigeria                   Niue                     
##  [9817] Niue                      Niue                     
##  [9819] Niue                      Niue                     
##  [9821] Niue                      Niue                     
##  [9823] Niue                      Niue                     
##  [9825] Niue                      Niue                     
##  [9827] Norfolk Island            Northern Mariana Is.     
##  [9829] Northern Mariana Is.      Northern Mariana Is.     
##  [9831] Northern Mariana Is.      Northern Mariana Is.     
##  [9833] Northern Mariana Is.      Northern Mariana Is.     
##  [9835] Northern Mariana Is.      Northern Mariana Is.     
##  [9837] Northern Mariana Is.      Northern Mariana Is.     
##  [9839] Northern Mariana Is.      Northern Mariana Is.     
##  [9841] Northern Mariana Is.      Northern Mariana Is.     
##  [9843] Northern Mariana Is.      Northern Mariana Is.     
##  [9845] Northern Mariana Is.      Northern Mariana Is.     
##  [9847] Norway                    Norway                   
##  [9849] Norway                    Norway                   
##  [9851] Norway                    Norway                   
##  [9853] Norway                    Norway                   
##  [9855] Norway                    Norway                   
##  [9857] Norway                    Norway                   
##  [9859] Norway                    Norway                   
##  [9861] Norway                    Norway                   
##  [9863] Norway                    Norway                   
##  [9865] Norway                    Norway                   
##  [9867] Norway                    Norway                   
##  [9869] Norway                    Norway                   
##  [9871] Norway                    Norway                   
##  [9873] Norway                    Norway                   
##  [9875] Norway                    Norway                   
##  [9877] Norway                    Norway                   
##  [9879] Norway                    Norway                   
##  [9881] Norway                    Norway                   
##  [9883] Norway                    Norway                   
##  [9885] Norway                    Norway                   
##  [9887] Norway                    Norway                   
##  [9889] Norway                    Norway                   
##  [9891] Norway                    Norway                   
##  [9893] Norway                    Norway                   
##  [9895] Norway                    Norway                   
##  [9897] Norway                    Norway                   
##  [9899] Norway                    Norway                   
##  [9901] Norway                    Norway                   
##  [9903] Norway                    Norway                   
##  [9905] Norway                    Norway                   
##  [9907] Norway                    Norway                   
##  [9909] Norway                    Norway                   
##  [9911] Norway                    Norway                   
##  [9913] Norway                    Norway                   
##  [9915] Norway                    Norway                   
##  [9917] Norway                    Norway                   
##  [9919] Norway                    Norway                   
##  [9921] Norway                    Norway                   
##  [9923] Norway                    Norway                   
##  [9925] Norway                    Norway                   
##  [9927] Norway                    Norway                   
##  [9929] Norway                    Norway                   
##  [9931] Norway                    Norway                   
##  [9933] Norway                    Norway                   
##  [9935] Norway                    Norway                   
##  [9937] Norway                    Norway                   
##  [9939] Norway                    Norway                   
##  [9941] Norway                    Norway                   
##  [9943] Norway                    Norway                   
##  [9945] Norway                    Norway                   
##  [9947] Norway                    Norway                   
##  [9949] Norway                    Norway                   
##  [9951] Norway                    Norway                   
##  [9953] Norway                    Norway                   
##  [9955] Norway                    Norway                   
##  [9957] Norway                    Norway                   
##  [9959] Norway                    Norway                   
##  [9961] Norway                    Norway                   
##  [9963] Norway                    Norway                   
##  [9965] Norway                    Norway                   
##  [9967] Norway                    Norway                   
##  [9969] Norway                    Norway                   
##  [9971] Norway                    Norway                   
##  [9973] Norway                    Norway                   
##  [9975] Norway                    Norway                   
##  [9977] Norway                    Norway                   
##  [9979] Norway                    Norway                   
##  [9981] Norway                    Norway                   
##  [9983] Norway                    Norway                   
##  [9985] Norway                    Norway                   
##  [9987] Norway                    Norway                   
##  [9989] Norway                    Norway                   
##  [9991] Norway                    Norway                   
##  [9993] Norway                    Norway                   
##  [9995] Norway                    Norway                   
##  [9997] Norway                    Norway                   
##  [9999] Norway                    Norway                   
## [10001] Norway                    Norway                   
## [10003] Norway                    Norway                   
## [10005] Norway                    Norway                   
## [10007] Norway                    Norway                   
## [10009] Norway                    Norway                   
## [10011] Norway                    Norway                   
## [10013] Norway                    Norway                   
## [10015] Norway                    Norway                   
## [10017] Norway                    Norway                   
## [10019] Norway                    Norway                   
## [10021] Norway                    Norway                   
## [10023] Norway                    Norway                   
## [10025] Norway                    Norway                   
## [10027] Norway                    Norway                   
## [10029] Norway                    Norway                   
## [10031] Norway                    Norway                   
## [10033] Norway                    Norway                   
## [10035] Oman                      Oman                     
## [10037] Oman                      Oman                     
## [10039] Oman                      Oman                     
## [10041] Oman                      Oman                     
## [10043] Oman                      Oman                     
## [10045] Oman                      Oman                     
## [10047] Oman                      Oman                     
## [10049] Oman                      Oman                     
## [10051] Oman                      Oman                     
## [10053] Oman                      Oman                     
## [10055] Oman                      Oman                     
## [10057] Oman                      Oman                     
## [10059] Oman                      Oman                     
## [10061] Oman                      Oman                     
## [10063] Oman                      Oman                     
## [10065] Oman                      Oman                     
## [10067] Oman                      Oman                     
## [10069] Oman                      Oman                     
## [10071] Oman                      Oman                     
## [10073] Oman                      Oman                     
## [10075] Oman                      Oman                     
## [10077] Oman                      Oman                     
## [10079] Oman                      Oman                     
## [10081] Oman                      Oman                     
## [10083] Oman                      Oman                     
## [10085] Oman                      Oman                     
## [10087] Oman                      Other nei                
## [10089] Other nei                 Other nei                
## [10091] Other nei                 Other nei                
## [10093] Other nei                 Other nei                
## [10095] Other nei                 Other nei                
## [10097] Other nei                 Other nei                
## [10099] Other nei                 Other nei                
## [10101] Other nei                 Other nei                
## [10103] Other nei                 Other nei                
## [10105] Other nei                 Other nei                
## [10107] Other nei                 Other nei                
## [10109] Other nei                 Other nei                
## [10111] Other nei                 Other nei                
## [10113] Other nei                 Other nei                
## [10115] Other nei                 Other nei                
## [10117] Other nei                 Other nei                
## [10119] Other nei                 Other nei                
## [10121] Other nei                 Other nei                
## [10123] Other nei                 Other nei                
## [10125] Other nei                 Other nei                
## [10127] Other nei                 Other nei                
## [10129] Other nei                 Other nei                
## [10131] Other nei                 Other nei                
## [10133] Other nei                 Other nei                
## [10135] Other nei                 Other nei                
## [10137] Other nei                 Other nei                
## [10139] Other nei                 Other nei                
## [10141] Other nei                 Other nei                
## [10143] Other nei                 Other nei                
## [10145] Other nei                 Other nei                
## [10147] Other nei                 Other nei                
## [10149] Other nei                 Other nei                
## [10151] Other nei                 Other nei                
## [10153] Other nei                 Other nei                
## [10155] Other nei                 Other nei                
## [10157] Other nei                 Other nei                
## [10159] Other nei                 Other nei                
## [10161] Other nei                 Other nei                
## [10163] Other nei                 Other nei                
## [10165] Other nei                 Other nei                
## [10167] Other nei                 Other nei                
## [10169] Other nei                 Other nei                
## [10171] Other nei                 Other nei                
## [10173] Other nei                 Other nei                
## [10175] Other nei                 Other nei                
## [10177] Other nei                 Other nei                
## [10179] Other nei                 Other nei                
## [10181] Other nei                 Other nei                
## [10183] Other nei                 Other nei                
## [10185] Other nei                 Other nei                
## [10187] Other nei                 Pakistan                 
## [10189] Pakistan                  Pakistan                 
## [10191] Pakistan                  Pakistan                 
## [10193] Pakistan                  Pakistan                 
## [10195] Pakistan                  Pakistan                 
## [10197] Pakistan                  Pakistan                 
## [10199] Pakistan                  Pakistan                 
## [10201] Pakistan                  Pakistan                 
## [10203] Pakistan                  Pakistan                 
## [10205] Pakistan                  Pakistan                 
## [10207] Pakistan                  Pakistan                 
## [10209] Pakistan                  Pakistan                 
## [10211] Pakistan                  Pakistan                 
## [10213] Pakistan                  Pakistan                 
## [10215] Pakistan                  Pakistan                 
## [10217] Pakistan                  Pakistan                 
## [10219] Pakistan                  Pakistan                 
## [10221] Pakistan                  Pakistan                 
## [10223] Pakistan                  Pakistan                 
## [10225] Pakistan                  Pakistan                 
## [10227] Pakistan                  Pakistan                 
## [10229] Pakistan                  Pakistan                 
## [10231] Pakistan                  Pakistan                 
## [10233] Pakistan                  Pakistan                 
## [10235] Pakistan                  Pakistan                 
## [10237] Pakistan                  Pakistan                 
## [10239] Pakistan                  Pakistan                 
## [10241] Pakistan                  Pakistan                 
## [10243] Pakistan                  Pakistan                 
## [10245] Pakistan                  Pakistan                 
## [10247] Pakistan                  Palau                    
## [10249] Palau                     Palau                    
## [10251] Palau                     Palau                    
## [10253] Palau                     Palau                    
## [10255] Palau                     Palau                    
## [10257] Palau                     Palau                    
## [10259] Palau                     Palau                    
## [10261] Palau                     Palau                    
## [10263] Palau                     Palau                    
## [10265] Palau                     Palau                    
## [10267] Palau                     Palau                    
## [10269] Palau                     Palau                    
## [10271] Palau                     Palau                    
## [10273] Palau                     Palau                    
## [10275] Palau                     Palau                    
## [10277] Palau                     Palau                    
## [10279] Palau                     Palau                    
## [10281] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10283] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10285] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10287] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10289] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10291] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10293] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10295] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10297] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10299] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10301] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10303] Palestine, Occupied Tr.   Palestine, Occupied Tr.  
## [10305] Palestine, Occupied Tr.   Panama                   
## [10307] Panama                    Panama                   
## [10309] Panama                    Panama                   
## [10311] Panama                    Panama                   
## [10313] Panama                    Panama                   
## [10315] Panama                    Panama                   
## [10317] Panama                    Panama                   
## [10319] Panama                    Panama                   
## [10321] Panama                    Panama                   
## [10323] Panama                    Panama                   
## [10325] Panama                    Panama                   
## [10327] Panama                    Panama                   
## [10329] Panama                    Panama                   
## [10331] Panama                    Panama                   
## [10333] Panama                    Panama                   
## [10335] Panama                    Panama                   
## [10337] Panama                    Panama                   
## [10339] Panama                    Panama                   
## [10341] Panama                    Panama                   
## [10343] Panama                    Panama                   
## [10345] Panama                    Panama                   
## [10347] Panama                    Panama                   
## [10349] Panama                    Panama                   
## [10351] Panama                    Panama                   
## [10353] Panama                    Panama                   
## [10355] Panama                    Panama                   
## [10357] Panama                    Panama                   
## [10359] Panama                    Panama                   
## [10361] Panama                    Panama                   
## [10363] Panama                    Panama                   
## [10365] Panama                    Panama                   
## [10367] Panama                    Panama                   
## [10369] Panama                    Panama                   
## [10371] Panama                    Panama                   
## [10373] Panama                    Panama                   
## [10375] Panama                    Panama                   
## [10377] Panama                    Panama                   
## [10379] Panama                    Panama                   
## [10381] Panama                    Panama                   
## [10383] Panama                    Panama                   
## [10385] Panama                    Panama                   
## [10387] Panama                    Panama                   
## [10389] Panama                    Panama                   
## [10391] Panama                    Panama                   
## [10393] Panama                    Panama                   
## [10395] Panama                    Panama                   
## [10397] Panama                    Panama                   
## [10399] Panama                    Panama                   
## [10401] Panama                    Panama                   
## [10403] Panama                    Panama                   
## [10405] Panama                    Panama                   
## [10407] Panama                    Panama                   
## [10409] Panama                    Panama                   
## [10411] Panama                    Panama                   
## [10413] Panama                    Panama                   
## [10415] Panama                    Panama                   
## [10417] Panama                    Panama                   
## [10419] Panama                    Panama                   
## [10421] Panama                    Panama                   
## [10423] Panama                    Panama                   
## [10425] Panama                    Panama                   
## [10427] Papua New Guinea          Papua New Guinea         
## [10429] Papua New Guinea          Papua New Guinea         
## [10431] Papua New Guinea          Papua New Guinea         
## [10433] Papua New Guinea          Papua New Guinea         
## [10435] Papua New Guinea          Papua New Guinea         
## [10437] Papua New Guinea          Papua New Guinea         
## [10439] Papua New Guinea          Papua New Guinea         
## [10441] Papua New Guinea          Papua New Guinea         
## [10443] Papua New Guinea          Papua New Guinea         
## [10445] Papua New Guinea          Papua New Guinea         
## [10447] Peru                      Peru                     
## [10449] Peru                      Peru                     
## [10451] Peru                      Peru                     
## [10453] Peru                      Peru                     
## [10455] Peru                      Peru                     
## [10457] Peru                      Peru                     
## [10459] Peru                      Peru                     
## [10461] Peru                      Peru                     
## [10463] Peru                      Peru                     
## [10465] Peru                      Peru                     
## [10467] Peru                      Peru                     
## [10469] Peru                      Peru                     
## [10471] Peru                      Peru                     
## [10473] Peru                      Peru                     
## [10475] Peru                      Peru                     
## [10477] Peru                      Peru                     
## [10479] Peru                      Peru                     
## [10481] Peru                      Peru                     
## [10483] Peru                      Peru                     
## [10485] Peru                      Peru                     
## [10487] Peru                      Peru                     
## [10489] Peru                      Peru                     
## [10491] Peru                      Peru                     
## [10493] Peru                      Peru                     
## [10495] Peru                      Peru                     
## [10497] Peru                      Peru                     
## [10499] Peru                      Peru                     
## [10501] Philippines               Philippines              
## [10503] Philippines               Philippines              
## [10505] Philippines               Philippines              
## [10507] Philippines               Philippines              
## [10509] Philippines               Philippines              
## [10511] Philippines               Philippines              
## [10513] Philippines               Philippines              
## [10515] Philippines               Philippines              
## [10517] Philippines               Philippines              
## [10519] Philippines               Philippines              
## [10521] Philippines               Philippines              
## [10523] Philippines               Philippines              
## [10525] Philippines               Philippines              
## [10527] Philippines               Philippines              
## [10529] Philippines               Philippines              
## [10531] Philippines               Philippines              
## [10533] Philippines               Philippines              
## [10535] Philippines               Philippines              
## [10537] Philippines               Philippines              
## [10539] Philippines               Philippines              
## [10541] Philippines               Philippines              
## [10543] Philippines               Philippines              
## [10545] Philippines               Philippines              
## [10547] Philippines               Philippines              
## [10549] Philippines               Philippines              
## [10551] Philippines               Philippines              
## [10553] Philippines               Philippines              
## [10555] Philippines               Philippines              
## [10557] Philippines               Philippines              
## [10559] Philippines               Philippines              
## [10561] Philippines               Philippines              
## [10563] Philippines               Philippines              
## [10565] Philippines               Philippines              
## [10567] Philippines               Philippines              
## [10569] Philippines               Philippines              
## [10571] Philippines               Philippines              
## [10573] Philippines               Philippines              
## [10575] Philippines               Philippines              
## [10577] Philippines               Philippines              
## [10579] Philippines               Philippines              
## [10581] Philippines               Philippines              
## [10583] Philippines               Philippines              
## [10585] Philippines               Philippines              
## [10587] Philippines               Philippines              
## [10589] Philippines               Philippines              
## [10591] Philippines               Philippines              
## [10593] Philippines               Philippines              
## [10595] Philippines               Philippines              
## [10597] Philippines               Philippines              
## [10599] Philippines               Philippines              
## [10601] Philippines               Philippines              
## [10603] Philippines               Philippines              
## [10605] Philippines               Philippines              
## [10607] Philippines               Philippines              
## [10609] Philippines               Philippines              
## [10611] Philippines               Philippines              
## [10613] Philippines               Philippines              
## [10615] Philippines               Philippines              
## [10617] Philippines               Philippines              
## [10619] Philippines               Philippines              
## [10621] Philippines               Philippines              
## [10623] Philippines               Philippines              
## [10625] Philippines               Philippines              
## [10627] Philippines               Philippines              
## [10629] Philippines               Philippines              
## [10631] Philippines               Philippines              
## [10633] Philippines               Philippines              
## [10635] Philippines               Philippines              
## [10637] Philippines               Philippines              
## [10639] Pitcairn Islands          Poland                   
## [10641] Poland                    Poland                   
## [10643] Poland                    Poland                   
## [10645] Poland                    Poland                   
## [10647] Poland                    Poland                   
## [10649] Poland                    Poland                   
## [10651] Poland                    Poland                   
## [10653] Poland                    Poland                   
## [10655] Poland                    Poland                   
## [10657] Poland                    Poland                   
## [10659] Poland                    Poland                   
## [10661] Poland                    Poland                   
## [10663] Poland                    Poland                   
## [10665] Poland                    Poland                   
## [10667] Poland                    Poland                   
## [10669] Poland                    Poland                   
## [10671] Poland                    Poland                   
## [10673] Poland                    Poland                   
## [10675] Poland                    Poland                   
## [10677] Poland                    Poland                   
## [10679] Poland                    Poland                   
## [10681] Poland                    Poland                   
## [10683] Poland                    Poland                   
## [10685] Poland                    Poland                   
## [10687] Poland                    Poland                   
## [10689] Poland                    Poland                   
## [10691] Poland                    Poland                   
## [10693] Poland                    Poland                   
## [10695] Poland                    Poland                   
## [10697] Poland                    Poland                   
## [10699] Poland                    Poland                   
## [10701] Poland                    Poland                   
## [10703] Poland                    Poland                   
## [10705] Poland                    Poland                   
## [10707] Poland                    Poland                   
## [10709] Poland                    Poland                   
## [10711] Poland                    Poland                   
## [10713] Poland                    Poland                   
## [10715] Poland                    Poland                   
## [10717] Poland                    Poland                   
## [10719] Poland                    Poland                   
## [10721] Poland                    Poland                   
## [10723] Poland                    Poland                   
## [10725] Poland                    Poland                   
## [10727] Poland                    Poland                   
## [10729] Poland                    Poland                   
## [10731] Poland                    Poland                   
## [10733] Poland                    Poland                   
## [10735] Poland                    Poland                   
## [10737] Poland                    Poland                   
## [10739] Poland                    Poland                   
## [10741] Poland                    Poland                   
## [10743] Poland                    Poland                   
## [10745] Poland                    Poland                   
## [10747] Poland                    Poland                   
## [10749] Poland                    Poland                   
## [10751] Poland                    Poland                   
## [10753] Poland                    Poland                   
## [10755] Poland                    Poland                   
## [10757] Poland                    Poland                   
## [10759] Poland                    Poland                   
## [10761] Poland                    Poland                   
## [10763] Poland                    Poland                   
## [10765] Poland                    Poland                   
## [10767] Poland                    Poland                   
## [10769] Poland                    Poland                   
## [10771] Poland                    Poland                   
## [10773] Poland                    Poland                   
## [10775] Poland                    Poland                   
## [10777] Poland                    Poland                   
## [10779] Poland                    Poland                   
## [10781] Poland                    Poland                   
## [10783] Poland                    Poland                   
## [10785] Poland                    Poland                   
## [10787] Poland                    Poland                   
## [10789] Poland                    Poland                   
## [10791] Poland                    Poland                   
## [10793] Poland                    Poland                   
## [10795] Poland                    Poland                   
## [10797] Poland                    Poland                   
## [10799] Poland                    Poland                   
## [10801] Poland                    Poland                   
## [10803] Poland                    Poland                   
## [10805] Poland                    Poland                   
## [10807] Poland                    Poland                   
## [10809] Poland                    Poland                   
## [10811] Poland                    Poland                   
## [10813] Poland                    Poland                   
## [10815] Poland                    Poland                   
## [10817] Poland                    Poland                   
## [10819] Poland                    Poland                   
## [10821] Poland                    Poland                   
## [10823] Poland                    Poland                   
## [10825] Poland                    Poland                   
## [10827] Poland                    Poland                   
## [10829] Poland                    Poland                   
## [10831] Poland                    Poland                   
## [10833] Poland                    Poland                   
## [10835] Poland                    Poland                   
## [10837] Poland                    Poland                   
## [10839] Poland                    Poland                   
## [10841] Poland                    Poland                   
## [10843] Poland                    Poland                   
## [10845] Poland                    Poland                   
## [10847] Poland                    Poland                   
## [10849] Poland                    Poland                   
## [10851] Poland                    Poland                   
## [10853] Poland                    Poland                   
## [10855] Poland                    Poland                   
## [10857] Poland                    Poland                   
## [10859] Poland                    Poland                   
## [10861] Poland                    Poland                   
## [10863] Poland                    Poland                   
## [10865] Poland                    Poland                   
## [10867] Poland                    Poland                   
## [10869] Poland                    Poland                   
## [10871] Poland                    Poland                   
## [10873] Poland                    Poland                   
## [10875] Poland                    Poland                   
## [10877] Poland                    Poland                   
## [10879] Poland                    Poland                   
## [10881] Poland                    Poland                   
## [10883] Poland                    Poland                   
## [10885] Poland                    Poland                   
## [10887] Poland                    Poland                   
## [10889] Poland                    Poland                   
## [10891] Poland                    Poland                   
## [10893] Poland                    Poland                   
## [10895] Poland                    Poland                   
## [10897] Poland                    Poland                   
## [10899] Poland                    Poland                   
## [10901] Poland                    Poland                   
## [10903] Portugal                  Portugal                 
## [10905] Portugal                  Portugal                 
## [10907] Portugal                  Portugal                 
## [10909] Portugal                  Portugal                 
## [10911] Portugal                  Portugal                 
## [10913] Portugal                  Portugal                 
## [10915] Portugal                  Portugal                 
## [10917] Portugal                  Portugal                 
## [10919] Portugal                  Portugal                 
## [10921] Portugal                  Portugal                 
## [10923] Portugal                  Portugal                 
## [10925] Portugal                  Portugal                 
## [10927] Portugal                  Portugal                 
## [10929] Portugal                  Portugal                 
## [10931] Portugal                  Portugal                 
## [10933] Portugal                  Portugal                 
## [10935] Portugal                  Portugal                 
## [10937] Portugal                  Portugal                 
## [10939] Portugal                  Portugal                 
## [10941] Portugal                  Portugal                 
## [10943] Portugal                  Portugal                 
## [10945] Portugal                  Portugal                 
## [10947] Portugal                  Portugal                 
## [10949] Portugal                  Portugal                 
## [10951] Portugal                  Portugal                 
## [10953] Portugal                  Portugal                 
## [10955] Portugal                  Portugal                 
## [10957] Portugal                  Portugal                 
## [10959] Portugal                  Portugal                 
## [10961] Portugal                  Portugal                 
## [10963] Portugal                  Portugal                 
## [10965] Portugal                  Portugal                 
## [10967] Portugal                  Portugal                 
## [10969] Portugal                  Portugal                 
## [10971] Portugal                  Portugal                 
## [10973] Portugal                  Portugal                 
## [10975] Portugal                  Portugal                 
## [10977] Portugal                  Portugal                 
## [10979] Portugal                  Portugal                 
## [10981] Portugal                  Portugal                 
## [10983] Portugal                  Portugal                 
## [10985] Portugal                  Portugal                 
## [10987] Portugal                  Portugal                 
## [10989] Portugal                  Portugal                 
## [10991] Portugal                  Portugal                 
## [10993] Portugal                  Portugal                 
## [10995] Portugal                  Portugal                 
## [10997] Portugal                  Portugal                 
## [10999] Portugal                  Portugal                 
## [11001] Portugal                  Portugal                 
## [11003] Portugal                  Portugal                 
## [11005] Portugal                  Portugal                 
## [11007] Portugal                  Portugal                 
## [11009] Portugal                  Portugal                 
## [11011] Portugal                  Portugal                 
## [11013] Portugal                  Portugal                 
## [11015] Portugal                  Portugal                 
## [11017] Portugal                  Portugal                 
## [11019] Portugal                  Portugal                 
## [11021] Portugal                  Portugal                 
## [11023] Portugal                  Portugal                 
## [11025] Portugal                  Portugal                 
## [11027] Portugal                  Portugal                 
## [11029] Portugal                  Portugal                 
## [11031] Portugal                  Portugal                 
## [11033] Portugal                  Portugal                 
## [11035] Portugal                  Portugal                 
## [11037] Portugal                  Portugal                 
## [11039] Portugal                  Portugal                 
## [11041] Portugal                  Portugal                 
## [11043] Portugal                  Portugal                 
## [11045] Portugal                  Portugal                 
## [11047] Portugal                  Portugal                 
## [11049] Portugal                  Portugal                 
## [11051] Portugal                  Portugal                 
## [11053] Portugal                  Portugal                 
## [11055] Portugal                  Portugal                 
## [11057] Portugal                  Portugal                 
## [11059] Portugal                  Portugal                 
## [11061] Portugal                  Portugal                 
## [11063] Portugal                  Portugal                 
## [11065] Portugal                  Portugal                 
## [11067] Portugal                  Portugal                 
## [11069] Portugal                  Portugal                 
## [11071] Portugal                  Portugal                 
## [11073] Portugal                  Portugal                 
## [11075] Portugal                  Portugal                 
## [11077] Portugal                  Portugal                 
## [11079] Portugal                  Portugal                 
## [11081] Portugal                  Portugal                 
## [11083] Portugal                  Portugal                 
## [11085] Portugal                  Portugal                 
## [11087] Portugal                  Portugal                 
## [11089] Portugal                  Portugal                 
## [11091] Portugal                  Portugal                 
## [11093] Portugal                  Portugal                 
## [11095] Portugal                  Portugal                 
## [11097] Portugal                  Portugal                 
## [11099] Portugal                  Portugal                 
## [11101] Portugal                  Portugal                 
## [11103] Portugal                  Portugal                 
## [11105] Portugal                  Portugal                 
## [11107] Portugal                  Portugal                 
## [11109] Portugal                  Portugal                 
## [11111] Portugal                  Portugal                 
## [11113] Portugal                  Portugal                 
## [11115] Portugal                  Portugal                 
## [11117] Portugal                  Portugal                 
## [11119] Portugal                  Portugal                 
## [11121] Portugal                  Portugal                 
## [11123] Portugal                  Portugal                 
## [11125] Portugal                  Portugal                 
## [11127] Portugal                  Portugal                 
## [11129] Portugal                  Portugal                 
## [11131] Portugal                  Portugal                 
## [11133] Portugal                  Portugal                 
## [11135] Portugal                  Portugal                 
## [11137] Portugal                  Portugal                 
## [11139] Portugal                  Portugal                 
## [11141] Portugal                  Portugal                 
## [11143] Portugal                  Portugal                 
## [11145] Portugal                  Portugal                 
## [11147] Portugal                  Portugal                 
## [11149] Portugal                  Portugal                 
## [11151] Portugal                  Portugal                 
## [11153] Portugal                  Portugal                 
## [11155] Portugal                  Portugal                 
## [11157] Portugal                  Portugal                 
## [11159] Portugal                  Portugal                 
## [11161] Portugal                  Portugal                 
## [11163] Portugal                  Portugal                 
## [11165] Portugal                  Portugal                 
## [11167] Portugal                  Portugal                 
## [11169] Portugal                  Portugal                 
## [11171] Portugal                  Portugal                 
## [11173] Portugal                  Portugal                 
## [11175] Portugal                  Portugal                 
## [11177] Portugal                  Portugal                 
## [11179] Portugal                  Portugal                 
## [11181] Portugal                  Portugal                 
## [11183] Portugal                  Portugal                 
## [11185] Portugal                  Portugal                 
## [11187] Portugal                  Portugal                 
## [11189] Portugal                  Portugal                 
## [11191] Portugal                  Portugal                 
## [11193] Portugal                  Portugal                 
## [11195] Portugal                  Portugal                 
## [11197] Portugal                  Portugal                 
## [11199] Portugal                  Portugal                 
## [11201] Portugal                  Portugal                 
## [11203] Portugal                  Portugal                 
## [11205] Portugal                  Portugal                 
## [11207] Portugal                  Portugal                 
## [11209] Portugal                  Portugal                 
## [11211] Portugal                  Portugal                 
## [11213] Portugal                  Portugal                 
## [11215] Portugal                  Portugal                 
## [11217] Portugal                  Portugal                 
## [11219] Portugal                  Portugal                 
## [11221] Portugal                  Portugal                 
## [11223] Portugal                  Portugal                 
## [11225] Portugal                  Portugal                 
## [11227] Portugal                  Portugal                 
## [11229] Portugal                  Portugal                 
## [11231] Portugal                  Portugal                 
## [11233] Portugal                  Portugal                 
## [11235] Portugal                  Portugal                 
## [11237] Portugal                  Portugal                 
## [11239] Portugal                  Portugal                 
## [11241] Portugal                  Portugal                 
## [11243] Portugal                  Portugal                 
## [11245] Portugal                  Portugal                 
## [11247] Portugal                  Portugal                 
## [11249] Portugal                  Portugal                 
## [11251] Portugal                  Portugal                 
## [11253] Portugal                  Portugal                 
## [11255] Portugal                  Portugal                 
## [11257] Portugal                  Portugal                 
## [11259] Portugal                  Portugal                 
## [11261] Portugal                  Portugal                 
## [11263] Portugal                  Portugal                 
## [11265] Portugal                  Portugal                 
## [11267] Portugal                  Portugal                 
## [11269] Portugal                  Portugal                 
## [11271] Portugal                  Portugal                 
## [11273] Portugal                  Portugal                 
## [11275] Portugal                  Portugal                 
## [11277] Portugal                  Portugal                 
## [11279] Portugal                  Portugal                 
## [11281] Portugal                  Portugal                 
## [11283] Portugal                  Portugal                 
## [11285] Portugal                  Portugal                 
## [11287] Portugal                  Portugal                 
## [11289] Portugal                  Portugal                 
## [11291] Portugal                  Portugal                 
## [11293] Portugal                  Portugal                 
## [11295] Portugal                  Portugal                 
## [11297] Portugal                  Portugal                 
## [11299] Portugal                  Portugal                 
## [11301] Portugal                  Portugal                 
## [11303] Portugal                  Portugal                 
## [11305] Portugal                  Portugal                 
## [11307] Portugal                  Portugal                 
## [11309] Portugal                  Portugal                 
## [11311] Portugal                  Portugal                 
## [11313] Portugal                  Portugal                 
## [11315] Portugal                  Portugal                 
## [11317] Portugal                  Portugal                 
## [11319] Portugal                  Portugal                 
## [11321] Portugal                  Portugal                 
## [11323] Portugal                  Portugal                 
## [11325] Portugal                  Portugal                 
## [11327] Portugal                  Portugal                 
## [11329] Portugal                  Portugal                 
## [11331] Portugal                  Portugal                 
## [11333] Portugal                  Portugal                 
## [11335] Portugal                  Portugal                 
## [11337] Portugal                  Portugal                 
## [11339] Portugal                  Portugal                 
## [11341] Portugal                  Portugal                 
## [11343] Portugal                  Portugal                 
## [11345] Portugal                  Portugal                 
## [11347] Portugal                  Portugal                 
## [11349] Portugal                  Portugal                 
## [11351] Portugal                  Portugal                 
## [11353] Portugal                  Portugal                 
## [11355] Portugal                  Portugal                 
## [11357] Portugal                  Portugal                 
## [11359] Portugal                  Portugal                 
## [11361] Portugal                  Portugal                 
## [11363] Portugal                  Portugal                 
## [11365] Portugal                  Portugal                 
## [11367] Portugal                  Portugal                 
## [11369] Portugal                  Portugal                 
## [11371] Portugal                  Portugal                 
## [11373] Portugal                  Portugal                 
## [11375] Portugal                  Portugal                 
## [11377] Portugal                  Portugal                 
## [11379] Portugal                  Portugal                 
## [11381] Portugal                  Portugal                 
## [11383] Portugal                  Portugal                 
## [11385] Portugal                  Portugal                 
## [11387] Portugal                  Portugal                 
## [11389] Portugal                  Portugal                 
## [11391] Portugal                  Portugal                 
## [11393] Portugal                  Portugal                 
## [11395] Portugal                  Portugal                 
## [11397] Portugal                  Portugal                 
## [11399] Portugal                  Portugal                 
## [11401] Portugal                  Portugal                 
## [11403] Portugal                  Portugal                 
## [11405] Portugal                  Portugal                 
## [11407] Portugal                  Portugal                 
## [11409] Portugal                  Portugal                 
## [11411] Portugal                  Portugal                 
## [11413] Portugal                  Portugal                 
## [11415] Portugal                  Portugal                 
## [11417] Portugal                  Portugal                 
## [11419] Portugal                  Portugal                 
## [11421] Portugal                  Portugal                 
## [11423] Portugal                  Portugal                 
## [11425] Portugal                  Portugal                 
## [11427] Portugal                  Portugal                 
## [11429] Portugal                  Portugal                 
## [11431] Portugal                  Portugal                 
## [11433] Portugal                  Portugal                 
## [11435] Portugal                  Portugal                 
## [11437] Portugal                  Portugal                 
## [11439] Portugal                  Portugal                 
## [11441] Portugal                  Portugal                 
## [11443] Portugal                  Portugal                 
## [11445] Portugal                  Portugal                 
## [11447] Portugal                  Portugal                 
## [11449] Portugal                  Portugal                 
## [11451] Portugal                  Portugal                 
## [11453] Portugal                  Portugal                 
## [11455] Portugal                  Portugal                 
## [11457] Portugal                  Portugal                 
## [11459] Portugal                  Portugal                 
## [11461] Portugal                  Portugal                 
## [11463] Portugal                  Portugal                 
## [11465] Portugal                  Portugal                 
## [11467] Portugal                  Portugal                 
## [11469] Portugal                  Portugal                 
## [11471] Portugal                  Portugal                 
## [11473] Portugal                  Portugal                 
## [11475] Portugal                  Portugal                 
## [11477] Portugal                  Portugal                 
## [11479] Portugal                  Portugal                 
## [11481] Portugal                  Portugal                 
## [11483] Portugal                  Portugal                 
## [11485] Portugal                  Portugal                 
## [11487] Portugal                  Portugal                 
## [11489] Portugal                  Portugal                 
## [11491] Portugal                  Portugal                 
## [11493] Portugal                  Portugal                 
## [11495] Portugal                  Portugal                 
## [11497] Portugal                  Portugal                 
## [11499] Portugal                  Portugal                 
## [11501] Portugal                  Portugal                 
## [11503] Portugal                  Portugal                 
## [11505] Portugal                  Portugal                 
## [11507] Portugal                  Portugal                 
## [11509] Portugal                  Portugal                 
## [11511] Portugal                  Portugal                 
## [11513] Portugal                  Portugal                 
## [11515] Portugal                  Portugal                 
## [11517] Portugal                  Portugal                 
## [11519] Portugal                  Portugal                 
## [11521] Portugal                  Portugal                 
## [11523] Portugal                  Portugal                 
## [11525] Portugal                  Portugal                 
## [11527] Portugal                  Portugal                 
## [11529] Portugal                  Portugal                 
## [11531] Portugal                  Portugal                 
## [11533] Portugal                  Portugal                 
## [11535] Portugal                  Portugal                 
## [11537] Portugal                  Portugal                 
## [11539] Portugal                  Portugal                 
## [11541] Portugal                  Portugal                 
## [11543] Portugal                  Portugal                 
## [11545] Portugal                  Portugal                 
## [11547] Portugal                  Portugal                 
## [11549] Portugal                  Portugal                 
## [11551] Portugal                  Portugal                 
## [11553] Portugal                  Portugal                 
## [11555] Portugal                  Portugal                 
## [11557] Portugal                  Portugal                 
## [11559] Portugal                  Portugal                 
## [11561] Portugal                  Portugal                 
## [11563] Portugal                  Portugal                 
## [11565] Portugal                  Portugal                 
## [11567] Portugal                  Portugal                 
## [11569] Portugal                  Portugal                 
## [11571] Portugal                  Portugal                 
## [11573] Portugal                  Portugal                 
## [11575] Portugal                  Portugal                 
## [11577] Portugal                  Portugal                 
## [11579] Portugal                  Portugal                 
## [11581] Portugal                  Portugal                 
## [11583] Portugal                  Portugal                 
## [11585] Portugal                  Portugal                 
## [11587] Portugal                  Portugal                 
## [11589] Portugal                  Portugal                 
## [11591] Portugal                  Portugal                 
## [11593] Portugal                  Portugal                 
## [11595] Portugal                  Portugal                 
## [11597] Portugal                  Portugal                 
## [11599] Portugal                  Portugal                 
## [11601] Portugal                  Portugal                 
## [11603] Portugal                  Portugal                 
## [11605] Portugal                  Portugal                 
## [11607] Portugal                  Portugal                 
## [11609] Portugal                  Portugal                 
## [11611] Portugal                  Portugal                 
## [11613] Portugal                  Portugal                 
## [11615] Portugal                  Portugal                 
## [11617] Portugal                  Portugal                 
## [11619] Portugal                  Portugal                 
## [11621] Portugal                  Portugal                 
## [11623] Portugal                  Portugal                 
## [11625] Portugal                  Portugal                 
## [11627] Portugal                  Portugal                 
## [11629] Portugal                  Portugal                 
## [11631] Portugal                  Portugal                 
## [11633] Portugal                  Portugal                 
## [11635] Portugal                  Portugal                 
## [11637] Portugal                  Portugal                 
## [11639] Portugal                  Portugal                 
## [11641] Portugal                  Portugal                 
## [11643] Portugal                  Portugal                 
## [11645] Portugal                  Portugal                 
## [11647] Portugal                  Portugal                 
## [11649] Portugal                  Portugal                 
## [11651] Portugal                  Portugal                 
## [11653] Portugal                  Portugal                 
## [11655] Portugal                  Portugal                 
## [11657] Portugal                  Portugal                 
## [11659] Portugal                  Portugal                 
## [11661] Portugal                  Portugal                 
## [11663] Portugal                  Portugal                 
## [11665] Portugal                  Puerto Rico              
## [11667] Puerto Rico               Puerto Rico              
## [11669] Puerto Rico               Puerto Rico              
## [11671] Puerto Rico               Puerto Rico              
## [11673] Puerto Rico               Puerto Rico              
## [11675] Puerto Rico               Puerto Rico              
## [11677] Puerto Rico               Puerto Rico              
## [11679] Puerto Rico               Puerto Rico              
## [11681] Puerto Rico               Puerto Rico              
## [11683] Puerto Rico               Puerto Rico              
## [11685] Puerto Rico               Puerto Rico              
## [11687] Puerto Rico               Puerto Rico              
## [11689] Puerto Rico               Puerto Rico              
## [11691] Puerto Rico               Puerto Rico              
## [11693] Puerto Rico               Puerto Rico              
## [11695] Puerto Rico               Puerto Rico              
## [11697] Puerto Rico               Puerto Rico              
## [11699] Puerto Rico               Puerto Rico              
## [11701] Puerto Rico               Puerto Rico              
## [11703] Puerto Rico               Puerto Rico              
## [11705] Puerto Rico               Puerto Rico              
## [11707] Puerto Rico               Puerto Rico              
## [11709] Puerto Rico               Puerto Rico              
## [11711] Puerto Rico               Puerto Rico              
## [11713] Puerto Rico               Puerto Rico              
## [11715] Qatar                     Qatar                    
## [11717] Qatar                     Qatar                    
## [11719] Qatar                     Qatar                    
## [11721] Qatar                     Qatar                    
## [11723] Qatar                     Qatar                    
## [11725] Qatar                     Qatar                    
## [11727] Qatar                     Qatar                    
## [11729] Qatar                     Qatar                    
## [11731] Qatar                     Qatar                    
## [11733] Qatar                     Qatar                    
## [11735] Qatar                     Qatar                    
## [11737] Qatar                     Qatar                    
## [11739] Qatar                     Qatar                    
## [11741] Qatar                     Qatar                    
## [11743] Qatar                     Qatar                    
## [11745] Qatar                     Qatar                    
## [11747] Qatar                     Qatar                    
## [11749] Qatar                     Romania                  
## [11751] Romania                   Romania                  
## [11753] Romania                   Romania                  
## [11755] Romania                   Romania                  
## [11757] Romania                   Romania                  
## [11759] Romania                   Romania                  
## [11761] Romania                   Romania                  
## [11763] Romania                   Romania                  
## [11765] Romania                   Romania                  
## [11767] Romania                   Romania                  
## [11769] Romania                   Romania                  
## [11771] Romania                   Romania                  
## [11773] Romania                   Romania                  
## [11775] Romania                   Romania                  
## [11777] Romania                   Romania                  
## [11779] Romania                   Romania                  
## [11781] Romania                   Romania                  
## [11783] Romania                   Romania                  
## [11785] Romania                   Romania                  
## [11787] Romania                   Romania                  
## [11789] Romania                   Romania                  
## [11791] Romania                   Romania                  
## [11793] Romania                   Romania                  
## [11795] Romania                   Romania                  
## [11797] Romania                   Romania                  
## [11799] Romania                   Romania                  
## [11801] Romania                   Romania                  
## [11803] Romania                   Romania                  
## [11805] Romania                   Romania                  
## [11807] Romania                   Romania                  
## [11809] Romania                   Romania                  
## [11811] Romania                   Romania                  
## [11813] Romania                   Romania                  
## [11815] Romania                   Romania                  
## [11817] Romania                   Romania                  
## [11819] Romania                   Romania                  
## [11821] Romania                   Romania                  
## [11823] Romania                   Romania                  
## [11825] Romania                   Romania                  
## [11827] Romania                   Romania                  
## [11829] Romania                   Romania                  
## [11831] Romania                   Romania                  
## [11833] Romania                   Romania                  
## [11835] Romania                   Romania                  
## [11837] Romania                   Romania                  
## [11839] Romania                   Romania                  
## [11841] Romania                   Romania                  
## [11843] Romania                   Romania                  
## [11845] Romania                   Romania                  
## [11847] Romania                   Romania                  
## [11849] Romania                   Romania                  
## [11851] Romania                   Romania                  
## [11853] Romania                   Romania                  
## [11855] Romania                   Romania                  
## [11857] Romania                   Romania                  
## [11859] Romania                   Romania                  
## [11861] Romania                   Romania                  
## [11863] Romania                   Romania                  
## [11865] Romania                   Romania                  
## [11867] Romania                   Romania                  
## [11869] Romania                   Romania                  
## [11871] Romania                   Romania                  
## [11873] Romania                   Romania                  
## [11875] Romania                   Romania                  
## [11877] Romania                   Romania                  
## [11879] Romania                   Romania                  
## [11881] Romania                   Romania                  
## [11883] Romania                   Romania                  
## [11885] Romania                   Romania                  
## [11887] Romania                   Romania                  
## [11889] Romania                   Romania                  
## [11891] Romania                   Romania                  
## [11893] Romania                   Romania                  
## [11895] Romania                   Romania                  
## [11897] Romania                   Romania                  
## [11899] Romania                   Romania                  
## [11901] Romania                   Romania                  
## [11903] Romania                   Romania                  
## [11905] Romania                   Romania                  
## [11907] Romania                   Romania                  
## [11909] Romania                   Romania                  
## [11911] Romania                   Romania                  
## [11913] Romania                   Romania                  
## [11915] Romania                   Romania                  
## [11917] Romania                   Romania                  
## [11919] Romania                   Romania                  
## [11921] Romania                   Romania                  
## [11923] Romania                   Romania                  
## [11925] Romania                   Romania                  
## [11927] Romania                   Romania                  
## [11929] Romania                   Romania                  
## [11931] Romania                   Romania                  
## [11933] Romania                   Romania                  
## [11935] Romania                   Romania                  
## [11937] Romania                   Romania                  
## [11939] Romania                   Romania                  
## [11941] Russian Federation        Russian Federation       
## [11943] Russian Federation        Russian Federation       
## [11945] Russian Federation        Russian Federation       
## [11947] Russian Federation        Russian Federation       
## [11949] Russian Federation        Russian Federation       
## [11951] Russian Federation        Russian Federation       
## [11953] Russian Federation        Russian Federation       
## [11955] Russian Federation        Russian Federation       
## [11957] Russian Federation        Russian Federation       
## [11959] Russian Federation        Russian Federation       
## [11961] Russian Federation        Russian Federation       
## [11963] Russian Federation        Russian Federation       
## [11965] Russian Federation        Russian Federation       
## [11967] Russian Federation        Russian Federation       
## [11969] Russian Federation        Russian Federation       
## [11971] Russian Federation        Russian Federation       
## [11973] Russian Federation        Russian Federation       
## [11975] Russian Federation        Russian Federation       
## [11977] Russian Federation        Russian Federation       
## [11979] Russian Federation        Russian Federation       
## [11981] Russian Federation        Russian Federation       
## [11983] Russian Federation        Russian Federation       
## [11985] Russian Federation        Russian Federation       
## [11987] Russian Federation        Russian Federation       
## [11989] Russian Federation        Russian Federation       
## [11991] Russian Federation        Russian Federation       
## [11993] Russian Federation        Russian Federation       
## [11995] Russian Federation        Russian Federation       
## [11997] Russian Federation        Russian Federation       
## [11999] Russian Federation        Russian Federation       
## [12001] Russian Federation        Russian Federation       
## [12003] Russian Federation        Russian Federation       
## [12005] Russian Federation        Russian Federation       
## [12007] Russian Federation        Russian Federation       
## [12009] Russian Federation        Russian Federation       
## [12011] Russian Federation        Russian Federation       
## [12013] Russian Federation        Russian Federation       
## [12015] Russian Federation        Russian Federation       
## [12017] Russian Federation        Russian Federation       
## [12019] Russian Federation        Russian Federation       
## [12021] Russian Federation        Russian Federation       
## [12023] Russian Federation        Russian Federation       
## [12025] Russian Federation        Russian Federation       
## [12027] Russian Federation        Russian Federation       
## [12029] Russian Federation        Russian Federation       
## [12031] Russian Federation        Russian Federation       
## [12033] Russian Federation        Russian Federation       
## [12035] Russian Federation        Russian Federation       
## [12037] Russian Federation        Russian Federation       
## [12039] Russian Federation        Russian Federation       
## [12041] Russian Federation        Russian Federation       
## [12043] Russian Federation        Russian Federation       
## [12045] Russian Federation        Russian Federation       
## [12047] Russian Federation        Russian Federation       
## [12049] Russian Federation        Russian Federation       
## [12051] Russian Federation        Russian Federation       
## [12053] Russian Federation        Russian Federation       
## [12055] Russian Federation        Russian Federation       
## [12057] Russian Federation        Russian Federation       
## [12059] Russian Federation        Russian Federation       
## [12061] Russian Federation        Russian Federation       
## [12063] Russian Federation        Russian Federation       
## [12065] Russian Federation        Russian Federation       
## [12067] Russian Federation        Russian Federation       
## [12069] Russian Federation        Russian Federation       
## [12071] Russian Federation        Russian Federation       
## [12073] Russian Federation        Russian Federation       
## [12075] Russian Federation        Russian Federation       
## [12077] Russian Federation        Russian Federation       
## [12079] Russian Federation        Russian Federation       
## [12081] Russian Federation        Russian Federation       
## [12083] Russian Federation        Russian Federation       
## [12085] Russian Federation        Russian Federation       
## [12087] Russian Federation        Russian Federation       
## [12089] Russian Federation        Russian Federation       
## [12091] Russian Federation        Russian Federation       
## [12093] Russian Federation        Russian Federation       
## [12095] Russian Federation        Russian Federation       
## [12097] Russian Federation        Russian Federation       
## [12099] Russian Federation        Russian Federation       
## [12101] Russian Federation        Russian Federation       
## [12103] Russian Federation        Russian Federation       
## [12105] Russian Federation        Russian Federation       
## [12107] Russian Federation        Russian Federation       
## [12109] Russian Federation        Russian Federation       
## [12111] Russian Federation        Russian Federation       
## [12113] Russian Federation        Russian Federation       
## [12115] Russian Federation        Russian Federation       
## [12117] Russian Federation        Russian Federation       
## [12119] Russian Federation        Russian Federation       
## [12121] Russian Federation        Russian Federation       
## [12123] Russian Federation        Russian Federation       
## [12125] Russian Federation        Russian Federation       
## [12127] Russian Federation        Russian Federation       
## [12129] Russian Federation        Russian Federation       
## [12131] Russian Federation        Russian Federation       
## [12133] Russian Federation        Russian Federation       
## [12135] Russian Federation        Russian Federation       
## [12137] Russian Federation        Russian Federation       
## [12139] Russian Federation        Russian Federation       
## [12141] Russian Federation        Russian Federation       
## [12143] Russian Federation        Russian Federation       
## [12145] Russian Federation        Russian Federation       
## [12147] Russian Federation        Russian Federation       
## [12149] Russian Federation        Russian Federation       
## [12151] Russian Federation        Russian Federation       
## [12153] Russian Federation        Russian Federation       
## [12155] Russian Federation        Russian Federation       
## [12157] Russian Federation        Russian Federation       
## [12159] Russian Federation        Russian Federation       
## [12161] Russian Federation        Russian Federation       
## [12163] Russian Federation        Russian Federation       
## [12165] Russian Federation        Russian Federation       
## [12167] Russian Federation        Russian Federation       
## [12169] Russian Federation        Russian Federation       
## [12171] Russian Federation        Russian Federation       
## [12173] Russian Federation        Russian Federation       
## [12175] Russian Federation        Russian Federation       
## [12177] Russian Federation        Russian Federation       
## [12179] Russian Federation        Russian Federation       
## [12181] Russian Federation        Russian Federation       
## [12183] Russian Federation        Russian Federation       
## [12185] Russian Federation        Russian Federation       
## [12187] Russian Federation        Russian Federation       
## [12189] Russian Federation        Russian Federation       
## [12191] Russian Federation        Russian Federation       
## [12193] Russian Federation        Russian Federation       
## [12195] Russian Federation        Russian Federation       
## [12197] Russian Federation        Russian Federation       
## [12199] Russian Federation        Russian Federation       
## [12201] Russian Federation        Russian Federation       
## [12203] Russian Federation        Russian Federation       
## [12205] Russian Federation        Russian Federation       
## [12207] Russian Federation        Russian Federation       
## [12209] Russian Federation        Russian Federation       
## [12211] Russian Federation        Russian Federation       
## [12213] Russian Federation        Russian Federation       
## [12215] Russian Federation        Russian Federation       
## [12217] Russian Federation        Russian Federation       
## [12219] Russian Federation        Russian Federation       
## [12221] Russian Federation        Russian Federation       
## [12223] Russian Federation        Russian Federation       
## [12225] Russian Federation        Russian Federation       
## [12227] Russian Federation        Russian Federation       
## [12229] Russian Federation        Russian Federation       
## [12231] Russian Federation        Russian Federation       
## [12233] Russian Federation        Russian Federation       
## [12235] Russian Federation        Russian Federation       
## [12237] Russian Federation        Russian Federation       
## [12239] Russian Federation        Russian Federation       
## [12241] Russian Federation        Russian Federation       
## [12243] Russian Federation        Russian Federation       
## [12245] Russian Federation        Russian Federation       
## [12247] Russian Federation        Russian Federation       
## [12249] Russian Federation        Russian Federation       
## [12251] Russian Federation        Russian Federation       
## [12253] Russian Federation        Russian Federation       
## [12255] Russian Federation        Russian Federation       
## [12257] Russian Federation        Russian Federation       
## [12259] Russian Federation        Russian Federation       
## [12261] Russian Federation        Russian Federation       
## [12263] Russian Federation        Russian Federation       
## [12265] Russian Federation        Russian Federation       
## [12267] Russian Federation        Russian Federation       
## [12269] Russian Federation        Russian Federation       
## [12271] Russian Federation        Russian Federation       
## [12273] Russian Federation        Russian Federation       
## [12275] Russian Federation        Russian Federation       
## [12277] Russian Federation        Russian Federation       
## [12279] Russian Federation        Russian Federation       
## [12281] Russian Federation        Russian Federation       
## [12283] Russian Federation        Russian Federation       
## [12285] Russian Federation        Russian Federation       
## [12287] Russian Federation        Russian Federation       
## [12289] Russian Federation        Russian Federation       
## [12291] Russian Federation        Russian Federation       
## [12293] Russian Federation        Russian Federation       
## [12295] Russian Federation        Russian Federation       
## [12297] Russian Federation        Russian Federation       
## [12299] Russian Federation        Russian Federation       
## [12301] Russian Federation        Russian Federation       
## [12303] Russian Federation        Russian Federation       
## [12305] Russian Federation        Russian Federation       
## [12307] Russian Federation        Russian Federation       
## [12309] Russian Federation        Russian Federation       
## [12311] Russian Federation        Russian Federation       
## [12313] Russian Federation        Russian Federation       
## [12315] Russian Federation        Russian Federation       
## [12317] Russian Federation        Russian Federation       
## [12319] Russian Federation        Russian Federation       
## [12321] Russian Federation        Russian Federation       
## [12323] Russian Federation        Russian Federation       
## [12325] Russian Federation        Russian Federation       
## [12327] Russian Federation        Russian Federation       
## [12329] Russian Federation        Russian Federation       
## [12331] Russian Federation        Russian Federation       
## [12333] Russian Federation        Russian Federation       
## [12335] Russian Federation        Russian Federation       
## [12337] Russian Federation        Russian Federation       
## [12339] Russian Federation        Russian Federation       
## [12341] Russian Federation        Russian Federation       
## [12343] Russian Federation        Russian Federation       
## [12345] Russian Federation        Russian Federation       
## [12347] Russian Federation        Russian Federation       
## [12349] Russian Federation        Russian Federation       
## [12351] Russian Federation        Russian Federation       
## [12353] Russian Federation        Russian Federation       
## [12355] Russian Federation        Russian Federation       
## [12357] Russian Federation        Russian Federation       
## [12359] Russian Federation        Russian Federation       
## [12361] Russian Federation        Russian Federation       
## [12363] Russian Federation        Russian Federation       
## [12365] Russian Federation        Russian Federation       
## [12367] Russian Federation        Russian Federation       
## [12369] Russian Federation        Russian Federation       
## [12371] Russian Federation        Russian Federation       
## [12373] Russian Federation        Russian Federation       
## [12375] Russian Federation        Russian Federation       
## [12377] Russian Federation        Russian Federation       
## [12379] Russian Federation        Russian Federation       
## [12381] Russian Federation        Russian Federation       
## [12383] Russian Federation        Russian Federation       
## [12385] Russian Federation        Russian Federation       
## [12387] Russian Federation        Russian Federation       
## [12389] Russian Federation        Russian Federation       
## [12391] Russian Federation        Russian Federation       
## [12393] Russian Federation        Russian Federation       
## [12395] Russian Federation        Russian Federation       
## [12397] Russian Federation        Russian Federation       
## [12399] Russian Federation        Russian Federation       
## [12401] Russian Federation        Russian Federation       
## [12403] Russian Federation        Russian Federation       
## [12405] Russian Federation        Russian Federation       
## [12407] Russian Federation        Russian Federation       
## [12409] Russian Federation        Russian Federation       
## [12411] Russian Federation        Russian Federation       
## [12413] Russian Federation        Russian Federation       
## [12415] Russian Federation        Russian Federation       
## [12417] Russian Federation        Russian Federation       
## [12419] Russian Federation        Russian Federation       
## [12421] Russian Federation        Russian Federation       
## [12423] Russian Federation        Russian Federation       
## [12425] Russian Federation        Russian Federation       
## [12427] Russian Federation        Russian Federation       
## [12429] Russian Federation        Russian Federation       
## [12431] Russian Federation        Russian Federation       
## [12433] Russian Federation        Russian Federation       
## [12435] Russian Federation        Russian Federation       
## [12437] Russian Federation        Russian Federation       
## [12439] Russian Federation        Russian Federation       
## [12441] Russian Federation        Russian Federation       
## [12443] Russian Federation        Russian Federation       
## [12445] Russian Federation        Russian Federation       
## [12447] Russian Federation        Russian Federation       
## [12449] Russian Federation        Russian Federation       
## [12451] Russian Federation        Russian Federation       
## [12453] Russian Federation        Russian Federation       
## [12455] Russian Federation        Russian Federation       
## [12457] Russian Federation        Russian Federation       
## [12459] Russian Federation        Russian Federation       
## [12461] Russian Federation        Russian Federation       
## [12463] Russian Federation        R<e9>union               
## [12465] R<e9>union                R<e9>union               
## [12467] R<e9>union                R<e9>union               
## [12469] R<e9>union                R<e9>union               
## [12471] R<e9>union                R<e9>union               
## [12473] R<e9>union                R<e9>union               
## [12475] R<e9>union                R<e9>union               
## [12477] R<e9>union                R<e9>union               
## [12479] R<e9>union                R<e9>union               
## [12481] R<e9>union                R<e9>union               
## [12483] R<e9>union                R<e9>union               
## [12485] R<e9>union                R<e9>union               
## [12487] R<e9>union                R<e9>union               
## [12489] R<e9>union                R<e9>union               
## [12491] R<e9>union                R<e9>union               
## [12493] R<e9>union                R<e9>union               
## [12495] R<e9>union                R<e9>union               
## [12497] R<e9>union                R<e9>union               
## [12499] R<e9>union                R<e9>union               
## [12501] Saint Barth<e9>lemy       Saint Helena             
## [12503] Saint Helena              Saint Helena             
## [12505] Saint Helena              Saint Helena             
## [12507] Saint Helena              Saint Helena             
## [12509] Saint Helena              Saint Helena             
## [12511] Saint Helena              Saint Helena             
## [12513] Saint Helena              Saint Helena             
## [12515] Saint Helena              Saint Helena             
## [12517] Saint Helena              Saint Helena             
## [12519] Saint Helena              Saint Helena             
## [12521] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12523] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12525] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12527] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12529] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12531] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12533] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12535] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12537] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12539] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12541] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12543] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12545] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12547] Saint Kitts and Nevis     Saint Kitts and Nevis    
## [12549] Saint Lucia               Saint Lucia              
## [12551] Saint Lucia               Saint Lucia              
## [12553] Saint Lucia               Saint Lucia              
## [12555] Saint Lucia               Saint Lucia              
## [12557] Saint Lucia               Saint Lucia              
## [12559] Saint Lucia               Saint Lucia              
## [12561] Saint Lucia               Saint Lucia              
## [12563] Saint Lucia               Saint Lucia              
## [12565] Saint Lucia               Saint Lucia              
## [12567] Saint Lucia               Saint Lucia              
## [12569] Saint Lucia               Saint Lucia              
## [12571] Saint Lucia               Saint Lucia              
## [12573] Saint Lucia               Saint Lucia              
## [12575] Saint Lucia               Saint Vincent/Grenadines 
## [12577] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12579] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12581] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12583] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12585] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12587] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12589] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12591] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12593] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12595] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12597] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12599] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12601] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12603] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12605] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12607] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12609] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12611] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12613] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12615] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12617] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12619] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12621] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12623] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12625] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12627] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12629] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12631] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12633] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12635] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12637] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12639] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12641] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12643] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12645] Saint Vincent/Grenadines  Saint Vincent/Grenadines 
## [12647] SaintMartin               Samoa                    
## [12649] Samoa                     Samoa                    
## [12651] Samoa                     Samoa                    
## [12653] Samoa                     Samoa                    
## [12655] Samoa                     Samoa                    
## [12657] Samoa                     Samoa                    
## [12659] Samoa                     Samoa                    
## [12661] Samoa                     Samoa                    
## [12663] Sao Tome and Principe     Sao Tome and Principe    
## [12665] Sao Tome and Principe     Sao Tome and Principe    
## [12667] Sao Tome and Principe     Sao Tome and Principe    
## [12669] Sao Tome and Principe     Sao Tome and Principe    
## [12671] Sao Tome and Principe     Sao Tome and Principe    
## [12673] Sao Tome and Principe     Sao Tome and Principe    
## [12675] Sao Tome and Principe     Sao Tome and Principe    
## [12677] Sao Tome and Principe     Sao Tome and Principe    
## [12679] Sao Tome and Principe     Sao Tome and Principe    
## [12681] Sao Tome and Principe     Sao Tome and Principe    
## [12683] Sao Tome and Principe     Sao Tome and Principe    
## [12685] Sao Tome and Principe     Sao Tome and Principe    
## [12687] Sao Tome and Principe     Sao Tome and Principe    
## [12689] Sao Tome and Principe     Sao Tome and Principe    
## [12691] Sao Tome and Principe     Sao Tome and Principe    
## [12693] Sao Tome and Principe     Sao Tome and Principe    
## [12695] Sao Tome and Principe     Sao Tome and Principe    
## [12697] Sao Tome and Principe     Saudi Arabia             
## [12699] Saudi Arabia              Saudi Arabia             
## [12701] Saudi Arabia              Saudi Arabia             
## [12703] Saudi Arabia              Saudi Arabia             
## [12705] Saudi Arabia              Saudi Arabia             
## [12707] Saudi Arabia              Saudi Arabia             
## [12709] Saudi Arabia              Saudi Arabia             
## [12711] Saudi Arabia              Saudi Arabia             
## [12713] Saudi Arabia              Saudi Arabia             
## [12715] Saudi Arabia              Saudi Arabia             
## [12717] Saudi Arabia              Saudi Arabia             
## [12719] Saudi Arabia              Saudi Arabia             
## [12721] Saudi Arabia              Saudi Arabia             
## [12723] Saudi Arabia              Saudi Arabia             
## [12725] Saudi Arabia              Saudi Arabia             
## [12727] Saudi Arabia              Saudi Arabia             
## [12729] Saudi Arabia              Saudi Arabia             
## [12731] Saudi Arabia              Saudi Arabia             
## [12733] Saudi Arabia              Saudi Arabia             
## [12735] Saudi Arabia              Saudi Arabia             
## [12737] Saudi Arabia              Saudi Arabia             
## [12739] Saudi Arabia              Saudi Arabia             
## [12741] Saudi Arabia              Saudi Arabia             
## [12743] Saudi Arabia              Saudi Arabia             
## [12745] Saudi Arabia              Saudi Arabia             
## [12747] Saudi Arabia              Saudi Arabia             
## [12749] Saudi Arabia              Saudi Arabia             
## [12751] Saudi Arabia              Saudi Arabia             
## [12753] Saudi Arabia              Saudi Arabia             
## [12755] Saudi Arabia              Saudi Arabia             
## [12757] Saudi Arabia              Saudi Arabia             
## [12759] Saudi Arabia              Saudi Arabia             
## [12761] Saudi Arabia              Saudi Arabia             
## [12763] Saudi Arabia              Saudi Arabia             
## [12765] Saudi Arabia              Saudi Arabia             
## [12767] Saudi Arabia              Saudi Arabia             
## [12769] Saudi Arabia              Saudi Arabia             
## [12771] Saudi Arabia              Saudi Arabia             
## [12773] Saudi Arabia              Saudi Arabia             
## [12775] Saudi Arabia              Saudi Arabia             
## [12777] Saudi Arabia              Saudi Arabia             
## [12779] Saudi Arabia              Saudi Arabia             
## [12781] Saudi Arabia              Saudi Arabia             
## [12783] Saudi Arabia              Saudi Arabia             
## [12785] Saudi Arabia              Saudi Arabia             
## [12787] Saudi Arabia              Saudi Arabia             
## [12789] Saudi Arabia              Saudi Arabia             
## [12791] Saudi Arabia              Saudi Arabia             
## [12793] Saudi Arabia              Saudi Arabia             
## [12795] Saudi Arabia              Saudi Arabia             
## [12797] Saudi Arabia              Saudi Arabia             
## [12799] Saudi Arabia              Saudi Arabia             
## [12801] Saudi Arabia              Saudi Arabia             
## [12803] Saudi Arabia              Saudi Arabia             
## [12805] Saudi Arabia              Saudi Arabia             
## [12807] Saudi Arabia              Saudi Arabia             
## [12809] Saudi Arabia              Saudi Arabia             
## [12811] Saudi Arabia              Saudi Arabia             
## [12813] Saudi Arabia              Saudi Arabia             
## [12815] Saudi Arabia              Saudi Arabia             
## [12817] Saudi Arabia              Saudi Arabia             
## [12819] Saudi Arabia              Saudi Arabia             
## [12821] Saudi Arabia              Saudi Arabia             
## [12823] Saudi Arabia              Saudi Arabia             
## [12825] Saudi Arabia              Senegal                  
## [12827] Senegal                   Senegal                  
## [12829] Senegal                   Senegal                  
## [12831] Senegal                   Senegal                  
## [12833] Senegal                   Senegal                  
## [12835] Senegal                   Senegal                  
## [12837] Senegal                   Senegal                  
## [12839] Senegal                   Senegal                  
## [12841] Senegal                   Senegal                  
## [12843] Senegal                   Senegal                  
## [12845] Senegal                   Senegal                  
## [12847] Senegal                   Senegal                  
## [12849] Senegal                   Senegal                  
## [12851] Senegal                   Senegal                  
## [12853] Senegal                   Senegal                  
## [12855] Senegal                   Senegal                  
## [12857] Senegal                   Senegal                  
## [12859] Senegal                   Senegal                  
## [12861] Senegal                   Senegal                  
## [12863] Senegal                   Senegal                  
## [12865] Senegal                   Senegal                  
## [12867] Senegal                   Senegal                  
## [12869] Senegal                   Senegal                  
## [12871] Senegal                   Senegal                  
## [12873] Senegal                   Senegal                  
## [12875] Senegal                   Senegal                  
## [12877] Senegal                   Senegal                  
## [12879] Senegal                   Senegal                  
## [12881] Senegal                   Senegal                  
## [12883] Senegal                   Senegal                  
## [12885] Senegal                   Senegal                  
## [12887] Senegal                   Senegal                  
## [12889] Senegal                   Senegal                  
## [12891] Senegal                   Senegal                  
## [12893] Senegal                   Senegal                  
## [12895] Senegal                   Senegal                  
## [12897] Senegal                   Senegal                  
## [12899] Senegal                   Senegal                  
## [12901] Senegal                   Senegal                  
## [12903] Senegal                   Senegal                  
## [12905] Senegal                   Senegal                  
## [12907] Senegal                   Senegal                  
## [12909] Senegal                   Senegal                  
## [12911] Senegal                   Senegal                  
## [12913] Senegal                   Senegal                  
## [12915] Senegal                   Senegal                  
## [12917] Senegal                   Senegal                  
## [12919] Senegal                   Senegal                  
## [12921] Senegal                   Senegal                  
## [12923] Senegal                   Senegal                  
## [12925] Senegal                   Senegal                  
## [12927] Senegal                   Senegal                  
## [12929] Senegal                   Senegal                  
## [12931] Senegal                   Senegal                  
## [12933] Senegal                   Senegal                  
## [12935] Senegal                   Senegal                  
## [12937] Senegal                   Senegal                  
## [12939] Senegal                   Senegal                  
## [12941] Senegal                   Senegal                  
## [12943] Senegal                   Senegal                  
## [12945] Senegal                   Senegal                  
## [12947] Senegal                   Senegal                  
## [12949] Senegal                   Senegal                  
## [12951] Senegal                   Senegal                  
## [12953] Senegal                   Senegal                  
## [12955] Senegal                   Senegal                  
## [12957] Senegal                   Senegal                  
## [12959] Senegal                   Senegal                  
## [12961] Senegal                   Senegal                  
## [12963] Senegal                   Senegal                  
## [12965] Senegal                   Serbia and Montenegro    
## [12967] Serbia and Montenegro     Serbia and Montenegro    
## [12969] Serbia and Montenegro     Serbia and Montenegro    
## [12971] Serbia and Montenegro     Serbia and Montenegro    
## [12973] Serbia and Montenegro     Serbia and Montenegro    
## [12975] Serbia and Montenegro     Serbia and Montenegro    
## [12977] Serbia and Montenegro     Serbia and Montenegro    
## [12979] Serbia and Montenegro     Serbia and Montenegro    
## [12981] Serbia and Montenegro     Serbia and Montenegro    
## [12983] Serbia and Montenegro     Serbia and Montenegro    
## [12985] Serbia and Montenegro     Serbia and Montenegro    
## [12987] Serbia and Montenegro     Serbia and Montenegro    
## [12989] Serbia and Montenegro     Serbia and Montenegro    
## [12991] Serbia and Montenegro     Serbia and Montenegro    
## [12993] Serbia and Montenegro     Serbia and Montenegro    
## [12995] Serbia and Montenegro     Serbia and Montenegro    
## [12997] Serbia and Montenegro     Serbia and Montenegro    
## [12999] Serbia and Montenegro     Serbia and Montenegro    
## [13001] Serbia and Montenegro     Serbia and Montenegro    
## [13003] Serbia and Montenegro     Serbia and Montenegro    
## [13005] Serbia and Montenegro     Serbia and Montenegro    
## [13007] Serbia and Montenegro     Serbia and Montenegro    
## [13009] Serbia and Montenegro     Serbia and Montenegro    
## [13011] Seychelles                Seychelles               
## [13013] Seychelles                Seychelles               
## [13015] Seychelles                Seychelles               
## [13017] Seychelles                Seychelles               
## [13019] Seychelles                Seychelles               
## [13021] Seychelles                Seychelles               
## [13023] Seychelles                Seychelles               
## [13025] Seychelles                Seychelles               
## [13027] Seychelles                Seychelles               
## [13029] Seychelles                Seychelles               
## [13031] Seychelles                Seychelles               
## [13033] Seychelles                Seychelles               
## [13035] Seychelles                Seychelles               
## [13037] Seychelles                Seychelles               
## [13039] Seychelles                Seychelles               
## [13041] Seychelles                Seychelles               
## [13043] Seychelles                Seychelles               
## [13045] Seychelles                Seychelles               
## [13047] Seychelles                Seychelles               
## [13049] Seychelles                Seychelles               
## [13051] Seychelles                Seychelles               
## [13053] Seychelles                Seychelles               
## [13055] Seychelles                Seychelles               
## [13057] Seychelles                Seychelles               
## [13059] Seychelles                Seychelles               
## [13061] Seychelles                Seychelles               
## [13063] Seychelles                Seychelles               
## [13065] Seychelles                Seychelles               
## [13067] Seychelles                Seychelles               
## [13069] Seychelles                Seychelles               
## [13071] Seychelles                Seychelles               
## [13073] Seychelles                Seychelles               
## [13075] Seychelles                Seychelles               
## [13077] Seychelles                Seychelles               
## [13079] Seychelles                Seychelles               
## [13081] Sierra Leone              Sierra Leone             
## [13083] Sierra Leone              Sierra Leone             
## [13085] Sierra Leone              Sierra Leone             
## [13087] Sierra Leone              Sierra Leone             
## [13089] Sierra Leone              Sierra Leone             
## [13091] Sierra Leone              Sierra Leone             
## [13093] Sierra Leone              Sierra Leone             
## [13095] Sierra Leone              Sierra Leone             
## [13097] Sierra Leone              Sierra Leone             
## [13099] Sierra Leone              Sierra Leone             
## [13101] Sierra Leone              Sierra Leone             
## [13103] Sierra Leone              Sierra Leone             
## [13105] Sierra Leone              Sierra Leone             
## [13107] Sierra Leone              Sierra Leone             
## [13109] Sierra Leone              Sierra Leone             
## [13111] Sierra Leone              Sierra Leone             
## [13113] Sierra Leone              Sierra Leone             
## [13115] Sierra Leone              Sierra Leone             
## [13117] Sierra Leone              Sierra Leone             
## [13119] Sierra Leone              Sierra Leone             
## [13121] Sierra Leone              Sierra Leone             
## [13123] Sierra Leone              Sierra Leone             
## [13125] Sierra Leone              Sierra Leone             
## [13127] Sierra Leone              Sierra Leone             
## [13129] Sierra Leone              Sierra Leone             
## [13131] Sierra Leone              Sierra Leone             
## [13133] Sierra Leone              Sierra Leone             
## [13135] Sierra Leone              Sierra Leone             
## [13137] Sierra Leone              Sierra Leone             
## [13139] Sierra Leone              Singapore                
## [13141] Singapore                 Singapore                
## [13143] Singapore                 Singapore                
## [13145] Singapore                 Singapore                
## [13147] Singapore                 Singapore                
## [13149] Singapore                 Singapore                
## [13151] Singapore                 Singapore                
## [13153] Singapore                 Singapore                
## [13155] Singapore                 Singapore                
## [13157] Singapore                 Singapore                
## [13159] Singapore                 Singapore                
## [13161] Singapore                 Singapore                
## [13163] Singapore                 Singapore                
## [13165] Singapore                 Singapore                
## [13167] Singapore                 Singapore                
## [13169] Singapore                 Singapore                
## [13171] Singapore                 Singapore                
## [13173] Singapore                 Singapore                
## [13175] Singapore                 Singapore                
## [13177] Singapore                 Singapore                
## [13179] Singapore                 Sint Maarten             
## [13181] Sint Maarten              Slovenia                 
## [13183] Slovenia                  Slovenia                 
## [13185] Slovenia                  Slovenia                 
## [13187] Slovenia                  Slovenia                 
## [13189] Slovenia                  Slovenia                 
## [13191] Slovenia                  Slovenia                 
## [13193] Slovenia                  Slovenia                 
## [13195] Slovenia                  Slovenia                 
## [13197] Slovenia                  Slovenia                 
## [13199] Slovenia                  Slovenia                 
## [13201] Slovenia                  Slovenia                 
## [13203] Slovenia                  Slovenia                 
## [13205] Slovenia                  Slovenia                 
## [13207] Slovenia                  Slovenia                 
## [13209] Slovenia                  Slovenia                 
## [13211] Slovenia                  Slovenia                 
## [13213] Slovenia                  Slovenia                 
## [13215] Slovenia                  Slovenia                 
## [13217] Slovenia                  Slovenia                 
## [13219] Slovenia                  Slovenia                 
## [13221] Slovenia                  Slovenia                 
## [13223] Slovenia                  Slovenia                 
## [13225] Slovenia                  Slovenia                 
## [13227] Slovenia                  Slovenia                 
## [13229] Slovenia                  Slovenia                 
## [13231] Slovenia                  Solomon Islands          
## [13233] Solomon Islands           Solomon Islands          
## [13235] Solomon Islands           Solomon Islands          
## [13237] Solomon Islands           Solomon Islands          
## [13239] Solomon Islands           Solomon Islands          
## [13241] Solomon Islands           Solomon Islands          
## [13243] Solomon Islands           Solomon Islands          
## [13245] Solomon Islands           Solomon Islands          
## [13247] Solomon Islands           Solomon Islands          
## [13249] Solomon Islands           Somalia                  
## [13251] Somalia                   Somalia                  
## [13253] South Africa              South Africa             
## [13255] South Africa              South Africa             
## [13257] South Africa              South Africa             
## [13259] South Africa              South Africa             
## [13261] South Africa              South Africa             
## [13263] South Africa              South Africa             
## [13265] South Africa              South Africa             
## [13267] South Africa              South Africa             
## [13269] South Africa              South Africa             
## [13271] South Africa              South Africa             
## [13273] South Africa              South Africa             
## [13275] South Africa              South Africa             
## [13277] South Africa              South Africa             
## [13279] South Africa              South Africa             
## [13281] South Africa              South Africa             
## [13283] South Africa              South Africa             
## [13285] South Africa              South Africa             
## [13287] South Africa              South Africa             
## [13289] South Africa              South Africa             
## [13291] South Africa              South Africa             
## [13293] South Africa              South Africa             
## [13295] South Africa              South Africa             
## [13297] South Africa              South Africa             
## [13299] South Africa              South Africa             
## [13301] South Africa              South Africa             
## [13303] South Africa              South Africa             
## [13305] South Africa              South Africa             
## [13307] South Africa              South Africa             
## [13309] South Africa              South Africa             
## [13311] South Africa              South Africa             
## [13313] South Africa              South Africa             
## [13315] South Africa              South Africa             
## [13317] South Africa              South Africa             
## [13319] South Africa              South Africa             
## [13321] South Africa              South Africa             
## [13323] South Africa              South Africa             
## [13325] South Africa              South Africa             
## [13327] South Africa              South Africa             
## [13329] South Africa              South Africa             
## [13331] South Africa              South Africa             
## [13333] South Africa              South Africa             
## [13335] South Africa              South Africa             
## [13337] South Africa              South Africa             
## [13339] South Africa              South Africa             
## [13341] South Africa              South Africa             
## [13343] South Africa              South Africa             
## [13345] South Africa              South Africa             
## [13347] South Africa              South Africa             
## [13349] South Africa              South Africa             
## [13351] South Africa              South Africa             
## [13353] South Africa              South Africa             
## [13355] South Africa              South Africa             
## [13357] South Africa              South Africa             
## [13359] South Africa              South Africa             
## [13361] South Africa              South Africa             
## [13363] South Africa              South Africa             
## [13365] South Africa              South Africa             
## [13367] South Africa              South Africa             
## [13369] South Africa              South Africa             
## [13371] South Africa              South Africa             
## [13373] South Africa              South Africa             
## [13375] South Africa              South Africa             
## [13377] South Africa              South Africa             
## [13379] South Africa              South Africa             
## [13381] South Africa              South Africa             
## [13383] South Africa              South Africa             
## [13385] South Africa              South Africa             
## [13387] South Africa              South Africa             
## [13389] South Africa              South Africa             
## [13391] South Africa              South Africa             
## [13393] South Africa              South Africa             
## [13395] South Africa              South Africa             
## [13397] South Africa              South Africa             
## [13399] South Africa              South Africa             
## [13401] South Africa              South Africa             
## [13403] South Africa              South Africa             
## [13405] South Africa              South Africa             
## [13407] South Africa              South Africa             
## [13409] South Africa              South Africa             
## [13411] South Africa              South Africa             
## [13413] South Africa              South Africa             
## [13415] South Africa              South Africa             
## [13417] South Africa              South Africa             
## [13419] South Africa              South Africa             
## [13421] South Africa              South Africa             
## [13423] South Africa              South Africa             
## [13425] South Africa              South Africa             
## [13427] South Africa              South Africa             
## [13429] South Africa              South Africa             
## [13431] South Africa              South Africa             
## [13433] South Africa              South Africa             
## [13435] South Africa              South Africa             
## [13437] South Africa              South Africa             
## [13439] South Africa              South Africa             
## [13441] South Africa              South Africa             
## [13443] South Africa              South Africa             
## [13445] South Africa              South Africa             
## [13447] South Africa              South Africa             
## [13449] South Africa              South Africa             
## [13451] South Africa              South Africa             
## [13453] Spain                     Spain                    
## [13455] Spain                     Spain                    
## [13457] Spain                     Spain                    
## [13459] Spain                     Spain                    
## [13461] Spain                     Spain                    
## [13463] Spain                     Spain                    
## [13465] Spain                     Spain                    
## [13467] Spain                     Spain                    
## [13469] Spain                     Spain                    
## [13471] Spain                     Spain                    
## [13473] Spain                     Spain                    
## [13475] Spain                     Spain                    
## [13477] Spain                     Spain                    
## [13479] Spain                     Spain                    
## [13481] Spain                     Spain                    
## [13483] Spain                     Spain                    
## [13485] Spain                     Spain                    
## [13487] Spain                     Spain                    
## [13489] Spain                     Spain                    
## [13491] Spain                     Spain                    
## [13493] Spain                     Spain                    
## [13495] Spain                     Spain                    
## [13497] Spain                     Spain                    
## [13499] Spain                     Spain                    
## [13501] Spain                     Spain                    
## [13503] Spain                     Spain                    
## [13505] Spain                     Spain                    
## [13507] Spain                     Spain                    
## [13509] Spain                     Spain                    
## [13511] Spain                     Spain                    
## [13513] Spain                     Spain                    
## [13515] Spain                     Spain                    
## [13517] Spain                     Spain                    
## [13519] Spain                     Spain                    
## [13521] Spain                     Spain                    
## [13523] Spain                     Spain                    
## [13525] Spain                     Spain                    
## [13527] Spain                     Spain                    
## [13529] Spain                     Spain                    
## [13531] Spain                     Spain                    
## [13533] Spain                     Spain                    
## [13535] Spain                     Spain                    
## [13537] Spain                     Spain                    
## [13539] Spain                     Spain                    
## [13541] Spain                     Spain                    
## [13543] Spain                     Spain                    
## [13545] Spain                     Spain                    
## [13547] Spain                     Spain                    
## [13549] Spain                     Spain                    
## [13551] Spain                     Spain                    
## [13553] Spain                     Spain                    
## [13555] Spain                     Spain                    
## [13557] Spain                     Spain                    
## [13559] Spain                     Spain                    
## [13561] Spain                     Spain                    
## [13563] Spain                     Spain                    
## [13565] Spain                     Spain                    
## [13567] Spain                     Spain                    
## [13569] Spain                     Spain                    
## [13571] Spain                     Spain                    
## [13573] Spain                     Spain                    
## [13575] Spain                     Spain                    
## [13577] Spain                     Spain                    
## [13579] Spain                     Spain                    
## [13581] Spain                     Spain                    
## [13583] Spain                     Spain                    
## [13585] Spain                     Spain                    
## [13587] Spain                     Spain                    
## [13589] Spain                     Spain                    
## [13591] Spain                     Spain                    
## [13593] Spain                     Spain                    
## [13595] Spain                     Spain                    
## [13597] Spain                     Spain                    
## [13599] Spain                     Spain                    
## [13601] Spain                     Spain                    
## [13603] Spain                     Spain                    
## [13605] Spain                     Spain                    
## [13607] Spain                     Spain                    
## [13609] Spain                     Spain                    
## [13611] Spain                     Spain                    
## [13613] Spain                     Spain                    
## [13615] Spain                     Spain                    
## [13617] Spain                     Spain                    
## [13619] Spain                     Spain                    
## [13621] Spain                     Spain                    
## [13623] Spain                     Spain                    
## [13625] Spain                     Spain                    
## [13627] Spain                     Spain                    
## [13629] Spain                     Spain                    
## [13631] Spain                     Spain                    
## [13633] Spain                     Spain                    
## [13635] Spain                     Spain                    
## [13637] Spain                     Spain                    
## [13639] Spain                     Spain                    
## [13641] Spain                     Spain                    
## [13643] Spain                     Spain                    
## [13645] Spain                     Spain                    
## [13647] Spain                     Spain                    
## [13649] Spain                     Spain                    
## [13651] Spain                     Spain                    
## [13653] Spain                     Spain                    
## [13655] Spain                     Spain                    
## [13657] Spain                     Spain                    
## [13659] Spain                     Spain                    
## [13661] Spain                     Spain                    
## [13663] Spain                     Spain                    
## [13665] Spain                     Spain                    
## [13667] Spain                     Spain                    
## [13669] Spain                     Spain                    
## [13671] Spain                     Spain                    
## [13673] Spain                     Spain                    
## [13675] Spain                     Spain                    
## [13677] Spain                     Spain                    
## [13679] Spain                     Spain                    
## [13681] Spain                     Spain                    
## [13683] Spain                     Spain                    
## [13685] Spain                     Spain                    
## [13687] Spain                     Spain                    
## [13689] Spain                     Spain                    
## [13691] Spain                     Spain                    
## [13693] Spain                     Spain                    
## [13695] Spain                     Spain                    
## [13697] Spain                     Spain                    
## [13699] Spain                     Spain                    
## [13701] Spain                     Spain                    
## [13703] Spain                     Spain                    
## [13705] Spain                     Spain                    
## [13707] Spain                     Spain                    
## [13709] Spain                     Spain                    
## [13711] Spain                     Spain                    
## [13713] Spain                     Spain                    
## [13715] Spain                     Spain                    
## [13717] Spain                     Spain                    
## [13719] Spain                     Spain                    
## [13721] Spain                     Spain                    
## [13723] Spain                     Spain                    
## [13725] Spain                     Spain                    
## [13727] Spain                     Spain                    
## [13729] Spain                     Spain                    
## [13731] Spain                     Spain                    
## [13733] Spain                     Spain                    
## [13735] Spain                     Spain                    
## [13737] Spain                     Spain                    
## [13739] Spain                     Spain                    
## [13741] Spain                     Spain                    
## [13743] Spain                     Spain                    
## [13745] Spain                     Spain                    
## [13747] Spain                     Spain                    
## [13749] Spain                     Spain                    
## [13751] Spain                     Spain                    
## [13753] Spain                     Spain                    
## [13755] Spain                     Spain                    
## [13757] Spain                     Spain                    
## [13759] Spain                     Spain                    
## [13761] Spain                     Spain                    
## [13763] Spain                     Spain                    
## [13765] Spain                     Spain                    
## [13767] Spain                     Spain                    
## [13769] Spain                     Spain                    
## [13771] Spain                     Spain                    
## [13773] Spain                     Spain                    
## [13775] Spain                     Spain                    
## [13777] Spain                     Spain                    
## [13779] Spain                     Spain                    
## [13781] Spain                     Spain                    
## [13783] Spain                     Spain                    
## [13785] Spain                     Spain                    
## [13787] Spain                     Spain                    
## [13789] Spain                     Spain                    
## [13791] Spain                     Spain                    
## [13793] Spain                     Spain                    
## [13795] Spain                     Spain                    
## [13797] Spain                     Spain                    
## [13799] Spain                     Spain                    
## [13801] Spain                     Spain                    
## [13803] Spain                     Spain                    
## [13805] Spain                     Spain                    
## [13807] Spain                     Spain                    
## [13809] Spain                     Spain                    
## [13811] Spain                     Spain                    
## [13813] Spain                     Spain                    
## [13815] Spain                     Spain                    
## [13817] Spain                     Spain                    
## [13819] Spain                     Spain                    
## [13821] Spain                     Spain                    
## [13823] Spain                     Spain                    
## [13825] Spain                     Spain                    
## [13827] Spain                     Spain                    
## [13829] Spain                     Spain                    
## [13831] Spain                     Spain                    
## [13833] Spain                     Spain                    
## [13835] Spain                     Spain                    
## [13837] Spain                     Spain                    
## [13839] Spain                     Spain                    
## [13841] Spain                     Spain                    
## [13843] Spain                     Spain                    
## [13845] Spain                     Spain                    
## [13847] Spain                     Spain                    
## [13849] Spain                     Spain                    
## [13851] Spain                     Spain                    
## [13853] Spain                     Spain                    
## [13855] Spain                     Spain                    
## [13857] Spain                     Spain                    
## [13859] Spain                     Spain                    
## [13861] Spain                     Spain                    
## [13863] Spain                     Spain                    
## [13865] Spain                     Spain                    
## [13867] Spain                     Spain                    
## [13869] Spain                     Spain                    
## [13871] Spain                     Spain                    
## [13873] Spain                     Spain                    
## [13875] Spain                     Spain                    
## [13877] Spain                     Spain                    
## [13879] Spain                     Spain                    
## [13881] Spain                     Spain                    
## [13883] Spain                     Spain                    
## [13885] Spain                     Spain                    
## [13887] Spain                     Spain                    
## [13889] Spain                     Spain                    
## [13891] Spain                     Spain                    
## [13893] Spain                     Spain                    
## [13895] Spain                     Spain                    
## [13897] Spain                     Spain                    
## [13899] Spain                     Spain                    
## [13901] Spain                     Spain                    
## [13903] Spain                     Spain                    
## [13905] Spain                     Spain                    
## [13907] Spain                     Spain                    
## [13909] Spain                     Spain                    
## [13911] Spain                     Spain                    
## [13913] Spain                     Spain                    
## [13915] Spain                     Spain                    
## [13917] Spain                     Spain                    
## [13919] Spain                     Spain                    
## [13921] Spain                     Spain                    
## [13923] Spain                     Spain                    
## [13925] Spain                     Spain                    
## [13927] Spain                     Spain                    
## [13929] Spain                     Spain                    
## [13931] Spain                     Spain                    
## [13933] Spain                     Spain                    
## [13935] Spain                     Spain                    
## [13937] Spain                     Spain                    
## [13939] Spain                     Spain                    
## [13941] Spain                     Spain                    
## [13943] Spain                     Spain                    
## [13945] Spain                     Spain                    
## [13947] Spain                     Spain                    
## [13949] Spain                     Spain                    
## [13951] Spain                     Spain                    
## [13953] Spain                     Spain                    
## [13955] Spain                     Spain                    
## [13957] Spain                     Spain                    
## [13959] Spain                     Spain                    
## [13961] Spain                     Spain                    
## [13963] Spain                     Spain                    
## [13965] Spain                     Spain                    
## [13967] Spain                     Spain                    
## [13969] Spain                     Spain                    
## [13971] Spain                     Spain                    
## [13973] Spain                     Spain                    
## [13975] Spain                     Spain                    
## [13977] Spain                     Spain                    
## [13979] Spain                     Spain                    
## [13981] Spain                     Spain                    
## [13983] Spain                     Spain                    
## [13985] Spain                     Spain                    
## [13987] Spain                     Spain                    
## [13989] Spain                     Spain                    
## [13991] Spain                     Spain                    
## [13993] Spain                     Spain                    
## [13995] Spain                     Spain                    
## [13997] Spain                     Spain                    
## [13999] Spain                     Spain                    
## [14001] Spain                     Spain                    
## [14003] Spain                     Spain                    
## [14005] Spain                     Spain                    
## [14007] Spain                     Spain                    
## [14009] Spain                     Spain                    
## [14011] Spain                     Spain                    
## [14013] Spain                     Spain                    
## [14015] Spain                     Spain                    
## [14017] Spain                     Spain                    
## [14019] Spain                     Spain                    
## [14021] Spain                     Spain                    
## [14023] Spain                     Spain                    
## [14025] Spain                     Spain                    
## [14027] Spain                     Spain                    
## [14029] Spain                     Spain                    
## [14031] Spain                     Spain                    
## [14033] Spain                     Spain                    
## [14035] Spain                     Spain                    
## [14037] Spain                     Spain                    
## [14039] Spain                     Spain                    
## [14041] Spain                     Spain                    
## [14043] Spain                     Spain                    
## [14045] Spain                     Spain                    
## [14047] Spain                     Spain                    
## [14049] Spain                     Spain                    
## [14051] Spain                     Spain                    
## [14053] Spain                     Spain                    
## [14055] Spain                     Spain                    
## [14057] Spain                     Spain                    
## [14059] Spain                     Spain                    
## [14061] Spain                     Spain                    
## [14063] Spain                     Spain                    
## [14065] Spain                     Spain                    
## [14067] Spain                     Spain                    
## [14069] Spain                     Spain                    
## [14071] Spain                     Spain                    
## [14073] Spain                     Spain                    
## [14075] Spain                     Spain                    
## [14077] Spain                     Spain                    
## [14079] Spain                     Spain                    
## [14081] Spain                     Spain                    
## [14083] Spain                     Spain                    
## [14085] Spain                     Spain                    
## [14087] Spain                     Spain                    
## [14089] Spain                     Spain                    
## [14091] Spain                     Spain                    
## [14093] Spain                     Spain                    
## [14095] Spain                     Spain                    
## [14097] Spain                     Spain                    
## [14099] Spain                     Spain                    
## [14101] Spain                     Spain                    
## [14103] Spain                     Spain                    
## [14105] Spain                     Spain                    
## [14107] Spain                     Spain                    
## [14109] Spain                     Spain                    
## [14111] Spain                     Spain                    
## [14113] Spain                     Spain                    
## [14115] Spain                     Spain                    
## [14117] Spain                     Spain                    
## [14119] Spain                     Spain                    
## [14121] Spain                     Spain                    
## [14123] Spain                     Spain                    
## [14125] Spain                     Spain                    
## [14127] Spain                     Spain                    
## [14129] Spain                     Spain                    
## [14131] Spain                     Spain                    
## [14133] Spain                     Spain                    
## [14135] Spain                     Spain                    
## [14137] Spain                     Spain                    
## [14139] Spain                     Spain                    
## [14141] Spain                     Spain                    
## [14143] Spain                     Spain                    
## [14145] Spain                     Spain                    
## [14147] Spain                     Spain                    
## [14149] Spain                     Spain                    
## [14151] Spain                     Spain                    
## [14153] Spain                     Spain                    
## [14155] Spain                     Spain                    
## [14157] Spain                     Spain                    
## [14159] Spain                     Spain                    
## [14161] Spain                     Spain                    
## [14163] Spain                     Spain                    
## [14165] Spain                     Spain                    
## [14167] Spain                     Spain                    
## [14169] Spain                     Spain                    
## [14171] Spain                     Spain                    
## [14173] Spain                     Spain                    
## [14175] Spain                     Spain                    
## [14177] Spain                     Spain                    
## [14179] Spain                     Spain                    
## [14181] Spain                     Spain                    
## [14183] Spain                     Spain                    
## [14185] Spain                     Spain                    
## [14187] Spain                     Spain                    
## [14189] Spain                     Spain                    
## [14191] Spain                     Spain                    
## [14193] Spain                     Spain                    
## [14195] Spain                     Spain                    
## [14197] Spain                     Spain                    
## [14199] Spain                     Spain                    
## [14201] Spain                     Spain                    
## [14203] Spain                     Spain                    
## [14205] Spain                     Spain                    
## [14207] Spain                     Spain                    
## [14209] Spain                     Spain                    
## [14211] Spain                     Spain                    
## [14213] Spain                     Spain                    
## [14215] Spain                     Spain                    
## [14217] Spain                     Spain                    
## [14219] Spain                     Spain                    
## [14221] Spain                     Spain                    
## [14223] Spain                     Spain                    
## [14225] Spain                     Spain                    
## [14227] Spain                     Spain                    
## [14229] Spain                     Spain                    
## [14231] Spain                     Spain                    
## [14233] Spain                     Spain                    
## [14235] Spain                     Spain                    
## [14237] Spain                     Spain                    
## [14239] Spain                     Spain                    
## [14241] Spain                     Spain                    
## [14243] Spain                     Spain                    
## [14245] Spain                     Spain                    
## [14247] Spain                     Spain                    
## [14249] Spain                     Spain                    
## [14251] Spain                     Spain                    
## [14253] Spain                     Spain                    
## [14255] Spain                     Spain                    
## [14257] Spain                     Spain                    
## [14259] Spain                     Spain                    
## [14261] Spain                     Spain                    
## [14263] Spain                     Spain                    
## [14265] Spain                     Spain                    
## [14267] Spain                     Spain                    
## [14269] Spain                     Spain                    
## [14271] Spain                     Spain                    
## [14273] Spain                     Spain                    
## [14275] Spain                     Spain                    
## [14277] Spain                     Spain                    
## [14279] Spain                     Spain                    
## [14281] Spain                     Spain                    
## [14283] Spain                     Spain                    
## [14285] Spain                     Spain                    
## [14287] Spain                     Spain                    
## [14289] Spain                     Spain                    
## [14291] Spain                     Spain                    
## [14293] Spain                     Spain                    
## [14295] Spain                     Spain                    
## [14297] Spain                     Spain                    
## [14299] Spain                     Spain                    
## [14301] Spain                     Spain                    
## [14303] Spain                     Spain                    
## [14305] Spain                     Spain                    
## [14307] Spain                     Spain                    
## [14309] Spain                     Spain                    
## [14311] Spain                     Spain                    
## [14313] Spain                     Spain                    
## [14315] Spain                     Spain                    
## [14317] Spain                     Spain                    
## [14319] Spain                     Spain                    
## [14321] Spain                     Spain                    
## [14323] Spain                     Spain                    
## [14325] Spain                     Spain                    
## [14327] Spain                     Spain                    
## [14329] Spain                     Spain                    
## [14331] Spain                     Spain                    
## [14333] Spain                     Spain                    
## [14335] Spain                     Spain                    
## [14337] Spain                     Spain                    
## [14339] Spain                     Spain                    
## [14341] Spain                     Spain                    
## [14343] Spain                     Spain                    
## [14345] Spain                     Spain                    
## [14347] Spain                     Spain                    
## [14349] Spain                     Spain                    
## [14351] Spain                     Spain                    
## [14353] Spain                     Spain                    
## [14355] Spain                     Spain                    
## [14357] Spain                     Spain                    
## [14359] Spain                     Spain                    
## [14361] Spain                     Spain                    
## [14363] Spain                     Spain                    
## [14365] Spain                     Spain                    
## [14367] Spain                     Sri Lanka                
## [14369] Sri Lanka                 Sri Lanka                
## [14371] Sri Lanka                 Sri Lanka                
## [14373] Sri Lanka                 Sri Lanka                
## [14375] Sri Lanka                 Sri Lanka                
## [14377] Sri Lanka                 Sri Lanka                
## [14379] Sri Lanka                 Sri Lanka                
## [14381] Sri Lanka                 Sri Lanka                
## [14383] Sri Lanka                 Sri Lanka                
## [14385] Sri Lanka                 Sri Lanka                
## [14387] Sri Lanka                 Sri Lanka                
## [14389] Sri Lanka                 Sri Lanka                
## [14391] Sri Lanka                 Sri Lanka                
## [14393] Sri Lanka                 Sri Lanka                
## [14395] Sri Lanka                 Sri Lanka                
## [14397] Sri Lanka                 Sri Lanka                
## [14399] Sri Lanka                 Sri Lanka                
## [14401] Sri Lanka                 St. Pierre and Miquelon  
## [14403] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14405] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14407] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14409] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14411] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14413] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14415] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14417] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14419] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14421] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14423] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14425] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14427] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14429] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14431] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14433] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14435] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14437] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14439] St. Pierre and Miquelon   St. Pierre and Miquelon  
## [14441] St. Pierre and Miquelon   Sudan                    
## [14443] Sudan                     Sudan                    
## [14445] Sudan (former)            Sudan (former)           
## [14447] Sudan (former)            Suriname                 
## [14449] Suriname                  Suriname                 
## [14451] Suriname                  Suriname                 
## [14453] Suriname                  Suriname                 
## [14455] Suriname                  Suriname                 
## [14457] Suriname                  Suriname                 
## [14459] Suriname                  Suriname                 
## [14461] Suriname                  Suriname                 
## [14463] Suriname                  Suriname                 
## [14465] Suriname                  Suriname                 
## [14467] Suriname                  Suriname                 
## [14469] Suriname                  Suriname                 
## [14471] Suriname                  Suriname                 
## [14473] Suriname                  Suriname                 
## [14475] Svalbard and Jan Mayen    Sweden                   
## [14477] Sweden                    Sweden                   
## [14479] Sweden                    Sweden                   
## [14481] Sweden                    Sweden                   
## [14483] Sweden                    Sweden                   
## [14485] Sweden                    Sweden                   
## [14487] Sweden                    Sweden                   
## [14489] Sweden                    Sweden                   
## [14491] Sweden                    Sweden                   
## [14493] Sweden                    Sweden                   
## [14495] Sweden                    Sweden                   
## [14497] Sweden                    Sweden                   
## [14499] Sweden                    Sweden                   
## [14501] Sweden                    Sweden                   
## [14503] Sweden                    Sweden                   
## [14505] Sweden                    Sweden                   
## [14507] Sweden                    Sweden                   
## [14509] Sweden                    Sweden                   
## [14511] Sweden                    Sweden                   
## [14513] Sweden                    Sweden                   
## [14515] Sweden                    Sweden                   
## [14517] Sweden                    Sweden                   
## [14519] Sweden                    Sweden                   
## [14521] Sweden                    Sweden                   
## [14523] Sweden                    Sweden                   
## [14525] Sweden                    Sweden                   
## [14527] Sweden                    Sweden                   
## [14529] Sweden                    Sweden                   
## [14531] Sweden                    Sweden                   
## [14533] Sweden                    Sweden                   
## [14535] Sweden                    Sweden                   
## [14537] Sweden                    Sweden                   
## [14539] Sweden                    Sweden                   
## [14541] Sweden                    Sweden                   
## [14543] Sweden                    Sweden                   
## [14545] Sweden                    Sweden                   
## [14547] Sweden                    Syrian Arab Republic     
## [14549] Syrian Arab Republic      Syrian Arab Republic     
## [14551] Syrian Arab Republic      Syrian Arab Republic     
## [14553] Syrian Arab Republic      Syrian Arab Republic     
## [14555] Syrian Arab Republic      Syrian Arab Republic     
## [14557] Syrian Arab Republic      Syrian Arab Republic     
## [14559] Syrian Arab Republic      Syrian Arab Republic     
## [14561] Syrian Arab Republic      Syrian Arab Republic     
## [14563] Syrian Arab Republic      Syrian Arab Republic     
## [14565] Syrian Arab Republic      Syrian Arab Republic     
## [14567] Syrian Arab Republic      Syrian Arab Republic     
## [14569] Syrian Arab Republic      Syrian Arab Republic     
## [14571] Syrian Arab Republic      Syrian Arab Republic     
## [14573] Syrian Arab Republic      Syrian Arab Republic     
## [14575] Syrian Arab Republic      Syrian Arab Republic     
## [14577] Syrian Arab Republic      Syrian Arab Republic     
## [14579] Syrian Arab Republic      Syrian Arab Republic     
## [14581] Syrian Arab Republic      Taiwan Province of China 
## [14583] Taiwan Province of China  Taiwan Province of China 
## [14585] Taiwan Province of China  Taiwan Province of China 
## [14587] Taiwan Province of China  Taiwan Province of China 
## [14589] Taiwan Province of China  Taiwan Province of China 
## [14591] Taiwan Province of China  Taiwan Province of China 
## [14593] Taiwan Province of China  Taiwan Province of China 
## [14595] Taiwan Province of China  Taiwan Province of China 
## [14597] Taiwan Province of China  Taiwan Province of China 
## [14599] Taiwan Province of China  Taiwan Province of China 
## [14601] Taiwan Province of China  Taiwan Province of China 
## [14603] Taiwan Province of China  Taiwan Province of China 
## [14605] Taiwan Province of China  Taiwan Province of China 
## [14607] Taiwan Province of China  Taiwan Province of China 
## [14609] Taiwan Province of China  Taiwan Province of China 
## [14611] Taiwan Province of China  Taiwan Province of China 
## [14613] Taiwan Province of China  Taiwan Province of China 
## [14615] Taiwan Province of China  Taiwan Province of China 
## [14617] Taiwan Province of China  Taiwan Province of China 
## [14619] Taiwan Province of China  Taiwan Province of China 
## [14621] Taiwan Province of China  Taiwan Province of China 
## [14623] Taiwan Province of China  Taiwan Province of China 
## [14625] Taiwan Province of China  Taiwan Province of China 
## [14627] Taiwan Province of China  Taiwan Province of China 
## [14629] Taiwan Province of China  Taiwan Province of China 
## [14631] Taiwan Province of China  Taiwan Province of China 
## [14633] Taiwan Province of China  Taiwan Province of China 
## [14635] Taiwan Province of China  Taiwan Province of China 
## [14637] Taiwan Province of China  Taiwan Province of China 
## [14639] Taiwan Province of China  Taiwan Province of China 
## [14641] Taiwan Province of China  Taiwan Province of China 
## [14643] Taiwan Province of China  Taiwan Province of China 
## [14645] Taiwan Province of China  Taiwan Province of China 
## [14647] Taiwan Province of China  Taiwan Province of China 
## [14649] Taiwan Province of China  Taiwan Province of China 
## [14651] Taiwan Province of China  Taiwan Province of China 
## [14653] Taiwan Province of China  Taiwan Province of China 
## [14655] Taiwan Province of China  Taiwan Province of China 
## [14657] Taiwan Province of China  Taiwan Province of China 
## [14659] Taiwan Province of China  Taiwan Province of China 
## [14661] Taiwan Province of China  Taiwan Province of China 
## [14663] Taiwan Province of China  Taiwan Province of China 
## [14665] Taiwan Province of China  Taiwan Province of China 
## [14667] Taiwan Province of China  Taiwan Province of China 
## [14669] Taiwan Province of China  Taiwan Province of China 
## [14671] Taiwan Province of China  Taiwan Province of China 
## [14673] Taiwan Province of China  Taiwan Province of China 
## [14675] Taiwan Province of China  Taiwan Province of China 
## [14677] Taiwan Province of China  Taiwan Province of China 
## [14679] Taiwan Province of China  Taiwan Province of China 
## [14681] Taiwan Province of China  Taiwan Province of China 
## [14683] Taiwan Province of China  Taiwan Province of China 
## [14685] Taiwan Province of China  Taiwan Province of China 
## [14687] Taiwan Province of China  Taiwan Province of China 
## [14689] Taiwan Province of China  Taiwan Province of China 
## [14691] Taiwan Province of China  Taiwan Province of China 
## [14693] Taiwan Province of China  Taiwan Province of China 
## [14695] Taiwan Province of China  Taiwan Province of China 
## [14697] Taiwan Province of China  Taiwan Province of China 
## [14699] Taiwan Province of China  Taiwan Province of China 
## [14701] Taiwan Province of China  Taiwan Province of China 
## [14703] Taiwan Province of China  Taiwan Province of China 
## [14705] Taiwan Province of China  Taiwan Province of China 
## [14707] Taiwan Province of China  Taiwan Province of China 
## [14709] Taiwan Province of China  Taiwan Province of China 
## [14711] Taiwan Province of China  Taiwan Province of China 
## [14713] Taiwan Province of China  Taiwan Province of China 
## [14715] Taiwan Province of China  Taiwan Province of China 
## [14717] Taiwan Province of China  Taiwan Province of China 
## [14719] Taiwan Province of China  Taiwan Province of China 
## [14721] Taiwan Province of China  Taiwan Province of China 
## [14723] Taiwan Province of China  Taiwan Province of China 
## [14725] Taiwan Province of China  Taiwan Province of China 
## [14727] Taiwan Province of China  Taiwan Province of China 
## [14729] Taiwan Province of China  Taiwan Province of China 
## [14731] Taiwan Province of China  Taiwan Province of China 
## [14733] Taiwan Province of China  Taiwan Province of China 
## [14735] Taiwan Province of China  Taiwan Province of China 
## [14737] Taiwan Province of China  Taiwan Province of China 
## [14739] Taiwan Province of China  Taiwan Province of China 
## [14741] Taiwan Province of China  Taiwan Province of China 
## [14743] Taiwan Province of China  Taiwan Province of China 
## [14745] Taiwan Province of China  Taiwan Province of China 
## [14747] Taiwan Province of China  Taiwan Province of China 
## [14749] Taiwan Province of China  Taiwan Province of China 
## [14751] Taiwan Province of China  Taiwan Province of China 
## [14753] Taiwan Province of China  Taiwan Province of China 
## [14755] Taiwan Province of China  Taiwan Province of China 
## [14757] Taiwan Province of China  Taiwan Province of China 
## [14759] Taiwan Province of China  Taiwan Province of China 
## [14761] Taiwan Province of China  Taiwan Province of China 
## [14763] Taiwan Province of China  Taiwan Province of China 
## [14765] Taiwan Province of China  Taiwan Province of China 
## [14767] Taiwan Province of China  Taiwan Province of China 
## [14769] Taiwan Province of China  Taiwan Province of China 
## [14771] Taiwan Province of China  Taiwan Province of China 
## [14773] Taiwan Province of China  Taiwan Province of China 
## [14775] Taiwan Province of China  Taiwan Province of China 
## [14777] Taiwan Province of China  Taiwan Province of China 
## [14779] Taiwan Province of China  Taiwan Province of China 
## [14781] Taiwan Province of China  Taiwan Province of China 
## [14783] Taiwan Province of China  Taiwan Province of China 
## [14785] Taiwan Province of China  Taiwan Province of China 
## [14787] Taiwan Province of China  Taiwan Province of China 
## [14789] Taiwan Province of China  Taiwan Province of China 
## [14791] Taiwan Province of China  Taiwan Province of China 
## [14793] Taiwan Province of China  Taiwan Province of China 
## [14795] Taiwan Province of China  Taiwan Province of China 
## [14797] Taiwan Province of China  Taiwan Province of China 
## [14799] Taiwan Province of China  Taiwan Province of China 
## [14801] Taiwan Province of China  Taiwan Province of China 
## [14803] Taiwan Province of China  Taiwan Province of China 
## [14805] Taiwan Province of China  Taiwan Province of China 
## [14807] Taiwan Province of China  Taiwan Province of China 
## [14809] Taiwan Province of China  Taiwan Province of China 
## [14811] Taiwan Province of China  Taiwan Province of China 
## [14813] Taiwan Province of China  Taiwan Province of China 
## [14815] Taiwan Province of China  Taiwan Province of China 
## [14817] Taiwan Province of China  Taiwan Province of China 
## [14819] Taiwan Province of China  Taiwan Province of China 
## [14821] Taiwan Province of China  Taiwan Province of China 
## [14823] Taiwan Province of China  Taiwan Province of China 
## [14825] Taiwan Province of China  Taiwan Province of China 
## [14827] Taiwan Province of China  Taiwan Province of China 
## [14829] Taiwan Province of China  Taiwan Province of China 
## [14831] Taiwan Province of China  Taiwan Province of China 
## [14833] Taiwan Province of China  Taiwan Province of China 
## [14835] Taiwan Province of China  Taiwan Province of China 
## [14837] Taiwan Province of China  Taiwan Province of China 
## [14839] Taiwan Province of China  Taiwan Province of China 
## [14841] Taiwan Province of China  Taiwan Province of China 
## [14843] Taiwan Province of China  Taiwan Province of China 
## [14845] Taiwan Province of China  Taiwan Province of China 
## [14847] Taiwan Province of China  Taiwan Province of China 
## [14849] Taiwan Province of China  Taiwan Province of China 
## [14851] Taiwan Province of China  Taiwan Province of China 
## [14853] Taiwan Province of China  Taiwan Province of China 
## [14855] Taiwan Province of China  Taiwan Province of China 
## [14857] Taiwan Province of China  Taiwan Province of China 
## [14859] Taiwan Province of China  Taiwan Province of China 
## [14861] Taiwan Province of China  Taiwan Province of China 
## [14863] Taiwan Province of China  Taiwan Province of China 
## [14865] Taiwan Province of China  Taiwan Province of China 
## [14867] Taiwan Province of China  Taiwan Province of China 
## [14869] Taiwan Province of China  Taiwan Province of China 
## [14871] Taiwan Province of China  Taiwan Province of China 
## [14873] Taiwan Province of China  Taiwan Province of China 
## [14875] Taiwan Province of China  Taiwan Province of China 
## [14877] Taiwan Province of China  Taiwan Province of China 
## [14879] Taiwan Province of China  Taiwan Province of China 
## [14881] Taiwan Province of China  Taiwan Province of China 
## [14883] Taiwan Province of China  Taiwan Province of China 
## [14885] Taiwan Province of China  Taiwan Province of China 
## [14887] Taiwan Province of China  Taiwan Province of China 
## [14889] Taiwan Province of China  Taiwan Province of China 
## [14891] Taiwan Province of China  Tanzania, United Rep. of 
## [14893] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14895] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14897] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14899] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14901] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14903] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14905] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14907] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14909] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14911] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14913] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14915] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14917] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14919] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14921] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14923] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14925] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14927] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14929] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14931] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14933] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14935] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14937] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14939] Tanzania, United Rep. of  Tanzania, United Rep. of 
## [14941] Thailand                  Thailand                 
## [14943] Thailand                  Thailand                 
## [14945] Thailand                  Thailand                 
## [14947] Thailand                  Thailand                 
## [14949] Thailand                  Thailand                 
## [14951] Thailand                  Thailand                 
## [14953] Thailand                  Thailand                 
## [14955] Thailand                  Thailand                 
## [14957] Thailand                  Thailand                 
## [14959] Thailand                  Thailand                 
## [14961] Thailand                  Thailand                 
## [14963] Thailand                  Thailand                 
## [14965] Thailand                  Thailand                 
## [14967] Thailand                  Thailand                 
## [14969] Thailand                  Thailand                 
## [14971] Thailand                  Thailand                 
## [14973] Thailand                  Thailand                 
## [14975] Thailand                  Thailand                 
## [14977] Thailand                  Thailand                 
## [14979] Thailand                  Thailand                 
## [14981] Thailand                  Thailand                 
## [14983] Thailand                  Thailand                 
## [14985] Thailand                  Thailand                 
## [14987] Thailand                  Thailand                 
## [14989] Thailand                  Thailand                 
## [14991] Thailand                  Thailand                 
## [14993] Thailand                  Thailand                 
## [14995] Thailand                  Thailand                 
## [14997] Thailand                  Thailand                 
## [14999] Thailand                  Thailand                 
## [15001] Thailand                  Thailand                 
## [15003] Thailand                  Thailand                 
## [15005] Thailand                  Thailand                 
## [15007] Thailand                  Thailand                 
## [15009] Thailand                  Thailand                 
## [15011] Thailand                  Thailand                 
## [15013] Thailand                  Thailand                 
## [15015] Thailand                  Thailand                 
## [15017] Thailand                  Thailand                 
## [15019] Thailand                  Thailand                 
## [15021] Thailand                  Thailand                 
## [15023] Thailand                  Thailand                 
## [15025] Thailand                  Thailand                 
## [15027] Thailand                  Thailand                 
## [15029] Thailand                  Thailand                 
## [15031] Thailand                  Thailand                 
## [15033] Thailand                  Thailand                 
## [15035] Thailand                  Thailand                 
## [15037] Thailand                  Thailand                 
## [15039] Thailand                  Thailand                 
## [15041] Thailand                  Thailand                 
## [15043] Thailand                  Thailand                 
## [15045] Thailand                  Thailand                 
## [15047] Thailand                  Thailand                 
## [15049] Thailand                  Thailand                 
## [15051] Thailand                  Thailand                 
## [15053] Thailand                  Thailand                 
## [15055] Thailand                  Thailand                 
## [15057] Thailand                  Thailand                 
## [15059] Thailand                  Thailand                 
## [15061] Thailand                  Thailand                 
## [15063] Thailand                  Thailand                 
## [15065] Thailand                  Thailand                 
## [15067] Thailand                  Thailand                 
## [15069] Thailand                  Thailand                 
## [15071] Thailand                  Thailand                 
## [15073] Thailand                  Thailand                 
## [15075] Thailand                  Thailand                 
## [15077] Thailand                  Thailand                 
## [15079] Thailand                  Thailand                 
## [15081] Thailand                  Thailand                 
## [15083] Thailand                  Thailand                 
## [15085] Thailand                  Thailand                 
## [15087] Thailand                  Thailand                 
## [15089] Thailand                  Thailand                 
## [15091] TimorLeste                TimorLeste               
## [15093] TimorLeste                TimorLeste               
## [15095] TimorLeste                TimorLeste               
## [15097] TimorLeste                Togo                     
## [15099] Togo                      Togo                     
## [15101] Togo                      Togo                     
## [15103] Togo                      Togo                     
## [15105] Togo                      Togo                     
## [15107] Togo                      Togo                     
## [15109] Togo                      Togo                     
## [15111] Togo                      Togo                     
## [15113] Togo                      Togo                     
## [15115] Togo                      Togo                     
## [15117] Togo                      Togo                     
## [15119] Togo                      Togo                     
## [15121] Togo                      Togo                     
## [15123] Togo                      Togo                     
## [15125] Togo                      Togo                     
## [15127] Togo                      Togo                     
## [15129] Togo                      Togo                     
## [15131] Togo                      Togo                     
## [15133] Togo                      Togo                     
## [15135] Togo                      Togo                     
## [15137] Togo                      Togo                     
## [15139] Togo                      Togo                     
## [15141] Togo                      Togo                     
## [15143] Togo                      Togo                     
## [15145] Togo                      Togo                     
## [15147] Togo                      Togo                     
## [15149] Togo                      Togo                     
## [15151] Togo                      Togo                     
## [15153] Togo                      Togo                     
## [15155] Togo                      Togo                     
## [15157] Togo                      Togo                     
## [15159] Togo                      Togo                     
## [15161] Togo                      Togo                     
## [15163] Togo                      Togo                     
## [15165] Togo                      Togo                     
## [15167] Togo                      Togo                     
## [15169] Togo                      Togo                     
## [15171] Togo                      Togo                     
## [15173] Togo                      Togo                     
## [15175] Togo                      Tokelau                  
## [15177] Tokelau                   Tokelau                  
## [15179] Tokelau                   Tokelau                  
## [15181] Tokelau                   Tokelau                  
## [15183] Tokelau                   Tokelau                  
## [15185] Tokelau                   Tonga                    
## [15187] Tonga                     Tonga                    
## [15189] Tonga                     Tonga                    
## [15191] Tonga                     Tonga                    
## [15193] Tonga                     Tonga                    
## [15195] Tonga                     Tonga                    
## [15197] Tonga                     Tonga                    
## [15199] Tonga                     Trinidad and Tobago      
## [15201] Trinidad and Tobago       Trinidad and Tobago      
## [15203] Trinidad and Tobago       Trinidad and Tobago      
## [15205] Trinidad and Tobago       Trinidad and Tobago      
## [15207] Trinidad and Tobago       Trinidad and Tobago      
## [15209] Trinidad and Tobago       Trinidad and Tobago      
## [15211] Trinidad and Tobago       Trinidad and Tobago      
## [15213] Trinidad and Tobago       Trinidad and Tobago      
## [15215] Trinidad and Tobago       Trinidad and Tobago      
## [15217] Trinidad and Tobago       Trinidad and Tobago      
## [15219] Trinidad and Tobago       Trinidad and Tobago      
## [15221] Trinidad and Tobago       Trinidad and Tobago      
## [15223] Trinidad and Tobago       Trinidad and Tobago      
## [15225] Trinidad and Tobago       Trinidad and Tobago      
## [15227] Trinidad and Tobago       Trinidad and Tobago      
## [15229] Trinidad and Tobago       Trinidad and Tobago      
## [15231] Trinidad and Tobago       Trinidad and Tobago      
## [15233] Trinidad and Tobago       Trinidad and Tobago      
## [15235] Trinidad and Tobago       Trinidad and Tobago      
## [15237] Trinidad and Tobago       Trinidad and Tobago      
## [15239] Tunisia                   Tunisia                  
## [15241] Tunisia                   Tunisia                  
## [15243] Tunisia                   Tunisia                  
## [15245] Tunisia                   Tunisia                  
## [15247] Tunisia                   Tunisia                  
## [15249] Tunisia                   Tunisia                  
## [15251] Tunisia                   Tunisia                  
## [15253] Tunisia                   Tunisia                  
## [15255] Tunisia                   Tunisia                  
## [15257] Tunisia                   Tunisia                  
## [15259] Tunisia                   Tunisia                  
## [15261] Tunisia                   Tunisia                  
## [15263] Tunisia                   Tunisia                  
## [15265] Tunisia                   Tunisia                  
## [15267] Tunisia                   Tunisia                  
## [15269] Tunisia                   Tunisia                  
## [15271] Tunisia                   Tunisia                  
## [15273] Tunisia                   Tunisia                  
## [15275] Tunisia                   Tunisia                  
## [15277] Tunisia                   Tunisia                  
## [15279] Tunisia                   Tunisia                  
## [15281] Tunisia                   Tunisia                  
## [15283] Tunisia                   Tunisia                  
## [15285] Tunisia                   Tunisia                  
## [15287] Tunisia                   Tunisia                  
## [15289] Tunisia                   Tunisia                  
## [15291] Tunisia                   Tunisia                  
## [15293] Tunisia                   Tunisia                  
## [15295] Tunisia                   Tunisia                  
## [15297] Tunisia                   Tunisia                  
## [15299] Tunisia                   Tunisia                  
## [15301] Tunisia                   Tunisia                  
## [15303] Tunisia                   Tunisia                  
## [15305] Tunisia                   Tunisia                  
## [15307] Tunisia                   Tunisia                  
## [15309] Tunisia                   Tunisia                  
## [15311] Tunisia                   Tunisia                  
## [15313] Tunisia                   Tunisia                  
## [15315] Tunisia                   Tunisia                  
## [15317] Tunisia                   Tunisia                  
## [15319] Tunisia                   Tunisia                  
## [15321] Tunisia                   Tunisia                  
## [15323] Tunisia                   Turkey                   
## [15325] Turkey                    Turkey                   
## [15327] Turkey                    Turkey                   
## [15329] Turkey                    Turkey                   
## [15331] Turkey                    Turkey                   
## [15333] Turkey                    Turkey                   
## [15335] Turkey                    Turkey                   
## [15337] Turkey                    Turkey                   
## [15339] Turkey                    Turkey                   
## [15341] Turkey                    Turkey                   
## [15343] Turkey                    Turkey                   
## [15345] Turkey                    Turkey                   
## [15347] Turkey                    Turkey                   
## [15349] Turkey                    Turkey                   
## [15351] Turkey                    Turkey                   
## [15353] Turkey                    Turkey                   
## [15355] Turkey                    Turkey                   
## [15357] Turkey                    Turkey                   
## [15359] Turkey                    Turkey                   
## [15361] Turkey                    Turkey                   
## [15363] Turkey                    Turkey                   
## [15365] Turkey                    Turkey                   
## [15367] Turkey                    Turkey                   
## [15369] Turkey                    Turkey                   
## [15371] Turkey                    Turkey                   
## [15373] Turkey                    Turkey                   
## [15375] Turkey                    Turkey                   
## [15377] Turkey                    Turkey                   
## [15379] Turkey                    Turkey                   
## [15381] Turkey                    Turkey                   
## [15383] Turkey                    Turkey                   
## [15385] Turkey                    Turkey                   
## [15387] Turkey                    Turkey                   
## [15389] Turkey                    Turkey                   
## [15391] Turkey                    Turkey                   
## [15393] Turkey                    Turkey                   
## [15395] Turkey                    Turkey                   
## [15397] Turkey                    Turkey                   
## [15399] Turkey                    Turks and Caicos Is.     
## [15401] Turks and Caicos Is.      Turks and Caicos Is.     
## [15403] Turks and Caicos Is.      Turks and Caicos Is.     
## [15405] Turks and Caicos Is.      Tuvalu                   
## [15407] Tuvalu                    Tuvalu                   
## [15409] Tuvalu                    Tuvalu                   
## [15411] Tuvalu                    Tuvalu                   
## [15413] Tuvalu                    Tuvalu                   
## [15415] Tuvalu                    US Virgin Islands        
## [15417] US Virgin Islands         US Virgin Islands        
## [15419] US Virgin Islands         US Virgin Islands        
## [15421] US Virgin Islands         US Virgin Islands        
## [15423] US Virgin Islands         US Virgin Islands        
## [15425] US Virgin Islands         US Virgin Islands        
## [15427] US Virgin Islands         US Virgin Islands        
## [15429] US Virgin Islands         US Virgin Islands        
## [15431] US Virgin Islands         US Virgin Islands        
## [15433] US Virgin Islands         US Virgin Islands        
## [15435] US Virgin Islands         US Virgin Islands        
## [15437] US Virgin Islands         US Virgin Islands        
## [15439] US Virgin Islands         US Virgin Islands        
## [15441] US Virgin Islands         US Virgin Islands        
## [15443] US Virgin Islands         US Virgin Islands        
## [15445] Ukraine                   Ukraine                  
## [15447] Ukraine                   Ukraine                  
## [15449] Ukraine                   Ukraine                  
## [15451] Ukraine                   Ukraine                  
## [15453] Ukraine                   Ukraine                  
## [15455] Ukraine                   Ukraine                  
## [15457] Ukraine                   Ukraine                  
## [15459] Ukraine                   Ukraine                  
## [15461] Ukraine                   Ukraine                  
## [15463] Ukraine                   Ukraine                  
## [15465] Ukraine                   Ukraine                  
## [15467] Ukraine                   Ukraine                  
## [15469] Ukraine                   Ukraine                  
## [15471] Ukraine                   Ukraine                  
## [15473] Ukraine                   Ukraine                  
## [15475] Ukraine                   Ukraine                  
## [15477] Ukraine                   Ukraine                  
## [15479] Ukraine                   Ukraine                  
## [15481] Ukraine                   Ukraine                  
## [15483] Ukraine                   Ukraine                  
## [15485] Ukraine                   Ukraine                  
## [15487] Ukraine                   Ukraine                  
## [15489] Ukraine                   Ukraine                  
## [15491] Ukraine                   Ukraine                  
## [15493] Ukraine                   Ukraine                  
## [15495] Ukraine                   Ukraine                  
## [15497] Ukraine                   Ukraine                  
## [15499] Ukraine                   Ukraine                  
## [15501] Ukraine                   Ukraine                  
## [15503] Ukraine                   Ukraine                  
## [15505] Ukraine                   Ukraine                  
## [15507] Ukraine                   Ukraine                  
## [15509] Ukraine                   Ukraine                  
## [15511] Ukraine                   Ukraine                  
## [15513] Ukraine                   Ukraine                  
## [15515] Ukraine                   Ukraine                  
## [15517] Ukraine                   Ukraine                  
## [15519] Ukraine                   Ukraine                  
## [15521] Ukraine                   Ukraine                  
## [15523] Ukraine                   Ukraine                  
## [15525] Ukraine                   Ukraine                  
## [15527] Ukraine                   Ukraine                  
## [15529] Ukraine                   Ukraine                  
## [15531] Ukraine                   Ukraine                  
## [15533] Ukraine                   Ukraine                  
## [15535] Ukraine                   Ukraine                  
## [15537] Ukraine                   Ukraine                  
## [15539] Ukraine                   Ukraine                  
## [15541] Ukraine                   Ukraine                  
## [15543] Ukraine                   Ukraine                  
## [15545] Ukraine                   Ukraine                  
## [15547] Ukraine                   Ukraine                  
## [15549] Ukraine                   Ukraine                  
## [15551] Ukraine                   Ukraine                  
## [15553] Ukraine                   Ukraine                  
## [15555] Ukraine                   Ukraine                  
## [15557] Ukraine                   Ukraine                  
## [15559] Ukraine                   Ukraine                  
## [15561] Ukraine                   Ukraine                  
## [15563] Ukraine                   Ukraine                  
## [15565] Ukraine                   Ukraine                  
## [15567] Ukraine                   Ukraine                  
## [15569] Ukraine                   Ukraine                  
## [15571] Ukraine                   Ukraine                  
## [15573] Ukraine                   Ukraine                  
## [15575] Ukraine                   Ukraine                  
## [15577] Ukraine                   Ukraine                  
## [15579] Ukraine                   Ukraine                  
## [15581] Ukraine                   Ukraine                  
## [15583] Ukraine                   Ukraine                  
## [15585] Ukraine                   Ukraine                  
## [15587] Ukraine                   Ukraine                  
## [15589] Ukraine                   Ukraine                  
## [15591] Ukraine                   Ukraine                  
## [15593] Ukraine                   Ukraine                  
## [15595] Ukraine                   Ukraine                  
## [15597] Ukraine                   Ukraine                  
## [15599] Ukraine                   Ukraine                  
## [15601] Ukraine                   Ukraine                  
## [15603] Ukraine                   Ukraine                  
## [15605] Ukraine                   Ukraine                  
## [15607] Ukraine                   Ukraine                  
## [15609] Ukraine                   Ukraine                  
## [15611] Ukraine                   Ukraine                  
## [15613] Ukraine                   Ukraine                  
## [15615] Ukraine                   Ukraine                  
## [15617] Ukraine                   Ukraine                  
## [15619] Ukraine                   Ukraine                  
## [15621] Ukraine                   Ukraine                  
## [15623] Ukraine                   Ukraine                  
## [15625] Ukraine                   Ukraine                  
## [15627] Ukraine                   Ukraine                  
## [15629] Ukraine                   Ukraine                  
## [15631] Ukraine                   Ukraine                  
## [15633] Ukraine                   Ukraine                  
## [15635] Ukraine                   Ukraine                  
## [15637] Ukraine                   Ukraine                  
## [15639] Ukraine                   Ukraine                  
## [15641] Ukraine                   Ukraine                  
## [15643] Ukraine                   Ukraine                  
## [15645] Ukraine                   Ukraine                  
## [15647] Ukraine                   Ukraine                  
## [15649] Ukraine                   Ukraine                  
## [15651] Ukraine                   Ukraine                  
## [15653] Ukraine                   Ukraine                  
## [15655] Ukraine                   Ukraine                  
## [15657] Ukraine                   Ukraine                  
## [15659] Ukraine                   Ukraine                  
## [15661] Ukraine                   Ukraine                  
## [15663] Ukraine                   Ukraine                  
## [15665] Ukraine                   Ukraine                  
## [15667] Ukraine                   Ukraine                  
## [15669] Ukraine                   Ukraine                  
## [15671] Ukraine                   Ukraine                  
## [15673] Ukraine                   Ukraine                  
## [15675] Ukraine                   Ukraine                  
## [15677] Ukraine                   Ukraine                  
## [15679] Ukraine                   Ukraine                  
## [15681] Ukraine                   Ukraine                  
## [15683] Ukraine                   Ukraine                  
## [15685] Ukraine                   Ukraine                  
## [15687] Ukraine                   Ukraine                  
## [15689] Ukraine                   Ukraine                  
## [15691] Ukraine                   Ukraine                  
## [15693] Ukraine                   Ukraine                  
## [15695] Ukraine                   Ukraine                  
## [15697] Ukraine                   Ukraine                  
## [15699] Ukraine                   Ukraine                  
## [15701] Ukraine                   Ukraine                  
## [15703] Ukraine                   Ukraine                  
## [15705] Ukraine                   Ukraine                  
## [15707] Ukraine                   Ukraine                  
## [15709] Ukraine                   Ukraine                  
## [15711] Ukraine                   Ukraine                  
## [15713] Ukraine                   Ukraine                  
## [15715] Ukraine                   Ukraine                  
## [15717] Ukraine                   Ukraine                  
## [15719] Ukraine                   Ukraine                  
## [15721] Ukraine                   Ukraine                  
## [15723] Ukraine                   Ukraine                  
## [15725] Ukraine                   Ukraine                  
## [15727] Ukraine                   Ukraine                  
## [15729] Ukraine                   Ukraine                  
## [15731] Ukraine                   Ukraine                  
## [15733] Ukraine                   Ukraine                  
## [15735] Ukraine                   Ukraine                  
## [15737] Ukraine                   Ukraine                  
## [15739] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15741] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15743] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15745] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15747] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15749] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15751] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15753] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15755] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15757] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15759] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15761] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15763] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15765] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15767] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15769] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15771] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15773] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15775] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15777] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15779] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15781] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15783] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15785] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15787] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15789] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15791] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15793] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15795] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15797] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15799] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15801] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15803] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15805] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15807] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15809] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15811] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15813] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15815] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15817] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15819] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15821] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15823] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15825] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15827] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15829] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15831] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15833] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15835] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15837] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15839] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15841] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15843] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15845] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15847] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15849] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15851] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15853] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15855] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15857] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15859] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15861] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15863] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15865] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15867] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15869] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15871] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15873] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15875] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15877] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15879] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15881] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15883] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15885] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15887] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15889] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15891] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15893] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15895] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15897] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15899] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15901] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15903] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15905] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15907] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15909] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15911] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15913] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15915] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15917] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15919] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15921] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15923] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15925] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15927] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15929] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15931] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15933] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15935] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15937] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15939] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15941] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15943] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15945] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15947] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15949] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15951] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15953] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15955] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15957] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15959] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15961] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15963] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15965] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15967] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15969] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15971] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15973] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15975] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15977] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15979] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15981] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15983] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15985] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15987] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15989] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15991] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15993] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15995] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15997] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [15999] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16001] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16003] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16005] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16007] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16009] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16011] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16013] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16015] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16017] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16019] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16021] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16023] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16025] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16027] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16029] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16031] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16033] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16035] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16037] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16039] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16041] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16043] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16045] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16047] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16049] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16051] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16053] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16055] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16057] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16059] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16061] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16063] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16065] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16067] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16069] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16071] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16073] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16075] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16077] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16079] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16081] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16083] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16085] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16087] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16089] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16091] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16093] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16095] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16097] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16099] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16101] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16103] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16105] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16107] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16109] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16111] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16113] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16115] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16117] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16119] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16121] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16123] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16125] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16127] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16129] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16131] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16133] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16135] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16137] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16139] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16141] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16143] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16145] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16147] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16149] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16151] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16153] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16155] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16157] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16159] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16161] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16163] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16165] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16167] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16169] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16171] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16173] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16175] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16177] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16179] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16181] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16183] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16185] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16187] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16189] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16191] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16193] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16195] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16197] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16199] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16201] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16203] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16205] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16207] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16209] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16211] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16213] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16215] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16217] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16219] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16221] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16223] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16225] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16227] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16229] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16231] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16233] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16235] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16237] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16239] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16241] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16243] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16245] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16247] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16249] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16251] Un. Sov. Soc. Rep.        Un. Sov. Soc. Rep.       
## [16253] Un. Sov. Soc. Rep.        United Arab Emirates     
## [16255] United Arab Emirates      United Arab Emirates     
## [16257] United Arab Emirates      United Arab Emirates     
## [16259] United Arab Emirates      United Arab Emirates     
## [16261] United Arab Emirates      United Arab Emirates     
## [16263] United Arab Emirates      United Arab Emirates     
## [16265] United Arab Emirates      United Arab Emirates     
## [16267] United Arab Emirates      United Arab Emirates     
## [16269] United Arab Emirates      United Arab Emirates     
## [16271] United Arab Emirates      United Arab Emirates     
## [16273] United Arab Emirates      United Arab Emirates     
## [16275] United Arab Emirates      United Arab Emirates     
## [16277] United Arab Emirates      United Arab Emirates     
## [16279] United Arab Emirates      United Arab Emirates     
## [16281] United Arab Emirates      United Arab Emirates     
## [16283] United Arab Emirates      United Arab Emirates     
## [16285] United Arab Emirates      United Arab Emirates     
## [16287] United Arab Emirates      United Arab Emirates     
## [16289] United Arab Emirates      United Arab Emirates     
## [16291] United Arab Emirates      United Arab Emirates     
## [16293] United Arab Emirates      United Arab Emirates     
## [16295] United Arab Emirates      United Arab Emirates     
## [16297] United Arab Emirates      United Arab Emirates     
## [16299] United Arab Emirates      United Arab Emirates     
## [16301] United Arab Emirates      United Arab Emirates     
## [16303] United Arab Emirates      United Arab Emirates     
## [16305] United Arab Emirates      United Kingdom           
## [16307] United Kingdom            United Kingdom           
## [16309] United Kingdom            United Kingdom           
## [16311] United Kingdom            United Kingdom           
## [16313] United Kingdom            United Kingdom           
## [16315] United Kingdom            United Kingdom           
## [16317] United Kingdom            United Kingdom           
## [16319] United Kingdom            United Kingdom           
## [16321] United Kingdom            United Kingdom           
## [16323] United Kingdom            United Kingdom           
## [16325] United Kingdom            United Kingdom           
## [16327] United Kingdom            United Kingdom           
## [16329] United Kingdom            United Kingdom           
## [16331] United Kingdom            United Kingdom           
## [16333] United Kingdom            United Kingdom           
## [16335] United Kingdom            United Kingdom           
## [16337] United Kingdom            United Kingdom           
## [16339] United Kingdom            United Kingdom           
## [16341] United Kingdom            United Kingdom           
## [16343] United Kingdom            United Kingdom           
## [16345] United Kingdom            United Kingdom           
## [16347] United Kingdom            United Kingdom           
## [16349] United Kingdom            United Kingdom           
## [16351] United Kingdom            United Kingdom           
## [16353] United Kingdom            United Kingdom           
## [16355] United Kingdom            United Kingdom           
## [16357] United Kingdom            United Kingdom           
## [16359] United Kingdom            United Kingdom           
## [16361] United Kingdom            United Kingdom           
## [16363] United Kingdom            United Kingdom           
## [16365] United Kingdom            United Kingdom           
## [16367] United Kingdom            United Kingdom           
## [16369] United Kingdom            United Kingdom           
## [16371] United Kingdom            United Kingdom           
## [16373] United Kingdom            United Kingdom           
## [16375] United Kingdom            United Kingdom           
## [16377] United Kingdom            United Kingdom           
## [16379] United Kingdom            United Kingdom           
## [16381] United Kingdom            United Kingdom           
## [16383] United Kingdom            United Kingdom           
## [16385] United Kingdom            United Kingdom           
## [16387] United Kingdom            United Kingdom           
## [16389] United Kingdom            United Kingdom           
## [16391] United Kingdom            United Kingdom           
## [16393] United Kingdom            United Kingdom           
## [16395] United Kingdom            United Kingdom           
## [16397] United Kingdom            United Kingdom           
## [16399] United Kingdom            United Kingdom           
## [16401] United Kingdom            United Kingdom           
## [16403] United Kingdom            United Kingdom           
## [16405] United Kingdom            United Kingdom           
## [16407] United Kingdom            United Kingdom           
## [16409] United Kingdom            United Kingdom           
## [16411] United Kingdom            United Kingdom           
## [16413] United Kingdom            United Kingdom           
## [16415] United Kingdom            United Kingdom           
## [16417] United Kingdom            United Kingdom           
## [16419] United Kingdom            United Kingdom           
## [16421] United Kingdom            United Kingdom           
## [16423] United Kingdom            United Kingdom           
## [16425] United Kingdom            United Kingdom           
## [16427] United Kingdom            United Kingdom           
## [16429] United Kingdom            United Kingdom           
## [16431] United Kingdom            United Kingdom           
## [16433] United Kingdom            United Kingdom           
## [16435] United Kingdom            United Kingdom           
## [16437] United Kingdom            United Kingdom           
## [16439] United Kingdom            United Kingdom           
## [16441] United Kingdom            United Kingdom           
## [16443] United Kingdom            United Kingdom           
## [16445] United Kingdom            United Kingdom           
## [16447] United Kingdom            United Kingdom           
## [16449] United Kingdom            United Kingdom           
## [16451] United Kingdom            United Kingdom           
## [16453] United Kingdom            United Kingdom           
## [16455] United Kingdom            United Kingdom           
## [16457] United Kingdom            United Kingdom           
## [16459] United Kingdom            United Kingdom           
## [16461] United Kingdom            United Kingdom           
## [16463] United Kingdom            United Kingdom           
## [16465] United Kingdom            United Kingdom           
## [16467] United Kingdom            United Kingdom           
## [16469] United Kingdom            United Kingdom           
## [16471] United Kingdom            United Kingdom           
## [16473] United Kingdom            United Kingdom           
## [16475] United Kingdom            United Kingdom           
## [16477] United Kingdom            United Kingdom           
## [16479] United Kingdom            United Kingdom           
## [16481] United Kingdom            United Kingdom           
## [16483] United Kingdom            United Kingdom           
## [16485] United Kingdom            United Kingdom           
## [16487] United Kingdom            United Kingdom           
## [16489] United Kingdom            United Kingdom           
## [16491] United Kingdom            United Kingdom           
## [16493] United Kingdom            United Kingdom           
## [16495] United Kingdom            United Kingdom           
## [16497] United Kingdom            United Kingdom           
## [16499] United Kingdom            United Kingdom           
## [16501] United Kingdom            United Kingdom           
## [16503] United Kingdom            United Kingdom           
## [16505] United Kingdom            United Kingdom           
## [16507] United Kingdom            United Kingdom           
## [16509] United Kingdom            United Kingdom           
## [16511] United Kingdom            United Kingdom           
## [16513] United Kingdom            United Kingdom           
## [16515] United Kingdom            United Kingdom           
## [16517] United Kingdom            United Kingdom           
## [16519] United Kingdom            United Kingdom           
## [16521] United Kingdom            United Kingdom           
## [16523] United Kingdom            United Kingdom           
## [16525] United Kingdom            United Kingdom           
## [16527] United Kingdom            United Kingdom           
## [16529] United Kingdom            United Kingdom           
## [16531] United Kingdom            United Kingdom           
## [16533] United Kingdom            United Kingdom           
## [16535] United Kingdom            United Kingdom           
## [16537] United Kingdom            United Kingdom           
## [16539] United Kingdom            United Kingdom           
## [16541] United Kingdom            United Kingdom           
## [16543] United Kingdom            United Kingdom           
## [16545] United Kingdom            United Kingdom           
## [16547] United Kingdom            United Kingdom           
## [16549] United Kingdom            United Kingdom           
## [16551] United Kingdom            United Kingdom           
## [16553] United Kingdom            United Kingdom           
## [16555] United Kingdom            United Kingdom           
## [16557] United Kingdom            United Kingdom           
## [16559] United Kingdom            United Kingdom           
## [16561] United Kingdom            United Kingdom           
## [16563] United Kingdom            United Kingdom           
## [16565] United Kingdom            United Kingdom           
## [16567] United Kingdom            United Kingdom           
## [16569] United Kingdom            United Kingdom           
## [16571] United Kingdom            United Kingdom           
## [16573] United Kingdom            United Kingdom           
## [16575] United Kingdom            United Kingdom           
## [16577] United Kingdom            United Kingdom           
## [16579] United Kingdom            United Kingdom           
## [16581] United Kingdom            United Kingdom           
## [16583] United Kingdom            United Kingdom           
## [16585] United Kingdom            United Kingdom           
## [16587] United Kingdom            United Kingdom           
## [16589] United Kingdom            United Kingdom           
## [16591] United Kingdom            United Kingdom           
## [16593] United Kingdom            United Kingdom           
## [16595] United Kingdom            United Kingdom           
## [16597] United Kingdom            United Kingdom           
## [16599] United Kingdom            United Kingdom           
## [16601] United Kingdom            United Kingdom           
## [16603] United Kingdom            United Kingdom           
## [16605] United Kingdom            United Kingdom           
## [16607] United Kingdom            United Kingdom           
## [16609] United Kingdom            United Kingdom           
## [16611] United Kingdom            United Kingdom           
## [16613] United Kingdom            United Kingdom           
## [16615] United Kingdom            United Kingdom           
## [16617] United Kingdom            United Kingdom           
## [16619] United Kingdom            United Kingdom           
## [16621] United Kingdom            United Kingdom           
## [16623] United Kingdom            United Kingdom           
## [16625] United Kingdom            United Kingdom           
## [16627] United Kingdom            United Kingdom           
## [16629] United Kingdom            United Kingdom           
## [16631] United Kingdom            United Kingdom           
## [16633] United Kingdom            United Kingdom           
## [16635] United Kingdom            United Kingdom           
## [16637] United Kingdom            United Kingdom           
## [16639] United Kingdom            United Kingdom           
## [16641] United Kingdom            United Kingdom           
## [16643] United Kingdom            United Kingdom           
## [16645] United Kingdom            United Kingdom           
## [16647] United Kingdom            United Kingdom           
## [16649] United Kingdom            United Kingdom           
## [16651] United Kingdom            United Kingdom           
## [16653] United Kingdom            United Kingdom           
## [16655] United Kingdom            United Kingdom           
## [16657] United Kingdom            United Kingdom           
## [16659] United Kingdom            United Kingdom           
## [16661] United Kingdom            United Kingdom           
## [16663] United Kingdom            United Kingdom           
## [16665] United Kingdom            United Kingdom           
## [16667] United Kingdom            United States of America 
## [16669] United States of America  United States of America 
## [16671] United States of America  United States of America 
## [16673] United States of America  United States of America 
## [16675] United States of America  United States of America 
## [16677] United States of America  United States of America 
## [16679] United States of America  United States of America 
## [16681] United States of America  United States of America 
## [16683] United States of America  United States of America 
## [16685] United States of America  United States of America 
## [16687] United States of America  United States of America 
## [16689] United States of America  United States of America 
## [16691] United States of America  United States of America 
## [16693] United States of America  United States of America 
## [16695] United States of America  United States of America 
## [16697] United States of America  United States of America 
## [16699] United States of America  United States of America 
## [16701] United States of America  United States of America 
## [16703] United States of America  United States of America 
## [16705] United States of America  United States of America 
## [16707] United States of America  United States of America 
## [16709] United States of America  United States of America 
## [16711] United States of America  United States of America 
## [16713] United States of America  United States of America 
## [16715] United States of America  United States of America 
## [16717] United States of America  United States of America 
## [16719] United States of America  United States of America 
## [16721] United States of America  United States of America 
## [16723] United States of America  United States of America 
## [16725] United States of America  United States of America 
## [16727] United States of America  United States of America 
## [16729] United States of America  United States of America 
## [16731] United States of America  United States of America 
## [16733] United States of America  United States of America 
## [16735] United States of America  United States of America 
## [16737] United States of America  United States of America 
## [16739] United States of America  United States of America 
## [16741] United States of America  United States of America 
## [16743] United States of America  United States of America 
## [16745] United States of America  United States of America 
## [16747] United States of America  United States of America 
## [16749] United States of America  United States of America 
## [16751] United States of America  United States of America 
## [16753] United States of America  United States of America 
## [16755] United States of America  United States of America 
## [16757] United States of America  United States of America 
## [16759] United States of America  United States of America 
## [16761] United States of America  United States of America 
## [16763] United States of America  United States of America 
## [16765] United States of America  United States of America 
## [16767] United States of America  United States of America 
## [16769] United States of America  United States of America 
## [16771] United States of America  United States of America 
## [16773] United States of America  United States of America 
## [16775] United States of America  United States of America 
## [16777] United States of America  United States of America 
## [16779] United States of America  United States of America 
## [16781] United States of America  United States of America 
## [16783] United States of America  United States of America 
## [16785] United States of America  United States of America 
## [16787] United States of America  United States of America 
## [16789] United States of America  United States of America 
## [16791] United States of America  United States of America 
## [16793] United States of America  United States of America 
## [16795] United States of America  United States of America 
## [16797] United States of America  United States of America 
## [16799] United States of America  United States of America 
## [16801] United States of America  United States of America 
## [16803] United States of America  United States of America 
## [16805] United States of America  United States of America 
## [16807] United States of America  United States of America 
## [16809] United States of America  United States of America 
## [16811] United States of America  United States of America 
## [16813] United States of America  United States of America 
## [16815] United States of America  United States of America 
## [16817] United States of America  United States of America 
## [16819] United States of America  United States of America 
## [16821] United States of America  United States of America 
## [16823] United States of America  United States of America 
## [16825] United States of America  United States of America 
## [16827] United States of America  United States of America 
## [16829] United States of America  United States of America 
## [16831] United States of America  United States of America 
## [16833] United States of America  United States of America 
## [16835] United States of America  United States of America 
## [16837] United States of America  United States of America 
## [16839] United States of America  United States of America 
## [16841] United States of America  United States of America 
## [16843] United States of America  United States of America 
## [16845] United States of America  United States of America 
## [16847] United States of America  United States of America 
## [16849] United States of America  United States of America 
## [16851] United States of America  United States of America 
## [16853] United States of America  United States of America 
## [16855] United States of America  United States of America 
## [16857] United States of America  United States of America 
## [16859] United States of America  United States of America 
## [16861] United States of America  United States of America 
## [16863] United States of America  United States of America 
## [16865] United States of America  United States of America 
## [16867] United States of America  United States of America 
## [16869] United States of America  United States of America 
## [16871] United States of America  United States of America 
## [16873] United States of America  United States of America 
## [16875] United States of America  United States of America 
## [16877] United States of America  United States of America 
## [16879] United States of America  United States of America 
## [16881] United States of America  United States of America 
## [16883] United States of America  United States of America 
## [16885] United States of America  United States of America 
## [16887] United States of America  United States of America 
## [16889] United States of America  United States of America 
## [16891] United States of America  United States of America 
## [16893] United States of America  United States of America 
## [16895] United States of America  United States of America 
## [16897] United States of America  United States of America 
## [16899] United States of America  United States of America 
## [16901] United States of America  United States of America 
## [16903] United States of America  United States of America 
## [16905] United States of America  United States of America 
## [16907] United States of America  United States of America 
## [16909] United States of America  United States of America 
## [16911] United States of America  United States of America 
## [16913] United States of America  United States of America 
## [16915] United States of America  United States of America 
## [16917] United States of America  United States of America 
## [16919] United States of America  United States of America 
## [16921] United States of America  United States of America 
## [16923] United States of America  United States of America 
## [16925] United States of America  United States of America 
## [16927] United States of America  United States of America 
## [16929] United States of America  United States of America 
## [16931] United States of America  United States of America 
## [16933] United States of America  United States of America 
## [16935] United States of America  United States of America 
## [16937] United States of America  United States of America 
## [16939] United States of America  United States of America 
## [16941] United States of America  United States of America 
## [16943] United States of America  United States of America 
## [16945] United States of America  United States of America 
## [16947] United States of America  United States of America 
## [16949] United States of America  United States of America 
## [16951] United States of America  United States of America 
## [16953] United States of America  United States of America 
## [16955] United States of America  United States of America 
## [16957] United States of America  United States of America 
## [16959] United States of America  United States of America 
## [16961] United States of America  United States of America 
## [16963] United States of America  United States of America 
## [16965] United States of America  United States of America 
## [16967] United States of America  United States of America 
## [16969] United States of America  United States of America 
## [16971] United States of America  United States of America 
## [16973] United States of America  United States of America 
## [16975] United States of America  United States of America 
## [16977] United States of America  United States of America 
## [16979] United States of America  United States of America 
## [16981] United States of America  United States of America 
## [16983] United States of America  United States of America 
## [16985] United States of America  United States of America 
## [16987] United States of America  United States of America 
## [16989] United States of America  United States of America 
## [16991] United States of America  United States of America 
## [16993] United States of America  United States of America 
## [16995] United States of America  United States of America 
## [16997] United States of America  United States of America 
## [16999] United States of America  United States of America 
## [17001] United States of America  United States of America 
## [17003] United States of America  United States of America 
## [17005] United States of America  United States of America 
## [17007] United States of America  United States of America 
## [17009] United States of America  United States of America 
## [17011] United States of America  United States of America 
## [17013] United States of America  United States of America 
## [17015] United States of America  United States of America 
## [17017] United States of America  United States of America 
## [17019] United States of America  United States of America 
## [17021] United States of America  United States of America 
## [17023] United States of America  United States of America 
## [17025] United States of America  United States of America 
## [17027] United States of America  United States of America 
## [17029] United States of America  United States of America 
## [17031] United States of America  United States of America 
## [17033] United States of America  United States of America 
## [17035] United States of America  United States of America 
## [17037] United States of America  United States of America 
## [17039] United States of America  United States of America 
## [17041] United States of America  United States of America 
## [17043] United States of America  United States of America 
## [17045] United States of America  United States of America 
## [17047] United States of America  United States of America 
## [17049] United States of America  United States of America 
## [17051] United States of America  United States of America 
## [17053] United States of America  United States of America 
## [17055] United States of America  United States of America 
## [17057] United States of America  United States of America 
## [17059] United States of America  United States of America 
## [17061] United States of America  United States of America 
## [17063] United States of America  United States of America 
## [17065] United States of America  United States of America 
## [17067] United States of America  United States of America 
## [17069] United States of America  United States of America 
## [17071] United States of America  United States of America 
## [17073] United States of America  United States of America 
## [17075] United States of America  United States of America 
## [17077] United States of America  United States of America 
## [17079] United States of America  United States of America 
## [17081] United States of America  United States of America 
## [17083] United States of America  United States of America 
## [17085] United States of America  United States of America 
## [17087] United States of America  United States of America 
## [17089] United States of America  United States of America 
## [17091] United States of America  United States of America 
## [17093] United States of America  United States of America 
## [17095] United States of America  United States of America 
## [17097] United States of America  United States of America 
## [17099] United States of America  United States of America 
## [17101] United States of America  United States of America 
## [17103] United States of America  United States of America 
## [17105] United States of America  United States of America 
## [17107] United States of America  United States of America 
## [17109] United States of America  United States of America 
## [17111] United States of America  United States of America 
## [17113] United States of America  United States of America 
## [17115] United States of America  United States of America 
## [17117] United States of America  United States of America 
## [17119] United States of America  United States of America 
## [17121] United States of America  United States of America 
## [17123] United States of America  United States of America 
## [17125] United States of America  United States of America 
## [17127] United States of America  United States of America 
## [17129] United States of America  United States of America 
## [17131] United States of America  United States of America 
## [17133] United States of America  United States of America 
## [17135] United States of America  United States of America 
## [17137] United States of America  United States of America 
## [17139] United States of America  United States of America 
## [17141] United States of America  United States of America 
## [17143] United States of America  United States of America 
## [17145] United States of America  United States of America 
## [17147] United States of America  United States of America 
## [17149] United States of America  United States of America 
## [17151] United States of America  United States of America 
## [17153] United States of America  United States of America 
## [17155] United States of America  United States of America 
## [17157] United States of America  United States of America 
## [17159] United States of America  United States of America 
## [17161] United States of America  United States of America 
## [17163] United States of America  United States of America 
## [17165] United States of America  United States of America 
## [17167] United States of America  United States of America 
## [17169] United States of America  United States of America 
## [17171] United States of America  United States of America 
## [17173] United States of America  United States of America 
## [17175] United States of America  United States of America 
## [17177] United States of America  United States of America 
## [17179] United States of America  United States of America 
## [17181] United States of America  United States of America 
## [17183] United States of America  United States of America 
## [17185] United States of America  United States of America 
## [17187] United States of America  United States of America 
## [17189] United States of America  United States of America 
## [17191] United States of America  United States of America 
## [17193] United States of America  United States of America 
## [17195] United States of America  United States of America 
## [17197] United States of America  United States of America 
## [17199] United States of America  United States of America 
## [17201] United States of America  United States of America 
## [17203] United States of America  United States of America 
## [17205] United States of America  United States of America 
## [17207] United States of America  United States of America 
## [17209] United States of America  United States of America 
## [17211] United States of America  United States of America 
## [17213] United States of America  United States of America 
## [17215] United States of America  United States of America 
## [17217] United States of America  United States of America 
## [17219] United States of America  United States of America 
## [17221] United States of America  United States of America 
## [17223] United States of America  United States of America 
## [17225] United States of America  United States of America 
## [17227] United States of America  United States of America 
## [17229] United States of America  United States of America 
## [17231] United States of America  United States of America 
## [17233] United States of America  United States of America 
## [17235] United States of America  United States of America 
## [17237] United States of America  United States of America 
## [17239] United States of America  United States of America 
## [17241] United States of America  United States of America 
## [17243] United States of America  United States of America 
## [17245] United States of America  United States of America 
## [17247] United States of America  United States of America 
## [17249] United States of America  United States of America 
## [17251] United States of America  United States of America 
## [17253] United States of America  United States of America 
## [17255] United States of America  United States of America 
## [17257] United States of America  United States of America 
## [17259] United States of America  United States of America 
## [17261] United States of America  United States of America 
## [17263] United States of America  United States of America 
## [17265] United States of America  United States of America 
## [17267] United States of America  United States of America 
## [17269] United States of America  United States of America 
## [17271] United States of America  United States of America 
## [17273] United States of America  United States of America 
## [17275] United States of America  United States of America 
## [17277] United States of America  United States of America 
## [17279] United States of America  United States of America 
## [17281] United States of America  United States of America 
## [17283] United States of America  United States of America 
## [17285] United States of America  United States of America 
## [17287] United States of America  United States of America 
## [17289] United States of America  United States of America 
## [17291] United States of America  United States of America 
## [17293] United States of America  United States of America 
## [17295] Uruguay                   Uruguay                  
## [17297] Uruguay                   Uruguay                  
## [17299] Uruguay                   Uruguay                  
## [17301] Uruguay                   Uruguay                  
## [17303] Uruguay                   Uruguay                  
## [17305] Uruguay                   Uruguay                  
## [17307] Uruguay                   Uruguay                  
## [17309] Uruguay                   Uruguay                  
## [17311] Uruguay                   Uruguay                  
## [17313] Uruguay                   Uruguay                  
## [17315] Uruguay                   Uruguay                  
## [17317] Uruguay                   Uruguay                  
## [17319] Uruguay                   Uruguay                  
## [17321] Uruguay                   Uruguay                  
## [17323] Uruguay                   Uruguay                  
## [17325] Uruguay                   Uruguay                  
## [17327] Uruguay                   Uruguay                  
## [17329] Uruguay                   Uruguay                  
## [17331] Uruguay                   Uruguay                  
## [17333] Uruguay                   Uruguay                  
## [17335] Uruguay                   Uruguay                  
## [17337] Uruguay                   Uruguay                  
## [17339] Uruguay                   Uruguay                  
## [17341] Uruguay                   Uruguay                  
## [17343] Uruguay                   Uruguay                  
## [17345] Uruguay                   Uruguay                  
## [17347] Uruguay                   Uruguay                  
## [17349] Uruguay                   Uruguay                  
## [17351] Uruguay                   Uruguay                  
## [17353] Uruguay                   Uruguay                  
## [17355] Uruguay                   Uruguay                  
## [17357] Uruguay                   Uruguay                  
## [17359] Uruguay                   Uruguay                  
## [17361] Uruguay                   Uruguay                  
## [17363] Uruguay                   Uruguay                  
## [17365] Uruguay                   Uruguay                  
## [17367] Uruguay                   Uruguay                  
## [17369] Uruguay                   Uruguay                  
## [17371] Uruguay                   Uruguay                  
## [17373] Uruguay                   Uruguay                  
## [17375] Uruguay                   Uruguay                  
## [17377] Uruguay                   Uruguay                  
## [17379] Uruguay                   Uruguay                  
## [17381] Uruguay                   Uruguay                  
## [17383] Uruguay                   Uruguay                  
## [17385] Uruguay                   Uruguay                  
## [17387] Uruguay                   Uruguay                  
## [17389] Uruguay                   Uruguay                  
## [17391] Uruguay                   Uruguay                  
## [17393] Uruguay                   Uruguay                  
## [17395] Uruguay                   Uruguay                  
## [17397] Uruguay                   Uruguay                  
## [17399] Uruguay                   Uruguay                  
## [17401] Uruguay                   Uruguay                  
## [17403] Uruguay                   Uruguay                  
## [17405] Uruguay                   Uruguay                  
## [17407] Uruguay                   Uruguay                  
## [17409] Uruguay                   Uruguay                  
## [17411] Uruguay                   Uruguay                  
## [17413] Uruguay                   Uruguay                  
## [17415] Uruguay                   Uruguay                  
## [17417] Uruguay                   Uruguay                  
## [17419] Uruguay                   Uruguay                  
## [17421] Uruguay                   Uruguay                  
## [17423] Uruguay                   Uruguay                  
## [17425] Uruguay                   Vanuatu                  
## [17427] Vanuatu                   Vanuatu                  
## [17429] Vanuatu                   Vanuatu                  
## [17431] Vanuatu                   Vanuatu                  
## [17433] Vanuatu                   Vanuatu                  
## [17435] Vanuatu                   Vanuatu                  
## [17437] Vanuatu                   Vanuatu                  
## [17439] Vanuatu                   Vanuatu                  
## [17441] Vanuatu                   Vanuatu                  
## [17443] Vanuatu                   Vanuatu                  
## [17445] Vanuatu                   Vanuatu                  
## [17447] Vanuatu                   Vanuatu                  
## [17449] Vanuatu                   Vanuatu                  
## [17451] Vanuatu                   Vanuatu                  
## [17453] Vanuatu                   Vanuatu                  
## [17455] Vanuatu                   Vanuatu                  
## [17457] Vanuatu                   Vanuatu                  
## [17459] Vanuatu                   Vanuatu                  
## [17461] Vanuatu                   Vanuatu                  
## [17463] Vanuatu                   Vanuatu                  
## [17465] Vanuatu                   Vanuatu                  
## [17467] Vanuatu                   Vanuatu                  
## [17469] Vanuatu                   Vanuatu                  
## [17471] Vanuatu                   Vanuatu                  
## [17473] Vanuatu                   Vanuatu                  
## [17475] Vanuatu                   Vanuatu                  
## [17477] Vanuatu                   Vanuatu                  
## [17479] Vanuatu                   Vanuatu                  
## [17481] Vanuatu                   Vanuatu                  
## [17483] Vanuatu                   Vanuatu                  
## [17485] Vanuatu                   Vanuatu                  
## [17487] Vanuatu                   Vanuatu                  
## [17489] Vanuatu                   Vanuatu                  
## [17491] Vanuatu                   Vanuatu                  
## [17493] Vanuatu                   Vanuatu                  
## [17495] Vanuatu                   Vanuatu                  
## [17497] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17499] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17501] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17503] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17505] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17507] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17509] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17511] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17513] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17515] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17517] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17519] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17521] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17523] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17525] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17527] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17529] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17531] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17533] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17535] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17537] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17539] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17541] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17543] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17545] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17547] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17549] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17551] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17553] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17555] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17557] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17559] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17561] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17563] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17565] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17567] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17569] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17571] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17573] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17575] Venezuela, Boliv Rep of   Venezuela, Boliv Rep of  
## [17577] Viet Nam                  Viet Nam                 
## [17579] Viet Nam                  Viet Nam                 
## [17581] Viet Nam                  Viet Nam                 
## [17583] Viet Nam                  Viet Nam                 
## [17585] Viet Nam                  Viet Nam                 
## [17587] Viet Nam                  Viet Nam                 
## [17589] Viet Nam                  Viet Nam                 
## [17591] Wallis and Futuna Is.     Wallis and Futuna Is.    
## [17593] Wallis and Futuna Is.     Wallis and Futuna Is.    
## [17595] Wallis and Futuna Is.     Western Sahara           
## [17597] Western Sahara            Western Sahara           
## [17599] Yemen                     Yemen                    
## [17601] Yemen                     Yemen                    
## [17603] Yemen                     Yemen                    
## [17605] Yemen                     Yemen                    
## [17607] Yemen                     Yemen                    
## [17609] Yemen                     Yemen                    
## [17611] Yemen                     Yemen                    
## [17613] Yemen                     Yemen                    
## [17615] Yemen                     Yemen                    
## [17617] Yemen                     Yemen                    
## [17619] Yemen                     Yemen                    
## [17621] Yemen                     Yemen                    
## [17623] Yemen                     Yemen                    
## [17625] Yemen                     Yemen                    
## [17627] Yemen                     Yemen                    
## [17629] Yemen                     Yemen                    
## [17631] Yemen                     Yemen                    
## [17633] Yemen                     Yemen                    
## [17635] Yemen                     Yemen                    
## [17637] Yemen                     Yugoslavia SFR           
## [17639] Yugoslavia SFR            Yugoslavia SFR           
## [17641] Yugoslavia SFR            Yugoslavia SFR           
## [17643] Yugoslavia SFR            Yugoslavia SFR           
## [17645] Yugoslavia SFR            Yugoslavia SFR           
## [17647] Yugoslavia SFR            Yugoslavia SFR           
## [17649] Yugoslavia SFR            Yugoslavia SFR           
## [17651] Yugoslavia SFR            Yugoslavia SFR           
## [17653] Yugoslavia SFR            Yugoslavia SFR           
## [17655] Yugoslavia SFR            Yugoslavia SFR           
## [17657] Yugoslavia SFR            Yugoslavia SFR           
## [17659] Yugoslavia SFR            Yugoslavia SFR           
## [17661] Yugoslavia SFR            Yugoslavia SFR           
## [17663] Yugoslavia SFR            Yugoslavia SFR           
## [17665] Yugoslavia SFR            Yugoslavia SFR           
## [17667] Yugoslavia SFR            Yugoslavia SFR           
## [17669] Yugoslavia SFR            Yugoslavia SFR           
## [17671] Yugoslavia SFR            Yugoslavia SFR           
## [17673] Yugoslavia SFR            Zanzibar                 
## [17675] Zanzibar                  Zanzibar                 
## [17677] Zanzibar                  Zanzibar                 
## [17679] Zanzibar                  Zanzibar                 
## [17681] Zanzibar                  Zanzibar                 
## [17683] Zanzibar                  Zanzibar                 
## [17685] Zanzibar                  Zanzibar                 
## [17687] Zanzibar                  Zanzibar                 
## [17689] Zanzibar                  Zanzibar                 
## [17691] Zanzibar                  Zanzibar                 
## 204 Levels: Albania Algeria American Samoa Angola ... Zanzibar
```

```r
as.factor(fisheries$isscaap_group_number)
```

```
##     [1] 38 36 37 45 32 37 33 45 38 57 33 57 31 43 57 33 45 38 35 34 31 32 43 35
##    [25] 33 35 31 37 33 33 37 33 33 33 38 34 37 34 37 39 54 42 31 34 33 43 33 33
##    [49] 32 38 33 38 32 35 33 37 34 33 34 37 38 76 56 33 36 31 34 36 36 37 33 37
##    [73] 45 33 38 57 35 57 33 45 45 31 57 45 38 35 34 32 43 35 33 36 37 32 33 33
##    [97] 33 37 34 36 37 47 39 58 34 33 43 57 43 33 38 36 33 38 33 33 33 33 35 34
##   [121] 38 36 33 36 33 32 36 37 36 36 36 38 37 37 33 33 36 38 42 39 58 57 37 33
##   [145] 37 38 36 36 33 33 36 33 36 38 43 36 36 36 36 37 35 36 37 37 33 36 33 37
##   [169] 37 33 33 37 37 34 34 37 33 37 37 57 57 45 34 33 37 31 36 33 33 33 33 34
##   [193] 34 34 33 34 34 37 36 43 42 39 39 33 33 33 45 45 57 57 33 37 34 33 37 33
##   [217] 38 38 33 33 33 35 35 33 33 33 32 38 38 36 31 35 33 45 36 33 33 43 36 57
##   [241] 36 33 33 24 31 36 43 39 52 33 37 42 33 37 43 37 33 33 33 39 33 33 33 38
##   [265] 33 43 33 52 33 33 36 34 37 36 37 56 52 31 33 33 38 38 34 35 38 34 33 33
##   [289] 32 45 33 57 45 33 36 36 34 36 31 36 38 33 34 34 32 32 37 38 32 33 35 33
##   [313] 38 38 56 34 34 54 37 35 57 34 38 34 57 34 38 38 38 35 32 32 32 33 33 33
##   [337] 34 34 34 33 42 47 39 39 58 38 32 33 34 38 37 57 57 33 37 33 32 34 34 55
##   [361] 38 57 34 34 34 38 34 38 38 38 38 38 38 33 32 38 54 37 38 34 33 57 37 36
##   [385] 32 38 34 44 33 34 32 32 44 33 37 38 33 33 36 32 38 36 38 57 33 32 34 33
##   [409] 36 38 37 36 33 39 33 36 38 36 36 36 34 37 37 35 35 38 34 33 33 38 34 77
##   [433] 77 77 77 32 57 54 54 33 33 43 45 45 25 25 38 32 36 36 36 34 36 34 52 52
##   [457] 32 32 32 36 42 42 42 34 34 34 37 37 37 34 57 35 35 35 34 34 34 57 57 57
##   [481] 34 34 34 32 38 76 45 45 33 33 33 31 31 33 33 33 32 32 32 52 33 38 45 45
##   [505] 45 43 37 37 32 33 33 33 33 33 38 38 37 37 37 36 36 36 77 34 34 36 38 44
##   [529] 34 38 34 34 36 36 36 34 37 37 37 33 47 47 47 39 39 39 39 39 58 58 58 58
##   [553] 36 38 43 43 34 34 34 34 34 33 33 33 38 36 36 36 37 34 57 57 57 57 34 34
##   [577] 38 33 33 32 57 34 34 34 37 37 37 45 45 45 33 33 33 34 34 34 56 56 38 33
##   [601] 33 33 38 38 38 38 38 34 34 34 32 34 33 31 31 38 55 55 55 34 34 33 33 33
##   [625] 76 76 36 36 36 38 38 38 38 36 36 36 33 33 33 34 34 34 33 33 33 33 34 34
##   [649] 36 36 36 34 43 43 43 32 34 33 33 33 34 34 34 32 36 36 36 33 33 33 37 43
##   [673] 34 34 76 36 36 36 36 36 36 32 33 33 33 38 38 33 33 43 43 34 34 36 36 36
##   [697] 34 57 57 57 57 36 36 36 34 45 37 37 37 32 33 33 33 36 36 36 37 42 37 43
##   [721] 33 33 33 39 33 57 42 76 38 33 52 37 37 33 24 42 37 37 33 43 33 33 33 33
##   [745] 37 33 45 33 33 33 37 34 37 77 36 31 37 33 33 39 25 33 33 36 37 37 33 33
##   [769] 57 33 33 37 38 33 35 37 33 37 33 33 33 33 33 33 33 38 33 37 33 37 33 33
##   [793] 33 33 24 33 47 39 33 36 38 36 36 36 36 36 37 37 37 47 39 58 36 36 38 36
##   [817] 33 52 36 36 36 36 32 31 35 37 37 34 34 38 31 35 57 31 45 31 57 38 38 42
##   [841] 34 31 32 43 31 33 35 55 34 39 34 32 31 32 47 58 31 34 43 57 39 38 32 32
##   [865] 38 34 32 38 38 38 38 33 38 34 31 38 52 32 31 33 36 36 36 36 36 36 34 32
##   [889] 57 36 36 36 37 32 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 42 37 36
##   [913] 36 36 36 36 36 38 38 38 38 38 34 37 43 37 37 37 33 37 57 35 35 32 33 32
##   [937] 36 37 34 36 36 39 39 39 39 39 36 36 36 36 34 45 57 57 34 43 32 57 34 45
##   [961] 45 34 33 38 35 33 38 38 38 38 38 38 38 38 36 36 36 36 36 36 36 32 36 36
##   [985] 36 36 36 52 36 36 36 36 36 36 32 36 36 36 36 57 57 57 36 36 36 36 36 36
##  [1009] 36 36 36 36 37 33 37 36 37 33 36 37 36 33 36 38 33 33 35 37 37 35 37 37
##  [1033] 57 33 35 31 37 36 33 33 33 38 34 37 38 37 34 33 36 42 39 33 45 37 33 33
##  [1057] 36 33 38 33 35 37 33 38 33 38 36 33 33 36 33 43 36 36 36 33 33 24 33 36
##  [1081] 33 36 36 36 37 37 36 36 36 33 36 36 36 36 37 43 35 37 33 37 33 33 33 36
##  [1105] 37 39 36 37 33 33 38 36 36 36 33 36 38 33 43 36 36 56 36 36 36 36 33 39
##  [1129] 52 39 33 36 37 37 35 38 34 33 32 45 45 33 36 36 37 37 36 45 34 35 36 37
##  [1153] 37 33 31 37 38 36 33 33 33 34 36 36 37 38 37 33 32 33 33 35 35 37 43 38
##  [1177] 37 35 37 37 57 33 53 34 42 34 37 36 33 33 33 33 33 37 33 36 33 33 33 33
##  [1201] 34 36 36 37 42 47 39 58 36 33 33 38 57 37 33 32 37 45 33 37 33 38 33 33
##  [1225] 45 38 37 38 35 38 33 33 54 36 36 38 38 33 38 37 34 36 33 33 33 36 33 45
##  [1249] 42 33 33 36 33 38 34 56 33 34 43 36 36 33 33 36 37 33 36 36 39 36 36 36
##  [1273] 36 36 33 43 35 37 33 37 39 36 36 38 33 52 36 36 36 36 33 37 47 39 58 45
##  [1297] 34 35 37 33 24 37 31 33 32 57 36 36 36 37 32 32 31 35 35 37 37 37 37 37
##  [1321] 35 37 34 34 34 34 21 37 33 32 24 37 37 37 33 32 37 32 37 37 37 37 33 37
##  [1345] 37 37 37 35 35 31 31 38 34 33 33 33 33 57 57 21 33 34 36 35 35 31 32 35
##  [1369] 35 35 33 35 35 39 31 33 33 36 37 33 33 33 32 32 33 33 33 32 32 34 37 37
##  [1393] 37 34 44 34 33 33 34 34 33 37 36 57 34 34 47 47 47 39 39 39 39 39 39 39
##  [1417] 39 58 58 33 37 54 45 45 32 45 57 33 57 37 32 34 57 34 34 39 45 33 38 34
##  [1441] 24 33 33 38 32 33 38 32 37 34 34 35 35 35 33 34 33 33 52 32 38 32 37 34
##  [1465] 36 32 33 33 34 32 31 35 32 21 21 56 21 44 33 36 38 33 31 43 36 36 36 31
##  [1489] 57 57 57 34 33 32 36 31 36 36 36 36 36 36 37 34 36 36 36 39 58 57 43 37
##  [1513] 38 36 36 36 36 43 36 36 36 36 57 57 42 39 58 45 76 36 33 37 32 33 33 35
##  [1537] 37 33 34 33 57 33 33 33 34 31 33 42 39 58 45 33 38 33 35 33 38 33 33 33
##  [1561] 31 43 36 33 45 33 52 32 36 36 36 36 24 31 34 53 43 55 24 34 31 36 32 31
##  [1585] 35 37 34 42 23 37 56 32 36 36 36 36 36 36 54 38 56 37 23 23 23 56 23 42
##  [1609] 23 39 31 31 32 31 39 32 55 33 36 57 34 42 39 58 58 77 45 32 45 56 57 56
##  [1633] 57 32 53 56 31 35 34 45 39 52 38 38 23 38 42 23 23 38 38 32 32 34 32 23
##  [1657] 56 33 34 76 76 76 76 38 38 32 36 36 36 36 23 56 25 21 21 23 36 36 36 36
##  [1681] 32 52 32 31 31 34 36 36 36 36 31 39 45 36 36 34 32 35 37 37 33 38 54 38
##  [1705] 32 31 56 57 31 45 31 57 38 42 34 53 32 43 31 33 32 37 33 55 56 34 32 34
##  [1729] 31 32 42 39 58 31 33 43 38 32 38 33 32 55 38 34 32 31 33 38 38 38 42 33
##  [1753] 52 31 38 38 52 32 31 34 33 36 34 34 35 33 33 34 34 34 77 35 57 37 36 34
##  [1777] 34 34 32 38 44 37 33 37 34 44 53 32 37 45 54 45 33 76 56 37 54 54 37 56
##  [1801] 23 37 33 44 33 33 34 57 36 38 35 52 33 31 52 56 47 42 32 32 32 32 33 34
##  [1825] 77 43 57 44 56 34 34 42 47 39 39 39 39 39 58 42 32 32 33 33 57 57 34 35
##  [1849] 33 33 32 32 34 34 34 34 34 45 55 34 33 38 34 34 38 33 38 38 38 38 38 34
##  [1873] 55 34 33 76 38 36 38 33 34 44 35 34 32 32 32 32 32 44 37 76 36 36 56 32
##  [1897] 56 36 57 34 36 33 45 32 36 36 36 36 36 36 36 36 36 36 36 36 34 34 57 36
##  [1921] 36 36 36 36 36 36 36 36 36 32 36 36 36 36 36 36 36 36 36 36 36 36 36 36
##  [1945] 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 38 38 38 38 38 38 38 38
##  [1969] 38 38 38 38 42 34 57 42 37 37 37 37 33 33 33 37 57 57 57 34 24 35 35 33
##  [1993] 33 31 33 45 32 42 33 33 34 32 37 35 37 35 77 57 33 34 36 42 42 47 39 39
##  [2017] 39 39 39 39 39 39 39 39 39 58 36 36 36 36 36 36 36 36 33 45 45 38 38 38
##  [2041] 38 38 38 57 57 57 34 34 34 34 35 33 34 34 45 33 33 33 35 37 33 76 36 38
##  [2065] 38 38 38 38 38 38 38 38 38 38 38 38 38 38 34 33 37 36 36 36 36 33 33 36
##  [2089] 45 47 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 33 33 34
##  [2113] 36 36 36 36 36 36 36 57 57 57 57 33 33 36 36 36 36 36 36 36 36 36 36 36
##  [2137] 36 33 37 33 57 33 33 34 34 37 33 33 42 39 58 45 34 34 33 35 37 36 38 33
##  [2161] 35 33 35 33 34 31 43 36 57 47 39 58 45 37 36 36 36 36 33 43 56 56 35 35
##  [2185] 33 33 34 34 36 31 52 43 33 33 33 37 37 33 45 33 33 33 53 42 42 39 39 58
##  [2209] 58 33 33 33 33 33 45 45 57 35 45 36 35 32 45 33 38 33 33 36 36 36 36 38
##  [2233] 38 33 33 33 33 33 33 52 36 33 33 36 36 57 57 34 45 33 36 36 36 33 33 36
##  [2257] 35 37 36 36 36 37 37 37 35 35 37 33 31 36 32 37 36 37 36 33 34 36 39 39
##  [2281] 58 45 33 35 35 33 36 38 36 33 36 33 43 36 36 33 36 33 33 32 37 34 34 33
##  [2305] 33 33 33 37 34 39 39 35 38 38 33 31 31 33 37 33 36 37 37 34 33 36 37 33
##  [2329] 35 33 37 57 34 33 37 57 45 33 37 33 33 33 38 37 34 33 35 42 39 39 33 45
##  [2353] 38 33 38 35 33 35 33 34 36 33 31 33 33 31 43 36 33 24 36 36 36 36 36 34
##  [2377] 34 36 36 36 36 36 34 36 36 36 34 34 34 37 33 36 36 37 47 39 58 36 33 57
##  [2401] 34 34 36 76 38 38 38 36 36 36 36 36 34 34 33 34 36 36 36 36 36 36 34 36
##  [2425] 36 36 56 36 36 36 36 43 35 37 37 45 33 33 36 42 39 39 58 36 36 45 57 45
##  [2449] 45 45 38 38 36 38 38 38 36 36 33 33 36 52 36 36 43 36 36 57 36 36 45 36
##  [2473] 33 77 36 36 37 33 37 34 33 33 33 32 33 33 38 57 37 56 33 57 33 37 38 57
##  [2497] 33 31 43 33 57 45 38 76 35 37 34 53 31 32 43 35 33 35 57 31 32 36 32 37
##  [2521] 33 55 37 33 56 33 34 57 37 34 37 36 47 39 77 33 33 54 37 31 34 33 56 43
##  [2545] 33 33 38 38 33 33 34 35 33 33 33 33 55 37 34 33 34 37 56 38 42 47 34 33
##  [2569] 36 31 57 56 33 32 36 36 36 24 31 34 24 35 33 35 32 57 34 36 36 37 32 31
##  [2593] 35 37 34 36 36 35 36 36 32 36 36 36 42 36 37 37 42 36 36 32 37 37 43 33
##  [2617] 37 37 37 37 37 56 37 34 33 34 34 34 38 35 35 31 31 31 33 37 32 32 52 31
##  [2641] 39 33 33 33 33 33 32 34 37 37 37 34 33 33 34 34 36 36 57 37 37 53 42 47
##  [2665] 47 39 39 39 39 39 33 33 33 45 45 45 57 39 37 37 45 33 38 33 33 33 33 33
##  [2689] 38 38 33 32 37 35 32 35 35 34 36 32 38 38 38 38 33 32 36 36 36 34 33 33
##  [2713] 33 33 35 32 31 33 33 52 31 36 36 36 32 57 57 57 34 32 31 34 36 36 31 33
##  [2737] 36 36 36 36 36 39 36 52 36 36 33 36 36 33 37 36 36 33 33 33 33 33 33 37
##  [2761] 37 33 57 57 33 33 43 33 45 38 33 35 35 34 32 35 35 33 57 36 37 33 37 33
##  [2785] 33 34 32 37 37 37 34 34 36 33 47 39 39 33 43 34 33 57 57 34 33 43 33 37
##  [2809] 45 33 33 33 38 33 33 33 33 33 35 33 34 38 33 33 36 36 33 38 33 33 36 36
##  [2833] 36 36 57 33 33 33 34 36 36 33 36 36 37 36 36 37 34 33 36 33 37 36 33 33
##  [2857] 35 37 33 37 35 34 33 57 36 38 34 38 37 34 37 33 36 37 35 42 47 39 58 33
##  [2881] 37 57 33 45 33 38 38 35 35 37 33 38 38 36 33 33 36 34 31 43 36 36 36 33
##  [2905] 33 24 33 36 31 34 77 34 36 32 31 31 35 37 37 37 23 23 34 34 34 32 54 38
##  [2929] 38 32 34 31 37 56 11 31 56 45 45 31 11 38 57 42 33 35 76 53 31 32 43 35
##  [2953] 31 33 23 35 23 39 11 37 33 34 33 31 31 34 39 39 32 31 32 34 42 47 31 33
##  [2977] 45 45 57 43 32 52 38 32 38 32 38 23 38 11 32 32 33 55 23 56 42 76 21 33
##  [3001] 11 38 25 38 34 31 32 38 52 32 31 37 37 37 33 33 47 39 33 36 38 33 43 36
##  [3025] 57 36 36 36 36 36 37 36 39 36 36 36 36 36 36 37 36 35 37 36 36 37 33 37
##  [3049] 43 36 37 57 57 33 33 33 37 36 53 42 39 58 33 33 37 38 33 45 37 33 38 33
##  [3073] 35 36 33 33 33 33 52 33 33 36 36 33 33 33 36 33 36 37 56 35 38 36 36 36
##  [3097] 36 36 36 36 36 36 38 45 38 37 38 37 37 37 56 37 33 45 34 34 36 38 43 33
##  [3121] 33 34 34 38 36 57 35 38 42 42 39 36 37 33 57 35 38 37 33 53 36 33 35 34
##  [3145] 38 45 37 38 35 38 38 33 76 54 76 38 38 37 38 36 36 36 38 38 34 33 33 35
##  [3169] 32 36 36 36 52 36 38 34 45 36 36 57 56 36 45 45 36 36 36 45 33 36 37 37
##  [3193] 42 37 33 35 37 33 33 31 57 57 57 34 76 33 35 32 33 31 33 33 33 33 34 33
##  [3217] 33 33 37 37 36 33 34 34 36 33 33 42 42 39 39 39 58 58 33 33 37 33 33 33
##  [3241] 36 45 45 45 37 57 33 33 33 47 35 35 33 35 35 37 33 38 38 37 37 33 33 33
##  [3265] 33 33 33 33 33 33 33 43 36 33 33 36 36 36 36 45 33 45 47 39 58 45 44 45
##  [3289] 37 33 38 36 36 33 43 57 45 36 36 45 36 37 35 34 31 36 47 39 58 37 38 36
##  [3313] 36 36 36 33 37 33 33 37 37 57 33 33 33 33 33 33 38 31 37 36 36 31 33 36
##  [3337] 39 25 33 33 36 37 33 45 33 33 42 37 38 35 33 38 33 33 33 33 43 33 33 33
##  [3361] 36 33 57 33 45 37 34 31 31 34 38 33 35 32 57 36 36 37 37 32 32 31 35 35
##  [3385] 37 37 37 34 34 23 34 34 37 34 33 33 38 38 34 34 37 37 32 32 37 37 33 32
##  [3409] 37 37 37 37 37 37 37 37 37 11 33 11 57 57 11 45 33 38 33 35 31 35 23 35
##  [3433] 23 39 39 31 31 11 36 32 37 37 31 31 38 32 33 33 34 34 32 32 37 37 34 33
##  [3457] 33 34 34 37 31 36 38 34 34 37 39 39 39 39 58 33 45 45 57 57 57 11 34 33
##  [3481] 32 57 34 34 37 37 33 38 38 23 38 38 38 38 38 32 25 11 32 32 35 32 32 11
##  [3505] 32 32 35 35 33 33 25 23 32 38 38 38 32 36 34 35 31 32 32 11 32 25 33 33
##  [3529] 36 38 57 57 57 57 11 36 33 33 11 32 32 32 31 31 34 34 36 31 35 39 58 45
##  [3553] 38 33 32 57 32 37 33 54 35 57 32 77 34 34 39 33 32 55 57 34 34 34 38 32
##  [3577] 57 38 37 36 44 32 32 43 44 32 34 31 31 34 34 36 32 32 31 31 35 37 37 34
##  [3601] 34 23 23 34 34 34 36 34 34 32 32 32 37 37 37 31 37 38 57 32 31 35 31 31
##  [3625] 32 32 34 32 32 32 31 31 34 39 39 32 32 34 38 31 32 34 34 42 39 32 45 45
##  [3649] 57 43 32 33 37 34 38 32 38 38 38 55 38 38 32 32 32 32 33 76 38 34 36 31
##  [3673] 32 32 52 32 32 31 31 34 34 36 36 56 77 37 36 36 36 38 35 33 56 34 33 33
##  [3697] 33 37 37 42 37 33 38 42 47 39 58 25 33 33 36 38 57 33 35 76 76 38 35 37
##  [3721] 36 33 33 36 33 36 38 33 43 36 33 36 32 35 23 31 31 23 35 23 11 11 11 23
##  [3745] 23 31 23 32 38 36 36 36 36 34 34 24 31 31 34 38 33 77 38 32 57 34 34 45
##  [3769] 38 36 36 36 36 32 32 31 31 35 35 37 37 37 37 37 37 37 34 34 23 36 34 33
##  [3793] 33 37 38 36 36 36 36 36 36 38 34 38 34 33 33 34 36 38 33 33 38 32 32 36
##  [3817] 36 54 38 38 38 38 32 32 38 38 33 33 31 31 57 57 33 57 32 37 45 37 33 56
##  [3841] 38 38 57 57 37 37 37 56 56 35 35 56 56 57 57 31 33 37 38 56 32 57 57 33
##  [3865] 33 52 45 45 45 45 31 31 31 43 43 57 38 44 34 38 38 57 57 45 45 45 34 34
##  [3889] 38 38 38 56 56 33 42 35 35 35 37 34 34 53 53 31 31 57 32 32 43 43 35 35
##  [3913] 35 31 33 33 23 35 35 39 39 31 31 31 33 32 36 36 36 36 32 32 37 37 52 52
##  [3937] 33 33 33 33 33 47 55 55 55 37 37 32 32 33 33 42 32 31 31 32 34 34 33 33
##  [3961] 56 56 39 33 33 38 34 34 32 32 32 33 37 37 37 56 34 34 34 34 38 38 45 34
##  [3985] 38 37 31 32 38 36 36 36 43 43 57 38 38 38 34 34 37 37 33 42 42 42 47 47
##  [4009] 39 39 39 39 39 58 58 36 33 33 37 37 33 54 42 38 38 31 31 34 34 34 32 33
##  [4033] 38 33 33 52 45 45 45 45 45 56 57 43 43 32 38 37 57 34 34 53 53 43 43 33
##  [4057] 33 32 57 34 34 38 52 33 33 38 38 34 43 43 32 32 32 38 33 33 33 33 38 42
##  [4081] 32 32 56 55 38 38 38 38 38 38 38 38 38 34 34 34 33 33 32 32 32 32 35 32
##  [4105] 33 33 32 32 33 33 23 31 33 33 33 33 38 35 33 33 55 34 34 25 54 23 31 24
##  [4129] 24 38 38 38 38 38 38 34 34 37 37 36 36 36 36 36 36 36 36 38 38 38 56 38
##  [4153] 38 34 56 31 31 56 34 32 43 42 42 34 47 38 38 33 34 38 38 76 76 34 56 21
##  [4177] 33 33 33 36 36 32 56 31 33 33 38 38 38 38 38 38 38 38 34 34 52 36 36 36
##  [4201] 31 31 32 24 38 34 57 57 57 42 56 56 36 31 52 32 33 33 38 38 32 32 31 31
##  [4225] 31 34 33 33 34 34 36 36 36 36 36 36 36 45 38 31 33 37 39 33 45 38 45 33
##  [4249] 36 33 45 33 34 33 24 36 37 36 36 36 37 76 34 37 36 42 47 39 58 36 34 37
##  [4273] 45 34 38 36 38 37 36 33 36 36 43 36 36 36 39 57 43 33 37 33 36 33 33 35
##  [4297] 57 45 33 31 33 33 33 45 37 33 36 37 42 39 36 33 57 33 45 38 33 35 37 33
##  [4321] 38 36 33 45 36 12 31 43 36 57 36 33 33 36 33 37 37 37 37 33 35 33 37 37
##  [4345] 33 57 37 52 33 33 45 34 37 37 33 33 42 39 33 33 57 43 33 33 37 33 33 33
##  [4369] 33 35 33 38 33 33 45 33 12 31 33 57 33 33 36 37 34 36 37 37 37 24 37 32
##  [4393] 37 37 37 37 34 34 32 37 37 37 37 37 57 33 35 35 35 35 31 32 33 37 32 37
##  [4417] 37 37 37 37 33 33 34 34 37 33 37 39 39 39 39 39 39 37 33 33 57 38 33 33
##  [4441] 33 33 38 38 32 35 35 33 52 32 38 38 33 34 35 32 21 33 33 36 36 36 57 57
##  [4465] 57 34 33 32 36 37 32 24 37 31 31 24 43 33 33 33 34 34 32 57 34 34 33 36
##  [4489] 36 37 32 32 31 31 35 35 37 37 37 37 35 37 34 34 23 37 34 34 34 37 37 34
##  [4513] 37 33 34 33 33 33 34 34 33 32 37 32 32 32 37 37 37 31 37 32 37 37 37 37
##  [4537] 37 33 33 37 37 37 37 37 37 56 35 11 31 56 45 31 33 33 33 34 34 11 37 53
##  [4561] 34 57 11 42 34 38 38 38 42 33 34 35 35 53 31 32 43 35 35 31 23 35 23 37
##  [4585] 39 39 31 31 31 31 31 11 36 32 32 32 37 34 32 31 31 38 32 33 33 33 33 33
##  [4609] 33 33 34 34 32 32 32 33 33 37 37 37 37 37 34 34 34 38 45 34 34 38 37 37
##  [4633] 31 31 32 32 36 57 34 34 35 33 42 47 47 39 39 39 39 39 39 39 31 31 34 32
##  [4657] 33 33 32 45 45 57 57 43 32 34 57 34 32 35 37 34 33 32 57 34 39 45 38 38
##  [4681] 38 34 32 32 38 38 33 33 33 33 38 38 38 38 38 38 38 32 33 11 37 37 32 32
##  [4705] 35 32 32 33 34 32 32 23 33 33 35 35 35 33 33 55 34 33 33 33 23 32 24 38
##  [4729] 38 32 34 34 34 34 36 34 33 34 32 35 32 32 34 34 76 33 21 33 11 33 36 36
##  [4753] 36 36 31 32 32 38 57 57 57 57 57 36 33 33 32 35 32 31 31 34 34 33 33 37
##  [4777] 33 33 33 57 36 37 36 36 37 32 33 36 37 36 38 33 35 32 37 37 37 37 37 35
##  [4801] 35 33 37 33 37 57 57 34 34 33 35 37 37 36 33 33 34 32 37 38 37 37 37 34
##  [4825] 34 33 36 35 42 39 39 39 33 33 45 57 57 33 33 33 33 38 38 33 33 35 35 35
##  [4849] 37 37 33 38 38 36 33 31 33 36 31 33 43 36 36 33 33 33 24 33 36 39 36 32
##  [4873] 36 36 36 36 37 37 33 33 33 32 32 37 37 33 33 45 45 37 37 37 57 57 33 33
##  [4897] 57 31 31 57 38 38 33 33 35 35 34 53 32 32 43 43 35 33 33 35 33 33 36 37
##  [4921] 33 37 33 33 33 38 34 34 37 34 34 33 33 36 42 39 39 58 58 33 33 37 54 42
##  [4945] 34 34 45 45 43 43 57 57 33 33 33 33 57 33 33 33 38 33 33 33 33 33 33 33
##  [4969] 34 34 24 24 33 33 36 38 38 56 33 33 33 36 36 38 36 36 31 57 57 33 33 33
##  [4993] 32 34 34 45 31 31 34 23 23 32 32 31 31 35 35 37 34 34 23 23 34 34 34 32
##  [5017] 32 37 37 38 38 31 39 34 34 32 32 31 31 38 38 39 32 32 55 55 32 34 34 39
##  [5041] 45 45 32 32 42 38 38 32 32 32 32 32 32 34 34 36 36 37 36 35 36 37 37 36
##  [5065] 36 36 35 35 37 43 37 33 37 36 33 33 33 37 36 36 39 37 33 37 33 33 37 35
##  [5089] 76 36 38 36 33 33 33 52 33 36 33 57 36 36 36 36 36 37 37 47 39 52 37 36
##  [5113] 37 37 33 33 36 39 45 57 33 37 37 38 36 33 33 33 43 36 36 33 36 36 36 36
##  [5137] 36 45 43 37 33 45 31 36 33 47 39 39 58 58 36 45 45 45 33 38 38 36 36 36
##  [5161] 52 36 43 36 57 57 45 36 36 36 45 33 36 36 36 37 33 37 33 36 36 36 36 38
##  [5185] 38 33 35 37 37 57 31 33 33 32 36 36 37 34 33 39 39 39 33 57 45 33 33 35
##  [5209] 33 38 38 38 36 36 38 38 36 36 36 36 36 36 57 33 36 36 36 33 33 37 57 33
##  [5233] 57 45 33 31 33 37 34 33 37 42 39 58 33 33 45 43 33 35 38 33 32 36 33 36
##  [5257] 36 57 36 45 38 38 36 39 45 36 38 38 33 45 43 42 39 45 76 52 36 32 57 36
##  [5281] 36 36 36 43 33 33 37 57 57 35 32 36 37 34 42 42 47 47 39 39 39 39 39 58
##  [5305] 58 36 45 45 57 57 57 32 57 34 45 45 45 34 33 33 38 76 57 38 38 36 36 32
##  [5329] 52 36 36 32 43 36 36 36 57 57 57 56 36 36 36 31 34 34 34 31 34 34 36 32
##  [5353] 32 31 35 35 37 37 37 34 34 23 34 34 34 36 38 34 34 32 32 54 38 32 32 37
##  [5377] 37 38 37 31 37 34 38 34 76 57 32 31 31 31 32 34 32 31 31 38 34 39 39 32
##  [5401] 55 55 37 34 34 31 32 34 37 42 39 31 45 45 43 32 34 56 34 39 38 32 38 38
##  [5425] 38 38 38 32 32 38 32 33 35 34 76 38 34 34 34 38 36 31 32 57 57 52 38 32
##  [5449] 31 34 34 36 36 35 35 37 37 36 36 36 36 36 36 33 33 37 37 37 37 57 57 35
##  [5473] 35 33 33 37 37 31 31 37 37 36 36 45 45 33 33 34 34 37 37 24 24 37 37 35
##  [5497] 35 36 36 36 36 37 37 77 36 36 34 33 33 36 36 42 42 47 47 39 39 58 58 36
##  [5521] 36 33 33 36 36 45 45 33 33 34 34 37 37 33 33 33 33 38 38 36 36 36 36 36
##  [5545] 36 36 36 33 33 36 36 32 32 36 36 35 35 36 36 45 36 77 77 35 35 45 45 25
##  [5569] 25 37 37 36 36 33 33 36 36 37 37 56 56 37 37 36 36 42 42 33 33 36 24 24
##  [5593] 33 33 52 52 37 37 57 57 33 33 53 53 57 57 38 38 38 38 33 33 37 37 31 31
##  [5617] 37 37 33 33 36 36 33 33 45 45 33 33 35 35 33 33 37 37 33 33 54 54 33 33
##  [5641] 38 38 34 34 37 37 38 38 56 56 33 33 33 33 33 33 31 31 37 37 36 36 36 36
##  [5665] 42 42 37 37 77 77 33 33 36 36 33 33 36 36 38 38 38 38 47 47 39 39 58 58
##  [5689] 36 45 45 33 33 36 36 45 45 37 37 57 57 37 37 33 33 37 37 37 37 35 35 38
##  [5713] 38 33 33 38 38 38 38 37 37 55 55 33 33 76 76 38 38 37 37 36 37 37 33 33
##  [5737] 36 36 33 33 36 33 33 35 35 38 38 35 35 36 36 36 36 33 33 36 36 33 33 33
##  [5761] 33 33 33 38 38 24 24 37 37 43 43 36 36 36 38 38 35 35 36 36 37 37 36 37
##  [5785] 33 33 36 36 36 37 36 42 33 35 37 37 33 33 36 38 37 33 33 24 31 37 35 37
##  [5809] 36 36 33 33 77 33 36 33 34 36 33 39 58 36 45 33 57 38 38 33 37 34 36 36
##  [5833] 33 33 38 33 36 36 37 33 43 36 33 35 36 36 32 37 37 37 31 45 33 24 39 39
##  [5857] 33 33 35 37 33 35 52 36 34 31 34 24 34 38 34 36 36 37 32 32 31 31 35 37
##  [5881] 37 37 37 34 34 23 34 34 34 36 34 34 34 38 33 38 32 54 38 32 37 34 31 37
##  [5905] 37 33 37 56 35 32 31 56 32 52 45 31 57 38 53 57 42 38 42 35 34 76 53 31
##  [5929] 57 32 43 35 35 31 33 35 39 31 31 36 32 37 34 55 34 32 33 42 31 31 34 56
##  [5953] 33 38 34 32 32 34 57 37 56 34 38 38 34 34 31 32 32 36 57 38 38 42 47 39
##  [5977] 39 58 31 33 33 57 57 43 32 34 38 37 57 34 45 43 38 36 56 32 38 33 38 42
##  [6001] 32 55 38 23 38 38 34 32 38 35 32 38 32 32 31 33 33 23 38 32 34 36 38 38
##  [6025] 56 56 42 38 38 31 33 56 36 36 38 38 36 36 31 32 32 38 57 42 52 32 32 31
##  [6049] 34 34 34 36 31 34 32 35 37 23 31 31 31 57 38 42 34 32 43 31 35 39 31 55
##  [6073] 34 32 31 32 31 43 57 32 55 38 34 32 33 23 33 31 57 42 52 23 32 31 32 36
##  [6097] 37 37 37 37 34 37 42 37 33 33 33 34 32 37 37 57 37 37 57 38 33 31 57 45
##  [6121] 34 33 35 32 33 36 33 33 37 33 33 34 34 45 36 36 47 39 39 39 39 39 33 43
##  [6145] 33 33 36 36 45 45 57 57 33 33 33 33 33 38 35 35 38 38 37 33 34 33 33 36
##  [6169] 33 57 57 31 33 36 36 34 33 32 45 36 36 36 36 37 32 31 37 37 37 37 34 32
##  [6193] 36 36 33 38 32 33 57 32 45 45 45 37 37 57 37 37 37 37 37 37 56 33 33 37
##  [6217] 57 57 45 31 31 43 57 57 57 57 57 33 33 33 33 33 37 57 57 57 57 57 57 45
##  [6241] 33 33 38 38 38 56 33 33 35 37 34 31 32 32 32 43 35 33 35 39 31 31 31 31
##  [6265] 31 31 32 36 32 37 52 33 33 33 33 33 55 37 32 33 33 33 33 33 33 33 33 34
##  [6289] 34 32 57 37 37 37 37 34 37 37 37 36 57 42 42 47 47 47 47 47 47 47 39 39
##  [6313] 39 39 39 39 39 58 58 58 58 58 58 58 36 54 36 34 33 45 45 45 45 45 57 43
##  [6337] 57 57 57 57 43 33 33 33 45 33 37 32 38 33 33 33 33 38 38 38 38 38 38 38
##  [6361] 56 32 33 33 37 35 33 32 33 33 33 33 33 33 33 55 37 34 34 34 34 34 33 38
##  [6385] 38 38 38 38 32 32 34 37 36 36 36 38 56 38 31 31 36 47 34 56 31 33 33 33
##  [6409] 33 36 38 31 31 31 33 43 43 43 36 36 36 31 57 57 57 57 57 57 33 33 33 32
##  [6433] 36 36 43 42 39 45 52 36 31 31 32 32 36 36 36 36 36 36 36 36 36 36 36 36
##  [6457] 36 36 36 36 34 34 37 37 37 37 37 37 37 31 33 33 33 44 34 34 77 77 77 77
##  [6481] 32 57 34 34 34 34 33 36 36 36 36 36 36 36 37 32 32 31 35 35 37 37 37 37
##  [6505] 35 34 34 36 36 36 36 36 34 36 36 36 36 36 36 34 33 37 37 37 37 37 37 31
##  [6529] 31 32 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
##  [6553] 36 36 34 32 32 32 37 37 32 37 36 36 36 36 36 36 36 36 36 36 36 36 36 32
##  [6577] 34 34 34 37 37 37 37 37 57 32 37 37 57 37 23 37 37 37 37 37 37 37 37 23
##  [6601] 56 56 35 23 37 37 37 37 37 37 37 57 34 33 33 33 33 33 33 33 33 34 37 57
##  [6625] 57 57 57 57 57 34 34 34 34 34 34 34 34 34 34 34 24 32 39 31 31 31 31 31
##  [6649] 31 31 31 31 31 31 31 33 31 31 37 36 36 36 36 36 36 36 36 32 32 32 32 32
##  [6673] 32 32 32 32 42 52 44 57 33 33 33 33 37 31 32 32 33 33 39 39 33 33 33 33
##  [6697] 33 33 33 33 33 33 33 33 33 33 33 33 37 34 34 34 32 32 32 56 52 33 56 37
##  [6721] 36 36 36 36 36 36 36 36 37 37 36 35 56 57 57 37 56 37 35 34 37 37 76 33
##  [6745] 34 34 34 34 34 34 57 57 31 31 44 44 45 34 33 34 34 36 36 57 43 34 34 37
##  [6769] 33 33 42 42 42 42 42 47 47 47 47 39 39 39 39 39 39 39 39 39 39 39 39 39
##  [6793] 39 39 39 58 58 58 58 58 58 36 23 34 45 45 45 45 45 45 45 45 45 45 57 57
##  [6817] 57 32 45 57 34 57 57 57 57 57 57 57 33 36 36 36 36 36 36 32 32 31 31 35
##  [6841] 35 37 37 34 34 34 34 23 33 37 37 36 45 33 33 32 57 34 34 34 34 39 39 37
##  [6865] 37 37 37 45 45 45 34 34 23 33 33 33 33 33 33 33 33 33 33 33 33 23 38 32
##  [6889] 44 33 42 35 32 31 31 32 34 34 34 32 32 34 34 34 34 33 76 36 36 36 57 24
##  [6913] 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 36 36 32 33 33 33 36 36 36
##  [6937] 36 36 36 36 36 36 36 36 36 34 33 34 34 34 23 34 32 32 36 36 36 36 36 36
##  [6961] 36 34 25 36 36 36 36 36 36 36 36 44 36 36 36 36 36 36 36 36 36 36 36 36
##  [6985] 36 36 36 32 42 42 34 34 33 43 43 23 36 36 36 36 36 36 36 36 36 36 36 36
##  [7009] 34 34 57 57 57 57 57 57 57 57 57 57 57 57 57 34 57 42 38 38 34 32 31 34
##  [7033] 33 33 31 31 36 36 36 36 36 36 36 36 36 36 36 36 36 36 55 33 36 33 36 36
##  [7057] 39 36 37 36 33 36 36 36 37 37 36 36 37 35 53 34 33 33 36 42 47 39 36 33
##  [7081] 36 45 57 37 76 38 36 33 33 36 43 36 57 36 36 37 36 36 36 35 33 37 33 33
##  [7105] 37 47 39 58 25 33 33 57 33 76 38 36 33 33 36 36 36 32 33 57 31 35 47 39
##  [7129] 39 45 57 33 33 76 57 34 52 33 45 32 32 36 36 36 36 36 36 36 36 36 36 36
##  [7153] 36 36 36 36 34 34 34 34 34 34 34 37 37 37 37 37 31 34 33 33 38 44 34 34
##  [7177] 34 77 32 57 56 33 36 36 36 36 32 31 34 36 36 36 36 36 36 36 36 37 37 33
##  [7201] 31 34 32 32 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
##  [7225] 36 36 36 34 34 34 34 56 32 32 37 32 37 36 36 36 36 36 36 36 36 36 36 36
##  [7249] 38 38 38 34 34 34 33 33 37 37 37 34 37 37 24 37 37 37 37 37 37 37 37 56
##  [7273] 35 35 35 56 57 34 34 34 34 34 33 33 33 33 33 33 33 33 33 33 33 33 33 37
##  [7297] 34 34 34 57 57 57 57 57 57 57 57 34 33 38 38 38 38 76 24 33 33 35 39 31
##  [7321] 31 31 31 31 31 31 31 31 31 31 33 45 36 32 32 32 32 32 32 32 32 32 32 52
##  [7345] 42 33 33 33 31 32 32 32 32 32 32 32 33 39 33 33 33 33 33 33 33 33 33 33
##  [7369] 33 34 34 34 34 34 34 34 34 34 32 32 32 33 52 56 36 36 36 36 36 36 37 37
##  [7393] 37 37 37 37 37 37 36 35 56 57 37 56 37 35 34 35 76 33 34 34 34 34 34 57
##  [7417] 38 44 44 34 54 33 45 34 33 34 34 31 31 31 31 31 31 31 31 31 43 34 34 42
##  [7441] 42 42 42 42 42 42 42 47 47 47 47 47 47 47 39 39 39 39 39 39 39 39 39 39
##  [7465] 39 39 39 39 39 58 58 58 58 58 58 58 58 58 77 36 36 36 36 36 36 36 36 36
##  [7489] 36 36 36 38 32 33 38 45 45 45 45 45 45 45 45 45 45 45 45 57 57 57 57 57
##  [7513] 57 57 57 57 57 57 57 34 33 34 36 36 36 36 32 32 53 35 35 37 34 33 37 37
##  [7537] 37 36 36 33 32 32 34 34 34 34 34 34 34 34 45 45 34 34 34 33 33 33 33 33
##  [7561] 33 33 33 33 33 33 33 33 33 33 33 38 38 38 38 38 38 38 38 38 38 38 38 38
##  [7585] 38 38 38 38 33 32 34 34 34 23 35 34 34 34 34 34 34 34 34 54 36 36 36 36
##  [7609] 36 57 38 38 38 38 38 38 38 38 38 38 38 38 38 45 33 32 37 34 34 33 36 36
##  [7633] 36 36 36 36 36 36 36 36 36 36 32 33 33 31 34 31 32 36 36 36 36 32 32 45
##  [7657] 36 36 36 36 36 36 36 33 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 32
##  [7681] 42 33 33 33 33 33 38 34 31 31 31 31 31 31 31 31 31 31 33 33 33 36 36 36
##  [7705] 36 36 36 36 36 36 36 36 36 36 36 57 57 57 57 57 57 57 57 57 57 57 57 57
##  [7729] 34 33 36 33 33 34 32 32 31 33 31 36 36 36 36 36 36 36 36 36 36 36 36 36
##  [7753] 36 31 55 37 42 33 37 37 33 33 33 33 33 24 36 33 33 39 33 36 45 37 33 33
##  [7777] 33 33 37 34 31 34 35 32 57 34 36 36 37 37 32 32 35 35 37 37 37 37 37 34
##  [7801] 34 23 34 33 33 33 37 32 37 37 33 32 32 37 37 37 37 37 37 37 37 37 37 35
##  [7825] 35 11 33 33 33 11 57 11 38 33 35 35 31 35 31 23 35 39 11 36 32 37 37 31
##  [7849] 31 32 39 33 33 34 34 32 32 37 37 34 34 33 33 34 34 37 36 34 34 37 39 39
##  [7873] 39 39 39 33 45 45 45 57 57 11 43 32 34 37 33 33 38 38 38 32 11 37 35 32
##  [7897] 32 32 32 23 35 35 33 33 33 33 25 23 32 38 38 38 33 32 34 36 34 35 32 25
##  [7921] 33 33 36 36 31 24 57 57 57 57 57 11 36 33 33 11 23 32 31 36 37 37 35 57
##  [7945] 57 34 31 32 33 37 47 39 33 33 33 34 38 37 33 36 37 33 36 37 36 36 37 34
##  [7969] 32 33 36 36 33 37 36 38 33 33 35 37 33 37 35 37 34 33 37 57 45 33 38 37
##  [7993] 37 33 33 38 37 38 38 34 37 33 38 42 47 39 36 33 45 37 57 33 38 33 35 38
##  [8017] 33 38 38 38 34 36 33 31 33 37 36 38 33 43 36 33 33 24 36 36 36 36 36 37
##  [8041] 36 33 33 45 37 37 57 33 37 57 33 31 57 57 33 57 38 33 33 33 37 33 38 32
##  [8065] 37 37 36 47 39 39 45 57 33 45 36 33 33 32 35 33 33 34 38 38 33 33 33 36
##  [8089] 36 36 33 36 37 33 33 37 34 34 34 37 37 31 34 35 35 32 34 11 36 36 37 37
##  [8113] 32 32 31 35 35 37 37 37 37 37 34 34 23 34 34 37 33 33 33 34 34 37 32 36
##  [8137] 32 37 37 33 33 35 34 32 32 37 37 37 37 37 37 37 37 37 35 45 33 33 11 37
##  [8161] 57 57 11 45 33 33 38 38 35 31 35 35 23 35 23 39 39 31 31 11 11 36 32 32
##  [8185] 37 33 37 31 31 32 32 33 33 34 34 32 32 34 32 32 37 37 37 34 34 33 34 34
##  [8209] 37 37 36 38 34 34 37 35 42 39 39 39 39 39 39 33 45 45 45 37 45 45 57 57
##  [8233] 37 32 34 37 33 33 38 38 38 38 38 38 38 32 33 11 32 32 32 35 32 32 33 11
##  [8257] 34 32 32 33 35 35 55 34 33 33 23 24 38 38 11 32 34 36 34 34 35 31 32 37
##  [8281] 36 25 33 36 36 36 36 31 37 57 57 57 57 57 57 57 11 36 33 33 32 32 33 31
##  [8305] 34 36 31 36 36 36 36 36 36 36 57 34 36 36 36 36 36 42 39 58 36 36 36 45
##  [8329] 76 38 38 36 36 36 36 36 36 36 43 36 36 36 36 35 37 37 25 25 37 37 36 36
##  [8353] 33 33 37 37 33 33 37 37 37 37 24 24 56 56 35 35 37 37 33 33 57 57 34 34
##  [8377] 34 34 24 24 33 33 33 33 37 37 31 31 33 33 36 36 33 33 33 33 33 33 33 33
##  [8401] 33 37 37 24 24 37 37 36 33 33 77 77 36 36 34 34 33 33 36 36 37 33 33 42
##  [8425] 42 47 39 39 58 36 36 33 33 33 33 33 33 45 45 37 37 57 57 37 37 33 33 33
##  [8449] 33 37 37 37 37 38 38 33 33 76 76 36 36 45 45 38 38 33 33 33 33 37 37 36
##  [8473] 36 33 33 33 33 33 33 33 33 35 35 36 36 33 33 33 33 31 31 37 37 33 33 43
##  [8497] 43 36 57 57 35 35 33 33 36 36 37 37 36 36 36 36 39 58 76 38 36 43 36 36
##  [8521] 36 38 33 36 36 33 33 33 34 33 45 38 32 38 33 57 33 37 38 37 35 33 57 33
##  [8545] 37 38 33 45 31 43 38 33 33 45 38 33 35 37 34 57 32 35 33 57 33 32 36 45
##  [8569] 33 33 45 37 32 33 33 33 38 34 57 37 34 36 39 39 33 33 36 34 33 45 43 57
##  [8593] 34 33 33 33 37 38 38 33 33 33 33 33 34 24 38 38 34 38 38 38 34 38 33 33
##  [8617] 36 38 33 36 33 33 33 34 36 36 36 36 42 39 39 45 36 36 36 43 36 36 36 36
##  [8641] 43 36 56 35 37 37 39 36 38 76 38 52 36 33 37 45 36 37 38 38 34 33 38 37
##  [8665] 37 35 33 37 57 37 35 37 37 34 33 57 45 33 33 38 35 35 31 36 33 33 33 33
##  [8689] 34 32 38 37 34 34 37 33 36 38 47 39 58 33 38 34 33 33 45 38 57 43 33 45
##  [8713] 52 36 33 33 38 33 33 35 33 37 38 45 34 33 76 38 36 38 31 33 38 43 33 31
##  [8737] 43 36 37 57 34 36 36 33 42 33 36 36 36 37 35 33 33 33 36 42 37 39 36 33
##  [8761] 45 57 33 38 76 38 36 33 33 36 36 43 36 32 36 36 36 36 36 36 39 36 38 36
##  [8785] 36 36 36 36 36 36 33 52 36 37 37 53 35 77 77 56 36 36 36 37 37 36 45 38
##  [8809] 36 37 37 33 37 38 36 36 36 36 33 33 36 42 36 42 36 37 38 45 33 33 33 35
##  [8833] 35 77 37 37 43 37 37 35 35 37 37 37 57 33 57 33 33 33 33 53 34 34 36 36
##  [8857] 76 76 39 31 31 33 33 32 32 52 52 33 33 33 33 33 33 33 33 34 34 38 38 33
##  [8881] 37 37 57 36 33 33 57 42 42 47 39 39 36 33 57 25 25 33 33 33 33 32 45 45
##  [8905] 33 33 57 45 38 34 57 57 35 38 36 55 35 37 35 33 36 35 45 45 37 37 33 33
##  [8929] 38 38 32 35 38 38 35 35 33 33 76 76 54 76 38 38 38 37 32 37 36 36 36 36
##  [8953] 33 33 33 33 38 33 33 33 52 52 36 36 33 38 38 34 33 33 33 43 56 56 33 33
##  [8977] 33 33 33 33 45 33 36 36 36 36 45 33 36 36 36 36 42 39 45 57 36 36 36 43
##  [9001] 36 39 37 37 33 38 37 33 57 57 57 35 32 35 35 33 57 47 39 58 33 38 33 38
##  [9025] 33 36 39 36 36 34 34 36 36 36 36 36 33 33 36 33 33 36 37 37 38 33 33 33
##  [9049] 33 37 37 31 31 56 33 33 31 31 33 33 57 57 33 35 35 34 34 32 32 43 43 35
##  [9073] 35 31 31 32 36 36 33 33 38 32 33 33 33 34 34 37 37 34 34 34 34 36 36 33
##  [9097] 35 42 42 47 47 39 39 58 58 54 43 34 34 33 33 33 45 45 43 43 57 57 43 43
##  [9121] 33 33 33 33 36 36 33 33 32 32 38 38 33 35 33 33 33 33 33 33 35 35 33 33
##  [9145] 34 34 54 33 33 24 24 38 38 38 36 36 43 38 42 42 33 33 36 36 38 38 36 36
##  [9169] 31 31 37 37 57 57 36 36 33 33 33 36 36 36 36 38 57 42 56 36 36 45 42 39
##  [9193] 36 43 38 57 45 76 36 38 38 38 36 43 36 36 45 36 57 36 77 36 39 45 36 34
##  [9217] 36 34 34 32 57 37 36 34 34 32 36 38 34 38 34 32 37 43 37 34 34 33 32 32
##  [9241] 33 38 77 34 34 33 34 39 39 36 32 33 37 57 34 34 34 33 32 57 34 34 34 34
##  [9265] 33 38 38 38 35 33 38 38 36 34 35 35 32 36 33 33 36 32 38 57 42 33 31 33
##  [9289] 35 32 36 36 36 37 39 36 37 38 36 36 36 24 34 34 57 34 38 36 36 37 32 31
##  [9313] 35 37 37 37 37 37 34 23 33 33 34 33 33 33 33 38 38 38 32 37 35 31 38 37
##  [9337] 37 37 57 31 56 45 31 38 57 33 38 42 35 35 34 53 31 32 43 35 35 31 33 33
##  [9361] 23 35 39 31 11 36 32 37 55 34 33 42 34 33 33 34 32 34 32 37 34 34 34 37
##  [9385] 31 32 36 57 34 35 39 39 39 36 31 33 33 45 43 32 57 53 32 57 45 52 38 32
##  [9409] 37 33 38 32 38 34 76 11 35 33 32 31 33 35 33 23 24 38 36 38 38 38 56 31
##  [9433] 56 37 38 21 33 33 36 38 38 38 34 31 32 24 38 57 36 52 33 32 31 34 36 36
##  [9457] 36 36 36 36 36 36 36 36 36 39 36 36 52 36 36 36 36 34 36 36 36 38 57 37
##  [9481] 42 47 39 58 33 45 34 76 36 38 38 36 33 36 36 43 36 36 52 36 36 34 37 57
##  [9505] 33 33 33 38 38 34 34 34 77 34 37 35 33 34 34 38 38 38 36 36 34 38 34 36
##  [9529] 34 34 32 32 32 37 36 38 34 34 33 38 36 34 38 23 56 35 37 32 34 34 38 34
##  [9553] 34 34 38 37 55 38 34 38 38 38 76 33 34 31 33 37 36 34 32 52 38 34 34 38
##  [9577] 43 32 32 32 32 32 32 37 34 37 34 44 34 37 38 34 38 38 38 33 34 42 39 39
##  [9601] 58 38 34 32 34 33 45 33 53 43 38 55 38 57 57 34 37 33 34 34 36 53 33 34
##  [9625] 34 34 34 34 34 38 34 33 34 38 33 38 38 38 38 38 38 32 43 44 34 32 32 34
##  [9649] 34 31 37 34 34 76 54 38 56 36 38 38 34 34 33 34 36 36 38 36 34 34 43 32
##  [9673] 38 34 34 32 36 32 31 34 38 34 76 76 36 56 44 36 34 32 38 38 34 36 57 33
##  [9697] 36 36 57 37 34 32 32 33 36 36 36 36 36 36 38 42 37 43 35 37 44 31 43 33
##  [9721] 33 33 33 37 42 77 53 42 39 39 39 45 38 57 57 36 33 33 45 45 38 38 34 38
##  [9745] 38 33 33 76 76 36 36 36 33 33 33 33 33 52 52 57 33 33 36 36 33 33 37 32
##  [9769] 33 37 37 35 37 34 33 57 31 37 52 33 33 33 34 37 34 33 37 35 42 47 39 39
##  [9793] 33 45 37 57 33 38 35 34 33 38 33 31 45 33 36 33 31 43 36 57 33 33 33 36
##  [9817] 77 36 36 36 39 36 36 36 36 36 39 36 37 37 33 33 33 39 45 57 33 37 36 33
##  [9841] 33 33 43 36 36 36 47 34 34 34 34 31 31 34 33 34 34 34 34 36 36 32 32 31
##  [9865] 31 35 37 37 37 34 34 23 23 34 33 38 34 34 36 34 38 32 32 32 32 54 38 32
##  [9889] 37 34 31 37 37 23 37 31 56 45 31 33 34 38 38 38 76 42 35 34 53 31 57 32
##  [9913] 43 35 35 31 33 35 37 39 39 31 31 32 32 32 32 37 34 34 34 33 55 34 32 31
##  [9937] 31 32 32 34 32 32 54 55 37 37 37 38 31 32 32 34 42 47 39 39 39 58 31 32
##  [9961] 32 33 45 45 34 43 32 56 57 34 34 34 34 34 34 34 34 52 38 32 32 38 38 33
##  [9985] 38 38 38 38 38 38 38 44 31 33 32 32 32 32 32 32 23 33 35 55 23 76 34 32
## [10009] 36 31 34 32 34 34 56 36 36 38 31 32 32 38 38 34 52 32 32 32 31 31 34 34
## [10033] 33 36 52 35 37 33 36 37 37 37 37 37 33 34 33 31 33 36 33 35 33 33 34 37
## [10057] 37 35 37 36 37 36 33 36 39 33 36 45 37 37 57 37 33 37 37 38 33 38 36 33
## [10081] 33 36 33 37 43 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
## [10105] 36 32 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 38 38 32 37 37 37
## [10129] 37 33 57 33 36 35 35 36 36 36 36 37 34 36 36 36 36 39 36 36 45 57 36 45
## [10153] 33 35 38 38 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
## [10177] 36 36 57 36 36 36 36 36 36 36 36 35 37 25 37 33 37 37 56 35 37 37 33 57
## [10201] 35 33 37 33 36 45 33 33 33 38 34 24 37 35 36 37 36 34 36 33 42 39 36 45
## [10225] 33 36 45 45 34 33 38 56 38 38 37 33 33 36 52 33 33 31 37 43 36 57 36 36
## [10249] 77 37 36 37 37 33 33 33 37 42 36 42 39 36 25 33 33 36 36 33 33 76 36 33
## [10273] 33 33 36 43 36 36 33 36 37 37 33 37 57 57 31 33 38 37 36 33 42 39 33 33
## [10297] 45 38 33 35 33 38 33 33 36 33 36 36 36 36 37 32 57 36 36 36 36 36 36 36
## [10321] 37 32 36 36 36 36 36 36 36 36 36 38 36 36 38 37 37 56 33 33 33 45 37 57
## [10345] 57 35 35 36 52 57 32 32 37 37 34 36 34 42 47 39 39 39 39 58 77 45 45 45
## [10369] 57 57 35 45 36 35 32 55 57 34 45 45 45 34 33 33 38 35 35 33 38 38 36 36
## [10393] 36 36 36 33 33 32 36 52 44 36 36 36 36 32 33 43 36 36 36 36 36 36 36 57
## [10417] 57 57 36 36 33 36 36 36 36 36 36 45 25 36 36 36 45 42 36 36 39 45 45 76
## [10441] 36 35 36 36 43 36 35 33 37 54 37 56 37 33 33 34 36 76 52 31 37 52 43 33
## [10465] 33 37 57 35 56 42 47 39 58 33 57 38 38 35 36 57 37 45 33 55 34 33 33 37
## [10489] 38 38 37 36 38 33 35 32 36 34 34 36 52 36 36 36 36 36 56 36 36 36 36 37
## [10513] 25 33 37 36 36 36 36 36 36 36 36 36 36 36 36 36 36 42 37 37 24 37 56 35
## [10537] 37 37 57 34 57 45 37 31 37 36 33 45 33 33 33 54 33 34 37 37 24 42 33 77
## [10561] 36 33 39 39 39 58 36 45 25 33 33 33 36 37 57 45 33 33 33 37 37 35 38 35
## [10585] 37 55 33 33 76 76 45 38 38 38 37 56 38 38 38 33 37 36 53 43 33 36 36 33
## [10609] 33 47 35 36 36 33 36 36 36 36 36 36 36 33 33 37 43 36 36 36 36 35 33 36
## [10633] 36 36 36 36 36 36 39 32 32 24 34 34 31 31 34 24 34 33 33 33 32 57 57 34
## [10657] 31 11 33 36 36 36 36 36 36 37 37 32 32 31 31 35 35 37 37 37 35 37 37 34
## [10681] 23 34 34 34 37 34 34 33 36 34 34 34 37 32 32 32 24 37 37 35 32 37 37 37
## [10705] 37 37 37 37 37 37 11 31 33 33 11 34 34 33 38 33 35 31 32 35 35 31 23 35
## [10729] 23 35 39 39 31 31 31 32 11 32 32 32 37 33 33 34 37 31 31 32 32 32 33 33
## [10753] 33 39 39 33 34 34 32 32 32 33 37 37 34 31 34 25 33 34 34 37 32 36 36 36
## [10777] 57 34 34 34 33 33 39 39 39 39 39 39 39 39 39 39 39 39 32 45 32 32 45 57
## [10801] 32 34 32 31 35 35 37 37 34 34 33 32 32 57 34 34 34 39 38 38 38 34 34 32
## [10825] 33 33 23 38 38 38 38 38 32 33 33 11 37 32 35 32 32 32 33 34 32 32 33 35
## [10849] 35 37 37 34 34 33 23 32 57 38 38 11 32 34 34 36 34 33 35 34 32 35 35 32
## [10873] 32 32 33 37 34 36 32 11 36 36 31 34 57 57 57 57 57 11 36 11 35 32 34 31
## [10897] 31 34 31 36 34 34 36 36 36 36 36 36 36 36 34 34 34 34 34 24 37 37 31 31
## [10921] 34 38 38 34 34 34 38 33 32 57 34 38 36 36 36 36 36 36 36 36 36 32 32 31
## [10945] 31 35 37 37 37 37 37 37 34 34 34 36 36 36 36 36 36 36 23 37 36 36 36 36
## [10969] 34 33 33 34 33 56 47 37 37 37 38 33 34 34 56 38 38 38 38 38 36 36 36 36
## [10993] 36 36 36 36 36 38 38 34 36 36 36 36 36 36 36 36 36 36 34 34 33 33 34 34
## [11017] 34 34 38 38 33 33 33 38 45 45 37 37 37 32 36 36 36 36 36 36 36 36 36 54
## [11041] 38 38 38 38 38 38 38 38 38 38 38 32 32 37 37 38 38 38 33 33 33 33 33 38
## [11065] 32 31 38 37 37 32 37 37 45 45 37 37 33 33 38 57 37 37 37 56 56 35 35 33
## [11089] 56 57 57 31 33 33 37 37 37 37 37 37 37 38 56 32 57 33 33 52 45 31 31 57
## [11113] 57 57 33 34 33 33 33 33 33 38 38 57 57 37 45 45 45 33 33 34 24 38 38 38
## [11137] 56 33 33 33 42 34 34 34 34 34 34 34 34 34 34 35 35 34 34 53 31 32 32 43
## [11161] 43 35 35 31 33 35 37 37 39 39 31 31 31 32 32 32 31 36 36 32 32 32 32 37
## [11185] 52 52 45 33 33 33 34 34 47 55 38 38 37 32 32 33 42 31 31 38 38 32 33 56
## [11209] 39 33 33 33 33 33 33 33 33 33 38 38 38 38 34 34 34 32 32 32 32 32 38 38
## [11233] 57 34 45 36 36 34 37 37 37 56 34 34 34 34 38 38 38 38 33 33 33 34 34 34
## [11257] 38 38 37 37 31 31 31 32 32 36 36 36 33 43 43 36 36 36 36 36 36 38 38 38
## [11281] 38 34 38 38 37 37 37 37 35 42 42 42 42 42 47 47 47 47 47 47 39 39 39 39
## [11305] 39 39 39 39 39 58 58 58 77 36 36 36 36 36 36 36 36 36 36 36 33 33 37 34
## [11329] 34 43 31 31 34 34 33 33 33 33 33 52 57 45 45 45 45 45 37 45 45 57 57 43
## [11353] 43 32 38 38 37 38 38 38 57 57 57 57 57 34 34 34 34 34 34 34 34 34 34 34
## [11377] 37 37 34 34 36 36 53 45 43 43 33 33 33 33 33 33 33 32 57 34 39 45 45 52
## [11401] 33 38 38 38 34 36 36 36 32 37 32 38 38 38 38 38 33 33 33 33 38 38 38 42
## [11425] 32 32 56 55 33 38 38 38 38 38 38 34 34 32 32 33 33 33 33 34 38 38 38 38
## [11449] 33 32 34 32 32 32 33 33 33 32 32 33 31 31 33 33 33 38 35 33 33 33 45 45
## [11473] 37 34 34 34 34 33 25 23 33 33 32 24 38 38 38 38 38 38 38 38 38 38 33 33
## [11497] 38 38 38 38 38 38 38 38 38 38 38 34 38 38 38 32 34 34 34 37 34 34 36 36
## [11521] 36 36 36 36 34 34 56 38 38 38 38 38 38 38 38 38 34 34 34 56 31 31 56 31
## [11545] 32 36 36 36 33 45 45 42 42 38 43 34 34 38 33 34 34 34 34 38 38 76 34 56
## [11569] 21 33 33 33 33 36 36 36 36 36 36 36 36 36 36 36 32 31 38 38 38 38 38 38
## [11593] 38 38 33 31 38 38 38 33 33 34 36 36 36 36 36 36 36 36 36 36 31 32 24 57
## [11617] 57 57 57 57 42 34 36 36 36 36 31 31 33 42 42 33 24 33 33 33 32 32 32 33
## [11641] 33 32 31 31 34 34 33 33 34 34 34 34 36 36 36 36 36 36 36 36 36 37 37 37
## [11665] 31 37 37 37 36 36 33 37 43 36 35 37 34 33 33 33 36 33 36 42 47 39 58 33
## [11689] 33 33 33 57 33 37 33 33 33 36 38 33 36 33 33 33 52 33 33 36 33 36 33 33
## [11713] 36 33 37 42 37 37 35 33 37 43 37 33 37 33 45 33 33 33 33 37 39 33 33 36
## [11737] 33 57 33 37 38 35 37 33 33 33 33 36 33 34 31 34 34 34 36 36 36 37 37 32
## [11761] 32 31 31 35 35 37 37 37 37 37 37 37 34 34 33 37 37 33 21 33 24 33 34 33
## [11785] 37 24 37 37 33 34 33 38 34 32 37 37 37 37 37 37 37 35 33 33 31 31 57 33
## [11809] 33 37 57 33 33 35 35 31 32 35 35 35 35 35 37 39 31 31 37 36 37 33 33 33
## [11833] 31 39 33 34 34 32 35 37 37 37 34 34 34 34 33 33 33 33 34 37 33 36 36 36
## [11857] 33 57 34 37 35 47 39 39 39 39 39 58 33 37 54 33 33 57 57 33 39 38 38 38
## [11881] 24 33 33 33 33 38 38 38 38 32 33 33 35 35 32 33 32 33 35 35 35 33 37 34
## [11905] 33 33 52 32 24 38 38 38 34 32 34 37 34 36 36 34 33 35 35 33 33 33 21 21
## [11929] 33 33 33 36 31 33 35 32 32 31 31 31 34 37 33 33 32 32 34 34 34 34 34 34
## [11953] 34 34 37 37 31 31 34 35 35 34 38 44 34 77 35 32 57 34 34 34 11 11 36 36
## [11977] 37 37 37 32 32 32 31 31 31 35 35 37 37 37 37 37 37 37 37 34 34 36 23 35
## [12001] 34 34 37 37 37 37 37 34 34 32 37 33 33 36 36 24 34 34 56 33 32 32 37 37
## [12025] 32 44 32 37 36 38 32 37 37 37 37 34 33 33 34 34 34 34 34 34 32 44 37 34
## [12049] 32 37 37 37 37 37 37 37 23 37 37 37 37 37 37 37 23 23 56 35 35 37 37 23
## [12073] 11 31 37 34 34 34 45 33 33 33 34 11 37 53 34 57 57 57 11 11 11 45 33 38
## [12097] 38 34 34 33 35 35 35 34 31 35 35 31 23 35 35 39 39 31 31 31 31 31 31 31
## [12121] 31 32 11 11 36 36 32 32 32 37 37 52 44 33 33 33 33 44 34 34 32 37 31 31
## [12145] 31 31 32 32 32 32 32 32 34 33 33 33 33 33 33 33 33 33 34 34 32 32 32 42
## [12169] 32 45 45 56 37 37 37 37 37 37 37 37 37 56 57 35 77 34 34 31 34 25 34 34
## [12193] 34 33 33 34 34 34 34 37 37 32 36 33 33 33 32 34 34 34 34 34 37 37 42 42
## [12217] 42 39 39 39 39 39 39 39 39 39 39 39 39 39 39 58 58 23 33 54 32 45 33 33
## [12241] 33 45 45 45 45 32 57 32 45 45 45 57 34 57 57 33 34 34 34 34 32 32 31 35
## [12265] 35 35 37 37 34 34 33 37 45 32 34 34 34 34 34 34 34 39 38 23 23 23 32 32
## [12289] 32 37 24 33 33 33 33 33 33 33 33 38 23 23 38 38 38 38 38 38 38 38 32 32
## [12313] 44 44 44 11 11 32 32 35 35 32 32 34 34 34 32 32 32 33 23 23 23 33 33 35
## [12337] 35 35 37 37 55 57 34 34 34 34 34 34 34 45 33 33 33 33 33 54 54 52 23 76
## [12361] 76 32 38 38 38 38 38 38 34 11 11 32 34 34 34 34 36 36 23 34 33 33 33 33
## [12385] 33 34 34 33 33 23 23 35 34 32 31 35 32 32 32 44 34 36 21 44 56 33 36 36
## [12409] 32 42 33 33 25 25 33 33 33 43 36 36 36 36 36 36 36 36 36 36 36 31 32 24
## [12433] 38 57 57 57 57 57 57 57 57 57 23 34 36 33 33 33 33 32 23 32 32 32 31 31
## [12457] 34 34 34 36 37 31 55 36 37 36 33 36 33 36 37 34 35 37 36 33 33 33 36 36
## [12481] 42 39 36 36 45 57 37 33 36 38 36 36 33 36 36 36 33 36 36 36 39 36 36 33
## [12505] 36 37 37 37 34 33 39 36 57 38 36 43 43 43 36 36 37 43 37 37 35 35 37 33
## [12529] 33 33 32 37 34 47 39 39 37 33 33 35 33 33 52 33 33 36 36 36 36 36 36 36
## [12553] 36 36 36 38 36 37 37 33 36 47 39 36 38 36 38 36 33 52 36 38 36 36 36 36
## [12577] 36 32 57 36 36 36 37 37 32 37 36 36 36 33 36 36 36 37 37 43 36 37 37 33
## [12601] 33 33 37 57 35 35 33 32 37 36 34 36 36 39 39 36 45 37 38 57 33 57 45 33
## [12625] 33 35 37 36 38 38 36 36 36 33 33 52 36 32 36 36 57 36 36 36 36 36 39 36
## [12649] 77 36 36 36 76 47 39 58 38 36 36 36 36 36 33 36 36 37 36 36 33 35 37 33
## [12673] 37 36 33 33 33 37 37 37 36 47 39 58 33 33 37 37 38 36 36 33 33 36 36 36
## [12697] 36 33 37 37 33 37 33 33 42 33 37 33 33 33 33 33 37 35 37 33 33 33 33 34
## [12721] 36 37 33 33 43 33 33 37 37 33 33 37 33 45 33 33 33 37 37 33 33 37 37 36
## [12745] 36 33 36 33 31 33 36 37 39 25 33 33 36 37 37 57 33 33 37 33 33 33 37 45
## [12769] 57 37 33 33 37 37 33 33 33 33 33 38 38 37 33 37 33 33 33 33 33 33 33 37
## [12793] 33 33 33 33 45 33 33 33 33 33 37 33 33 33 37 33 33 36 33 33 57 33 35 33
## [12817] 33 33 33 33 33 33 37 33 37 37 33 36 36 37 37 33 36 37 33 36 37 34 33 36
## [12841] 36 36 33 36 36 33 37 36 36 38 37 33 33 33 33 35 37 33 37 37 37 56 34 33
## [12865] 33 53 57 45 34 33 33 33 35 35 31 36 52 33 38 33 33 33 33 38 38 34 37 38
## [12889] 36 36 37 34 33 34 33 37 33 36 36 35 42 39 39 39 58 33 33 52 45 37 57 43
## [12913] 33 34 36 37 33 33 38 33 35 33 33 38 37 34 33 32 38 38 38 36 38 34 36 36
## [12937] 43 38 33 45 33 36 36 33 36 36 36 12 34 31 33 36 57 52 36 36 33 33 24 33
## [12961] 33 33 36 36 36 36 36 37 37 33 33 38 37 33 57 57 57 38 35 34 53 32 43 35
## [12985] 35 31 33 36 37 33 37 57 36 47 39 58 43 33 38 35 33 33 37 34 33 37 38 42
## [13009] 33 36 36 36 32 36 37 36 36 36 36 36 36 76 36 36 37 34 33 36 33 33 37 37
## [13033] 36 36 36 36 42 39 39 39 36 36 36 57 32 57 34 34 34 76 38 76 76 38 38 38
## [13057] 38 36 36 33 33 36 36 33 36 36 36 36 36 36 32 43 36 36 36 76 36 36 36 36
## [13081] 37 33 36 57 36 36 37 37 32 33 36 33 33 33 35 37 35 37 53 57 33 35 34 33
## [13105] 33 37 34 33 33 42 47 39 58 36 33 57 33 45 37 33 38 33 35 37 33 38 36 33
## [13129] 36 33 31 33 43 36 57 33 33 24 36 37 25 37 37 35 57 33 57 33 33 54 33 33
## [13153] 37 42 37 34 33 42 39 33 33 45 33 38 37 33 36 38 33 36 43 33 33 33 33 33
## [13177] 43 36 35 39 52 36 37 37 32 33 37 56 57 38 57 33 31 35 34 53 31 32 35 33
## [13201] 35 33 37 33 33 33 34 57 37 34 39 58 54 33 33 38 32 34 35 33 33 33 33 37
## [13225] 38 47 56 33 31 57 32 52 36 45 36 36 52 36 56 52 39 36 36 76 38 36 36 36
## [13249] 36 57 39 43 44 36 36 34 33 33 38 44 34 34 34 36 37 37 38 36 36 36 36 33
## [13273] 33 34 32 32 32 36 36 38 38 37 37 38 33 57 34 38 37 34 32 32 37 43 37 33
## [13297] 42 37 37 37 37 38 33 34 53 53 57 57 33 33 34 34 56 38 38 33 33 33 33 33
## [13321] 38 32 32 32 33 33 33 33 34 34 34 36 37 34 34 36 44 44 44 34 45 34 37 37
## [13345] 42 47 39 39 39 39 58 58 36 36 32 32 43 31 31 33 38 36 43 57 57 57 34 34
## [13369] 34 34 33 34 34 34 34 34 45 52 34 33 33 38 38 38 38 38 33 33 44 33 33 33
## [13393] 35 33 34 33 36 57 38 38 38 38 38 38 34 34 36 36 43 32 32 38 34 33 33 34
## [13417] 35 35 35 36 36 33 33 43 36 33 44 44 36 36 33 38 33 31 31 38 36 36 57 57
## [13441] 42 31 33 33 35 32 32 34 36 36 37 37 34 36 36 36 36 36 36 36 36 36 36 24
## [13465] 24 34 34 34 34 34 34 34 34 37 37 31 31 34 34 43 38 34 34 33 33 33 38 38
## [13489] 44 34 34 77 77 77 77 38 32 57 34 34 36 36 36 36 36 37 32 32 31 31 35 35
## [13513] 37 37 37 37 37 37 37 34 34 42 36 36 36 36 37 37 34 36 36 36 36 36 36 34
## [13537] 34 33 33 33 34 34 47 37 37 37 38 38 33 34 34 34 32 32 33 38 38 38 38 38
## [13561] 36 36 36 36 36 36 36 36 36 36 36 38 34 34 34 36 36 36 36 34 34 34 33 33
## [13585] 33 34 34 34 34 34 34 34 34 36 38 38 33 33 38 45 32 32 32 32 37 32 32 36
## [13609] 36 36 36 36 36 36 54 38 38 38 38 38 38 38 38 38 38 38 38 32 32 32 37 37
## [13633] 37 34 38 34 34 33 33 33 33 32 31 31 37 37 37 33 57 57 32 32 37 37 45 45
## [13657] 45 37 37 37 37 38 38 38 57 57 42 33 38 38 37 37 56 56 56 56 35 35 35 33
## [13681] 57 31 33 33 33 37 37 37 56 56 57 33 33 33 52 45 45 45 45 31 31 31 43 57
## [13705] 57 33 33 33 33 33 34 38 57 57 57 57 57 45 45 45 45 34 34 34 34 33 33 33
## [13729] 34 38 38 38 38 56 56 33 33 33 38 38 76 76 42 34 34 34 35 35 35 37 34 34
## [13753] 34 53 53 31 31 57 57 32 32 32 43 43 43 35 35 35 31 33 33 33 35 35 39 39
## [13777] 31 31 31 31 31 31 33 32 32 32 32 31 36 36 36 36 36 32 32 32 32 32 37 37
## [13801] 52 52 45 33 33 33 33 33 34 55 34 37 37 37 32 32 57 33 33 42 31 31 38 32
## [13825] 32 32 32 33 33 33 56 56 39 39 33 33 33 33 33 33 33 33 45 38 38 34 34 34
## [13849] 34 32 32 34 32 38 38 38 38 38 38 33 34 45 36 36 37 37 37 37 45 37 34 34
## [13873] 34 34 34 38 38 34 38 33 33 33 33 34 34 34 38 37 37 37 31 31 33 32 32 38
## [13897] 36 36 36 36 43 43 33 33 36 36 36 36 32 38 57 38 34 34 37 37 37 38 35 38
## [13921] 33 42 42 42 42 42 42 42 42 47 47 47 47 47 47 47 39 39 39 39 39 39 39 39
## [13945] 39 39 39 39 39 58 58 58 58 58 58 36 36 36 36 36 36 36 36 33 33 33 37 42
## [13969] 33 54 42 34 36 31 31 31 31 34 34 34 33 33 38 33 33 33 33 52 45 45 45 45
## [13993] 45 45 37 45 45 33 57 57 43 43 43 34 57 57 57 57 34 34 34 34 53 53 43 43
## [14017] 33 33 33 32 34 34 57 34 34 34 34 34 34 34 39 37 45 52 33 33 38 38 38 38
## [14041] 34 34 32 37 37 32 32 38 38 38 38 38 38 38 38 38 33 33 33 33 33 33 33 38
## [14065] 38 42 32 32 32 56 56 42 38 38 38 38 38 38 38 38 38 38 56 34 34 32 33 33
## [14089] 33 33 33 38 38 38 38 38 32 32 32 35 35 32 32 36 36 33 33 33 34 34 34 34
## [14113] 33 33 38 32 32 33 33 33 23 23 33 33 33 33 33 33 38 35 35 35 35 35 33 33
## [14137] 38 38 55 55 45 45 34 34 34 34 34 33 33 76 76 33 32 57 24 24 38 38 38 38
## [14161] 38 38 38 38 38 38 38 38 38 38 36 36 38 38 38 38 38 38 38 38 38 38 38 34
## [14185] 38 38 38 32 34 34 34 34 37 37 36 36 36 36 36 36 36 36 36 36 34 38 38 32
## [14209] 38 38 38 38 38 38 38 38 34 34 34 34 34 34 34 33 56 31 34 32 36 36 32 32
## [14233] 33 33 45 32 42 42 34 47 47 38 33 34 38 38 34 36 36 36 36 45 45 56 56 21
## [14257] 33 33 33 33 33 36 36 36 36 36 36 36 36 36 36 36 36 36 32 38 32 33 38 38
## [14281] 38 38 38 38 38 38 38 34 38 38 38 38 38 38 33 36 36 36 36 36 36 36 36 36
## [14305] 36 36 31 31 32 38 57 57 57 57 57 57 57 38 38 34 36 36 36 36 31 31 31 33
## [14329] 42 42 33 31 52 32 32 33 33 38 32 31 31 31 34 34 33 33 34 34 34 34 34 34
## [14353] 33 33 36 36 36 36 36 36 36 36 36 36 36 37 31 36 36 36 36 38 37 35 57 34
## [14377] 36 38 36 36 36 36 37 47 39 58 36 36 38 33 76 38 38 38 36 36 36 36 38 36
## [14401] 36 36 31 34 43 55 36 32 31 35 37 34 23 36 54 38 37 39 31 32 55 34 58 45
## [14425] 57 52 38 38 42 38 32 32 76 38 32 36 52 32 31 34 31 39 36 38 39 36 38 36
## [14449] 37 45 37 38 37 37 33 33 33 34 42 39 33 45 33 36 38 36 33 33 45 33 34 36
## [14473] 45 36 39 31 34 34 36 32 31 35 37 37 34 23 34 32 54 32 31 37 23 31 56 31
## [14497] 57 11 42 53 31 32 43 35 31 23 35 23 39 31 11 32 37 32 33 34 32 31 32 34
## [14521] 47 58 31 45 43 32 45 38 32 38 23 38 11 32 32 23 33 23 38 56 25 31 32 57
## [14545] 23 32 31 36 36 37 37 37 33 34 32 36 33 37 33 33 34 37 36 33 47 39 58 33
## [14569] 33 33 38 33 35 37 34 38 36 33 33 36 33 52 32 36 36 36 36 36 36 36 36 36
## [14593] 36 36 36 36 36 57 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
## [14617] 37 25 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
## [14641] 37 33 33 56 36 36 36 36 36 36 36 36 36 36 36 36 36 38 38 38 38 38 38 42
## [14665] 34 33 37 57 24 37 56 35 37 37 57 57 57 57 33 57 34 35 33 31 33 37 33 36
## [14689] 36 52 45 33 33 37 33 33 37 36 36 36 36 36 36 36 36 42 37 36 35 56 43 57
## [14713] 56 37 37 38 57 36 36 45 34 43 36 36 36 36 36 36 42 39 39 39 39 39 39 39
## [14737] 39 39 39 39 39 58 36 36 36 36 36 36 36 36 36 45 33 25 33 11 36 45 37 38
## [14761] 38 57 34 36 36 36 36 53 34 37 33 33 38 33 35 45 37 33 76 76 36 57 38 38
## [14785] 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38
## [14809] 38 38 38 38 33 33 37 33 35 36 36 36 36 36 36 36 36 36 36 36 36 36 33 36
## [14833] 36 36 36 36 45 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36
## [14857] 36 36 36 34 37 33 36 36 36 36 36 36 36 36 36 36 33 36 36 57 33 36 36 36
## [14881] 36 36 36 36 36 36 36 36 36 36 55 36 37 37 36 36 36 38 37 37 33 36 33 33
## [14905] 33 37 31 37 57 36 36 39 36 33 38 57 43 45 33 38 35 33 76 36 38 36 38 38
## [14929] 36 33 33 36 33 36 33 36 35 35 33 36 36 36 35 35 77 77 45 45 37 37 25 25
## [14953] 37 37 36 36 33 33 57 57 36 36 37 37 37 37 56 56 36 36 42 42 37 37 37 57
## [14977] 57 33 33 53 53 57 57 34 34 35 35 33 33 37 37 43 43 36 36 45 45 54 54 45
## [15001] 45 33 33 54 54 31 31 37 37 37 37 37 37 36 36 42 42 77 77 36 36 34 34 33
## [15025] 33 36 36 42 42 39 39 58 58 45 45 33 33 33 33 57 57 45 45 38 38 35 35 55
## [15049] 55 33 33 36 36 45 45 38 38 38 56 56 36 33 33 37 37 36 36 33 33 36 36 47
## [15073] 47 36 36 36 36 33 33 33 33 31 31 37 37 36 45 45 36 36 57 42 39 45 43 36
## [15097] 36 33 37 33 36 33 36 36 37 33 36 37 33 36 33 36 33 33 37 33 37 35 37 33
## [15121] 37 57 33 35 34 37 36 33 33 37 38 37 33 34 33 36 37 35 42 47 39 58 36 33
## [15145] 37 33 33 45 33 37 38 33 35 33 38 33 38 38 36 33 31 33 33 31 36 33 33 43
## [15169] 36 36 33 33 24 33 36 37 36 37 39 37 38 36 36 36 36 36 36 36 36 47 39 58
## [15193] 76 36 33 36 36 36 36 36 36 36 45 36 36 36 38 36 38 38 43 35 34 36 38 37
## [15217] 36 36 38 38 39 36 38 45 42 36 38 38 36 38 52 36 38 38 36 57 36 36 36 38
## [15241] 36 36 37 38 33 45 37 33 33 45 38 57 37 57 33 37 57 33 52 31 57 33 45 38
## [15265] 35 34 53 32 43 35 31 33 36 37 33 37 32 33 33 56 33 33 34 57 37 34 37 36
## [15289] 38 47 39 58 33 54 42 34 33 43 43 33 36 33 38 33 33 33 33 33 35 33 34 33
## [15313] 24 33 34 37 38 45 33 33 36 36 31 36 38 36 36 37 37 37 33 32 37 33 33 45
## [15337] 37 57 33 57 31 43 57 45 33 35 34 53 31 32 43 35 35 31 36 37 33 33 55 32
## [15361] 33 33 34 77 34 33 37 36 33 42 39 58 33 37 54 34 33 45 43 33 33 38 33 33
## [15385] 33 33 33 34 33 24 33 37 38 56 33 36 31 56 32 36 43 39 36 52 36 36 36 36
## [15409] 36 39 36 36 36 36 36 37 37 36 33 33 37 43 35 37 33 33 33 33 36 39 58 37
## [15433] 33 33 36 36 33 33 52 33 33 36 36 36 33 34 34 37 32 34 34 34 34 37 31 33
## [15457] 38 34 77 35 32 34 36 37 37 35 37 37 37 37 34 34 35 33 45 34 37 37 38 34
## [15481] 32 37 32 38 24 34 34 34 32 32 37 37 32 37 36 32 34 37 37 37 37 34 33 34
## [15505] 34 34 32 37 34 32 37 37 34 37 34 37 37 37 37 37 35 35 37 11 32 38 34 33
## [15529] 34 37 57 57 21 37 45 33 38 33 35 35 31 35 35 39 39 32 11 36 34 32 32 37
## [15553] 38 33 33 11 57 37 32 32 33 33 33 33 34 37 37 37 37 37 37 34 34 34 57 57
## [15577] 44 34 38 34 34 33 33 34 34 37 33 34 34 34 37 33 33 42 42 47 39 39 39 39
## [15601] 39 39 39 39 58 38 37 54 32 32 33 33 33 45 45 34 45 57 37 34 34 33 32 34
## [15625] 34 34 34 34 34 34 34 33 38 38 34 24 38 33 33 33 33 33 38 38 38 38 38 38
## [15649] 38 32 33 11 35 32 34 34 34 34 32 34 35 35 35 37 34 34 33 33 76 52 32 24
## [15673] 38 38 38 11 11 34 34 34 33 34 36 34 34 33 33 34 34 33 35 34 35 32 32 32
## [15697] 37 34 38 76 21 36 33 21 33 36 32 34 38 32 38 38 33 43 36 36 36 31 57 57
## [15721] 57 57 33 36 34 57 36 33 33 24 37 34 32 32 34 36 37 31 34 37 33 33 32 32
## [15745] 36 24 34 34 34 34 34 34 34 34 34 34 31 31 34 35 35 35 33 33 33 33 33 34
## [15769] 35 32 34 34 34 33 36 36 36 37 37 37 32 32 31 31 35 35 37 37 37 37 37 37
## [15793] 34 34 36 23 37 34 35 36 37 37 37 37 32 32 37 33 33 36 36 24 34 34 37 37
## [15817] 32 37 36 36 32 37 37 37 37 37 33 33 34 34 34 37 37 37 34 32 37 37 37 37
## [15841] 37 37 34 37 23 37 37 37 37 37 37 37 37 23 35 35 35 35 35 35 37 23 45 45
## [15865] 34 34 34 33 33 33 37 37 57 57 57 57 57 11 11 11 34 45 34 34 34 34 34 34
## [15889] 34 34 34 34 34 34 34 33 34 38 36 33 34 35 35 35 32 35 35 31 23 35 35 39
## [15913] 39 31 31 31 31 31 31 31 31 31 32 11 11 36 36 32 32 32 32 32 32 33 33 33
## [15937] 33 33 57 37 34 31 31 31 31 31 32 32 32 33 33 33 33 33 33 33 33 33 33 33
## [15961] 33 33 33 33 33 34 34 32 32 32 33 33 37 37 36 37 37 37 37 37 37 37 37 37
## [15985] 35 34 34 34 34 31 31 34 34 34 34 33 33 34 34 34 34 37 32 36 36 33 33 33
## [16009] 32 57 34 34 34 34 34 34 34 34 37 37 37 37 33 33 42 42 47 47 47 47 47 47
## [16033] 47 47 39 39 39 39 39 39 39 39 39 39 39 39 39 39 39 39 39 58 58 58 58 58
## [16057] 58 54 32 33 33 33 45 45 45 45 32 32 45 45 57 32 33 57 57 33 34 34 32 32
## [16081] 31 31 35 35 37 37 34 34 33 37 45 32 34 34 34 34 34 37 37 37 37 34 23 32
## [16105] 32 24 33 33 33 33 33 33 33 38 38 38 38 38 38 38 38 32 32 44 44 11 35 35
## [16129] 32 32 32 34 34 34 32 32 32 23 23 33 35 35 35 35 37 37 37 55 33 33 33 33
## [16153] 33 33 25 54 76 32 38 38 38 38 38 38 38 38 38 38 38 34 11 32 37 34 34 36
## [16177] 36 34 23 33 33 33 33 34 34 23 35 34 32 31 35 32 32 34 33 33 21 31 33 36
## [16201] 36 36 33 33 25 33 33 43 43 43 43 36 36 36 36 36 36 36 36 36 57 57 57 57
## [16225] 57 57 57 57 57 57 57 57 57 34 36 33 33 33 32 23 23 32 32 32 31 31 34 34
## [16249] 31 36 36 31 55 37 24 42 37 37 37 33 37 36 33 37 33 33 33 34 37 37 35 36
## [16273] 36 33 36 39 36 25 33 33 36 33 37 33 57 33 33 37 35 37 33 36 38 33 33 33
## [16297] 33 35 33 37 33 35 33 33 37 34 36 36 36 36 36 36 34 31 31 38 34 31 57 33
## [16321] 33 38 44 34 34 77 38 32 57 34 36 36 32 32 31 31 35 37 37 37 34 34 36 23
## [16345] 34 34 36 36 36 36 36 38 34 36 36 36 34 33 33 33 34 34 34 33 38 32 32 32
## [16369] 32 36 36 54 38 38 38 38 38 38 38 32 37 34 31 37 37 38 38 33 37 56 35 31
## [16393] 37 56 45 45 31 57 44 34 34 38 53 57 38 42 38 38 38 38 33 42 34 34 34 34
## [16417] 35 35 34 53 31 57 32 43 35 35 31 33 23 35 39 31 31 31 31 31 36 32 37 33
## [16441] 44 55 38 32 57 33 42 31 31 32 32 32 34 33 33 56 39 39 33 38 34 32 32 32
## [16465] 33 36 36 37 77 77 34 38 44 44 44 38 38 34 34 38 37 31 31 32 36 38 38 34
## [16489] 34 34 35 38 33 42 42 42 47 39 39 39 39 39 39 58 36 36 36 33 31 34 32 32
## [16513] 32 33 33 45 34 45 45 56 43 32 38 38 57 34 34 53 33 43 43 45 33 32 34 55
## [16537] 57 34 34 39 52 38 34 34 32 37 38 38 33 38 42 32 55 38 38 38 38 38 38 38
## [16561] 34 44 34 44 32 32 38 35 32 38 32 32 56 31 33 38 35 38 38 38 55 33 33 23
## [16585] 76 57 24 38 38 38 38 38 38 38 38 38 38 38 38 38 34 34 37 38 38 32 38 56
## [16609] 56 34 32 36 42 42 34 38 76 38 38 38 33 33 44 36 36 36 36 36 36 32 38 38
## [16633] 38 34 36 36 36 36 31 32 32 38 38 57 38 42 56 36 36 31 42 52 38 32 32 31
## [16657] 31 34 34 33 34 33 36 36 36 36 37 52 52 32 36 36 36 36 36 36 36 24 24 37
## [16681] 37 37 31 34 34 34 53 53 24 24 37 37 43 55 55 24 24 24 24 33 33 44 34 34
## [16705] 23 31 31 33 56 36 36 55 55 36 36 36 36 36 32 33 33 34 34 31 35 37 35 35
## [16729] 37 37 37 33 34 42 36 23 45 34 38 38 37 56 35 35 36 37 37 37 37 37 34 56
## [16753] 31 34 37 37 38 36 36 36 36 36 36 36 33 34 33 33 33 36 34 33 33 36 36 42
## [16777] 34 34 34 36 36 38 38 38 56 56 42 42 36 36 43 54 37 37 38 38 38 24 37 37
## [16801] 34 34 38 47 47 38 38 38 56 37 37 37 33 33 55 31 31 35 35 33 35 35 34 34
## [16825] 43 34 34 23 23 37 37 37 23 56 56 56 56 35 37 37 23 23 37 37 37 38 45 37
## [16849] 37 34 33 53 53 31 34 37 38 38 38 31 31 42 42 38 38 38 36 33 31 31 34 34
## [16873] 34 23 38 38 39 31 31 31 31 33 33 31 37 37 31 36 32 32 32 33 52 52 52 43
## [16897] 33 33 33 42 34 34 38 38 37 37 42 33 21 31 31 32 32 32 33 33 34 34 39 33
## [16921] 33 33 33 33 33 35 32 33 33 33 37 38 24 24 33 75 75 33 55 36 37 37 77 77
## [16945] 42 57 36 33 44 44 36 36 33 33 33 34 34 34 38 38 37 33 33 38 36 36 36 38
## [16969] 38 57 57 37 37 34 38 38 33 42 42 42 42 39 39 39 39 58 58 58 58 77 36 36
## [16993] 33 33 33 33 33 45 45 45 32 32 45 45 33 45 45 45 33 56 56 33 57 57 45 45
## [17017] 38 33 56 45 45 34 34 57 57 57 57 32 34 34 53 37 37 37 57 57 33 36 36 36
## [17041] 32 53 53 56 31 31 35 35 56 37 37 56 34 34 37 56 42 42 45 23 31 31 31 32
## [17065] 32 33 34 34 34 52 31 31 38 38 38 38 33 33 33 23 23 37 38 33 37 23 38 38
## [17089] 38 38 38 42 42 33 33 33 32 33 33 33 35 45 31 31 57 33 45 45 31 31 37 35
## [17113] 35 45 45 34 34 32 56 56 38 33 33 33 33 38 38 33 37 37 38 55 33 34 34 33
## [17137] 33 33 33 33 33 76 76 76 54 54 54 76 76 76 38 38 38 38 33 33 38 38 38 38
## [17161] 34 33 38 32 32 37 34 36 36 36 36 36 36 36 36 36 43 23 23 38 33 33 33 33
## [17185] 23 34 33 33 33 38 38 34 34 33 33 45 38 38 33 33 33 33 33 76 76 31 56 47
## [17209] 25 25 25 36 21 31 31 33 36 36 36 36 42 33 38 38 38 38 38 38 38 38 34 33
## [17233] 38 38 33 33 33 33 34 43 36 36 36 36 36 36 32 57 57 57 57 33 36 36 36 33
## [17257] 55 52 33 33 32 32 33 33 25 25 21 33 34 34 31 31 31 31 34 34 33 33 33 33
## [17281] 31 36 36 36 36 36 36 36 36 37 31 34 34 33 38 36 36 52 33 33 38 34 34 77
## [17305] 35 38 34 33 32 35 45 33 57 33 36 36 36 31 38 38 36 36 33 34 34 32 32 36
## [17329] 36 38 38 38 37 34 32 33 34 38 37 56 37 37 34 34 34 38 56 34 34 34 32 32
## [17353] 32 32 38 52 44 33 33 34 47 39 39 39 39 58 35 36 36 32 33 38 37 37 32 55
## [17377] 34 34 34 34 34 34 34 37 34 38 38 38 38 38 38 38 33 44 38 54 56 38 45 33
## [17401] 38 38 38 38 38 38 33 32 36 44 42 33 44 36 36 36 38 34 38 36 36 33 34 36
## [17425] 36 36 36 36 36 36 57 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 38 38
## [17449] 38 37 37 37 33 37 57 32 34 42 47 39 39 39 58 45 57 45 33 35 76 38 38 38
## [17473] 38 36 36 36 36 36 36 36 36 36 36 36 36 36 36 36 57 36 36 36 36 36 36 36
## [17497] 36 37 56 35 36 32 37 36 35 36 37 37 36 36 36 36 36 36 42 36 38 37 37 43
## [17521] 37 37 37 33 57 34 36 31 33 36 33 33 33 37 37 36 34 33 36 36 53 42 39 58
## [17545] 36 33 57 37 45 37 33 38 38 35 38 33 36 38 38 36 36 36 33 54 52 36 36 36
## [17569] 56 36 33 33 36 36 36 33 36 36 36 36 57 43 42 39 58 45 36 36 36 36 42 39
## [17593] 57 76 43 47 39 58 43 37 33 35 37 57 34 33 36 33 33 33 31 37 35 36 36 37
## [17617] 37 36 36 42 58 33 36 57 37 45 38 43 33 76 38 36 33 36 33 36 36 36 36 33
## [17641] 33 33 57 57 57 38 35 34 32 43 35 33 31 33 36 37 33 37 36 39 58 37 43 33
## [17665] 38 35 33 33 37 34 37 42 33 35 37 37 35 33 33 33 39 58 36 33 33 35 36 38
## [17689] 33 33 43 36
## 30 Levels: 11 12 21 23 24 25 31 32 33 34 35 36 37 38 39 42 43 44 45 47 ... 77
```

```r
as.factor(fisheries$asfis_species_number)
```

```
##     [1] 10903XXXXX    1750100101    17710001XX    2280203101    1480403301   
##     [6] 1702021301    1703926101    2280100117    10801003XX    3210200202   
##    [11] 1703906006    3210900507    1830300701    2290100804    32104001XX   
##    [16] 17037XXXXX    2280101701    10901XXXXX    1210600201    1431300101   
##    [21] 1830204802    1480500401    2294200718    1210506401    1700634503   
##    [26] 1210506601    183XXXXXXX    1470100101    1703923508    17321XXXXX023
##    [31] 1702304801    1721201002    1901000201    17002042XX    11001XXXXX   
##    [36] 17802XXXXX    17023004XX    1620100101    1702307202    199XXXXXXX010
##    [41] 3161000112    2311109002    1830500301    19501001XX    16501XXXXX   
##    [46] 2294200602    17039008XX    17040075XX    1480403202    1060800301   
##    [51] 17039XXXXX    110XXXXXXX    14804028XX    1210501210    1703929301   
##    [56] 17501002XX    17801XXXXX    1703707001    1750600601    16302XXXXX   
##    [61] 10804007XX    6930400701    3161100105    17041007XX    1750400301   
##    [66] 1830509201    1700505801    1750102601    1750100101    1750100205   
##    [71] 1703900803    17710001XX    2280203101    1703926101    10801003XX   
##    [76] 321XXXXXXX    121XXXXXXX020 3210200202    1703900802    2281201810   
##    [81] 2282300303    1830300701    32104001XX    2280101701    10901XXXXX   
##    [86] 1210600201    1431300101    1480500401    2294200718    1210506401   
##    [91] 1700634503    17501023XX018 1702304801    1480400601    1721201002   
##    [96] 17002042XX    17002XXXXX    17023004XX    1620100101    1750102401   
##   [101] 17501XXXXX    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 19501001XX   
##   [106] 16501XXXXX    2294200602    32109XXXXX    22901008XX    17039191XX   
##   [111] 1090100704    1750100601    17039XXXXX    110XXXXXXX    1703919103   
##   [116] 1703907601    1703929301    1703927702    12105012XX    17801XXXXX   
##   [121] 199XXXXXXX054 1750102501    17041007XX    1750400301    1703903303   
##   [126] 1480403401    1750102605    17710001XX    1750102612    1750300507   
##   [131] 1750300505    1080200401    17023XXXXX    1702807101    17038XXXXX   
##   [136] 17002042XX    1750300402    10608002XX    231XXXXXXX    199XXXXXXX010
##   [141] 399XXXXXXX016 32109XXXXX    1520100102    17065XXXXX    17027XXXXX   
##   [146] 199XXXXXXX054 1750300905    1750102501    17032XXXXX    16111XXXXX   
##   [151] 1750300903    17402XXXXX    1750400301    10606006XX    22901001XX   
##   [156] 175XXXXXXX    1750101001    1750102610    1750102605    17023048XX   
##   [161] 12106XXXXX    1750100101    1702326801    17710001XX    1703626303   
##   [166] 1750102612    1703906302    1760300401    1702021301    1703926101   
##   [171] 1703707009    1702300413    1750100201    14313XXXXX    14313XXXXX   
##   [176] 1702304429    17037XXXXX    1702300414    1702300414    32102XXXXX026
##   [181] 32102XXXXX026 2280101701    199XXXXXXX012 17039060XX    1702304442   
##   [186] 183XXXXXXX    17501023XX018 17002042XX    17002XXXXX    17036XXXXX   
##   [191] 17036XXXXX    17802XXXXX    1620100101    1620100101    1703906002   
##   [196] 1750600302    1750600302    1702307202    1750102401    229XXXXXXX   
##   [201] 231XXXXXXX    199XXXXXXX010 199XXXXXXX010 1703710601    16501XXXXX   
##   [206] 16501XXXXX    228XXXXXXX    228XXXXXXX    32109XXXXX    32109XXXXX   
##   [211] 17039191XX    199XXXXXXX013 1760800310    17040075XX    1702304706   
##   [216] 17039XXXXX    110XXXXXXX    110XXXXXXX    1703900807    1703919103   
##   [221] 1703927702    12105012XX    12105012XX    17039033XX    14102XXXXX   
##   [226] 14102XXXXX    1480500419    199XXXXXXX054 199XXXXXXX054 1750102501   
##   [231] 18303XXXXX    1210501305    1703710606    2280203102    1750400301   
##   [236] 17077XXXXX    17077XXXXX    22901001XX    175XXXXXXX    32105XXXXX036
##   [241] 1750101511    17037457XX    1704149903    1211200112    1830305701   
##   [246] 1750102610    2290100108    199XXXXXXX010 30706002XX    17066XXXXX   
##   [251] 17710001XX    2311000201    19001XXXXX    17023XXXXX    2290100108   
##   [256] 1702807101    19009XXXXX    17002XXXXX    17036XXXXX    199XXXXXXX010
##   [261] 17065XXXXX    17039XXXXX    17047XXXXX    199XXXXXXX054 17032XXXXX   
##   [266] 2291504102    16111XXXXX    30706002XX    17402XXXXX    19010XXXXX   
##   [271] 175XXXXXXX    1709345201    1630200204    1750102605    1760301102   
##   [276] 3162301004    3074200701    1831000201    17092XXXXX    17092XXXXX   
##   [281] 1100400132    1100400132    1709201501    1210600206    1090300404   
##   [286] 1431300102    1703707003    1704100703    1480500406    2282900601   
##   [291] 1700225901    3210501003    2280106701    1720900602    1750102601   
##   [296] 1750100101    17802020XX    1750300904    18308046XX    1750102612   
##   [301] 1100403602    1703721002    1780101703    1709441601    1480203001   
##   [306] 1480203001    1702021301    1050200201    1480400801    1720820201   
##   [311] 1210502401    1720928801    1050200502    1100400233    31611020XX   
##   [316] 1707027002    1760801001    3161003801    1750100201    121XXXXXXX020
##   [321] 32104001XX    14313XXXXX    1080201020    17094XXXXX    32102XXXXX026
##   [326] 199XXXXXXX012 11007XXXXX    1100400201    1100400154    1210506602   
##   [331] 148XXXXXXX    14806001XX    14806001XX    1709201906    1709201903   
##   [336] 1703709601    13208XXXXX    1750600302    1709441701    1709201902   
##   [341] 231XXXXXXX    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016
##   [346] 1100400202    14801001XX    16501XXXXX    1709446603    1080400712   
##   [351] 1900800201    32109XXXXX    32109XXXXX    1709243001    1702328301   
##   [356] 1709200702    1480501701    1780100148    1709244001    3160806702   
##   [361] 1100400234    3210400102    1709201502    1709201502    1709201502   
##   [366] 1090100704    1580200101    1120300102    1060800301    11004XXXXX   
##   [371] 110XXXXXXX    110XXXXXXX    110XXXXXXX    1703919103    1480600105   
##   [376] 1100403201    3161000108    1702300411    1060200501    17801XXXXX   
##   [381] 14102XXXXX    3210506001    16302XXXXX    1750102501    1480100101   
##   [386] 1100403601    1750500101    2302012301    1703903301    1709441801   
##   [391] 1480403302    1480500403    2302007001    1703703901    1760300405   
##   [396] 1100400146    1709252901    1703701617    1750400301    1480204001   
##   [401] 1080401103    175XXXXXXX    199XXXXXXX053 32105XXXXX036 1703703802   
##   [406] 1480600104    1700505801    1709243002    1750102610    1100402002   
##   [411] 1702304806    1750300404    17002042XX    199XXXXXXX010 17032XXXXX   
##   [416] 1750101001    1100400118    1750102605    1750102605    1750102605   
##   [421] 16102003XX    17023048XX    17023048XX    12106XXXXX    12106XXXXX   
##   [426] 10903XXXXX    1781103001    17092XXXXX    1709253501    1100400132   
##   [431] 1709201501    699XXXXXXX    699XXXXXXX    699XXXXXXX    699XXXXXXX   
##   [436] 1480500406    3210501003    3161000117    3161000117    1702905102   
##   [441] 1702905102    2290100115    2280100103    2280100103    1700116701   
##   [446] 1700116701    11004002XX    1480600106    1750102612    1750102612   
##   [451] 1750102612    1709637301    1750300507    1709441601    3070300113   
##   [456] 3070300113    1480203001    1480501702    1480501702    1750300505   
##   [461] 2311100401    2311100401    2311100401    1780200301    1780200301   
##   [466] 1780200301    1702021301    1702021301    1702021301    1760801502   
##   [471] 321XXXXXXX    121XXXXXXX020 121XXXXXXX020 121XXXXXXX020 1760801002   
##   [476] 1760801002    17094XXXXX    32102XXXXX026 32102XXXXX026 32102XXXXX026
##   [481] 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 1480601401    1100400201   
##   [486] 689XXXXXXX    2280101606    2280101606    19009XXXXX    19009XXXXX   
##   [491] 19009XXXXX    183XXXXXXX    183XXXXXXX    17809XXXXX    17809XXXXX   
##   [496] 17809XXXXX    148XXXXXXX    148XXXXXXX    148XXXXXXX    307XXXXXXX   
##   [501] 1703710801    1120300101    2280100112    2280100112    2280100112   
##   [506] 2290100203    1702300415    1702300415    14806001XX    1709201906   
##   [511] 1709201906    17002XXXXX    17002XXXXX    17002XXXXX    1080400701   
##   [516] 1080400701    14703004XX    14703004XX    14703004XX    1750300402   
##   [521] 1750300402    1750300402    61841007XX    1620100101    1620100101   
##   [526] 1750102406    1100400212    23020XXXXX    13208XXXXX    10901010XX   
##   [531] 1780202501    1780202501    1750102603    1750102603    1750102603   
##   [536] 1709441701    17501XXXXX    17501XXXXX    17501XXXXX    1709201902   
##   [541] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010
##   [546] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016
##   [551] 399XXXXXXX016 399XXXXXXX016 17503XXXXX    1100400202    22942005XX   
##   [556] 22942005XX    1620100402    1620100402    17070305XX    17070305XX   
##   [561] 17070305XX    16501XXXXX    16501XXXXX    16501XXXXX    1100400203   
##   [566] 1750101503    1750101503    1750101503    14701XXXXX    1709446601   
##   [571] 32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX    1610500202   
##   [576] 1610500202    1090100203    1704700302    1704700302    1480501701   
##   [581] 3210400102    1709201502    1709201502    1709201502    199XXXXXXX013
##   [586] 199XXXXXXX013 199XXXXXXX013 22801001XX    22801001XX    22801001XX   
##   [591] 170XXXXXXX    170XXXXXXX    170XXXXXXX    1580200101    1580200101   
##   [596] 1580200101    3162400201    3162400201    1060800301    17039XXXXX   
##   [601] 17039XXXXX    17039XXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##   [606] 110XXXXXXX    110XXXXXXX    1610201201    1610201201    1610201201   
##   [611] 1480600105    1760800101    1702905101    18302053XX    18302053XX   
##   [616] 10902004XX    31608XXXXX    31608XXXXX    31608XXXXX    17801XXXXX   
##   [621] 17801XXXXX    14102XXXXX    14102XXXXX    14102XXXXX    694XXXXXXX   
##   [626] 693XXXXXXX    17501015XX    17501015XX    17501015XX    199XXXXXXX054
##   [631] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1750300905    1750300905   
##   [636] 1750300905    17015XXXXX    17015XXXXX    17015XXXXX    1750500901   
##   [641] 1750500901    1750500901    1703620904    1703919115    1703919115   
##   [646] 1703919115    1760801004    1760801004    1750102501    1750102501   
##   [651] 1750102501    12314007XX    22915XXXXX    22915XXXXX    22915XXXXX   
##   [656] 1480100101    1620400201    17032XXXXX    17032XXXXX    17032XXXXX   
##   [661] 1750500101    1750500101    1709441801    1480403302    1750102608   
##   [666] 1750102608    1750102608    1703710606    1703710606    1703710606   
##   [671] 1520100103    2290100207    1620400102    1709448001    691XXXXXXX   
##   [676] 1750300903    1750300903    1750300903    1750400301    1750400301   
##   [681] 1750400301    1480204001    17077XXXXX    17077XXXXX    1709243003   
##   [686] 1080401103    1080401103    17092448XX    1709201911    22901001XX   
##   [691] 22901001XX    17071XXXXX    17071XXXXX    175XXXXXXX    175XXXXXXX   
##   [696] 175XXXXXXX    1709447001    32105XXXXX036 32105XXXXX036 32105XXXXX036
##   [701] 32105XXXXX036 1750101001    1750101001    1750101001    17608010XX   
##   [706] 2280100128    1702301127    1702301127    1702301127    1480600104   
##   [711] 17063XXXXX    17063XXXXX    17063XXXXX    1750102610    1750102610   
##   [716] 1750102610    1702304806    2311005001    17023XXXXX    2290100108   
##   [721] 17037XXXXX    17002042XX    17036XXXXX    199XXXXXXX010 1700204220   
##   [726] 32109XXXXX    2312400101    694XXXXXXX    199XXXXXXX054 17032027XX   
##   [731] 30706002XX    17023048XX    17710001XX    17405206XX    1210504001   
##   [736] 2311100401    17023XXXXX    1702222101    17038XXXXX    2291500501   
##   [741] 17809XXXXX    1700420101    1410200606    17041XXXXX    1702315101   
##   [746] 1703933001    2280100120    17002042XX    17036XXXXX    1703922406   
##   [751] 14703004XX    1760401201    17023004XX    61841007XX    1750102406   
##   [756] 1830101805    1704200101    13116XXXXX    1703202702    199XXXXXXX010
##   [761] 1220200101    17046036XX    16501XXXXX    1750101503    14701XXXXX   
##   [766] 1771000104    1703600201    17065XXXXX    3210200229    1703817215   
##   [771] 17039XXXXX    17023231XX    10802XXXXX    1703911802    12105012XX   
##   [776] 1702300101    17015XXXXX    16302XXXXX    1700204284    1703817216   
##   [781] 17032XXXXX    1703930001    1703620708    1703817202    17407001XX   
##   [786] 11005XXXXX    1703620901    1702323101    17033XXXXX    1702317901   
##   [791] 1703620702    1703933006    1706600704    1311600102    1210503801   
##   [796] 1707700601    299XXXXXXX013 199XXXXXXX010 14102XXXXX    17501015XX   
##   [801] 199XXXXXXX054 1750102605    1750300404    1750300904    1750102612   
##   [806] 1750300505    17023XXXXX    1702807101    14704XXXXX    299XXXXXXX013
##   [811] 199XXXXXXX010 399XXXXXXX016 17503XXXXX    17501015XX    199XXXXXXX054
##   [816] 1750102501    17032XXXXX    30706002XX    1750400301    175XXXXXXX   
##   [821] 1750101001    1750102610    1480400202    1830200201    1210500105   
##   [826] 1702300401    1750100205    17801001XX    1710200101    1100400105   
##   [831] 1830506401    121XXXXXXX020 3210200202    1830202405    2282300303   
##   [836] 1830300701    32104001XX    1100400110    10901XXXXX040 2310901006   
##   [841] 1431300101    1830204802    1480500401    2294200718    1830200405   
##   [846] 1700634503    1210506601    3160800309    1780207001    199XXXXXXX007
##   [851] 17802XXXXX    1480401001    1830204504    1480400501    299XXXXXXX013
##   [856] 399XXXXXXX016 1830500301    19501001XX    2294200602    32109XXXXX   
##   [861] 199XXXXXXX008 1090100704    1480401502    1480403203    11004001XX   
##   [866] 1780200403    1480401501    1100400106    1100400109    1100400104   
##   [871] 1100400103    1704100701    1100400102    1780200302    1830509201   
##   [876] 199XXXXXXX053 3070800101    1480403401    1830201102    1705013202   
##   [881] 1750102605    1750102605    1750102605    1750102605    1750102605   
##   [886] 1750102605    16102003XX    1480500406    3210501003    1750300404   
##   [891] 1750300404    1750300904    17710001XX    1480500408    1750102612   
##   [896] 1750102612    1750102612    1750102612    1750102612    1750102612   
##   [901] 1750102612    1750102612    1750300507    1750300507    1750300507   
##   [906] 1750300507    1750300507    1750102404    1750102404    2311005001   
##   [911] 1760300401    1750300505    1750300505    1750300505    1750300505   
##   [916] 1750300505    1750300505    1080200401    1080200401    1080200401   
##   [921] 1080200401    1080200401    16203XXXXX    17023XXXXX    2290100108   
##   [926] 1702300405    1750100201    1750100201    17037XXXXX    1702300414   
##   [931] 32102XXXXX026 1210600201    1210506401    14806XXXXX    17036XXXXX   
##   [936] 14805004XX    1750300402    17023004XX    1750600302    1750300906   
##   [941] 1750300906    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##   [946] 199XXXXXXX010 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
##   [951] 19501001XX    228XXXXXXX    32109XXXXX    32109XXXXX    1610500202   
##   [956] 22901008XX    1480501701    3210400102    1709201502    22801001XX   
##   [961] 22801001XX    1580200101    17039XXXXX    110XXXXXXX    12105012XX   
##   [966] 14102XXXXX    199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1060800201   
##   [971] 1060800201    1060800201    1060800201    1060800201    1750102501   
##   [976] 1750102501    1750102501    1750102501    1750102501    1750102501   
##   [981] 1750102501    1480403302    1750102608    1750102608    1750300903   
##   [986] 1750300903    1750300903    30706002XX    1750400301    1750400301   
##   [991] 1750400301    1750400301    1750400301    1750400301    1480204001   
##   [996] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    32105XXXXX036
##  [1001] 32105XXXXX036 32105XXXXX036 1750101001    1750101001    1750102610   
##  [1006] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [1011] 1750102610    1750102610    1702304605    1705013202    1702309003   
##  [1016] 1750100101    1702326801    1703817204    1750300404    17710001XX   
##  [1021] 1750102612    1703906302    1750300505    1080200401    1703716607   
##  [1026] 1300100501    1210503002    17023XXXXX    1750100201    121XXXXXXX020
##  [1031] 1702222101    1702807101    32102XXXXX026 17039060XX    1210600201   
##  [1036] 183XXXXXXX    14704XXXXX    17501023XX018 1707700109    17002042XX   
##  [1041] 17036XXXXX    11001XXXXX    17802XXXXX    14703004XX    10803XXXXX   
##  [1046] 17023004XX    1750600302    1707700302    1750102401    231XXXXXXX   
##  [1051] 199XXXXXXX010 16501XXXXX    228XXXXXXX    14701XXXXX    17039008XX   
##  [1056] 17039191XX    1750100601    19002XXXXX    110XXXXXXX    1707700401   
##  [1061] 12105012XX    17023043XX    14102XXXXX    199XXXXXXX054 1703707001   
##  [1066] 1060800201    1750102501    17032027XX    17405XXXXX    1750400301   
##  [1071] 17077XXXXX    22901001XX    175XXXXXXX    1750101001    1750101511   
##  [1076] 17037457XX    1704149903    1211200112    1290100304    1750102610   
##  [1081] 17036030XX    1750102605    1750102601    1750300904    1702304431   
##  [1086] 17710001XX    1750102612    1750102612    1750102612    1700204001   
##  [1091] 1750102404    1750102404    1750102604    1750300505    17023XXXXX   
##  [1096] 2290100108    121XXXXXXX020 1702807101    1700211502    1702304801   
##  [1101] 1703202728    17002042XX    1703202733    1750102401    1702304814   
##  [1106] 199XXXXXXX010 17503XXXXX    14701XXXXX    17039XXXXX    1700204225   
##  [1111] 199XXXXXXX054 1750102501    1750102501    1750102501    17032XXXXX   
##  [1116] 1750400301    1080201703    19010XXXXX    22901001XX    175XXXXXXX   
##  [1121] 175XXXXXXX    3160400106    1750101001    1750102610    1750102610   
##  [1126] 1750102610    1703202801    199XXXXXXX010 30706002XX    199XXXXXXX010
##  [1131] 1703701601    1750102605    17023048XX    1760301102    12106XXXXX   
##  [1136] 1090300404    1431300102    1703707003    1480500406    2282900601   
##  [1141] 2280106701    1720900602    1750102601    1750100101    1702326801   
##  [1146] 1702304604    1750300404    2280102201    17802020XX    1210504202   
##  [1151] 1750300904    1470300406    17710001XX    1703639501    18308046XX   
##  [1156] 1702329101    1060600603    1750102612    17011026XX    1703731402   
##  [1161] 1703721002    1950100107    1750102604    1750300505    1702304426   
##  [1166] 1080200401    1702021301    1930100101    1480400801    1720820201   
##  [1171] 17002040XX    1210502401    1210501224    17023XXXXX    2290100108   
##  [1176] 1100100509    1750100201    121XXXXXXX020 1702222101    1702807101   
##  [1181] 32104001XX    17037XXXXX    31607008XX    15802XXXXX    2311101205   
##  [1186] 199XXXXXXX012 14704XXXXX    17501023XX018 17041XXXXX    1703701618   
##  [1191] 17002042XX    17036XXXXX    1704603701    17023044XX    1703701606   
##  [1196] 1750101506    1703709601    17037039XX    1290100302    1703202733   
##  [1201] 1750600302    1750102401    1750300906    17501XXXXX    231XXXXXXX   
##  [1206] 299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 17503XXXXX    14306XXXXX   
##  [1211] 16501XXXXX    1080201011    32109XXXXX    1520100102    17065XXXXX   
##  [1216] 1480501701    199XXXXXXX013 22801001XX    170XXXXXXX    17023047XX   
##  [1221] 19002XXXXX    110XXXXXXX    1700204228    1703919103    2280100119   
##  [1226] 10802XXXXX    1702300411    11002XXXXX    12105033XX    1080300506   
##  [1231] 14102XXXXX    17047XXXXX    31610XXXXX    17501015XX    1750101515   
##  [1236] 199XXXXXXX054 1060800201    1703716603    1080201017    16302XXXXX   
##  [1241] 1620100401    1750102501    1703701607    17032XXXXX    17001025XX   
##  [1246] 1750102608    1703202722    2280100108    2314300113    17405XXXXX   
##  [1251] 1703701632    1750400301    1290200401    1080201703    17016XXXXX   
##  [1256] 3161102502    19010XXXXX    1703402901    22901001XX    175XXXXXXX   
##  [1261] 1750101001    17037016XX    1703703802    1750102610    1702304806   
##  [1266] 1703202801    1750300402    1750102406    199XXXXXXX010 1750102501   
##  [1271] 175XXXXXXX    1750101001    1750102610    1750100101    19001XXXXX   
##  [1276] 2290100108    121XXXXXXX020 1702807101    17002042XX    17023044XX   
##  [1281] 199XXXXXXX010 17503XXXXX    17501015XX    199XXXXXXX054 17032027XX   
##  [1286] 30706002XX    1750400301    175XXXXXXX    1750101001    1750102610   
##  [1291] 1703202801    1750101403    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016
##  [1296] 228XXXXXXX    14309011XX    12105012XX    17023043XX    1705013202   
##  [1301] 1210501106    17023048XX    1830201401    17092XXXXX    1480500406   
##  [1306] 3210501003    1750100101    1750100101    1750100101    1760301104   
##  [1311] 1480400202    1480400202    1830200201    1210500105    1210500105   
##  [1316] 1702300401    1702300401    1750100205    1750100205    1750100205   
##  [1321] 1210502403    1702700301    17801001XX    17801001XX    1710200101   
##  [1326] 1780100112    1170100501    1630200301    1703900801    1480403301   
##  [1331] 1210501107    1702021301    1702021301    1702021301    1703926101   
##  [1336] 1480400801    17603XXXXX    14805004XX034 1702300413    1230400201   
##  [1341] 1230400201    17023XXXXX    1703910701    1702300405    1750100201   
##  [1346] 1750100201    1750100201    121XXXXXXX020 121XXXXXXX020 1830202405   
##  [1351] 1830300701    1100500326    14313XXXXX    17037XXXXX    17037XXXXX   
##  [1356] 17037XXXXX    17037XXXXX    32102XXXXX026 32102XXXXX026 1170100102   
##  [1361] 17039060XX    1950100106    1750100104    1210600201    1210600201   
##  [1366] 1830204802    1480500401    1210506401    1210506401    1210506401   
##  [1371] 1700634503    1210506601    1210506602    199XXXXXXX009 183XXXXXXX   
##  [1376] 1650100102    1650100102    17501023XX018 1470100101    1703923508   
##  [1381] 17321XXXXX023 1650101203    14806001XX    14806001XX    1709201906   
##  [1386] 1709201906    17036XXXXX    1480401001    1480401001    17506XXXXX   
##  [1391] 1750101403    17023004XX    17023004XX    1620100101    23020018XX   
##  [1396] 1580200105    1703906002    1703906002    1750600302    1750600302   
##  [1401] 1650101206    1702307202    1750102401    3210400105    1709244002   
##  [1406] 1709441701    299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 199XXXXXXX010
##  [1411] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [1416] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 1703710601   
##  [1421] 1702300408    3161000112    228XXXXXXX    228XXXXXXX    1480500407   
##  [1426] 2280400203    3210501001    1711501202    32109XXXXX    1702300406   
##  [1431] 1480501701    1709244001    3210400102    1709201502    1709201502   
##  [1436] 199XXXXXXX008 22801001XX    17040075XX    1090100704    1580200101   
##  [1441] 1210501102    17039XXXXX    17039XXXXX    110XXXXXXX    1480400802   
##  [1446] 1704100702    10802XXXXX    14804028XX    1702300411    17608XXXXX   
##  [1451] 1780800401    12105012XX    12105012XX    12105012XX    17039033XX   
##  [1456] 17801XXXXX    1703935301    14102XXXXX    30702018XX    1480500402   
##  [1461] 199XXXXXXX054 1480500404    1760300901    1750600601    1750102501   
##  [1466] 1480100101    17032027XX    1650100128    1709441801    1480500405   
##  [1471] 18303057XX    1210501305    1480403302    1170100105    1170100104   
##  [1476] 3161100105    11701XXXXX    2302007002    1704100701    1750400301   
##  [1481] 1100400102    17033184XX    18304XXXXX    22901001XX    175XXXXXXX   
##  [1486] 175XXXXXXX    175XXXXXXX    1830509201    32105XXXXX036 32105XXXXX036
##  [1491] 32105XXXXX036 17608010XX    17037457XX    1480403401    1750102610   
##  [1496] 1830202404    1750102605    1750102605    1750102601    1750300404   
##  [1501] 1750102612    1750102612    1750100201    199XXXXXXX012 17501023XX018
##  [1506] 1750102401    1750102401    199XXXXXXX010 399XXXXXXX016 32109XXXXX   
##  [1511] 22901008XX    199XXXXXXX013 199XXXXXXX054 1750102501    1750102501   
##  [1516] 1750102501    1750400301    22901001XX    175XXXXXXX    1750101001   
##  [1521] 1750102610    1750102610    3210501003    321XXXXXXX    231XXXXXXX   
##  [1526] 199XXXXXXX010 399XXXXXXX016 228XXXXXXX    694XXXXXXX    175XXXXXXX   
##  [1531] 1705013202    17710001XX    1480500408    1703626303    1703745705   
##  [1536] 1210503002    17023XXXXX    1703745702    14313XXXXX    17037XXXXX   
##  [1541] 32102XXXXX026 1707700109    17002042XX    17036XXXXX    1750600302   
##  [1546] 18301XXXXX    1707700302    231XXXXXXX    199XXXXXXX010 399XXXXXXX016
##  [1551] 22801001XX    17039XXXXX    110XXXXXXX    1707700401    12105012XX   
##  [1556] 14102XXXXX    199XXXXXXX054 17032027XX    1703620919    17077XXXXX   
##  [1561] 18304XXXXX    22901001XX    175XXXXXXX    17037457XX    2281200301   
##  [1566] 1704149903    30703001XX    1480401601    1750102605    1750102605   
##  [1571] 1750102605    1750102605    1210501106    1830201401    1950100103   
##  [1576] 3160700803    2294200701    3160801404    1210501103    12305015XX   
##  [1581] 1830200801    1750102601    1480400202    1830200201    1210500105   
##  [1586] 1750100205    17801001XX    2310901003    1230100401    1630201302   
##  [1591] 3161202001    1480401302    1750300904    1750102612    1750102612   
##  [1596] 1750102612    1750102404    1750102404    3161000105    1080200401   
##  [1601] 3161103702    1230400201    12301010XX    1230100907    1230100903   
##  [1606] 316XXXXXXX    1230100908    2310901004    1230401201    199XXXXXXX009
##  [1611] 183XXXXXXX    183XXXXXXX    1480400212    1830200501    199XXXXXXX007
##  [1616] 1480401001    3160803603    1780700501    1750102401    3210400105   
##  [1621] 1782000301    231XXXXXXX    199XXXXXXX010 399XXXXXXX016 399XXXXXXX016
##  [1626] 649XXXXXXX    228XXXXXXX    1480500407    2280400203    3161107501   
##  [1631] 3210501001    3160904501    32109XXXXX    1480400211    3160700801   
##  [1636] 3161808901    1830200202    1210500107    1780100109    22804002XX   
##  [1641] 199XXXXXXX008 30701001XX    1090100704    1090100704    1230100902   
##  [1646] 1060800301    2312114501    1230400303    1230100909    11004001XX   
##  [1651] 110XXXXXXX    1480400802    1480600401    1780800401    1480401501   
##  [1656] 123XXXXXXX    3161700601    17204002XX    17801XXXXX    694XXXXXXX   
##  [1661] 694XXXXXXX    69302004XX    69302004XX    199XXXXXXX054 1060800201   
##  [1666] 1480500404    1750102501    1750102501    1750102501    1750102501   
##  [1671] 1230100906    3161202002    1700600602    11701XXXXX    11701XXXXX   
##  [1676] 1230400802    1750400301    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [1681] 1480400101    30709003XX    1480400803    1830205003    1830201102   
##  [1686] 17102001XX    1750102610    1750102610    1750102610    1750102610   
##  [1691] 1830202404    199XXXXXXX010 228XXXXXXX    1750102501    1750102610   
##  [1696] 1950100101    1480400202    1210500105    1702300401    1750100205   
##  [1701] 1706300501    1100400105    3161000105    1080200401    1480403301   
##  [1706] 1830506401    316XXXXXXX    3210200202    1830202405    2281201810   
##  [1711] 1830300701    32104001XX    10901XXXXX040 2310901006    1431300101   
##  [1716] 3160700205    1480500401    2294200718    1830200405    1700634503   
##  [1721] 148XXXXXXX    1470100101    1703923508    3160800309    3161102001   
##  [1726] 17802XXXXX    1480401001    1620100101    1830204504    1480400501   
##  [1731] 231XXXXXXX    199XXXXXXX010 399XXXXXXX016 1830500301    16501XXXXX   
##  [1736] 22901008XX    1090100704    1480401502    1060800301    17039XXXXX   
##  [1741] 1480403203    3160800105    11004001XX    1780200403    1480401501   
##  [1746] 1830300704    17204002XX    1100400106    1100400109    1080100301   
##  [1751] 2312100501    1704100701    3070300114    1830509201    1100400112   
##  [1756] 199XXXXXXX053 3070800101    1480403401    1830201102    1700505801   
##  [1761] 1706902102    1750102605    16102003XX    16102003XX    1210600208   
##  [1766] 17092XXXXX    17092XXXXX    1709201501    1709201501    1709201501   
##  [1771] 699XXXXXXX    1210507801    3210501003    1470200201    1750102612   
##  [1776] 1580200103    1709441601    1709441601    1480203001    1080200401   
##  [1781] 2301900301    17603XXXXX    1703616301    17023XXXXX    17096373XX   
##  [1786] 2301900102    3160700203    1480600512    1702300405    2282907303   
##  [1791] 3161000103    2280400501    1720928802    6930401701    3163900103   
##  [1796] 1630200201    3161003801    3161002601    1750100201    316XXXXXXX   
##  [1801] 1230100908    1702807101    1703756501    23019XXXXX    17037038XX   
##  [1806] 17037XXXXX    17094XXXXX    32102XXXXX026 1750100104    11203XXXXX   
##  [1811] 1210506602    3070202301    19009XXXXX    183XXXXXXX    307XXXXXXX   
##  [1816] 3161102401    2130301201    2311001001    14806001XX    14806001XX   
##  [1821] 14806001XX    14806XXXXX    17002XXXXX    1700505802    61841007XX   
##  [1826] 2290100202    3210502301    23020XXXXX    3162403901    1709441701   
##  [1831] 1709441701    231XXXXXXX    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010
##  [1836] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 2310901010   
##  [1841] 14801001XX    14801001XX    1781602205    16501XXXXX    32109XXXXX   
##  [1846] 32109XXXXX    1610500202    1210506702    1720900501    1709200702   
##  [1851] 1480501701    1480501701    1709201502    1709201502    1709201502   
##  [1856] 1709201502    1709201502    22801001XX    3160803003    1707027003   
##  [1861] 1703701604    1090100704    1580200101    1580200101    1120300102   
##  [1866] 17039XXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##  [1871] 110XXXXXXX    1580200102    31608XXXXX    17801XXXXX    17047XXXXX   
##  [1876] 694XXXXXXX    1060800201    1750102501    10804007XX    14315XXXXX   
##  [1881] 1750500101    2302012301    1210501303    1709441801    1480500405   
##  [1886] 1480403302    1480403302    1480500403    1480500403    2302007001   
##  [1891] 1702700302    691XXXXXXX    1750300903    1750400301    3161105503   
##  [1896] 1480204001    31612040XX    175XXXXXXX    32105XXXXX036 17608010XX   
##  [1901] 1750102610    1705013202    2280700903    1480401601    1750102605   
##  [1906] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [1911] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [1916] 1750102605    16102003XX    16102003XX    3210501003    1750102601   
##  [1921] 1750102601    1750102601    1750300404    1750300404    1750300404   
##  [1926] 1750300404    1750300904    1750300904    1750300904    1480500408   
##  [1931] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [1936] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [1941] 1750102612    1750102612    1750300507    1750300507    1750300507   
##  [1946] 1750300507    1750300507    1750300507    1750300507    1750300505   
##  [1951] 1750300505    1750300505    1750300505    1750300505    1750300505   
##  [1956] 1750300505    1750300505    1750300505    1750300505    1750300505   
##  [1961] 1080200401    1080200401    1080200401    1080200401    1080200401   
##  [1966] 1080200401    1080200401    1080200401    1080200401    1080200401   
##  [1971] 1080200401    1080200401    2311100401    17096373XX    321XXXXXXX   
##  [1976] 23111003XX    1702300405    1750100201    1750100201    1750100201   
##  [1981] 17037XXXXX    17037XXXXX    17037XXXXX    1702300414    32102XXXXX026
##  [1986] 32102XXXXX026 32102XXXXX026 1430901102    1211200103    1210600201   
##  [1991] 1210506401    19009004XX    1704614110    183XXXXXXX    1650100102   
##  [1996] 2280100116    148XXXXXXX    2311100404    17002042XX    17036XXXXX   
##  [2001] 17506XXXXX    14805004XX    17023004XX    1210600202    1702300403   
##  [2006] 1210501301    61841007XX    3210502301    1703730304    1750600302   
##  [2011] 1750300906    231XXXXXXX    231XXXXXXX    299XXXXXXX013 199XXXXXXX010
##  [2016] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [2021] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [2026] 399XXXXXXX016 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
##  [2031] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    1703702801   
##  [2036] 228XXXXXXX    228XXXXXXX    1080201011    1080201011    1080201011   
##  [2041] 1080201011    1080201011    1080201011    32109XXXXX    32109XXXXX   
##  [2046] 32109XXXXX    1610500202    1610500202    16204XXXXX    16204XXXXX   
##  [2051] 1210500107    1720400204    1705700701    1705700701    22801001XX   
##  [2056] 17039XXXXX    17039XXXXX    17039XXXXX    12105012XX    17023043XX   
##  [2061] 14102XXXXX    69302004XX    17501015XX    199XXXXXXX054 199XXXXXXX054
##  [2066] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1060800201    1060800201   
##  [2071] 1060800201    1060800201    1060800201    1060800201    1060800201   
##  [2076] 1060800201    1060800201    1060800201    1950100105    1703756101   
##  [2081] 17603009XX    1750102501    1750102501    1750102501    1750102501   
##  [2086] 17032XXXXX    1650100204    1750102608    2280104302    22501XXXXX   
##  [2091] 1750300903    1750300903    1750300903    1750300903    1750300903   
##  [2096] 1750300903    1750300903    1750400301    1750400301    1750400301   
##  [2101] 1750400301    1750400301    1750400301    1750400301    1750400301   
##  [2106] 1750400301    1750400301    1750400301    1750400301    17033184XX   
##  [2111] 17077XXXXX    17016XXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [2116] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    32105XXXXX036
##  [2121] 32105XXXXX036 32105XXXXX036 32105XXXXX036 1704149903    1703730305   
##  [2126] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [2131] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [2136] 1750102610    1750102610    17011026XX    17603XXXXX    17037XXXXX   
##  [2141] 32102XXXXX026 17041251XX    17002XXXXX    17506XXXXX    1760401201   
##  [2146] 17023044XX    17038155XX    13116XXXXX    231XXXXXXX    199XXXXXXX010
##  [2151] 399XXXXXXX016 228XXXXXXX    1760802001    14309011XX    17039XXXXX   
##  [2156] 12105012XX    17023043XX    17501015XX    199XXXXXXX054 1703919115   
##  [2161] 1210502902    17032XXXXX    12106050XX    17033184XX    17016XXXXX   
##  [2166] 18304XXXXX    22901001XX    175XXXXXXX    32105XXXXX036 299XXXXXXX013
##  [2171] 199XXXXXXX010 399XXXXXXX016 228XXXXXXX    17023048XX    1750102612   
##  [2176] 1750102612    1750102404    1750102404    1700204010    2290100108   
##  [2181] 316XXXXXXX    316XXXXXXX    121XXXXXXX020 121XXXXXXX020 17037038XX   
##  [2186] 17037XXXXX    199XXXXXXX012 199XXXXXXX012 1750100104    183XXXXXXX   
##  [2191] 307XXXXXXX    2290100116    17002XXXXX    17002XXXXX    17036XXXXX   
##  [2196] 17023044XX    17023044XX    17037039XX    2282907201    1290100302   
##  [2201] 1703202733    1650100112    3160700802    231XXXXXXX    231XXXXXXX   
##  [2206] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 17046XXXXX   
##  [2211] 17046XXXXX    16501XXXXX    16501XXXXX    1700204220    228XXXXXXX   
##  [2216] 228XXXXXXX    32109XXXXX    1210601503    2280102202    1750101509   
##  [2221] 1210504201    1480500414    22801001XX    1703701604    110XXXXXXX   
##  [2226] 14102XXXXX    14102XXXXX    17501015XX    1750102501    1750102501   
##  [2231] 1750102501    10804007XX    10804007XX    17032027XX    17032XXXXX   
##  [2236] 17001025XX    17001025XX    1703202722    1700204222    30706002XX   
##  [2241] 1750400301    1290200401    17077XXXXX    175XXXXXXX    175XXXXXXX   
##  [2246] 32105XXXXX036 32105XXXXX036 17608010XX    2280100129    1703202720   
##  [2251] 1750102610    1750102610    1750102610    1703202801    1705013202   
##  [2256] 1750102605    12106XXXXX    17710001XX    1750102612    1750300507   
##  [2261] 1750300505    17023XXXXX    17023XXXXX    1750100201    1210600201   
##  [2266] 1210506401    1702304442    1704614110    183XXXXXXX    17501023XX018
##  [2271] 14805004XX    17501014XX    1750300402    17023004XX    1750102406   
##  [2276] 1703906002    1750600302    1750102603    199XXXXXXX010 199XXXXXXX010
##  [2281] 399XXXXXXX016 228XXXXXXX    17039XXXXX    12105012XX    12105012XX   
##  [2286] 14102XXXXX    17501015XX    199XXXXXXX054 1750102501    1703620919   
##  [2291] 1750400301    17077XXXXX    22901001XX    175XXXXXXX    1750101001   
##  [2296] 1290100304    1750102610    1703626303    1703626303    14805004XX034
##  [2301] 1702300413    14313XXXXX    14313XXXXX    17037XXXXX    17037XXXXX   
##  [2306] 17039060XX    17002042XX    17023004XX    1580200105    199XXXXXXX010
##  [2311] 199XXXXXXX010 12105012XX    199XXXXXXX054 199XXXXXXX054 17077XXXXX   
##  [2316] 18304XXXXX    18304XXXXX    17037457XX    1702304605    1705013202   
##  [2321] 1750100101    1702326801    17710001XX    1580200502    1703626303   
##  [2326] 1750102612    1760300401    1703716607    1210503002    1703707009   
##  [2331] 1750100201    3210900507    14313XXXXX    17037XXXXX    1702300414   
##  [2336] 32102XXXXX026 2280101701    17039060XX    14704XXXXX    1707700109   
##  [2341] 17002042XX    17036XXXXX    10803XXXXX    17023044XX    1750600302   
##  [2346] 1707700302    1210501217    231XXXXXXX    199XXXXXXX010 199XXXXXXX010
##  [2351] 16501XXXXX    22801001XX    110XXXXXXX    1703900807    10802XXXXX   
##  [2356] 1210501210    1707700401    12105012XX    14102XXXXX    1950100105   
##  [2361] 1750102501    17032027XX    18303XXXXX    1703620919    1703710606   
##  [2366] 18304XXXXX    22901001XX    175XXXXXXX    17037457XX    1211200112   
##  [2371] 1750102610    1750102605    1750102605    1750102605    1750102605   
##  [2376] 16102003XX    16102003XX    1750102612    1750102612    1750102612   
##  [2381] 1750300507    1750300507    1620400701    1750300505    1750300505   
##  [2386] 1750300505    1760801502    16203XXXXX    17096373XX    14704XXXXX   
##  [2391] 17002042XX    1750300402    1750300402    17023044XX    299XXXXXXX013
##  [2396] 199XXXXXXX010 399XXXXXXX016 17503XXXXX    16501XXXXX    32109XXXXX   
##  [2401] 1610500202    16204XXXXX    1750102602    69302004XX    199XXXXXXX054
##  [2406] 199XXXXXXX054 199XXXXXXX054 1750300905    1750300905    1750102501   
##  [2411] 1750102501    1750102501    1620400201    1250300801    17032027XX   
##  [2416] 1620400102    1750300903    1750300903    1750300903    1750400301   
##  [2421] 1750400301    1750400301    1600200101    1750102610    1750102610   
##  [2426] 1750102610    31604001XX    1750300904    1750102612    1750102612   
##  [2431] 1750102404    2290100108    121XXXXXXX020 1702807101    1702807101   
##  [2436] 2280100123    17002XXXXX    17002XXXXX    1750300402    231XXXXXXX   
##  [2441] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 17503XXXXX    17503XXXXX   
##  [2446] 228XXXXXXX    32109XXXXX    22801XXXXX027 22801001XX    22801001XX   
##  [2451] 199XXXXXXX054 199XXXXXXX054 1750300905    1060800201    1080201017   
##  [2456] 1080201017    1750102501    1750102501    17032XXXXX    17032XXXXX   
##  [2461] 1750300903    30706002XX    1750400301    1750400301    22901001XX   
##  [2466] 175XXXXXXX    175XXXXXXX    32105XXXXX036 1750102610    1750102610   
##  [2471] 2280100104    1750102605    1703903302    699XXXXXXX    1750102601   
##  [2476] 1750100101    1750100205    1703900803    1630200301    1780100901   
##  [2481] 1703906302    1703900801    1704007501    1480403301    1703926101   
##  [2486] 1706300506    10801003XX    321XXXXXXX    1750100201    316XXXXXXX   
##  [2491] 1700206101    3210200202    1703906006    1702807101    1100700801   
##  [2496] 3210900507    1703900802    1830300701    2290100804    1703903305   
##  [2501] 32102XXXXX026 2280101701    10901XXXXX    689XXXXXXX    1210600201   
##  [2506] 1771000101    1431300101    3160700205    1830204802    1480500401   
##  [2511] 2294200718    1210506401    1700634503    1210506601    3210400109   
##  [2516] 183XXXXXXX    14804006XX    17501023XX018 148XXXXXXX    1470100101   
##  [2521] 1703923508    3160800311    1702304801    1721201002    3161102001   
##  [2526] 17002XXXXX    17802XXXXX    32109024XX    17023004XX    1620100101   
##  [2531] 1702307202    1750102401    299XXXXXXX013 199XXXXXXX010 649XXXXXXX   
##  [2536] 1703710601    1430600701    3161000112    1630200302    1830500301   
##  [2541] 19501001XX    16501XXXXX    3160400103    2294200602    1704007502   
##  [2546] 17040075XX    1090100704    110XXXXXXX    1704100702    1703919103   
##  [2551] 1780100902    1210501210    1703907601    1703929301    1703927702   
##  [2556] 17039033XX    31608XXXXX    17501002XX    17801XXXXX    1703903307   
##  [2561] 1750600601    16302XXXXX    3161100601    1080400713    2312100501   
##  [2566] 2250100102    1721335202    1704100701    1750400301    1830509201   
##  [2571] 32105XXXXX036 3161102701    1703903303    1480403401    1750102605   
##  [2576] 1750102605    1750102605    1210501106    1830201401    1950100103   
##  [2581] 1210501103    12106XXXXX    1703906010    1210507801    1480500406   
##  [2586] 3210501003    12305015XX    1750102601    1750100101    1760301104   
##  [2591] 1480400202    1830200201    1210500105    1750100205    17801001XX   
##  [2596] 1750300404    1750300404    1210504202    1750300904    1750300904   
##  [2601] 1480500408    1750102612    1750102612    1750102612    2311005001   
##  [2606] 1750102604    1760300401    1760300401    2311101202    1750300505   
##  [2611] 1750300505    14805004XX034 1702300413    1230400201    2290100108   
##  [2616] 1703745702    1702300405    1702300405    1750100201    1750100201   
##  [2621] 1750100201    316XXXXXXX    1702807101    14313XXXXX    17037XXXXX   
##  [2626] 15802XXXXX    199XXXXXXX012 1950100106    10901XXXXX    1210600201   
##  [2631] 1210506401    183XXXXXXX    183XXXXXXX    183XXXXXXX    1650100102   
##  [2636] 14704XXXXX    148XXXXXXX    148XXXXXXX    307XXXXXXX    1830200501   
##  [2641] 199XXXXXXX007 17002042XX    17002042XX    17036XXXXX    17036XXXXX   
##  [2646] 17036XXXXX    1480401001    1320801601    17023004XX    17023044XX   
##  [2651] 17023044XX    1580200105    1703202733    1703906002    1750600302   
##  [2656] 1750600302    1750102401    1750102401    3210400105    17501XXXXX   
##  [2661] 17501XXXXX    3160700802    231XXXXXXX    299XXXXXXX013 299XXXXXXX013
##  [2666] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [2671] 17046XXXXX    16501XXXXX    1700204220    228XXXXXXX    2280100105   
##  [2676] 2280400203    3210501001    199XXXXXXX008 199XXXXXXX013 199XXXXXXX013
##  [2681] 22801001XX    1700240505    1090100704    17039034XX    17039XXXXX   
##  [2686] 17039XXXXX    17039XXXXX    17039XXXXX    11004001XX    110XXXXXXX   
##  [2691] 1700204228    1480400802    1702300411    1210501210    1480401501   
##  [2696] 12105012XX    12105033XX    17801XXXXX    17501015XX    1480500402   
##  [2701] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1703707001   
##  [2706] 1480500404    1750102501    1750102501    1750102501    17505XXXXX   
##  [2711] 17032027XX    17032XXXXX    17032XXXXX    17032XXXXX    1210501303   
##  [2716] 1480500405    18303057XX    1703710606    1703202722    30706002XX   
##  [2721] 1830804606    1750400301    1750400301    175XXXXXXX    1480400101   
##  [2726] 32105XXXXX036 32105XXXXX036 32105XXXXX036 17608010XX    1480400803   
##  [2731] 1830201102    17102001XX    1750102610    1750102610    1830202404   
##  [2736] 1703202801    1750102605    1750100101    1750102612    1750102301   
##  [2741] 1750102401    199XXXXXXX010 1750102501    30706002XX    1750102610   
##  [2746] 1750102605    1703903302    1750102601    1750100101    1703900803   
##  [2751] 17710001XX    1750102612    1750102612    1703906302    1703900801   
##  [2756] 1704007501    1510200104    1703926101    1703700921    1750100201   
##  [2761] 1750100201    1700206101    3210200202    3210200202    1703906006   
##  [2766] 1703900802    2290100804    1703903305    2280101701    10901XXXXX   
##  [2771] 1700204201    1210600201    1210600201    1431300101    1480500401   
##  [2776] 1210506401    1210506401    1700634503    3210400109    17501023XX018
##  [2781] 1470100101    1703923508    1702304801    17002042XX    17002XXXXX   
##  [2786] 17802XXXXX    14805004XX    17023004XX    17023004XX    17023044XX   
##  [2791] 1620100101    1750600302    1750102401    13116XXXXX    299XXXXXXX013
##  [2796] 199XXXXXXX010 199XXXXXXX010 1430600701    2291504101    19501001XX   
##  [2801] 16501XXXXX    32109XXXXX    32109XXXXX    1750500701    1700206102   
##  [2806] 22901008XX    1706505506    199XXXXXXX013 22801001XX    17040075XX   
##  [2811] 17039XXXXX    17039XXXXX    110XXXXXXX    1704100702    1703919103   
##  [2816] 1703907601    1703929301    1703927702    12105012XX    17039033XX   
##  [2821] 17801XXXXX    199XXXXXXX054 1703707001    1900200505    1750102501   
##  [2826] 1750102501    17407001XX    11005XXXXX    1704100701    17041007XX   
##  [2831] 1750400301    175XXXXXXX    175XXXXXXX    175XXXXXXX    32105XXXXX036
##  [2836] 1700204202    1703903303    17063XXXXX    1700505801    1750102610   
##  [2841] 1750102610    1705013202    1750102605    1750100101    1702326801   
##  [2846] 1750300404    1750300904    17710001XX    1580200502    1703626303   
##  [2851] 1750102612    17011026XX    1760300401    1750300505    1703745705   
##  [2856] 1300100501    1210503002    17023XXXXX    1703745702    1750100201   
##  [2861] 121XXXXXXX020 14313XXXXX    17037XXXXX    32102XXXXX026 1750102301   
##  [2866] 11001XXXXX    17802XXXXX    10803XXXXX    17023044XX    1750600302   
##  [2871] 1702307202    1707700302    1750102401    17501XXXXX    1210501217   
##  [2876] 231XXXXXXX    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 1703710601   
##  [2881] 14701XXXXX    32109XXXXX    17039008XX    22801001XX    17039XXXXX   
##  [2886] 110XXXXXXX    10802XXXXX    1210501210    12105012XX    17023043XX   
##  [2891] 14102XXXXX    199XXXXXXX054 1060800201    1750102501    17032027XX   
##  [2896] 1703620919    1750400301    17016XXXXX    18304XXXXX    22901001XX   
##  [2901] 175XXXXXXX    1750101001    1750101511    17037457XX    1704149903   
##  [2906] 1211200112    1700204202    1750102610    1830201401    1950100101   
##  [2911] 699XXXXXXX    12305015XX    1750102601    1480400202    1830200201   
##  [2916] 1830200201    1210500105    1702300401    1750100205    1702700301   
##  [2921] 1230100401    1230100401    1710200101    1780100112    1780100112   
##  [2926] 1480400502    3161000105    1080200401    1100400101    1480403301   
##  [2931] 1620300201    1830506401    1230400201    316XXXXXXX    1400200201   
##  [2936] 1830202405    3162300203    2281201810    2282300303    1830300701   
##  [2941] 1400201601    1100400110    32102XXXXX026 2310901006    1711500401   
##  [2946] 1210600201    6930401401    3160700205    1830204802    1480500401   
##  [2951] 2294200718    1210506401    1830200405    1700634503    1230400301   
##  [2956] 1210506601    1231200102    199XXXXXXX009 1400200102    1470100101   
##  [2961] 17321XXXXX023 1780100101    1721201002    1830200501    1830200501   
##  [2966] 1780207001    199XXXXXXX007 199XXXXXXX007 1480401001    1830204504   
##  [2971] 1480400501    1782000301    231XXXXXXX    299XXXXXXX013 1830500301   
##  [2976] 16501XXXXX    2280400203    2280400203    3210501001    2294200602   
##  [2981] 1480403201    30701001XX    1090100704    1480401502    1060800301   
##  [2986] 1480403203    1120100301    1230100909    11004001XX    1400201801   
##  [2991] 1480600401    1480401501    17204002XX    31608XXXXX    1230100402   
##  [2996] 3161202005    2312100501    691XXXXXXX    11701XXXXX    1704100701   
##  [3001] 1400200701    1100400102    1500100101    1080401103    1780200302   
##  [3006] 1830509201    1480400101    199XXXXXXX053 3070800101    1480403401   
##  [3011] 1830201102    17710001XX    17023XXXXX    1702222101    17038XXXXX   
##  [3016] 17002042XX    299XXXXXXX013 199XXXXXXX010 16501XXXXX    17501015XX   
##  [3021] 199XXXXXXX054 17032XXXXX    22901001XX    175XXXXXXX    32105XXXXX036
##  [3026] 1750100101    1750300404    1750102612    1750102604    1750300505   
##  [3031] 1702807101    1750101506    199XXXXXXX010 1750102501    1750400301   
##  [3036] 175XXXXXXX    1750101001    1750102610    1750102605    17023048XX   
##  [3041] 1750300404    1210504202    17710001XX    1750102604    1750300505   
##  [3046] 1702304426    1300100501    17023XXXXX    2290100108    1750101508   
##  [3051] 1702807101    3210900507    32104001XX    17041XXXXX    17002042XX   
##  [3056] 17036XXXXX    17023044XX    1750101506    3160700802    231XXXXXXX   
##  [3061] 199XXXXXXX010 399XXXXXXX016 17046XXXXX    16501XXXXX    14701XXXXX   
##  [3066] 1070300901    17065XXXXX    22801001XX    17023047XX    17039034XX   
##  [3071] 110XXXXXXX    1700204228    12105033XX    1750102501    17032XXXXX   
##  [3076] 17001025XX    1703202722    16111XXXXX    30706002XX    1290200401   
##  [3081] 19010XXXXX    175XXXXXXX    1750101001    17037016XX    1703910202   
##  [3086] 17063XXXXX    1750102610    1703202801    1750102605    17023048XX   
##  [3091] 31604071XX    1210600208    1060600603    1750102612    1750102612   
##  [3096] 1750102612    1750300507    1750300507    1750102404    1750102404   
##  [3101] 1750300505    1750300505    1080200401    2280100110    1080400707   
##  [3106] 17603XXXXX    1101001505    17023XXXXX    1702300405    1750100201   
##  [3111] 316XXXXXXX    1702807101    17037XXXXX    2280100123    15802XXXXX   
##  [3116] 199XXXXXXX012 17501023XX018 1100800702    2290100116    17002XXXXX   
##  [3121] 17036XXXXX    17802XXXXX    17506XXXXX    10803XXXXX    1750300402   
##  [3126] 3210502301    1210602005    1100500320    2310300302    231XXXXXXX   
##  [3131] 199XXXXXXX010 17503XXXXX    1771000108    16501XXXXX    32109XXXXX   
##  [3136] 1210601503    1090300406    1702326802    1510200101    3160700801   
##  [3141] 1750101509    1740526702    1210504201    1703402902    1060600602   
##  [3146] 22801001XX    1702304609    110XXXXXXX    1210503101    10802XXXXX   
##  [3151] 1080300506    14102XXXXX    694XXXXXXX    31610XXXXX    69302004XX   
##  [3156] 199XXXXXXX054 1060800201    1702304303    1080201017    1750102501   
##  [3161] 1750102501    1750102501    1080300501    10804007XX    17505XXXXX   
##  [3166] 17032027XX    17001025XX    1210501303    1480500405    1750100102   
##  [3171] 1750100102    1750300903    30706002XX    1750400301    10606006XX   
##  [3176] 17016XXXXX    2280100301    175XXXXXXX    175XXXXXXX    32105XXXXX036
##  [3181] 31611XXXXX    1750101001    2280100129    2280100111    1750102610   
##  [3186] 1750102610    1750102610    2280100104    1703903302    1750102601   
##  [3191] 17710001XX    17710001XX    2311100401    1702021301    1703926101   
##  [3196] 1210600703    1750100201    1703906006    1704603611    1830300701   
##  [3201] 32104001XX    32102XXXXX026 32102XXXXX026 199XXXXXXX012 689XXXXXXX   
##  [3206] 17038XXXXX    1210600201    1480500401    1700634503    183XXXXXXX   
##  [3211] 1650100102    1703923508    17041XXXXX    1700204219    1780207001   
##  [3216] 17002042XX    17002042XX    17002XXXXX    1750101403    17023044XX   
##  [3221] 1750102406    1703910501    1750600302    1750600302    1750102401   
##  [3226] 13116XXXXX    13116XXXXX    231XXXXXXX    231XXXXXXX    199XXXXXXX010
##  [3231] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 1703710601   
##  [3236] 1703710601    1702300408    1703620703    16501XXXXX    16501XXXXX   
##  [3241] 1750101503    228XXXXXXX    228XXXXXXX    228XXXXXXX    14701013XX   
##  [3246] 32109XXXXX    17065XXXXX    17039XXXXX    1703919103    2250100402   
##  [3251] 1210503101    1210503101    1703929301    12105012XX    12105012XX   
##  [3256] 17023043XX    14102XXXXX    199XXXXXXX054 199XXXXXXX054 16302XXXXX   
##  [3261] 16302XXXXX    1703817207    17032XXXXX    1703817226    17407001XX   
##  [3266] 17407001XX    1700634501    1703620901    17041007XX    17033184XX   
##  [3271] 19010XXXXX    22901001XX    175XXXXXXX    1703903303    1700255701   
##  [3276] 1750102612    1750102612    1750300507    1750300505    2280100110   
##  [3281] 17037XXXXX    2280100123    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016
##  [3286] 22801XXXXX027 2301900101    22801001XX    17023043XX    14102XXXXX   
##  [3291] 199XXXXXXX054 1750102501    1750102501    17032XXXXX    22901001XX   
##  [3296] 32105XXXXX036 2280100111    1750102610    1750102610    2280100104   
##  [3301] 1750102612    1750100201    121XXXXXXX020 199XXXXXXX012 183XXXXXXX   
##  [3306] 1750102301    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 199XXXXXXX013
##  [3311] 199XXXXXXX054 1750102501    175XXXXXXX    1750101001    1750102610   
##  [3316] 17066XXXXX    17710001XX    17405206XX    17011026XX    17023XXXXX   
##  [3321] 1702222101    32102XXXXX026 17038XXXXX    17809XXXXX    17041251XX   
##  [3326] 17002042XX    17002XXXXX    17036XXXXX    11001XXXXX    1830700101   
##  [3331] 1750101403    1750300402    1750102406    18301XXXXX    13116XXXXX   
##  [3336] 1750102603    199XXXXXXX010 1220200101    1703620703    16501XXXXX   
##  [3341] 1750101503    14701XXXXX    17065XXXXX    22801001XX    17035XXXXX   
##  [3346] 17039XXXXX    23111004XX    17023231XX    10802XXXXX    12105012XX   
##  [3351] 14102XXXXX    199XXXXXXX054 1703620904    17032XXXXX    17405XXXXX   
##  [3356] 17407001XX    22901XXXXX    17402XXXXX    17033184XX    19010XXXXX   
##  [3361] 175XXXXXXX    1703933006    32105XXXXX036 17063XXXXX    2280400205   
##  [3366] 1702304605    16102003XX    1830201401    1830201401    1950100103   
##  [3371] 1090300401    17092XXXXX    1210600206    1480500406    3210501003   
##  [3376] 1750100101    1750100101    1702326801    1702326801    1480400202   
##  [3381] 1480400202    1830200201    1210500105    1210500105    1702300401   
##  [3386] 1750100205    1750100205    17801001XX    17801001XX    1230100401   
##  [3391] 1710200101    1231400701    17710001XX    1780100112    1703626303   
##  [3396] 1703626303    1090101901    1090101901    1750601201    1701300701   
##  [3401] 1760300401    1760300401    1480400502    1480403301    1702021301   
##  [3406] 1702021301    1300100501    14805004XX034 1702300413    1230400201   
##  [3411] 1230400201    17023XXXXX    1702300405    1750100201    1750100201   
##  [3416] 1750100201    1750100201    1400200201    17037XXXXX    1400201601   
##  [3421] 32102XXXXX026 32102XXXXX026 14002XXXXX    2280101701    17039060XX   
##  [3426] 10901XXXXX    1711500401    1210600201    1830204802    1210506401   
##  [3431] 1230400301    1210506601    1231200102    199XXXXXXX009 199XXXXXXX009
##  [3436] 183XXXXXXX    183XXXXXXX    1400200102    17501023XX018 148XXXXXXX   
##  [3441] 1470100101    1702300415    1830200501    1830200501    1090100201   
##  [3446] 14806001XX    17036XXXXX    17036XXXXX    17802XXXXX    17802XXXXX   
##  [3451] 1480401001    1480401001    17023004XX    17023044XX    1580200105   
##  [3456] 1703906002    1703906002    1750600302    1750600302    1702307202   
##  [3461] 18301XXXXX    1750102401    1090101602    1510300401    1709244002   
##  [3466] 17501XXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [3471] 399XXXXXXX016 16501XXXXX    2280400203    2280400203    3210501001   
##  [3476] 32109XXXXX    32109XXXXX    1400202001    1780100109    1709200702   
##  [3481] 1480501701    3210400102    1709201502    1580200101    17023047XX   
##  [3486] 17023047XX    17039XXXXX    1090101601    1120100301    1230100909   
##  [3491] 11004001XX    11004001XX    11004001XX    110XXXXXXX    110XXXXXXX   
##  [3496] 1480400802    1020100201    1400201801    1480600103    1480600103   
##  [3501] 1210501210    1480600401    1480600401    1400201901    1480401501   
##  [3506] 1480401501    12105012XX    12105012XX    14102XXXXX    17047XXXXX   
##  [3511] 1020100101    1230100402    1480500402    199XXXXXXX054 199XXXXXXX054
##  [3516] 1060800201    1480500404    1750102501    1750500101    1210501303   
##  [3521] 18303057XX    1480403302    1480204001    1400200701    1480402801   
##  [3526] 1500100101    19010XXXXX    19010XXXXX    175XXXXXXX    199XXXXXXX053
##  [3531] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 1400209701   
##  [3536] 1750101511    17037457XX    17037457XX    1400233301    1480400803   
##  [3541] 1480400803    1480403401    1830205003    1830201102    17102001XX   
##  [3546] 17102001XX    1750102610    1830202404    121XXXXXXX020 199XXXXXXX010
##  [3551] 399XXXXXXX016 228XXXXXXX    199XXXXXXX054 17092XXXXX    1480500406   
##  [3556] 3210501003    1480203001    17603XXXXX    1709100301    3161000103   
##  [3561] 1210506602    3210603301    14806001XX    61841007XX    1709244002   
##  [3566] 1709441701    199XXXXXXX010 1709200702    1480501701    3160806702   
##  [3571] 3210400102    1709201502    1709441702    1580200101    110XXXXXXX   
##  [3576] 1480600105    3210506001    199XXXXXXX054 16302XXXXX    1750102701   
##  [3581] 2302012301    1480403302    1480500403    2294200901    2301900206   
##  [3586] 1480204001    16102003XX    1830201401    1830201401    1950100101   
##  [3591] 12305015XX    1750102601    1480400202    1480400202    1830200201   
##  [3596] 1830200201    1210500105    1702300401    1750100205    17801001XX   
##  [3601] 17801001XX    1230100401    1230100401    1710200101    1231400701   
##  [3606] 1780100112    1750102612    1709637301    1750601201    1480400502   
##  [3611] 1480400502    1480403301    1230400201    1702300405    1750100201   
##  [3616] 1830202405    1520400203    10901XXXXX    3210505801    1480500401   
##  [3621] 1830200405    1210506601    183XXXXXXX    183XXXXXXX    148XXXXXXX   
##  [3626] 148XXXXXXX    1780100101    1480400601    1480400212    1480400212   
##  [3631] 1830200501    1830200501    1780207001    199XXXXXXX007 199XXXXXXX007
##  [3636] 1480401001    1480401001    13208XXXXX    1090100803    1830204504   
##  [3641] 1480400501    1782000301    1782000301    231XXXXXXX    199XXXXXXX010
##  [3646] 14802XXXXX    2280400203    2280400203    3210501001    2294200602   
##  [3651] 1480403201    1711501202    1520100102    1610500202    1090100704   
##  [3656] 1480401502    1060800301    1060800301    1090101601    3160800105   
##  [3661] 11004001XX    11004001XX    1480600401    1480600401    1480401501   
##  [3666] 1480401501    17204002XX    69302004XX    199XXXXXXX054 1250203001   
##  [3671] 1750400301    1830509201    1480400101    1480400101    3070800101   
##  [3676] 1480400803    1480403401    1830201102    1830201102    17102001XX   
##  [3681] 17102001XX    1750102610    1750102605    31604071XX    699XXXXXXX   
##  [3686] 17710001XX    1750102612    1750300507    1750300505    1080200401   
##  [3691] 1210507201    17012XXXXX    316XXXXXXX    199XXXXXXX012 17038XXXXX   
##  [3696] 17041251XX    17002042XX    14703004XX    1750101403    2311114001   
##  [3701] 17023044XX    17038155XX    10608002XX    231XXXXXXX    299XXXXXXX013
##  [3706] 199XXXXXXX010 399XXXXXXX016 1220200101    17046036XX    16501XXXXX   
##  [3711] 1750101503    1080201011    32109XXXXX    17035169XX    12105012XX   
##  [3716] 694XXXXXXX    69302004XX    1080201017    1210504901    16302XXXXX   
##  [3721] 1750102501    17032027XX    17407001XX    1750300903    17402XXXXX   
##  [3726] 1750400301    10606006XX    19010XXXXX    22901001XX    1750101001   
##  [3731] 17063XXXXX    1750102610    1480400202    1210500105    1230100401   
##  [3736] 1830204802    1830200405    1230400301    1210506601    1231200102   
##  [3741] 1400200102    1400202001    1400201801    123XXXXXXX    1230100402   
##  [3746] 1830509201    1231200101    1480403401    1100400118    1750102605   
##  [3751] 1750102605    1750102605    1750102605    16102003XX    16102003XX   
##  [3756] 1210501104    1830201401    1830201401    1950100103    1090300401   
##  [3761] 1703903302    699XXXXXXX    1100400168    1480500406    3210501003   
##  [3766] 12305015XX    12305015XX    22802XXXXX    1090101403    1750102601   
##  [3771] 1750102601    1750100101    1750100101    1480400202    1480400202   
##  [3776] 1830200201    1830200201    1210500105    1210500105    1702300401   
##  [3781] 1702300401    1750100205    1750100205    1750100205    1702700301   
##  [3786] 1702700301    17801001XX    17801001XX    1230100401    1750300904   
##  [3791] 1710200101    1703900803    1703900803    17710001XX    1060100301   
##  [3796] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [3801] 1750102612    1090101401    1709637301    1090101901    1750601201   
##  [3806] 1703906302    1703906302    1780101703    1750102604    1080100104   
##  [3811] 1703900801    1703900801    1100400105    1480203001    1480400502   
##  [3816] 1750300505    1750300505    3161000105    1080200401    1080200401   
##  [3821] 1080200401    1100400101    1480403301    1480403301    1050200201   
##  [3826] 1050200201    1703926101    1703926101    1830506401    1830506401   
##  [3831] 3210501002    3210501002    1703707009    3210400112    14805004XX034
##  [3836] 1230400201    2280100117    17023XXXXX    17012XXXXX    31611020XX   
##  [3841] 10801XXXXX    10801003XX    321XXXXXXX    321XXXXXXX    1750100201   
##  [3846] 1750100201    1750100201    316XXXXXXX    316XXXXXXX    121XXXXXXX020
##  [3851] 121XXXXXXX020 31623XXXXX    3161300102    3210200202    3210200202   
##  [3856] 1830202405    1703906006    1702807101    1100700801    3162300203   
##  [3861] 1480201001    3210900507    3210900507    1703900802    1703900802   
##  [3866] 3070100101    2281201810    2281201810    2282300303    2282300303   
##  [3871] 1830300701    1830300701    1830300701    2290100804    2290100804   
##  [3876] 32104001XX    1100500326    23019XXXXX    17094XXXXX    1100400110   
##  [3881] 1100400110    32102XXXXX026 32102XXXXX026 2280101701    2280101701   
##  [3886] 2281201806    199XXXXXXX012 1950100106    10901XXXXX    10901XXXXX   
##  [3891] 10901XXXXX040 31615002XX    31615002XX    1700204201    2310901006   
##  [3896] 1210600201    1210600201    1210600201    1771000101    1431300101   
##  [3901] 1431300101    3160700205    3160700205    1830204802    1830204802   
##  [3906] 3210505801    1480500401    1480500401    2294200718    2294200718   
##  [3911] 1210506401    1210506401    1210506401    1830200405    1700634503   
##  [3916] 1700634503    1230400301    1210506601    1210506601    199XXXXXXX009
##  [3921] 199XXXXXXX009 183XXXXXXX    183XXXXXXX    183XXXXXXX    1650100102   
##  [3926] 1480400602    17501023XX018 17501023XX018 17501023XX018 17501023XX018
##  [3931] 148XXXXXXX    148XXXXXXX    1470100101    1470100101    307XXXXXXX   
##  [3936] 307XXXXXXX    1703923508    1703923508    17321XXXXX023 17321XXXXX023
##  [3941] 1650101203    21302007XX    3160800309    3160800309    3160800311   
##  [3946] 1702304801    1702304801    1480400601    1480400601    1721201002   
##  [3951] 1721201002    2311109001    1480400212    1830200501    1830200501   
##  [3956] 14806001XX    1780207001    1780207001    1709201906    1901000201   
##  [3961] 3161102001    3161102001    199XXXXXXX007 17002042XX    17002XXXXX   
##  [3966] 1090100801    17802XXXXX    17802XXXXX    1480401001    1480401001   
##  [3971] 14805004XX    1709201903    17023004XX    17023004XX    17023004XX   
##  [3976] 3161102002    1620100101    1620100101    1620100101    1580200105   
##  [3981] 1090101801    1090101702    2280100109    1750600302    1090100803   
##  [3986] 1702307202    1830204504    1480400501    1090100202    1750102401   
##  [3991] 1750102401    1750102401    229XXXXXXX    229XXXXXXX    3210400105   
##  [3996] 1090100701    1090101602    1100400111    1709441701    1709441701   
##  [4001] 17501XXXXX    17501XXXXX    1709201902    231XXXXXXX    231XXXXXXX   
##  [4006] 231XXXXXXX    299XXXXXXX013 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010
##  [4011] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016
##  [4016] 17503XXXXX    1703710601    1703710601    1702300408    1702300408   
##  [4021] 1430600701    3161000112    2311109002    1100400137    1100400137   
##  [4026] 1830500301    1830500301    19501001XX    19501001XX    19501001XX   
##  [4031] 14802XXXXX    14306XXXXX    1080100106    16501XXXXX    16501XXXXX   
##  [4036] 30702002XX    228XXXXXXX    228XXXXXXX    228XXXXXXX    2280400203   
##  [4041] 2280400203    3161107501    3210501001    2294200602    2294200602   
##  [4046] 1480403201    1080100302    1900800201    32109XXXXX    1750500701   
##  [4051] 1610500202    3160700801    3160700801    22901008XX    22901008XX   
##  [4056] 17039008XX    17039191XX    1480501701    3210400102    1709201502   
##  [4061] 1709201502    1100500316    30701001XX    17040075XX    17040075XX   
##  [4066] 1090100704    1090100704    1580200101    2290100802    2290100802   
##  [4071] 1480401502    1480403202    1480403202    1060800301    17039XXXXX   
##  [4076] 17039XXXXX    17039XXXXX    17039XXXXX    1090101601    23111004XX   
##  [4081] 1480403203    1480403203    3161100301    3160800105    1120100301   
##  [4086] 11004001XX    11004001XX    11201004XX    11004XXXXX    110XXXXXXX   
##  [4091] 110XXXXXXX    110XXXXXXX    110XXXXXXX    1706008301    1780200403   
##  [4096] 1780200403    1703919103    1703919103    1480600105    14804028XX   
##  [4101] 14804028XX    1480600103    1210501210    1480600401    1703907601   
##  [4106] 1703907601    1480401501    1480401501    1703929301    1703929301   
##  [4111] 123XXXXXXX    1830300704    1703927702    1703927702    17204002XX   
##  [4116] 17204002XX    1100400106    12105012XX    17039033XX    17039033XX   
##  [4121] 31608XXXXX    17801XXXXX    17801XXXXX    1020100101    31610XXXXX   
##  [4126] 1230100402    1830300708    12105011XX    12105011XX    1100400107   
##  [4131] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1060800201    1060800201   
##  [4136] 1750600601    1750600601    16302XXXXX    16302XXXXX    1750102501   
##  [4141] 1750102501    1750102501    1750102501    1750102501    1750102501   
##  [4146] 1750102501    1750102501    1100400109    1080100301    1080100301   
##  [4151] 3161100601    10804007XX    10804007XX    1750500101    31616003XX   
##  [4156] 18303XXXXX    18303XXXXX    3161202005    1709441801    1480403302   
##  [4161] 2290100806    2312100501    2312100501    1780108003    2250100102   
##  [4166] 1100400104    1100400104    1700634501    1721335202    1100400103   
##  [4171] 11005003XX    6930400701    6930400701    1780200304    3161100105   
##  [4176] 11701XXXXX    1704100701    1704100701    17041007XX    1750400301   
##  [4181] 1750400301    1480204001    31642002XX    18303081XX    1650100202   
##  [4186] 1650100202    1100400102    1100400102    1060600601    1060600601   
##  [4191] 1060600601    1080401103    1080401103    11101002XX    1780200302   
##  [4196] 1780200302    3070300114    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [4201] 1830509201    1830509201    1480400101    1210501105    1100400112   
##  [4206] 1709447001    32105XXXXX036 32105XXXXX036 32105XXXXX036 2311119501   
##  [4211] 31611XXXXX    31611XXXXX    1750101001    1830301701    3070800101   
##  [4216] 1480400803    1703903303    1703903303    1100400125    1100400125   
##  [4221] 1480403401    1480403401    1830205003    1830201102    1830201102   
##  [4226] 17102001XX    17063XXXXX    17063XXXXX    1700505801    1700505801   
##  [4231] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [4236] 1750102610    1750102610    2280102201    10901XXXXX    183XXXXXXX   
##  [4241] 17002042XX    17023044XX    199XXXXXXX010 1650100122    22801001XX   
##  [4246] 11004001XX    2280100119    14102XXXXX    17501015XX    17001025XX   
##  [4251] 2280100133    1290200401    1703402901    17037016XX    1211200302   
##  [4256] 1750102605    17710001XX    1750102612    1750300507    1750300505   
##  [4261] 1702807101    689XXXXXXX    1750500501    14704XXXXX    1750300402   
##  [4266] 2311114001    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 17503XXXXX   
##  [4271] 1750500701    1520100102    22801001XX    1750501701    199XXXXXXX054
##  [4276] 1750300905    1060800201    1702700404    1750102501    17032XXXXX   
##  [4281] 1750300903    1750400301    22901001XX    175XXXXXXX    1750101001   
##  [4286] 1750102610    199XXXXXXX010 32109XXXXX    2290100208    1705013202   
##  [4291] 17710001XX    1703626303    1750102612    1703745705    1300100501   
##  [4296] 1210503002    32102XXXXX026 2280101701    17039060XX    183XXXXXXX   
##  [4301] 1707700109    17002042XX    17036XXXXX    2280101902    17023044XX   
##  [4306] 1707700302    1750102401    17501XXXXX    231XXXXXXX    199XXXXXXX010
##  [4311] 17503XXXXX    16501XXXXX    32109XXXXX    17039008XX    22801001XX   
##  [4316] 110XXXXXXX    1707700401    12105012XX    17023043XX    14102XXXXX   
##  [4321] 199XXXXXXX054 1750102501    17032027XX    2280100131    1750400301   
##  [4326] 17059051XX    18304XXXXX    22901001XX    175XXXXXXX    32105XXXXX036
##  [4331] 1750101511    17037457XX    1704149903    1750102610    1705013202   
##  [4336] 1702309003    17710001XX    1760300401    1702021301    1703745705   
##  [4341] 1210503002    1703745702    1750100201    1702222101    17037XXXXX   
##  [4346] 32102XXXXX026 1702304442    307XXXXXXX    1707700109    17002042XX   
##  [4351] 2280101902    17506XXXXX    17023004XX    17023044XX    1703745701   
##  [4356] 1707700302    231XXXXXXX    199XXXXXXX010 1703710601    16501XXXXX   
##  [4361] 32109XXXXX    22901008XX    17039008XX    17065XXXXX    17023047XX   
##  [4366] 17039XXXXX    19002XXXXX    1707700401    1703620705    12105012XX   
##  [4371] 14102XXXXX    199XXXXXXX054 17032027XX    1703620919    2280100131   
##  [4376] 17077XXXXX    17059051XX    18304XXXXX    19010XXXXX    32105XXXXX036
##  [4381] 17037457XX    1290100304    1750102610    1702304605    16102003XX   
##  [4386] 1750100101    17710001XX    17710001XX    17710001XX    1210505901   
##  [4391] 1760300401    1480501702    1750100207    1702021301    1702021301   
##  [4396] 1702021301    17030XXXXX    17030XXXXX    14805004XX034 1702300413   
##  [4401] 1702300405    1750100201    1750100201    1750100201    32102XXXXX026
##  [4406] 17038XXXXX    1210600201    1210600201    1210506401    1210506601   
##  [4411] 183XXXXXXX    148XXXXXXX    17321XXXXX023 1702300415    14805004XX   
##  [4416] 17501014XX    17023004XX    17023004XX    17023044XX    17023044XX   
##  [4421] 1703906002    1703906002    1750600302    1750600302    1702307202   
##  [4426] 13116XXXXX    17501XXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [4431] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 1702300408    16501XXXXX   
##  [4436] 16501XXXXX    32109XXXXX    1090100704    17039XXXXX    17039XXXXX   
##  [4441] 17039XXXXX    17039XXXXX    110XXXXXXX    110XXXXXXX    1480201401   
##  [4446] 12105012XX    12105012XX    14102XXXXX    30702018XX    1480500402   
##  [4451] 199XXXXXXX054 199XXXXXXX054 17032XXXXX    1750500101    1210501303   
##  [4456] 1480403302    11701XXXXX    17041007XX    19010XXXXX    175XXXXXXX   
##  [4461] 175XXXXXXX    175XXXXXXX    32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [4466] 17608010XX    17037457XX    1480403401    1750102610    1702304605   
##  [4471] 1480401601    1210501106    17023048XX    1830201401    1830201401   
##  [4476] 1210501103    2294200503    17092XXXXX    17092XXXXX    1709253501   
##  [4481] 1709201501    1230501504    1480500406    3210501003    12305015XX   
##  [4486] 12305015XX    1780701403    1750102601    1750100101    1760301104   
##  [4491] 1480400202    1480400202    1830200201    1830200201    1210500105   
##  [4496] 1210500105    1702300401    1702300401    1750100205    1750100205   
##  [4501] 1210502403    1702700301    17801001XX    17801001XX    1230100401   
##  [4506] 1470200201    1710200101    1231400701    1231400701    17710001XX   
##  [4511] 17710001XX    1709637301    1702309901    1709201909    1750601201   
##  [4516] 1703906302    1703906302    1703906302    1709441601    1709441601   
##  [4521] 1703900801    1480203001    1760300401    1480400502    1480403301   
##  [4526] 1480403301    1702021301    1702021301    1702021301    1830506401   
##  [4531] 17603XXXXX    14805004XX034 1702300413    1230400201    1230400201   
##  [4536] 17023XXXXX    17023XXXXX    17012XXXXX    1703745702    1702300405   
##  [4541] 1750100201    1750100201    1750100201    1750100201    1750100201   
##  [4546] 316XXXXXXX    121XXXXXXX020 1400200201    1830202405    3162300203   
##  [4551] 2282300303    1830300701    17037XXXXX    17037XXXXX    17037XXXXX   
##  [4556] 17094XXXXX    17094XXXXX    1400201601    1702300414    31607008XX   
##  [4561] 15802001XX    32102XXXXX026 14002XXXXX    2314300109    1950100106   
##  [4566] 10901XXXXX    10901XXXXX    10901XXXXX    2310901006    1711500401   
##  [4571] 17115024XX    1210600201    1210600201    3160700205    1830204802   
##  [4576] 1480500401    2294200718    1210506401    1210506401    1830200405   
##  [4581] 1230400301    1210506601    1231200102    1702304442    199XXXXXXX009
##  [4586] 199XXXXXXX009 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
##  [4591] 183XXXXXXX    14002001XX    17501023XX018 148XXXXXXX    148XXXXXXX   
##  [4596] 148XXXXXXX    1470100101    1230501503    1480400601    1830200501   
##  [4601] 1830200501    1090100201    14806001XX    17002042XX    17002XXXXX   
##  [4606] 17002XXXXX    17002XXXXX    17036XXXXX    17036XXXXX    17036XXXXX   
##  [4611] 17802XXXXX    17802XXXXX    1480401001    1480401001    14805004XX   
##  [4616] 1709201903    1709201903    17023004XX    17023004XX    17023004XX   
##  [4621] 17023044XX    17023044XX    1620100101    1620100101    1580200105   
##  [4626] 1090101801    2282907301    1750600302    1750600302    1090100803   
##  [4631] 1702307202    1702307202    18301XXXXX    1830204504    1480400501   
##  [4636] 1480400501    1750102401    3210400105    1782000301    1709441701   
##  [4641] 1210501217    1709201902    231XXXXXXX    299XXXXXXX013 299XXXXXXX013
##  [4646] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [4651] 199XXXXXXX010 199XXXXXXX010 1830500301    18305003XX    19501001XX   
##  [4656] 14802XXXXX    16501XXXXX    16501XXXXX    1480500407    2280400203   
##  [4661] 2280400203    3210501001    3210501001    2294200602    1480403201   
##  [4666] 1709446601    32109XXXXX    1610500202    1480400211    1210500107   
##  [4671] 1702300406    1780100109    17039008XX    1480501701    3210400102   
##  [4676] 1709201502    199XXXXXXX008 22801001XX    1090100704    1090100704   
##  [4681] 1090100704    1580200101    1480401901    1480401502    1060800301   
##  [4686] 1060800301    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
##  [4691] 1090101601    11004001XX    11004001XX    110XXXXXXX    110XXXXXXX   
##  [4696] 110XXXXXXX    110XXXXXXX    1480400802    1703900807    1400201801   
##  [4701] 1702300411    1702300411    1480600103    1480600103    1210501210   
##  [4706] 1480600401    1480600401    1703620705    1780800401    1480401501   
##  [4711] 1480401501    123XXXXXXX    17204002XX    17204002XX    12105012XX   
##  [4716] 12105012XX    12105012XX    17039033XX    17039033XX    31608XXXXX   
##  [4721] 17801XXXXX    1703935301    14102XXXXX    14102XXXXX    1230100402   
##  [4726] 1480500402    12105011XX    199XXXXXXX054 199XXXXXXX054 1480500404   
##  [4731] 1750600601    1750600601    1750600601    1750600601    1750102501   
##  [4736] 17505XXXXX    17032XXXXX    1709441801    1480500405    1210501305   
##  [4741] 1480403302    1480403302    1709448001    1710200103    691XXXXXXX   
##  [4746] 1709201910    11701XXXXX    17041007XX    1400200701    17077XXXXX   
##  [4751] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    1830509201   
##  [4756] 1480400101    1480400101    199XXXXXXX053 32105XXXXX036 32105XXXXX036
##  [4761] 32105XXXXX036 32105XXXXX036 32105XXXXX036 1750101511    17037457XX   
##  [4766] 17037457XX    1480400803    1210503104    1480403401    1830201102   
##  [4771] 1830201102    17102001XX    17102001XX    1709201904    1709243002   
##  [4776] 1702304605    1705013202    1703906010    1703906010    3210501003   
##  [4781] 1750100101    1702326801    1750300404    1750300904    17710001XX   
##  [4786] 1480500408    1703626303    1750102612    1760300401    1750300505   
##  [4791] 1080200401    1703926101    1210503002    14805004XX034 17023XXXXX   
##  [4796] 1702300405    1750100201    1750100201    1750100201    121XXXXXXX020
##  [4801] 121XXXXXXX020 1703906011    1702304429    17037XXXXX    1702300414   
##  [4806] 32102XXXXX026 32102XXXXX026 199XXXXXXX012 199XXXXXXX012 17039060XX   
##  [4811] 1210600201    1702304442    14704XXXXX    17501023XX018 17002042XX   
##  [4816] 17036XXXXX    17802XXXXX    14805004XX    14703004XX    10803XXXXX   
##  [4821] 17023004XX    17023004XX    17023044XX    1750600302    1750600302   
##  [4826] 1707700302    1750102401    1210501217    231XXXXXXX    199XXXXXXX010
##  [4831] 199XXXXXXX010 199XXXXXXX010 1703710601    16501XXXXX    228XXXXXXX   
##  [4836] 32109XXXXX    32109XXXXX    17039191XX    17039XXXXX    17039XXXXX   
##  [4841] 19002XXXXX    110XXXXXXX    110XXXXXXX    1703900807    1703900807   
##  [4846] 1210501210    12105012XX    12105012XX    17023043XX    17023043XX   
##  [4851] 14102XXXXX    199XXXXXXX054 199XXXXXXX054 1750102501    17032027XX   
##  [4856] 18303XXXXX    1703620919    1750400301    18304XXXXX    19010XXXXX   
##  [4861] 22901001XX    175XXXXXXX    1750101511    17037457XX    17037457XX   
##  [4866] 1704149903    1211200112    1700204202    1750102610    199XXXXXXX010
##  [4871] 1750102605    1480500406    1750102601    1750102601    1750100101   
##  [4876] 1750100101    1702300401    1750100205    1703906302    1703906302   
##  [4881] 1704007501    1480403301    1480403301    1702021301    1702021301   
##  [4886] 1703926101    1703926101    2280100117    2280100117    17023XXXXX   
##  [4891] 1750100201    1750100201    3210200202    3210200202    1703906006   
##  [4896] 1703906006    3210900507    1830300701    1830300701    32104001XX   
##  [4901] 10901XXXXX    10901XXXXX    1700204201    1700204201    1210600201   
##  [4906] 1210600201    1431300101    3160700205    1480500401    1480500401   
##  [4911] 2294200718    2294200718    1210506401    1700634503    1700634503   
##  [4916] 1210506601    1650100102    1650100102    17501023XX018 1470100101   
##  [4921] 1703923508    1702304801    17002042XX    17002XXXXX    17002XXXXX   
##  [4926] 11001XXXXX    17802XXXXX    17802XXXXX    17023004XX    1620100101   
##  [4931] 1620100101    1703906002    1703906002    1750102401    231XXXXXXX   
##  [4936] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 1703710601   
##  [4941] 1703710601    1702300408    3161000112    2311109002    19501001XX   
##  [4946] 19501001XX    228XXXXXXX    228XXXXXXX    2294200602    2294200602   
##  [4951] 32109XXXXX    32109XXXXX    17039008XX    17039008XX    17039191XX   
##  [4956] 17039191XX    3210400102    17040075XX    17040075XX    17039XXXXX   
##  [4961] 11004001XX    1704100702    1703919103    1703919103    1703907601   
##  [4966] 1703907601    1703929301    17039033XX    17801XXXXX    17801XXXXX   
##  [4971] 12105011XX    12105011XX    1703707001    1703707001    1750102501   
##  [4976] 10804007XX    10804007XX    3161100105    1704100701    17041007XX   
##  [4981] 17041007XX    1750400301    1750400301    1100400102    175XXXXXXX   
##  [4986] 175XXXXXXX    1830509201    32105XXXXX036 32105XXXXX036 1704149903   
##  [4991] 1700204202    1703903303    1480403401    1700505801    1700505801   
##  [4996] 2280400205    1830201401    1830201401    1950100101    1230101005   
##  [5001] 1230101005    1480400202    1480400202    1830200201    1830200201   
##  [5006] 1210500105    1210500105    1750100205    17801001XX    17801001XX   
##  [5011] 1230100401    1230100401    1710200101    1780100112    1780100112   
##  [5016] 1480400502    1480403301    1230400201    1230400201    10901XXXXX   
##  [5021] 10901XXXXX    1830200405    199XXXXXXX009 1780100101    1780100101   
##  [5026] 1480400212    1480400212    1830200501    1830200501    1090100201   
##  [5031] 1090100201    199XXXXXXX007 1480401001    1480401001    3160803603   
##  [5036] 3160803603    1480400501    1782000301    1782000301    199XXXXXXX010
##  [5041] 2280400203    2280400203    1480401901    1480401901    2312114501   
##  [5046] 11004001XX    11004001XX    1480600401    1480600401    1480401501   
##  [5051] 1480401501    1480400101    1480400101    17102001XX    17102001XX   
##  [5056] 1750102605    1750100101    1702304604    1750300404    1210504202   
##  [5061] 1750300904    17710001XX    1702329101    1750102612    1750102604   
##  [5066] 1750300505    1210501224    1210602011    17023XXXXX    2290100108   
##  [5071] 1702807101    1700211502    14704XXXXX    17501023XX018 17041XXXXX   
##  [5076] 17002XXXXX    17036XXXXX    14703004XX    1750101506    1750102401   
##  [5081] 199XXXXXXX010 14701XXXXX    17065XXXXX    1702313401    1700204225   
##  [5086] 1701735702    17023043XX    12105033XX    69302004XX    1750101515   
##  [5091] 199XXXXXXX054 1750102501    17032XXXXX    17001025XX    16111XXXXX   
##  [5096] 30706002XX    17402XXXXX    1750400301    19010XXXXX    32105XXXXX036
##  [5101] 1750101001    1750102610    1750100101    1750102604    1750101508   
##  [5106] 1702807101    17501XXXXX    299XXXXXXX013 199XXXXXXX010 30706002XX   
##  [5111] 17710001XX    1750300505    17023XXXXX    1702807101    17038XXXXX   
##  [5116] 17002042XX    1750300402    199XXXXXXX010 228XXXXXXX    32109XXXXX   
##  [5121] 17065XXXXX    1702313401    17023043XX    199XXXXXXX054 1750102501   
##  [5126] 17032XXXXX    17407001XX    17402XXXXX    22901001XX    175XXXXXXX   
##  [5131] 1750101001    17063XXXXX    1750102610    1750102605    1750102612   
##  [5136] 1750102612    1750102612    2280100110    2290100108    1702807101   
##  [5141] 17037XXXXX    2280100123    183XXXXXXX    1750102301    17036XXXXX   
##  [5146] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016
##  [5151] 17503XXXXX    22801XXXXX027 22801001XX    22801001XX    14102XXXXX   
##  [5156] 199XXXXXXX054 1080201017    1750102501    1750102501    1750102501   
##  [5161] 30706002XX    1750400301    22901001XX    175XXXXXXX    32105XXXXX036
##  [5166] 32105XXXXX036 2280100111    1750102610    1750102610    1750102610   
##  [5171] 2280100104    1705013202    1750102605    1750102605    1750102601   
##  [5176] 1702326801    1703817204    17710001XX    1703626303    1750102612   
##  [5181] 1750102612    1750300507    1750300505    1080200401    1080200401   
##  [5186] 1703745705    1210503002    17023XXXXX    1750100201    32102XXXXX026
##  [5191] 183XXXXXXX    1707700109    17036XXXXX    14805004XX    1750300402   
##  [5196] 1750300402    17023004XX    1750600302    1707700302    199XXXXXXX010
##  [5201] 199XXXXXXX010 199XXXXXXX010 16501XXXXX    32109XXXXX    22801001XX   
##  [5206] 17039XXXXX    1707700401    12105012XX    14102XXXXX    199XXXXXXX054
##  [5211] 199XXXXXXX054 199XXXXXXX054 1750300905    1750300905    1060800201   
##  [5216] 1060800201    1750102501    1750300903    1750300903    1750400301   
##  [5221] 1750400301    175XXXXXXX    32105XXXXX036 17037457XX    1750102610   
##  [5226] 1750102610    1750102610    1705013202    1703626303    1702021301   
##  [5231] 3210900507    17037XXXXX    32102XXXXX026 2280101701    17039060XX   
##  [5236] 183XXXXXXX    1707700109    17023044XX    1750600302    1707700302   
##  [5241] 17501XXXXX    231XXXXXXX    199XXXXXXX010 399XXXXXXX016 1703710601   
##  [5246] 16501XXXXX    228XXXXXXX    22901008XX    17039XXXXX    12105012XX   
##  [5251] 1080300506    14102XXXXX    1480500402    1750102501    1703620919   
##  [5256] 1750400301    175XXXXXXX    32105XXXXX036 1750101511    2280102201   
##  [5261] 1080201003    10803XXXXX    1750101506    199XXXXXXX010 22801001XX   
##  [5266] 1750101515    199XXXXXXX054 1080201012    1703202722    2281200302   
##  [5271] 2290100108    231XXXXXXX    199XXXXXXX010 228XXXXXXX    694XXXXXXX   
##  [5276] 30706002XX    1750102605    1480500406    3210501003    1750102612   
##  [5281] 1750102612    1750102612    1750300507    2290100108    17037XXXXX   
##  [5286] 17037XXXXX    1702300414    32102XXXXX026 32102XXXXX026 1210506401   
##  [5291] 14805004XX    1750300402    17023004XX    1750600302    231XXXXXXX   
##  [5296] 231XXXXXXX    299XXXXXXX013 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010
##  [5301] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016
##  [5306] 17503XXXXX    228XXXXXXX    2280400203    3210501001    32109XXXXX   
##  [5311] 32109XXXXX    1480501701    3210400102    1709201502    22801001XX   
##  [5316] 22801001XX    22801001XX    1580200101    17039XXXXX    17039XXXXX   
##  [5321] 110XXXXXXX    694XXXXXXX    3210506001    199XXXXXXX054 199XXXXXXX054
##  [5326] 1750102501    1750102501    1480403302    30706002XX    1750400301   
##  [5331] 1750400301    1480204001    22901001XX    175XXXXXXX    175XXXXXXX   
##  [5336] 175XXXXXXX    32105XXXXX036 32105XXXXX036 32105XXXXX036 31611XXXXX   
##  [5341] 1750102610    1750102610    1750102610    1830202404    16102003XX   
##  [5346] 16102003XX    16102003XX    1830201401    1950100101    12305015XX   
##  [5351] 1750102601    1480400202    1480400202    1830200201    1210500105   
##  [5356] 1210500105    1702300401    1750100205    1702700301    17801001XX   
##  [5361] 17801001XX    1230100401    1710200101    1231400701    1780100112   
##  [5366] 1750102612    1090101901    1750601201    1750601201    1480203001   
##  [5371] 1480400502    3161000105    1100400101    1480403301    14805004XX034
##  [5376] 1230400201    1230400201    112XXXXXXX    1750100201    1830202405   
##  [5381] 1520400203    1950100106    10901XXXXX    1311100701    6930401401   
##  [5386] 3210505801    1480500401    1830200405    183XXXXXXX    183XXXXXXX   
##  [5391] 148XXXXXXX    1780100101    1480400601    1830200501    1830200501   
##  [5396] 1090100201    1780207001    199XXXXXXX007 199XXXXXXX007 1480401001   
##  [5401] 3160803603    3160803603    17023004XX    1620100101    1580200105   
##  [5406] 1830204504    1480400501    1782000301    17501XXXXX    231XXXXXXX   
##  [5411] 199XXXXXXX010 1830500301    2280400203    2280400203    2294200602   
##  [5416] 1480403201    1780100102    3160904501    1610500202    199XXXXXXX008
##  [5421] 1090100704    1480401502    1060800301    1090101601    1120100301   
##  [5426] 11004001XX    110XXXXXXX    1480600103    1480600401    1100400181   
##  [5431] 1480401501    17204002XX    12105012XX    17801XXXXX    694XXXXXXX   
##  [5436] 1100400107    1250203001    1750500101    1710200103    1100400103   
##  [5441] 1750400301    1830509201    1480400101    32105XXXXX036 32105XXXXX036
##  [5446] 3070800101    1100400125    1480403401    1830201102    17102001XX   
##  [5451] 17102001XX    1750102605    1750102605    12106XXXXX    12106XXXXX   
##  [5456] 17710001XX    17710001XX    1750102612    1750102612    1750300507   
##  [5461] 1750300507    1750300505    1750300505    1311600102    1311600102   
##  [5466] 17603XXXXX    17603XXXXX    17023XXXXX    17023XXXXX    321XXXXXXX   
##  [5471] 321XXXXXXX    121XXXXXXX020 121XXXXXXX020 17037XXXXX    17037XXXXX   
##  [5476] 1701916502    1701916502    183XXXXXXX    183XXXXXXX    14704XXXXX   
##  [5481] 14704XXXXX    17501023XX018 17501023XX018 2280100112    2280100112   
##  [5486] 17041251XX    17041251XX    17506XXXXX    17506XXXXX    14703004XX   
##  [5491] 14703004XX    1210503801    1210503801    1750101403    1750101403   
##  [5496] 1210501204    1210501204    1750101504    1750101504    1750300402   
##  [5501] 1750300402    17023044XX    17023044XX    61841007XX    1750102406   
##  [5506] 1750102406    1320801715    13116XXXXX    13116XXXXX    1750102603   
##  [5511] 1750102603    231XXXXXXX    231XXXXXXX    299XXXXXXX013 299XXXXXXX013
##  [5516] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 17503XXXXX   
##  [5521] 17503XXXXX    16501XXXXX    16501XXXXX    1750101503    1750101503   
##  [5526] 228XXXXXXX    228XXXXXXX    170XXXXXXX    170XXXXXXX    14309011XX   
##  [5531] 14309011XX    17023047XX    17023047XX    17035XXXXX    17035XXXXX   
##  [5536] 14102XXXXX    14102XXXXX    199XXXXXXX054 199XXXXXXX054 1750102501   
##  [5541] 1750102501    1750101505    1750101505    1750300903    1750300903   
##  [5546] 1750400301    1750400301    17077XXXXX    17077XXXXX    175XXXXXXX   
##  [5551] 175XXXXXXX    1480301801    1480301801    1750101001    1750101001   
##  [5556] 12111002XX    12111002XX    1750102610    1750102610    2280700903   
##  [5561] 1750102605    699XXXXXXX    699XXXXXXX    1210501223    1210501223   
##  [5566] 2280100103    2280100103    1700116701    1700116701    1702329101   
##  [5571] 1702329101    1750102612    1750102612    17011026XX    17011026XX   
##  [5576] 1750300507    1750300507    1702309901    1702309901    3160407101   
##  [5581] 3160407101    1750100207    1750100207    1750300505    1750300505   
##  [5586] 2311100401    2311100401    1311600102    1311600102    1750102303   
##  [5591] 1210502301    1210502301    1700211519    1700211519    3070400603   
##  [5596] 3070400603    1702807101    1702807101    32104001XX    32104001XX   
##  [5601] 17037XXXXX    17037XXXXX    31607008XX    31607008XX    32102XXXXX026
##  [5606] 32102XXXXX026 10901XXXXX    10901XXXXX    11007XXXXX    11007XXXXX   
##  [5611] 17038XXXXX    17038XXXXX    1701916502    1701916502    183XXXXXXX   
##  [5616] 183XXXXXXX    14704XXXXX    14704XXXXX    1707700201    1707700201   
##  [5621] 17501023XX018 1750102301    17000XXXXX    17000XXXXX    2280100112   
##  [5626] 2280100112    17041251XX    17041251XX    1210501203    1210501203   
##  [5631] 1700204219    1700204219    1771000107    1771000107    1311606801   
##  [5636] 1311606801    3161003202    3161003202    17036XXXXX    17036XXXXX   
##  [5641] 11001XXXXX    11001XXXXX    17506XXXXX    17506XXXXX    14703004XX   
##  [5646] 14703004XX    10803XXXXX    10803XXXXX    31611017XX    31611017XX   
##  [5651] 1700204211    1700204211    1700212501    1700212501    1706311703   
##  [5656] 1706311703    1830700101    1830700101    1750101403    1750101403   
##  [5661] 1750101504    1750101504    1750300402    1750300402    2311114001   
##  [5666] 2311114001    17023044XX    17023044XX    61841007XX    61841007XX   
##  [5671] 17032217XX    17032217XX    1750102406    1750102406    1700220804   
##  [5676] 1700220804    1750102603    1750102603    10608XXXXX    10608XXXXX   
##  [5681] 11008XXXXX    11008XXXXX    299XXXXXXX013 299XXXXXXX013 199XXXXXXX010
##  [5686] 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 17503XXXXX    22801016XX   
##  [5691] 22801016XX    16501XXXXX    16501XXXXX    1750101503    1750101503   
##  [5696] 228XXXXXXX    228XXXXXXX    14701013XX    14701013XX    32109XXXXX   
##  [5701] 32109XXXXX    1771000103    1771000103    17035XXXXX    17035XXXXX   
##  [5706] 17023231XX    17023231XX    1702313401    1702313401    1210502901   
##  [5711] 1210502901    110XXXXXXX    110XXXXXXX    1701102605    1701102605   
##  [5716] 10802XXXXX    10802XXXXX    11002XXXXX    11002XXXXX    17023043XX   
##  [5721] 17023043XX    31608XXXXX    31608XXXXX    14102XXXXX    14102XXXXX   
##  [5726] 694XXXXXXX    694XXXXXXX    199XXXXXXX054 199XXXXXXX054 1750101401   
##  [5731] 1750101401    1750300905    1760300901    1760300901    1701523304   
##  [5736] 1701523304    1750102501    1750102501    17032027XX    17032027XX   
##  [5741] 1750102608    17407001XX    17407001XX    1210500503    1210500503   
##  [5746] 11005XXXXX    11005XXXXX    12106050XX    12106050XX    1750100102   
##  [5751] 1750100102    1750300903    1750300903    17036207XX    17036207XX   
##  [5756] 1750400301    1750400301    17004089XX    17004089XX    17033184XX   
##  [5761] 17033184XX    17077XXXXX    17077XXXXX    10606006XX    10606006XX   
##  [5766] 1210503804    1210503804    1702317901    1702317901    22901001XX   
##  [5771] 22901001XX    175XXXXXXX    175XXXXXXX    1750101001    1100100401   
##  [5776] 1100100401    12111002XX    12111002XX    1750102610    1750102610   
##  [5781] 1702342201    1702342201    1750102605    17710001XX    1780901801   
##  [5786] 1703756105    1750102612    1750102612    1750300507    1702309901   
##  [5791] 1750300505    2311100401    1650104302    121XXXXXXX020 1702222101   
##  [5796] 1702807101    17037XXXXX    1707700201    17501023XX018 1100100402   
##  [5801] 1702304405    1311606801    1706505609    1210503801    1830700101   
##  [5806] 1750101403    1210501204    1702304721    1750101504    1750300402   
##  [5811] 1703318404    1703620923    61841007XX    1703202707    1750102406   
##  [5816] 1650101217    1750600302    1750102603    1703202713    199XXXXXXX010
##  [5821] 399XXXXXXX016 1750101503    228XXXXXXX    1700204257    3210200229   
##  [5826] 110XXXXXXX    11002XXXXX    14102XXXXX    1760300901    1320802403   
##  [5831] 1750102501    1750102501    1703817202    17407001XX    1080201031   
##  [5836] 1705013201    1750300903    1750400301    1702323101    1703718603   
##  [5841] 22901001XX    175XXXXXXX    1703933006    1211100202    1750102610   
##  [5846] 1750102610    14805004XX034 1702300413    1750100201    1702323102   
##  [5851] 183XXXXXXX    2280100120    17002XXXXX    1210503801    199XXXXXXX010
##  [5856] 199XXXXXXX010 16501XXXXX    17039XXXXX    1210501210    1760300901   
##  [5861] 1703718603    12111002XX    30703001XX    1750102605    16102003XX   
##  [5866] 1830201401    1950100103    1210501103    1950100101    1100400168   
##  [5871] 12305015XX    1750102601    1750100101    1760301104    1480400202   
##  [5876] 1480400202    1830200201    1830200201    1210500105    1702300401   
##  [5881] 1750100205    1750100205    1702700301    17801001XX    17801001XX   
##  [5886] 1230100401    1710200101    1231400701    1780100112    1750102612   
##  [5891] 1709637301    1750601201    1780101703    1080100104    1703900801   
##  [5896] 1100400105    1480400502    3161000105    1080200401    1480403301   
##  [5901] 1702021301    1620300201    1830506401    1230400201    1230400201   
##  [5906] 17012XXXXX    1750100201    316XXXXXXX    121XXXXXXX020 1480602102   
##  [5911] 1830202405    3162300203    1480201001    3070100101    2282300303   
##  [5916] 1830300701    32104001XX    1100400110    31607008XX    32102XXXXX026
##  [5921] 2314300109    10901XXXXX    2310901006    1210600201    1431300101   
##  [5926] 6930401401    3160700205    1830204802    3210505801    1480500401   
##  [5931] 2294200718    1210506401    1210506401    1830200405    1700634503   
##  [5936] 1210506601    199XXXXXXX009 183XXXXXXX    183XXXXXXX    17501023XX018
##  [5941] 148XXXXXXX    1470100101    1780100101    3160800309    1701640002   
##  [5946] 1480400601    1721201002    2311109001    1830200501    1830200501   
##  [5951] 1780207001    3161102001    17036XXXXX    1090100801    17802XXXXX   
##  [5956] 1480401001    1480401001    17506XXXXX    3210902401    17023004XX   
##  [5961] 3161102002    1620100101    1090101801    1090101702    1750600302   
##  [5966] 1750600302    1830204504    1480400501    14804005XX    1750102401   
##  [5971] 3210400105    1090101602    1100400111    231XXXXXXX    299XXXXXXX013
##  [5976] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 1830500301    16501XXXXX   
##  [5981] 16501XXXXX    3210501001    3210501001    2294200602    1480403201   
##  [5986] 1780100102    1080100302    1900800201    32109XXXXX    1610500202   
##  [5991] 22812XXXXX046 22901008XX    1090100704    1750100601    3161600503   
##  [5996] 1480401502    1060800301    17039XXXXX    1090101601    23111004XX   
##  [6001] 1480403203    3160800105    1120100301    1230100909    11004001XX   
##  [6006] 11201004XX    1780200403    1480600103    1100400131    1210501210   
##  [6011] 1480600401    1090500602    1480401501    1480401501    1830300704   
##  [6016] 17204002XX    1703935301    1230100402    1100400107    1480500404   
##  [6021] 1750600601    1750102501    1080100301    10804007XX    31616003XX   
##  [6026] 3161202005    2312100501    1100400104    1100400103    1830804606   
##  [6031] 1704100701    3161600505    1750400301    1750400301    1100400102   
##  [6036] 1080401103    175XXXXXXX    175XXXXXXX    1830509201    1480400101   
##  [6041] 1480400101    199XXXXXXX053 32105XXXXX036 2311119501    3070800101   
##  [6046] 1480400803    1480403401    1830201102    17102001XX    17102001XX   
##  [6051] 1700505801    1750102610    1830202404    1950100101    1480400202   
##  [6056] 1210500105    1750100205    1230100401    1830506401    1830202405   
##  [6061] 1830300701    32104001XX    10901XXXXX    2310901006    1431300101   
##  [6066] 1480500401    2294200718    1830200405    1210506601    199XXXXXXX009
##  [6071] 183XXXXXXX    3160800309    17802XXXXX    1480401001    1830204504   
##  [6076] 1480400501    1830500301    2294200602    32109XXXXX    1480401502   
##  [6081] 3160800105    11004001XX    1780200403    1480401501    17204002XX   
##  [6086] 1230100402    1704100701    1830509201    32105XXXXX036 2311119501   
##  [6091] 3070800101    12312001XX    1480403401    1830201102    1480500406   
##  [6096] 1750102601    1702300401    1702700301    17710001XX    17710001XX   
##  [6101] 1780101703    1760300401    2311100401    1702021301    1703926101   
##  [6106] 1311606804    1311606804    1780200307    14805004XX034 1702300413   
##  [6111] 17023XXXXX    321XXXXXXX    1750100201    1750100201    3210200202   
##  [6116] 1100100524    1703900802    1830300701    32104001XX    2280101701   
##  [6121] 1950100106    1700204201    1210600201    1480500401    1700634503   
##  [6126] 17501023XX018 1703923508    17041251XX    1702304801    17002042XX   
##  [6131] 17002XXXXX    1620100101    1580200105    2280100109    1750102401   
##  [6136] 1750102401    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [6141] 199XXXXXXX010 199XXXXXXX010 1703710601    2291504101    16501XXXXX   
##  [6146] 16501XXXXX    1750101503    1750101503    228XXXXXXX    228XXXXXXX   
##  [6151] 32109XXXXX    32109XXXXX    17039191XX    17040075XX    17039XXXXX   
##  [6156] 17039XXXXX    1703318416    110XXXXXXX    1210501210    1210501210   
##  [6161] 199XXXXXXX054 199XXXXXXX054 1702300101    17032XXXXX    1750500101   
##  [6166] 17407001XX    17041007XX    1750400301    19010XXXXX    32105XXXXX036
##  [6171] 32105XXXXX036 1830305701    1700204202    1750102605    1750102605   
##  [6176] 1950100103    1703906010    1480500406    22802XXXXX    1750102601   
##  [6181] 1750102601    1750102601    1750100101    1760301104    1480400202   
##  [6186] 1830200201    1702300401    1750100205    1750100205    1750100205   
##  [6191] 17801001XX    1480500408    1750102612    1750102612    1703906302   
##  [6196] 1080200401    1480403301    1703926101    3210501002    14805004XX034
##  [6201] 2280100117    2280100117    2280100117    17023XXXXX    17023XXXXX   
##  [6206] 321XXXXXXX    1750100201    1750100201    1750100201    1750100201   
##  [6211] 1750100201    1750100201    31623XXXXX    1703906006    1703906006   
##  [6216] 1702807101    3210900507    3210900507    2282300303    1830300701   
##  [6221] 1830300701    2290100804    32104001XX    32104001XX    32104001XX   
##  [6226] 32104001XX    32104001XX    17037XXXXX    17037XXXXX    17037XXXXX   
##  [6231] 17037XXXXX    17037XXXXX    1702300414    32102XXXXX026 32102XXXXX026
##  [6236] 32102XXXXX026 32102XXXXX026 32102XXXXX026 32102XXXXX026 2280101701   
##  [6241] 17039060XX    17039060XX    10901XXXXX    10901XXXXX    109XXXXXXX   
##  [6246] 31615002XX    1700204201    1700204201    1210600201    1771000101   
##  [6251] 1431300101    1830204802    1480500401    1480500401    1480500401   
##  [6256] 2294200718    1210506401    1700634503    1210506601    199XXXXXXX009
##  [6261] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
##  [6266] 183XXXXXXX    1480400602    17501023XX018 148XXXXXXX    1470100101   
##  [6271] 307XXXXXXX    1703923508    1703923508    17041XXXXX    17041XXXXX   
##  [6276] 17321XXXXX023 3160800311    1702304801    1480400601    17002042XX   
##  [6281] 17002042XX    17002042XX    17002XXXXX    17002XXXXX    17002XXXXX   
##  [6286] 17002XXXXX    17002XXXXX    17802XXXXX    17802XXXXX    14805004XX   
##  [6291] 32109024XX    17023004XX    17023004XX    17023004XX    17023004XX   
##  [6296] 1620100101    1702307202    1702307202    1702307202    1750102401   
##  [6301] 3210400105    231XXXXXXX    231XXXXXXX    299XXXXXXX013 299XXXXXXX013
##  [6306] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013
##  [6311] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [6316] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016
##  [6321] 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 17503XXXXX   
##  [6326] 3161000112    1750300901    19501001XX    16501XXXXX    228XXXXXXX   
##  [6331] 228XXXXXXX    228XXXXXXX    228XXXXXXX    2280400203    3210501001   
##  [6336] 2294200602    32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX   
##  [6341] 22901008XX    17039008XX    17039191XX    1706307901    22801001XX   
##  [6346] 17040075XX    1702305001    1480403202    1060800301    17039XXXXX   
##  [6351] 17039XXXXX    17039XXXXX    17039XXXXX    11004001XX    11004001XX   
##  [6356] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##  [6361] 31616XXXXX    1480400802    1704100702    1703919103    1702300411   
##  [6366] 1210501210    1703907601    1480401501    1703929301    1703927702   
##  [6371] 17204002XX    17039033XX    17039033XX    17039033XX    17039033XX   
##  [6376] 31608XXXXX    17501002XX    17801XXXXX    17801XXXXX    17801XXXXX   
##  [6381] 17801XXXXX    17801XXXXX    1703935301    199XXXXXXX054 199XXXXXXX054
##  [6386] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1480500404    1480500404   
##  [6391] 1750600601    16302XXXXX    1750102501    1750102501    1750102501   
##  [6396] 1080100301    3161100601    10804007XX    18303XXXXX    18303057XX   
##  [6401] 1750102608    2250100102    1721335202    3161100105    1830804606   
##  [6406] 1704100701    17041007XX    17041007XX    17041007XX    1750400301   
##  [6411] 1060600601    18304XXXXX    18304XXXXX    18304XXXXX    1732100401   
##  [6416] 22901001XX    22901001XX    22901001XX    175XXXXXXX    175XXXXXXX   
##  [6421] 175XXXXXXX    18305XXXXX    32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [6426] 32105XXXXX036 32105XXXXX036 32105XXXXX036 17212XXXXX    1704149903   
##  [6431] 1704149903    1480403401    1750102610    1750102610    2290100108   
##  [6436] 231XXXXXXX    199XXXXXXX010 22801001XX    30706002XX    175XXXXXXX   
##  [6441] 1830200408    1830200408    1480401601    1480401601    1750102605   
##  [6446] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [6451] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [6456] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [6461] 1610200301    1610200301    17023048XX    17023048XX    17023048XX   
##  [6466] 17023048XX    17023048XX    17023048XX    17023048XX    1830201401   
##  [6471] 17092XXXXX    17092XXXXX    1709253501    2302012303    1709201501   
##  [6476] 1709201501    699XXXXXXX    699XXXXXXX    699XXXXXXX    699XXXXXXX   
##  [6481] 1480500406    3210501003    12305015XX    12305015XX    12305015XX   
##  [6486] 12305015XX    1780701403    1750102601    1750102601    1750102601   
##  [6491] 1750102601    1750102601    1750102601    1750102601    1760301104   
##  [6496] 1480400202    1480400202    1830200201    1210500105    1210500105   
##  [6501] 1702300401    1702300401    1750100205    1750100205    1210502403   
##  [6506] 17801001XX    17801001XX    1750300404    1750300404    1750300404   
##  [6511] 1750300404    1750300404    17802020XX    1750300904    1750300904   
##  [6516] 1750300904    1750300904    1750300904    1750300904    1710200101   
##  [6521] 1703900803    17710001XX    17710001XX    17710001XX    17710001XX   
##  [6526] 17710001XX    17710001XX    1830804601    1830804601    1480500408   
##  [6531] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [6536] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [6541] 1750102612    1750102612    1750102612    1750102612    1750300507   
##  [6546] 1750300507    1750300507    1750300507    1750300507    1750300507   
##  [6551] 1750300507    1750300507    1750300507    1750300507    1709441601   
##  [6556] 1480203001    1480203001    1480203001    1760300401    1760300401   
##  [6561] 1480501702    1750100207    1750300505    1750300505    1750300505   
##  [6566] 1750300505    1750300505    1750300505    1750300505    1750300505   
##  [6571] 1750300505    1750300505    1750300505    1750300505    1750300505   
##  [6576] 1480403301    1780200301    1780200301    1780200301    17603XXXXX   
##  [6581] 17603XXXXX    17603XXXXX    17603XXXXX    17603XXXXX    3210400112   
##  [6586] 14805004XX034 1702300413    1230400201    321XXXXXXX    1702300405   
##  [6591] 1230100907    1750100201    1750100201    1750100201    1750100201   
##  [6596] 1750100201    1750100201    1750100201    1750100201    1230100903   
##  [6601] 316XXXXXXX    316XXXXXXX    121XXXXXXX020 1230100908    1702807101   
##  [6606] 1702807101    1702807101    1702807101    1702807101    1702807101   
##  [6611] 1702807101    32104001XX    14313XXXXX    17037XXXXX    17037XXXXX   
##  [6616] 17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
##  [6621] 17037XXXXX    17094XXXXX    1702300414    32102XXXXX026 32102XXXXX026
##  [6626] 32102XXXXX026 32102XXXXX026 32102XXXXX026 32102XXXXX026 1430901102   
##  [6631] 1430901102    1230502901    199XXXXXXX012 199XXXXXXX012 199XXXXXXX012
##  [6636] 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012
##  [6641] 1210506001    1480500401    199XXXXXXX009 183XXXXXXX    183XXXXXXX   
##  [6646] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
##  [6651] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
##  [6656] 1650100102    1830201404    1830201404    14704XXXXX    17501023XX018
##  [6661] 17501023XX018 17501023XX018 17501023XX018 17501023XX018 17501023XX018
##  [6666] 17501023XX018 17501023XX018 148XXXXXXX    148XXXXXXX    148XXXXXXX   
##  [6671] 148XXXXXXX    148XXXXXXX    148XXXXXXX    148XXXXXXX    148XXXXXXX   
##  [6676] 148XXXXXXX    2311100404    3070300109    2302012304    3210603301   
##  [6681] 1311606801    1311606801    1311606801    1311606801    1702300415   
##  [6686] 1830200501    14806001XX    14806001XX    1709201906    1709201906   
##  [6691] 199XXXXXXX007 199XXXXXXX007 17002042XX    17002XXXXX    17002XXXXX   
##  [6696] 17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX   
##  [6701] 17002XXXXX    17036XXXXX    17036XXXXX    17036XXXXX    17036XXXXX   
##  [6706] 17036XXXXX    17036XXXXX    17036XXXXX    17603011XX    17802XXXXX   
##  [6711] 17802XXXXX    17802XXXXX    1480401001    1480401001    14805004XX   
##  [6716] 3160400508    3070500202    1709201903    3161200102    17501014XX   
##  [6721] 1750300402    1750300402    1750300402    1750300402    1750300402   
##  [6726] 1750300402    1750300402    1750300402    17023004XX    17023004XX   
##  [6731] 1750101512    1210600202    3161102002    3210505803    3210505803   
##  [6736] 1470401002    3161101701    1702300403    1210501301    1727210301   
##  [6741] 1702304307    1702304307    6941400401    1700829701    1620100101   
##  [6746] 1620100101    1620100101    1620100101    1620100101    1620100101   
##  [6751] 3210502301    3210502301    1830200802    1830200802    23020018XX   
##  [6756] 23020018XX    2280100109    13208XXXXX    1703906002    1750600302   
##  [6761] 1750600302    1750300906    1750300906    3210400105    2290100101   
##  [6766] 1709441701    1709441701    17501XXXXX    1709201902    1709201902   
##  [6771] 231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX   
##  [6776] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 199XXXXXXX010
##  [6781] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [6786] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [6791] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [6796] 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016
##  [6801] 399XXXXXXX016 17503XXXXX    1230100905    1620100402    228XXXXXXX   
##  [6806] 228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX   
##  [6811] 228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX    3210500301   
##  [6816] 3210500301    3210500301    1480500407    2280400203    3210501001   
##  [6821] 1709446601    32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX   
##  [6826] 32109XXXXX    32109XXXXX    32109XXXXX    1780701402    1750102602   
##  [6831] 1750102602    1750102602    1750102602    1750102602    1750102602   
##  [6836] 1480400211    1480400211    1830200202    1830200202    1210500107   
##  [6841] 1210500107    1702300406    1702300406    1780100109    1780100109   
##  [6846] 1780100109    1760802001    12301009XX    1720400204    1470200701   
##  [6851] 1470200701    1750101509    22804002XX    17039008XX    1703922001   
##  [6856] 1480501701    3210400102    1709201502    1709201502    1709201502   
##  [6861] 1709201502    199XXXXXXX008 199XXXXXXX008 199XXXXXXX013 199XXXXXXX013
##  [6866] 199XXXXXXX013 199XXXXXXX013 22801001XX    22801001XX    22801001XX   
##  [6871] 1707027003    1580200101    1230100902    17039XXXXX    17039XXXXX   
##  [6876] 17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
##  [6881] 17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX    19002XXXXX   
##  [6886] 1230100909    110XXXXXXX    1480201401    2302001801    1703900807   
##  [6891] 2312114503    1210503101    1480600105    1830204301    1830204301   
##  [6896] 1480600401    1780800401    1780800401    1780800401    1480401501   
##  [6901] 1480401501    17801XXXXX    17801XXXXX    17801XXXXX    17801XXXXX   
##  [6906] 1703935301    69302004XX    17501015XX    17501015XX    17501015XX   
##  [6911] 3210506001    12105011XX    199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
##  [6916] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
##  [6921] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
##  [6926] 199XXXXXXX054 199XXXXXXX054 1750300905    1750300905    1480500404   
##  [6931] 1703919115    1703919115    1703919115    1750102501    1750102501   
##  [6936] 1750102501    1750102501    1750102501    1750102501    1750102501   
##  [6941] 1750102501    1750102501    1750102501    1750102501    1750102501   
##  [6946] 1705700703    17032027XX    1750500101    1750500101    1750500101   
##  [6951] 1230100906    1709441801    1480403302    1480403302    1750102608   
##  [6956] 1750102608    1750102608    1750102608    1750102608    1750102608   
##  [6961] 1750102608    1709448001    1700600602    1750300903    1750300903   
##  [6966] 1750300903    1750300903    1750300903    1750300903    1750300903   
##  [6971] 1750300903    2302007002    1750400301    1750400301    1750400301   
##  [6976] 1750400301    1750400301    1750400301    1750400301    1750400301   
##  [6981] 1750400301    1750400301    1750400301    1750400301    1750400301   
##  [6986] 1750400301    1750400301    1480204001    23121145XX    23121145XX   
##  [6991] 1707030504    17016XXXXX    17092448XX    22901001XX    22901001XX   
##  [6996] 12301004XX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [7001] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [7006] 175XXXXXXX    175XXXXXXX    175XXXXXXX    1709447001    1709447001   
##  [7011] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [7016] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [7021] 32105XXXXX036 32105XXXXX036 32105XXXXX036 1620400702    3210505901   
##  [7026] 2314300102    1100500301    1100500301    1750500201    1480600104   
##  [7031] 1830201102    17102001XX    1703730305    1709243002    1830202402   
##  [7036] 1830202402    1750102610    1750102610    1750102610    1750102610   
##  [7041] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [7046] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [7051] 3160806607    17038XXXXX    17501023XX018 17000XXXXX    1750102406   
##  [7056] 1750102603    199XXXXXXX010 1750101503    17023043XX    1750102501   
##  [7061] 17407001XX    175XXXXXXX    1750102610    1750102605    17023048XX   
##  [7066] 17710001XX    1750102612    1750300507    17023XXXXX    121XXXXXXX020
##  [7071] 31607008XX    199XXXXXXX012 17038XXXXX    17036XXXXX    1750300402   
##  [7076] 231XXXXXXX    299XXXXXXX013 199XXXXXXX010 17503XXXXX    16501XXXXX   
##  [7081] 1750101503    228XXXXXXX    32109XXXXX    199XXXXXXX013 694XXXXXXX   
##  [7086] 199XXXXXXX054 1750102501    17032XXXXX    17407001XX    1750400301   
##  [7091] 22901001XX    175XXXXXXX    32105XXXXX036 1750102610    1750102605   
##  [7096] 17710001XX    1750102612    1750300507    1750300505    121XXXXXXX020
##  [7101] 17038XXXXX    14704XXXXX    17041251XX    17002XXXXX    17023044XX   
##  [7106] 299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 1220200101    17046036XX   
##  [7111] 16501XXXXX    32109XXXXX    170XXXXXXX    694XXXXXXX    199XXXXXXX054
##  [7116] 1750102501    17032XXXXX    16111XXXXX    1750300903    1750400301   
##  [7121] 1750102610    1480401601    17037XXXXX    32102XXXXX026 183XXXXXXX   
##  [7126] 1210501301    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 228XXXXXXX   
##  [7131] 32109XXXXX    1780701402    17039XXXXX    69302004XX    32105XXXXX036
##  [7136] 1709400101    30703001XX    1705013202    2280700903    1480401601   
##  [7141] 1480401601    1750102605    1750102605    1750102605    1750102605   
##  [7146] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [7151] 1750102605    1750102605    1750102605    1750102605    1750102605   
##  [7156] 1750102605    16102003XX    16102003XX    16102003XX    16102003XX   
##  [7161] 16102003XX    16102003XX    16102003XX    17023048XX    17023048XX   
##  [7166] 17023048XX    17023048XX    17023048XX    1830201401    19501XXXXX   
##  [7171] 1703906010    17092XXXXX    1100400132    2302012303    1709201501   
##  [7176] 1709201501    1709201501    699XXXXXXX    1480500406    3210501003   
##  [7181] 31604001XX    1780701403    1750102601    1750102601    1750102601   
##  [7186] 1750102601    1480400202    1830200201    17801001XX    1750300404   
##  [7191] 1750300404    1750300404    1750300404    1750300404    1750300904   
##  [7196] 1750300904    1750300904    17710001XX    17710001XX    1780901801   
##  [7201] 1830804601    1580200502    1480500408    1480500408    1750102612   
##  [7206] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [7211] 1750102612    1750102612    1750102612    1750102612    1750102612   
##  [7216] 1750102612    1750102612    1750300507    1750300507    1750300507   
##  [7221] 1750300507    1750300507    1750300507    1750300507    1750300507   
##  [7226] 1750300507    1750300507    1780101703    1709441601    1709441601   
##  [7231] 1709441601    3160407101    1480203001    1480203001    1760300401   
##  [7236] 1480501702    1750100207    1750300505    1750300505    1750300505   
##  [7241] 1750300505    1750300505    1750300505    1750300505    1750300505   
##  [7246] 1750300505    1750300505    1750300505    1080200401    1080200401   
##  [7251] 1080200401    1780200301    1780200301    16203XXXXX    1703700921   
##  [7256] 1311606804    17603XXXXX    17603XXXXX    17603XXXXX    1703001001   
##  [7261] 1702300413    1702300405    1210505803    1750100201    1750100201   
##  [7266] 1750100201    1750100201    1750100201    1750100201    1750100201   
##  [7271] 1750100201    316XXXXXXX    121XXXXXXX020 121XXXXXXX020 121XXXXXXX020
##  [7276] 31623XXXXX    32104001XX    14313XXXXX    14313XXXXX    14313XXXXX   
##  [7281] 14313XXXXX    14313XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
##  [7286] 17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
##  [7291] 17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
##  [7296] 1702300414    15802001XX    15802001XX    15802XXXXX    32102XXXXX026
##  [7301] 32102XXXXX026 32102XXXXX026 32102XXXXX026 32102XXXXX026 32102XXXXX026
##  [7306] 32102XXXXX026 32102XXXXX026 1430901102    17039060XX    10901XXXXX   
##  [7311] 109XXXXXXX    1100400201    1100400201    689XXXXXXX    1211200103   
##  [7316] 17038XXXXX    17038XXXXX    1210506401    199XXXXXXX009 183XXXXXXX   
##  [7321] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
##  [7326] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
##  [7331] 1650100102    2280100116    17501023XX018 148XXXXXXX    148XXXXXXX   
##  [7336] 148XXXXXXX    148XXXXXXX    148XXXXXXX    148XXXXXXX    148XXXXXXX   
##  [7341] 148XXXXXXX    148XXXXXXX    148XXXXXXX    307XXXXXXX    2311100404   
##  [7346] 17041XXXXX    17041XXXXX    17321XXXXX023 1830200501    14806001XX   
##  [7351] 14806001XX    14806001XX    14806001XX    14806XXXXX    14806XXXXX   
##  [7356] 14806XXXXX    1709201906    199XXXXXXX007 17002042XX    17002042XX   
##  [7361] 17002042XX    17002042XX    17002042XX    17002XXXXX    17002XXXXX   
##  [7366] 17036XXXXX    17036XXXXX    17036XXXXX    10303XXXXX    17506XXXXX   
##  [7371] 17506XXXXX    17506XXXXX    17506XXXXX    17506XXXXX    17506XXXXX   
##  [7376] 17506XXXXX    17506XXXXX    17506XXXXX    14805004XX    14805004XX   
##  [7381] 14805004XX    1703729805    3070500202    3161200102    1750300402   
##  [7386] 1750300402    1750300402    1750300402    1750300402    1750300402   
##  [7391] 17023004XX    17023004XX    17023004XX    17023004XX    17023044XX   
##  [7396] 17023044XX    17023044XX    17023044XX    1750101512    1210600202   
##  [7401] 3161102002    3210505803    1470300311    3161101701    1702300403   
##  [7406] 1210501301    1727210301    1210501222    6941400401    1700829701   
##  [7411] 1620100101    1620100101    1620100101    1620100101    1620100101   
##  [7416] 3210502301    1100400212    23020018XX    23020XXXXX    1580200105   
##  [7421] 3161000101    1500500901    2280100109    13208XXXXX    1703730304   
##  [7426] 1750600302    1750600302    18301XXXXX    18301XXXXX    18301XXXXX   
##  [7431] 18301XXXXX    18301XXXXX    18301XXXXX    18301XXXXX    18301XXXXX   
##  [7436] 18301XXXXX    2290100101    1709244002    1709441701    231XXXXXXX   
##  [7441] 231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX   
##  [7446] 231XXXXXXX    231XXXXXXX    299XXXXXXX013 299XXXXXXX013 299XXXXXXX013
##  [7451] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 199XXXXXXX010
##  [7456] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [7461] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [7466] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016
##  [7471] 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016
##  [7476] 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 649XXXXXXX    17503XXXXX   
##  [7481] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
##  [7486] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
##  [7491] 17503XXXXX    1100400202    14801001XX    16501XXXXX    1100400203   
##  [7496] 228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX   
##  [7501] 228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX   
##  [7506] 228XXXXXXX    228XXXXXXX    32109XXXXX    32109XXXXX    32109XXXXX   
##  [7511] 32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX   
##  [7516] 32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX    1750500701   
##  [7521] 1780701402    1610500202    1750102602    1750102602    1750102602   
##  [7526] 1750102602    1480400211    1480400211    3160700801    1210500107   
##  [7531] 1210500107    1702300406    1780100109    1720400204    1470200701   
##  [7536] 1470200701    1470200701    1750101509    1750101509    17039191XX   
##  [7541] 1480501701    1480501701    1709201502    1709201502    1709201502   
##  [7546] 1709201502    1709201502    1709201502    1709201502    1705700701   
##  [7551] 22801001XX    22801001XX    1580200101    1580200101    1708800101   
##  [7556] 17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
##  [7561] 17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
##  [7566] 17039XXXXX    19002XXXXX    19002XXXXX    19002XXXXX    19002XXXXX   
##  [7571] 19002XXXXX    11004001XX    11004XXXXX    110XXXXXXX    110XXXXXXX   
##  [7576] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##  [7581] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##  [7586] 110XXXXXXX    110XXXXXXX    110XXXXXXX    1703900807    1480600105   
##  [7591] 17608XXXXX    17608XXXXX    17608XXXXX    123XXXXXXX    12105012XX   
##  [7596] 17801XXXXX    17801XXXXX    17801XXXXX    17801XXXXX    17801XXXXX   
##  [7601] 17801XXXXX    17801XXXXX    17801XXXXX    31610XXXXX    17501015XX   
##  [7606] 17501015XX    17501015XX    17501015XX    17501015XX    3210506001   
##  [7611] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
##  [7616] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
##  [7621] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 2280101607    17015XXXXX   
##  [7626] 1480500404    1760300901    1750600601    1750600601    1703919115   
##  [7631] 1750102501    1750102501    1750102501    1750102501    1750102501   
##  [7636] 1750102501    1750102501    1750102501    1750102501    1750102501   
##  [7641] 1750102501    1750102501    1480100101    17032027XX    17032XXXXX   
##  [7646] 18303XXXXX    1709441801    18303057XX    1480403302    1750102608   
##  [7651] 1750102608    1750102608    1750102608    1480500403    1480500403   
##  [7656] 2280104302    1750300903    1750300903    1750300903    1750300903   
##  [7661] 1750300903    1750300903    1750300903    17041007XX    1750400301   
##  [7666] 1750400301    1750400301    1750400301    1750400301    1750400301   
##  [7671] 1750400301    1750400301    1750400301    1750400301    1750400301   
##  [7676] 1750400301    1750400301    1750400301    1750400301    1480204001   
##  [7681] 23121145XX    17077XXXXX    17077XXXXX    17077XXXXX    17077XXXXX   
##  [7686] 1900901001    1060600601    17016XXXXX    18304XXXXX    18304XXXXX   
##  [7691] 18304XXXXX    18304XXXXX    18304XXXXX    18304XXXXX    18304XXXXX   
##  [7696] 18304XXXXX    18304XXXXX    18304XXXXX    19010XXXXX    19010XXXXX   
##  [7701] 19010XXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [7706] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [7711] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
##  [7716] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [7721] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [7726] 32105XXXXX036 32105XXXXX036 32105XXXXX036 1760800309    1772301101   
##  [7731] 1750101511    1704149903    1704149903    1431300105    1480600104   
##  [7736] 1480600104    1830201102    1703730305    1830205001    1750102610   
##  [7741] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [7746] 1750102610    1750102610    1750102610    1750102610    1750102610   
##  [7751] 1750102610    1750102610    1750102610    1830202404    3160806607   
##  [7756] 1702309901    2311100401    1311606804    17023XXXXX    1702222101   
##  [7761] 17037XXXXX    17038XXXXX    1707700201    17002042XX    17036XXXXX   
##  [7766] 1210503801    1750101504    1703910501    1650101217    199XXXXXXX010
##  [7771] 16501XXXXX    1750101503    228XXXXXXX    1760300901    17032027XX   
##  [7776] 17033184XX    1703718603    1703933005    1702304605    16102003XX   
##  [7781] 1830201401    1950100103    1210600206    1480500406    3210501003   
##  [7786] 12305015XX    1750100101    1750100101    1702326801    1702326801   
##  [7791] 1480400202    1480400202    1210500105    1210500105    1702300401   
##  [7796] 1750100205    1750100205    1702700301    1702700301    17801001XX   
##  [7801] 17801001XX    1230100401    1710200101    1703626303    1703626303   
##  [7806] 1703900801    1760300401    1480403301    1702021301    1702021301   
##  [7811] 1300100501    1480400801    14805004XX034 1702300413    1230400201   
##  [7816] 1230400201    17023XXXXX    17023XXXXX    17023XXXXX    1702300405   
##  [7821] 1750100201    1750100201    1750100201    121XXXXXXX020 121XXXXXXX020
##  [7826] 1400200201    1703906006    1732101702    17037XXXXX    1400201601   
##  [7831] 32102XXXXX026 14002XXXXX    10901XXXXX    1711500401    1210600201   
##  [7836] 1210600201    1830204802    1210506401    1830200405    1230400301   
##  [7841] 1210506601    199XXXXXXX009 1400200102    17501023XX018 148XXXXXXX   
##  [7846] 1470100101    1702300415    1830200501    1830200501    14806001XX   
##  [7851] 199XXXXXXX007 17036XXXXX    17036XXXXX    17802XXXXX    17802XXXXX   
##  [7856] 1480401001    1480401001    17023004XX    17023044XX    1620100101   
##  [7861] 1580200105    1703906002    1703906002    1750600302    1750600302   
##  [7866] 1702307202    1750102401    1510300401    1709244002    17501XXXXX   
##  [7871] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [7876] 16501XXXXX    228XXXXXXX    2280400203    2280400203    3210501001   
##  [7881] 32109XXXXX    1400202001    22901008XX    1480501701    1709201502   
##  [7886] 199XXXXXXX013 17039XXXXX    17039XXXXX    11004001XX    110XXXXXXX   
##  [7891] 110XXXXXXX    1480400802    1400201801    1702300411    1210501210   
##  [7896] 1480600401    1480600401    1480401501    1480401501    123XXXXXXX   
##  [7901] 12105012XX    12105012XX    17039033XX    17813XXXXX    14102XXXXX   
##  [7906] 14102XXXXX    1020100101    1230100402    1480500402    199XXXXXXX054
##  [7911] 199XXXXXXX054 199XXXXXXX054 1781301203    1480500404    1750600601   
##  [7916] 1750102501    1750500101    1210501303    1480403302    1500100101   
##  [7921] 19010XXXXX    19010XXXXX    175XXXXXXX    175XXXXXXX    1830509201   
##  [7926] 1210501105    32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [7931] 32105XXXXX036 1400209701    1750101511    17037457XX    17037457XX   
##  [7936] 1400233301    12312001XX    1480403401    1830201102    1750102610   
##  [7941] 17710001XX    17023XXXXX    121XXXXXXX020 3210900507    32102XXXXX026
##  [7946] 1431300101    183XXXXXXX    148XXXXXXX    17002XXXXX    17501XXXXX   
##  [7951] 299XXXXXXX013 199XXXXXXX010 16501XXXXX    17040075XX    17039XXXXX   
##  [7956] 17801XXXXX    199XXXXXXX054 16302XXXXX    17041007XX    175XXXXXXX   
##  [7961] 1702304605    1705013202    1750102605    1702326801    1750300404   
##  [7966] 1750300904    17710001XX    1580200502    1480500408    1703626303   
##  [7971] 1750102612    1750102612    1703906302    1760300401    1750300505   
##  [7976] 1080200401    1703745705    1300100501    1210503002    17023XXXXX   
##  [7981] 1703745702    1750100201    121XXXXXXX020 1702807101    14313XXXXX   
##  [7986] 17037XXXXX    1702300414    32102XXXXX026 2280101701    17039060XX   
##  [7991] 10901XXXXX    1702304442    14704XXXXX    17002042XX    17036XXXXX   
##  [7996] 11001XXXXX    14703004XX    10803XXXXX    1090101801    1750600302   
##  [8001] 1702307202    1707700302    11008XXXXX    231XXXXXXX    299XXXXXXX013
##  [8006] 199XXXXXXX010 17503XXXXX    16501XXXXX    228XXXXXXX    14701XXXXX   
##  [8011] 32109XXXXX    17039XXXXX    110XXXXXXX    1707700401    12105012XX   
##  [8016] 11002XXXXX    14102XXXXX    199XXXXXXX054 1060800201    1080201017   
##  [8021] 1750600601    1750102501    17032027XX    18303XXXXX    1703620919   
##  [8026] 17042XXXXX    1750400301    1060600601    19010XXXXX    22901001XX   
##  [8031] 175XXXXXXX    17037457XX    1704149903    1211200112    1750102610   
##  [8036] 1750102610    1750102601    1750102601    1750100101    17710001XX   
##  [8041] 1750102612    1703926101    1703700921    2280100117    1750100201   
##  [8046] 1750100201    3210200202    1703906006    1702807101    3210900507   
##  [8051] 1703900802    1830300701    32104001XX    32104001XX    17037XXXXX   
##  [8056] 32102XXXXX026 10901XXXXX    1700204201    1650100102    1703923508   
##  [8061] 1702304801    1901000201    11001XXXXX    14805004XX    17023004XX   
##  [8066] 17023004XX    1750102401    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010
##  [8071] 228XXXXXXX    32109XXXXX    1706505506    22801001XX    1750100601   
##  [8076] 17039XXXXX    17039XXXXX    1480403203    1210501210    1703907601   
##  [8081] 1703929301    17801XXXXX    1060800201    10804007XX    17407001XX   
##  [8086] 1700634501    17041007XX    1750400301    1750400301    175XXXXXXX   
##  [8091] 1703903303    1750102610    1702304605    1705013202    1703619705   
##  [8096] 1702309003    16102003XX    16102003XX    16102003XX    17023048XX   
##  [8101] 17023048XX    1830201401    1950100103    12106XXXXX    1210600206   
##  [8106] 1480500406    12305015XX    1400211501    1750100101    1750100101   
##  [8111] 1702326801    1702326801    1480400202    1480400202    1830200201   
##  [8116] 1210500105    1210500105    1702300401    1750100205    1750100205   
##  [8121] 1702700301    1702700301    17801001XX    17801001XX    1230100401   
##  [8126] 1710200101    1231400701    17710001XX    1703620918    1703626303   
##  [8131] 1703626303    1750601201    1701300701    1760300401    1480400502   
##  [8136] 1750300505    1480403301    1702021301    1702021301    1703926101   
##  [8141] 1300100501    1210503002    17030XXXXX    1480400801    14805004XX034
##  [8146] 1702300413    1230400201    1230400201    17023XXXXX    1702300405   
##  [8151] 1750100201    1750100201    1750100201    1750100201    121XXXXXXX020
##  [8156] 2282300303    17037XXXXX    17037XXXXX    1400201601    1702300414   
##  [8161] 32102XXXXX026 32102XXXXX026 14002XXXXX    2280101701    17039060XX   
##  [8166] 17039060XX    10901XXXXX    10901XXXXX    1210600201    1830204802   
##  [8171] 1210506401    1210506401    1230400301    1210506601    1231200102   
##  [8176] 199XXXXXXX009 199XXXXXXX009 183XXXXXXX    183XXXXXXX    1400200102   
##  [8181] 14002001XX    17501023XX018 148XXXXXXX    148XXXXXXX    1470100101   
##  [8186] 17321XXXXX023 1702300415    1830200501    1830200501    14806001XX   
##  [8191] 14806XXXXX    17036XXXXX    17036XXXXX    17802XXXXX    17802XXXXX   
##  [8196] 1480401001    1480401001    17506XXXXX    14805004XX    14805004XX   
##  [8201] 17023004XX    17023004XX    17023044XX    1620100101    1580200105   
##  [8206] 1703906002    1750600302    1750600302    1702307202    1702307202   
##  [8211] 1750102401    1090101602    1510300401    1709244002    17501XXXXX   
##  [8216] 1210501217    231XXXXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
##  [8221] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 16501XXXXX    228XXXXXXX   
##  [8226] 228XXXXXXX    228XXXXXXX    14701XXXXX    2280400203    2280400203   
##  [8231] 3210501001    32109XXXXX    1702300406    1480501701    1709201502   
##  [8236] 1702304706    17039XXXXX    17039XXXXX    1090101601    11004001XX   
##  [8241] 11004001XX    11201004XX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##  [8246] 1480400802    1703919103    1400201801    1480600103    1480600103   
##  [8251] 1480600802    1210501210    1480600401    1480600401    1703620705   
##  [8256] 1400201901    17608XXXXX    1480401501    1480401501    17204002XX   
##  [8261] 12105012XX    12105012XX    31608XXXXX    17801XXXXX    14102XXXXX   
##  [8266] 14102XXXXX    1230100402    12105011XX    199XXXXXXX054 199XXXXXXX054
##  [8271] 1400210001    1480500404    1750600601    1750102501    17505XXXXX   
##  [8276] 1750500101    1210501303    18303057XX    1480403302    1702700302   
##  [8281] 1750400301    1500100101    19010XXXXX    175XXXXXXX    175XXXXXXX   
##  [8286] 175XXXXXXX    175XXXXXXX    1830509201    1702352601    32105XXXXX036
##  [8291] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
##  [8296] 32105XXXXX036 1400209701    1750101511    17037457XX    17037457XX   
##  [8301] 1480400803    1480400803    1703903303    1830201102    17102001XX   
##  [8306] 1750102610    1830202404    1750102605    1750102605    1750102612   
##  [8311] 1750102612    1750300507    1750300505    1750300505    321XXXXXXX   
##  [8316] 199XXXXXXX012 17501023XX018 1750101504    1750300402    1750102406   
##  [8321] 1750102603    231XXXXXXX    199XXXXXXX010 399XXXXXXX016 17503XXXXX   
##  [8326] 17503XXXXX    1750101503    228XXXXXXX    694XXXXXXX    199XXXXXXX054
##  [8331] 199XXXXXXX054 1750300905    1750102501    1750102608    1750300903   
##  [8336] 1750300903    1750400301    1750400301    22901001XX    1750101001   
##  [8341] 1750102610    1750102610    1750102605    12106XXXXX    17710001XX   
##  [8346] 17710001XX    1700116701    1700116701    1702329101    1702329101   
##  [8351] 1750102612    1750102612    17011026XX    17011026XX    1702309901   
##  [8356] 1702309901    1311600102    1311600102    17603XXXXX    17603XXXXX   
##  [8361] 17023XXXXX    17023XXXXX    1210502301    1210502301    316XXXXXXX   
##  [8366] 316XXXXXXX    121XXXXXXX020 121XXXXXXX020 1702222101    1702222101   
##  [8371] 17037XXXXX    17037XXXXX    32102XXXXX026 32102XXXXX026 1430901102   
##  [8376] 1430901102    199XXXXXXX012 199XXXXXXX012 121XXXXXXX019 121XXXXXXX019
##  [8381] 14106064XX    14106064XX    17038XXXXX    17038XXXXX    1701916502   
##  [8386] 1701916502    183XXXXXXX    183XXXXXXX    17809XXXXX    17809XXXXX   
##  [8391] 17501023XX018 17501023XX018 17000XXXXX    17000XXXXX    17041251XX   
##  [8396] 17041251XX    1700204219    17002042XX    17002042XX    17036XXXXX   
##  [8401] 17036XXXXX    17501014XX    17501014XX    1211200303    1211200303   
##  [8406] 1702304308    1702304308    1750300402    1290200402    1290200402   
##  [8411] 61841007XX    61841007XX    1750102406    1750102406    1750600302   
##  [8416] 1750600302    13116XXXXX    13116XXXXX    1750102603    1750102603   
##  [8421] 17501XXXXX    1703202702    1703202702    231XXXXXXX    231XXXXXXX   
##  [8426] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 17503XXXXX   
##  [8431] 17503XXXXX    17046036XX    17046036XX    17033230XX    17033230XX   
##  [8436] 16501XXXXX    16501XXXXX    228XXXXXXX    228XXXXXXX    14701013XX   
##  [8441] 14701013XX    32109XXXXX    32109XXXXX    199XXXXXXX013 199XXXXXXX013
##  [8446] 170XXXXXXX    170XXXXXXX    17035169XX    17035169XX    17023231XX   
##  [8451] 17023231XX    1702313401    1702313401    110XXXXXXX    110XXXXXXX   
##  [8456] 14102XXXXX    14102XXXXX    694XXXXXXX    694XXXXXXX    17501015XX   
##  [8461] 17501015XX    22807XXXXX    22807XXXXX    199XXXXXXX054 199XXXXXXX054
##  [8466] 17015XXXXX    17015XXXXX    1703620904    1703620904    1760300901   
##  [8471] 1760300901    1750102501    1750102501    17032027XX    17032027XX   
##  [8476] 17032XXXXX    17032XXXXX    17407001XX    17407001XX    1705013201   
##  [8481] 1705013201    12106050XX    12106050XX    1750400301    1750400301   
##  [8486] 17033184XX    17033184XX    17077XXXXX    17077XXXXX    18304XXXXX   
##  [8491] 18304XXXXX    1702317901    1702317901    19010XXXXX    19010XXXXX   
##  [8496] 22901001XX    22901001XX    175XXXXXXX    32105XXXXX036 32105XXXXX036
##  [8501] 12111002XX    12111002XX    17063XXXXX    17063XXXXX    1750102610   
##  [8506] 1750102610    1702342201    1702342201    1750102612    1750101202   
##  [8511] 17501023XX018 1750102406    199XXXXXXX010 399XXXXXXX016 694XXXXXXX   
##  [8516] 199XXXXXXX054 1750102501    22901001XX    175XXXXXXX    1750102610   
##  [8521] 1750102605    10903XXXXX    1703903302    1750102601    1750100101   
##  [8526] 1311601003    1703900803    1703906302    1780101703    1703900801   
##  [8531] 2280203101    1080200401    1480403301    1050200201    1703926101   
##  [8536] 3210501002    1703700921    17023XXXXX    10801003XX    1750100201   
##  [8541] 121XXXXXXX020 1700206101    3210200202    1703906006    1702807101   
##  [8546] 1100700801    1703900802    2281201810    1830300701    2290100804   
##  [8551] 1100500326    1703903305    17037XXXXX    2280101701    10901007XX   
##  [8556] 1700204201    1210600201    1771000101    1431300101    3210505801   
##  [8561] 1480500401    1210506401    1700634503    3210400109    1782400201   
##  [8566] 14804006XX    17501023XX018 2280203001    1703923508    17321XXXXX023
##  [8571] 2280403201    1702304801    1480400601    1721201002    17002042XX   
##  [8576] 17002XXXXX    1090100801    17802XXXXX    32109024XX    17023004XX   
##  [8581] 1620100101    1750102401    199XXXXXXX010 199XXXXXXX010 1703710601   
##  [8586] 1430600701    1750300901    19501001XX    16501XXXXX    228XXXXXXX   
##  [8591] 2294200602    32109XXXXX    1750500701    1700206102    1706505506   
##  [8596] 17040075XX    1702305001    1060800301    110XXXXXXX    1704100702   
##  [8601] 1703919103    1703907601    1703929301    17039033XX    17801XXXXX   
##  [8606] 12105011XX    199XXXXXXX054 1050200301    1750600601    1080100301   
##  [8611] 10804007XX    1100400104    1721335202    11005XXXXX    1704100701   
##  [8616] 17041007XX    1750400301    1100400102    1732100401    175XXXXXXX   
##  [8621] 1700204202    1703903303    17063XXXXX    1700505801    1750102605   
##  [8626] 1750102612    1750300507    1750300505    2311114001    199XXXXXXX010
##  [8631] 199XXXXXXX010 228XXXXXXX    1750102501    1750300903    1750400301   
##  [8636] 22901001XX    1750102610    1750100101    1750300404    1750102604   
##  [8641] 2290100108    1750101508    316XXXXXXX    121XXXXXXX020 1702807101   
##  [8646] 14704XXXXX    199XXXXXXX010 17503XXXXX    110XXXXXXX    69302004XX   
##  [8651] 199XXXXXXX054 30706002XX    1750102610    1705013202    1702309003   
##  [8656] 22802031XX    1750100101    1702326801    1080600302    1080702001   
##  [8661] 1580200502    1703626303    1100100507    1760300401    1702021301   
##  [8666] 1210503002    1703707009    17023XXXXX    321XXXXXXX    1750100201   
##  [8671] 121XXXXXXX020 1702222101    1702807101    14313XXXXX    17037XXXXX   
##  [8676] 32102XXXXX026 2280101701    17039060XX    1700204201    11007XXXXX   
##  [8681] 1210600201    1210506401    183XXXXXXX    17501023XX018 1703923508   
##  [8686] 17041XXXXX    17002XXXXX    17036XXXXX    17802XXXXX    14805004XX   
##  [8691] 10803XXXXX    17023004XX    1620100101    1750600302    1702307202   
##  [8696] 1707700302    1750102401    1100702406    299XXXXXXX013 199XXXXXXX010
##  [8701] 399XXXXXXX016 1703710601    1080204002    19501001XX    14306XXXXX   
##  [8706] 16501XXXXX    228XXXXXXX    1070300901    32109XXXXX    22901008XX   
##  [8711] 17039008XX    22801001XX    3074200401    1750100601    17039XXXXX   
##  [8716] 19002XXXXX    110XXXXXXX    1703620705    1703927702    12105012XX   
##  [8721] 17039033XX    17023043XX    1080300506    2280202101    17801XXXXX   
##  [8726] 14102XXXXX    694XXXXXXX    199XXXXXXX054 1750102501    1080400713   
##  [8731] 18303XXXXX    17405XXXXX    1101001501    22901XXXXX    1700634501   
##  [8736] 18304XXXXX    22901001XX    175XXXXXXX    1702352601    32105XXXXX036
##  [8741] 1760800309    1750101001    1750101511    17037457XX    2314300102   
##  [8746] 1700204202    1750102605    1750102612    1750300507    17023XXXXX   
##  [8751] 121XXXXXXX020 17038XXXXX    17041251XX    17002XXXXX    1750300402   
##  [8756] 2311114001    17501XXXXX    199XXXXXXX010 17503XXXXX    16501XXXXX   
##  [8761] 228XXXXXXX    32109XXXXX    170XXXXXXX    110XXXXXXX    694XXXXXXX   
##  [8766] 199XXXXXXX054 1750102501    17032XXXXX    17407001XX    1750300903   
##  [8771] 1750400301    22901001XX    175XXXXXXX    1480301801    1750101001   
##  [8776] 1750102610    1750102605    1750102612    1750102612    1750300402   
##  [8781] 199XXXXXXX010 17503XXXXX    199XXXXXXX054 1750102501    1750102501   
##  [8786] 1750400301    175XXXXXXX    1750101001    1750102610    1750102610   
##  [8791] 17002405XX    30703001XX    1750102605    17023048XX    17023048XX   
##  [8796] 3160700803    12106XXXXX    699XXXXXXX    699XXXXXXX    31604001XX   
##  [8801] 1750101507    1750102601    1750100101    1760301104    1750100205   
##  [8806] 1750300404    2280102201    1080204001    1750300904    17710001XX   
##  [8811] 17710001XX    1703639501    1702329101    1060600603    1750102612   
##  [8816] 1750102612    1750102612    1750102612    1703721002    1703721002   
##  [8821] 1750102404    2311005001    1750102604    2311101202    1750300505   
##  [8826] 1702304426    1080200401    2280100110    1650101001    1650101001   
##  [8831] 17002040XX    1210501302    1210600207    6180200101    17023XXXXX   
##  [8836] 17023XXXXX    2290100108    1750100201    1750100201    121XXXXXXX020
##  [8841] 121XXXXXXX020 1702222101    1702807101    1702807101    3210900507   
##  [8846] 1700102510    32104001XX    17037038XX    17037XXXXX    17037XXXXX   
##  [8851] 1703202727    31607008XX    199XXXXXXX012 199XXXXXXX012 1750100104   
##  [8856] 1750100104    689XXXXXXX    689XXXXXXX    199XXXXXXX009 183XXXXXXX   
##  [8861] 183XXXXXXX    1650100102    1650100102    148XXXXXXX    148XXXXXXX   
##  [8866] 307XXXXXXX    307XXXXXXX    1703202728    17002042XX    17002042XX   
##  [8871] 17002XXXXX    17002XXXXX    17036XXXXX    17036XXXXX    1703703908   
##  [8876] 17506XXXXX    17506XXXXX    10803XXXXX    10803XXXXX    1706316401   
##  [8881] 17023044XX    17023044XX    3210502301    1750101506    1290100302   
##  [8886] 1703202733    3210400105    231XXXXXXX    231XXXXXXX    299XXXXXXX013
##  [8891] 199XXXXXXX010 199XXXXXXX010 17503XXXXX    1703235901    3210900519   
##  [8896] 1220200101    1220200101    17046XXXXX    17046XXXXX    16501XXXXX   
##  [8901] 16501XXXXX    1480500407    2280100101    2280100105    1703202725   
##  [8906] 1703202725    3210501001    2280100122    1070300901    1701600103   
##  [8911] 32109XXXXX    3210400103    1210601503    1090300406    1750102602   
##  [8916] 3160803004    1210503307    1702300406    1210506302    1703202757   
##  [8921] 1750101509    1210504201    22801001XX    22801001XX    17023047XX   
##  [8926] 17023047XX    17039034XX    17039XXXXX    110XXXXXXX    110XXXXXXX   
##  [8931] 1480400802    1210503101    10802XXXXX    10802XXXXX    1210501210   
##  [8936] 12105033XX    14102XXXXX    14102XXXXX    694XXXXXXX    694XXXXXXX   
##  [8941] 31610XXXXX    69302004XX    199XXXXXXX054 199XXXXXXX054 1060800201   
##  [8946] 1702304903    1480500404    16302XXXXX    1750102501    1750102501   
##  [8951] 1750102501    1750102501    17032XXXXX    17032XXXXX    17001025XX   
##  [8956] 17001025XX    1100500302    1703202729    1703701609    1703701609   
##  [8961] 30706002XX    30706002XX    1750400301    1750400301    1290200401   
##  [8966] 1080201703    1080201703    17016XXXXX    1703700501    19010XXXXX   
##  [8971] 19010XXXXX    22901001XX    31611XXXXX    31611XXXXX    1703222501   
##  [8976] 17037016XX    17037016XX    1703603010    1650100121    1650100121   
##  [8981] 2280100111    1703202720    1750102610    1750102610    1750102610   
##  [8986] 1750102610    2280100104    1703202801    1750102605    1750102612   
##  [8991] 1750300507    1750300505    2311114001    199XXXXXXX010 228XXXXXXX   
##  [8996] 32109XXXXX    1750102501    1750300903    1750400301    22901001XX   
##  [9001] 1750102610    199XXXXXXX010 1702300401    1750100205    1703926101   
##  [9006] 10801003XX    1750100201    1703906006    3210900507    32104001XX   
##  [9011] 32102XXXXX026 1210600201    1480500401    1210506401    1210506601   
##  [9016] 1650100102    32109024XX    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016
##  [9021] 17040075XX    110XXXXXXX    1703929301    10804007XX    17041007XX   
##  [9026] 175XXXXXXX    199XXXXXXX010 1750102605    1750102605    12305015XX   
##  [9031] 12305015XX    1750102601    1750102601    1750100101    1750100101   
##  [9036] 1750300404    1703900803    1703900803    1750102612    1703906302   
##  [9041] 1703906302    1750300505    1702021301    1702021301    1050200201   
##  [9046] 1703926101    1703926101    1703707009    1703707009    1750100201   
##  [9051] 1750100201    18306XXXXX    18306XXXXX    316XXXXXXX    1703900802   
##  [9056] 1703900802    1830300701    1830300701    17037XXXXX    17037XXXXX   
##  [9061] 32102XXXXX026 32102XXXXX026 1700204232    1210600201    1210600201   
##  [9066] 1431300101    1431300101    1480500401    1480500401    2294200718   
##  [9071] 2294200718    1210506401    1210506401    183XXXXXXX    183XXXXXXX   
##  [9076] 14804006XX    17501023XX018 17501023XX018 1703923508    1703923508   
##  [9081] 1060800701    1480400601    17002042XX    17002042XX    17036XXXXX   
##  [9086] 17802XXXXX    17802XXXXX    17023004XX    17023004XX    1620100101   
##  [9091] 1620100101    1750600302    1750600302    1750102401    1750102401   
##  [9096] 1930100601    1210501217    231XXXXXXX    231XXXXXXX    299XXXXXXX013
##  [9101] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016
##  [9106] 3161000112    2291504101    19501001XX    19501001XX    14306XXXXX   
##  [9111] 16501XXXXX    16501XXXXX    228XXXXXXX    228XXXXXXX    2294200602   
##  [9116] 2294200602    32109XXXXX    32109XXXXX    22901008XX    22901008XX   
##  [9121] 17039008XX    17039008XX    17039191XX    17039191XX    1750100601   
##  [9126] 1750100601    17039XXXXX    17039XXXXX    1480403203    1480403203   
##  [9131] 110XXXXXXX    110XXXXXXX    1703900807    1210501210    1703620705   
##  [9136] 1703620705    1703929301    1703929301    1703927702    1703927702   
##  [9141] 12105012XX    12105012XX    17039033XX    17039033XX    17801XXXXX   
##  [9146] 17801XXXXX    31610XXXXX    17006345XX    17006345XX    12105011XX   
##  [9151] 12105011XX    199XXXXXXX054 199XXXXXXX054 1060800201    1750102501   
##  [9156] 1750102501    22915XXXXX    1080300501    2312100501    2312100501   
##  [9161] 17041007XX    17041007XX    1750400301    1750400301    1080401103   
##  [9166] 1080401103    175XXXXXXX    175XXXXXXX    1830509201    1830509201   
##  [9171] 1702352601    1702352601    32105XXXXX036 32105XXXXX036 1750101001   
##  [9176] 1750101001    17212010XX    17212010XX    1700204202    1750102610   
##  [9181] 1750102605    1750102612    1750300505    1080200401    321XXXXXXX   
##  [9186] 23143001XX    316XXXXXXX    1750300402    1750102406    2282907301   
##  [9191] 231XXXXXXX    199XXXXXXX010 17503XXXXX    2294200502    1080201011   
##  [9196] 32109XXXXX    22801001XX    694XXXXXXX    17501015XX    199XXXXXXX054
##  [9201] 1060800201    1080201017    1750102501    22901XXXXX    1750300903   
##  [9206] 1750400301    2280700901    175XXXXXXX    32105XXXXX036 1750102610   
##  [9211] 61841007XX    1750102406    199XXXXXXX010 228XXXXXXX    17501015XX   
##  [9216] 1709400101    1750102605    16102003XX    1709201501    1480500406   
##  [9221] 3210501003    1702700301    1750102612    1709637301    1780101703   
##  [9226] 1480203001    1750300505    1080200401    16203XXXXX    1120300103   
##  [9231] 1780200307    14805004XX034 1702300413    2290100201    1750100201   
##  [9236] 17094XXXXX    1950100106    17321XXXXX023 14806001XX    14806XXXXX   
##  [9241] 1709201906    10803XXXXX    61841007XX    1620100101    1580200105   
##  [9246] 1703906002    1750600302    199XXXXXXX010 199XXXXXXX010 17503XXXXX   
##  [9251] 14801001XX    16501XXXXX    1900800201    32109XXXXX    1750500701   
##  [9256] 1610500202    16204XXXXX    1703922001    1480501701    3210400102   
##  [9261] 1709201502    1709201502    1705700701    1580200101    17039XXXXX   
##  [9266] 110XXXXXXX    110XXXXXXX    110XXXXXXX    12105012XX    14102XXXXX   
##  [9271] 199XXXXXXX054 1060800201    1750102501    1750500101    1210600212   
##  [9276] 1210501305    1480403302    1750102608    1703710606    17039277XX   
##  [9281] 1750400301    1480204001    10606006XX    32105XXXXX036 2314300102   
##  [9286] 1704149903    1830305701    1703903303    1210503104    1480600104   
##  [9291] 1750102610    1750102605    1750102612    17023XXXXX    199XXXXXXX010
##  [9296] 17503XXXXX    1702313401    199XXXXXXX054 1750102501    1750102610   
##  [9301] 1750102605    1210501106    1950100101    1230501504    3210501003   
##  [9306] 12305015XX    1090101403    1750102601    1750100101    1702326801   
##  [9311] 1480400202    1830200201    1210500105    1702300401    1750100205   
##  [9316] 1750100205    1702700301    1702700301    17801001XX    1230100401   
##  [9321] 1703900803    1703626303    1750601201    1703906302    1703906302   
##  [9326] 1703900801    1703900801    1100400105    1080200401    1100400101   
##  [9331] 1480403301    1702021301    1210503002    1830506401    10801003XX   
##  [9336] 1702300405    1750100201    1750100201    3210200202    1830202405   
##  [9341] 3162300203    2282300303    1830300701    1100400110    32102XXXXX026
##  [9346] 17039060XX    10901XXXXX    2310901006    1210600201    1210600201   
##  [9351] 1431300101    3160700205    1830204802    1480500401    2294200718   
##  [9356] 1210506401    1210506401    1830200405    1700634503    1700634503   
##  [9361] 1230400301    1210506601    199XXXXXXX009 183XXXXXXX    1400200102   
##  [9366] 17501023XX018 148XXXXXXX    1470100101    3160800309    1230501503   
##  [9371] 1721201002    2311109001    1780207001    17002XXXXX    17036XXXXX   
##  [9376] 17802XXXXX    1480401001    17506XXXXX    14805004XX    17023004XX   
##  [9381] 1620100101    1750600302    1750600302    1702307202    1830204504   
##  [9386] 1480400501    1750102401    3210400105    1782000301    1210501217   
##  [9391] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 17503XXXXX    1830500301   
##  [9396] 16501XXXXX    16501XXXXX    2280400203    2294200602    1480403201   
##  [9401] 32109XXXXX    3160700801    1480501701    3210400102    22801001XX   
##  [9406] 30701001XX    1090100704    1480401502    17023047XX    17039XXXXX   
##  [9411] 1090101601    1480403203    11004001XX    1780200403    6910500101   
##  [9416] 1400201801    1210501210    1703620705    1480401501    1830300704   
##  [9421] 17204002XX    12105012XX    14102XXXXX    1230100402    12105011XX   
##  [9426] 199XXXXXXX054 1750102501    1080100301    1080400713    10804007XX   
##  [9431] 31616003XX    18303XXXXX    3161202005    1702700302    1100400104   
##  [9436] 11701XXXXX    1704100701    17041007XX    1750400301    1100400102   
##  [9441] 1080201703    1080401103    1780200302    1830509201    1480400101   
##  [9446] 1210501105    199XXXXXXX053 32105XXXXX036 1750101511    3070800101   
##  [9451] 1703903303    1480403401    1830201102    17102001XX    1750102610   
##  [9456] 1750102605    1750100101    1750300404    1750102612    1750102604   
##  [9461] 1750300505    1750102301    1750102301    1750102401    1750102401   
##  [9466] 199XXXXXXX010 1750102501    1750102501    30706002XX    1750101001   
##  [9471] 1750102610    1750102610    1750102605    16102003XX    1750102612   
##  [9476] 1750300507    1750300505    1080200401    32102XXXXX026 17501XXXXX   
##  [9481] 231XXXXXXX    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 16501XXXXX   
##  [9486] 22801001XX    17608XXXXX    694XXXXXXX    17501015XX    199XXXXXXX054
##  [9491] 1060800201    1750102501    17032027XX    1750300903    1750400301   
##  [9496] 22901001XX    175XXXXXXX    1750102610    30703001XX    1750102605   
##  [9501] 1750102605    16102003XX    17023048XX    3210505802    17092XXXXX   
##  [9506] 17092XXXXX    1709253501    1100400132    1100400132    1709201501   
##  [9511] 1709201501    1709201501    699XXXXXXX    12305015XX    1702700301   
##  [9516] 1210501309    1702905102    1510402101    1431804501    1060100301   
##  [9521] 11004002XX    1060600603    1750102612    1750102612    1705700602   
##  [9526] 1090101401    1709637301    1750300507    1620400701    1709441601   
##  [9531] 1480203001    1480203001    1480501702    1750100207    1750300505   
##  [9536] 1080200401    1780200301    1760801502    1030300603    1050200502   
##  [9541] 1750101801    1703001001    112XXXXXXX    1230100907    316XXXXXXX   
##  [9546] 121XXXXXXX020 1702807101    1480201001    1760801002    14313XXXXX   
##  [9551] 1080201020    1510302204    17094XXXXX    17094XXXXX    1120100411   
##  [9556] 15204002XX    3160806701    10901XXXXX    16201XXXXX    1080103402   
##  [9561] 11007XXXXX    1100400201    689XXXXXXX    17038XXXXX    1750500501   
##  [9566] 183XXXXXXX    17809XXXXX    14704XXXXX    17501023XX018 17506002XX   
##  [9571] 148XXXXXXX    307XXXXXXX    1120300101    1705700402    1721348401   
##  [9576] 1060800701    2290100203    1480201901    14806001XX    14806001XX   
##  [9581] 14806001XX    14806XXXXX    14806004XX    14703004XX    1700505802   
##  [9586] 17023004XX    1620100101    23020XXXXX    1620101102    1520500101   
##  [9591] 1090101801    13208XXXXX    10901010XX    1090100803    1090101602   
##  [9596] 1900300601    1510300401    231XXXXXXX    199XXXXXXX010 199XXXXXXX010
##  [9601] 399XXXXXXX016 1100400202    1620100402    14801001XX    17070305XX   
##  [9606] 16501XXXXX    228XXXXXXX    1720919602    3160700220    2294200504   
##  [9611] 1100403001    3160800313    1100402001    32109XXXXX    32109XXXXX   
##  [9616] 1750500701    1520100102    1700207201    1610500202    16204XXXXX   
##  [9621] 1750102602    3160700801    1704700302    1709201502    1709201502   
##  [9626] 1709201502    1709201502    1709201502    1705700701    1090100704   
##  [9631] 1580200101    1700200901    1708800101    1060800301    17039034XX   
##  [9636] 11201004XX    11004XXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
##  [9641] 110XXXXXXX    1480201401    2290100206    2302012302    1610201201   
##  [9646] 1480600105    1480600105    1703028602    17608XXXXX    18302053XX   
##  [9651] 17023043XX    1780200803    17801XXXXX    694XXXXXXX    31610XXXXX   
##  [9656] 199XXXXXXX054 31611041XX    1750300905    1060800201    1120100302   
##  [9661] 1750500901    1750600601    1703919115    1760801004    1750102501   
##  [9666] 1750102501    1080800301    1750102701    12314007XX    16105XXXXX   
##  [9671] 22915XXXXX    1480100101    1080300501    1620400201    1750500101   
##  [9676] 1480403302    1750102608    1480500403    1830201801    1620400102   
##  [9681] 1080400709    1780202502    691XXXXXXX    691XXXXXXX    1750300903   
##  [9686] 3161100704    2302007002    1750400301    1707030504    1480603001   
##  [9691] 1060600601    1080401103    17071XXXXX    175XXXXXXX    32105XXXXX036
##  [9696] 1900901801    1750101001    1750101001    3210505901    1702301127   
##  [9701] 1760801005    1480600104    1480600104    17063XXXXX    1750102610   
##  [9706] 1750102610    1750102612    1750102612    1750102404    1750102404   
##  [9711] 1080201003    2311101202    17023XXXXX    2290100108    121XXXXXXX020
##  [9716] 1702807101    23019XXXXX    183XXXXXXX    2290100116    17002XXXXX   
##  [9721] 17002XXXXX    17036XXXXX    17036XXXXX    14703004XX    2312100102   
##  [9726] 61841007XX    3160700802    231XXXXXXX    199XXXXXXX010 199XXXXXXX010
##  [9731] 199XXXXXXX010 2280400508    1070300901    32109XXXXX    32109XXXXX   
##  [9736] 1750101509    17065XXXXX    17065XXXXX    22801001XX    22801001XX   
##  [9741] 110XXXXXXX    110XXXXXXX    1430902102    10802XXXXX    10802XXXXX   
##  [9746] 14102XXXXX    14102XXXXX    694XXXXXXX    694XXXXXXX    17501015XX   
##  [9751] 1750102501    1750102501    17032027XX    17032027XX    17001025XX   
##  [9756] 17001025XX    1703202729    30706002XX    30706002XX    32105XXXXX036
##  [9761] 17037016XX    17037016XX    1750102610    1750102610    1703202801   
##  [9766] 1705013202    17710001XX    1480500408    1703626303    1760300401   
##  [9771] 1702021301    1210503002    17023XXXXX    14313XXXXX    17037XXXXX   
##  [9776] 32102XXXXX026 183XXXXXXX    14704XXXXX    307XXXXXXX    1707700109   
##  [9781] 17002XXXXX    17036XXXXX    17506XXXXX    17023044XX    1750600302   
##  [9786] 1707700302    17501XXXXX    1210501217    231XXXXXXX    299XXXXXXX013
##  [9791] 199XXXXXXX010 199XXXXXXX010 16501XXXXX    228XXXXXXX    14701XXXXX   
##  [9796] 32109XXXXX    17039XXXXX    110XXXXXXX    12105012XX    17801XXXXX   
##  [9801] 14102XXXXX    199XXXXXXX054 17032027XX    18303XXXXX    2280100131   
##  [9806] 17402XXXXX    1750400301    17077XXXXX    18304XXXXX    22901001XX   
##  [9811] 175XXXXXXX    32105XXXXX036 17037457XX    1704149903    1290100304   
##  [9816] 1750102605    699XXXXXXX    1750102612    1750300507    1750300505   
##  [9821] 199XXXXXXX010 1750102501    1750300903    1750400301    175XXXXXXX   
##  [9826] 1750102610    199XXXXXXX010 1750300505    17023XXXXX    1702807101   
##  [9831] 17038XXXXX    17041XXXXX    17002042XX    199XXXXXXX010 228XXXXXXX   
##  [9836] 32109XXXXX    17065XXXXX    17023043XX    1750102501    17032XXXXX   
##  [9841] 17407001XX    17402XXXXX    22901001XX    175XXXXXXX    1750101001   
##  [9846] 1750102610    2090100101    16102003XX    16102003XX    16102003XX   
##  [9851] 16102003XX    1830201401    1830201401    1950100101    17092XXXXX   
##  [9856] 1709201501    1709201501    1230501504    12305015XX    1750102601   
##  [9861] 1750102601    1480400202    1480400202    1830200201    1830200201   
##  [9866] 1210500105    1702300401    1750100205    1702700301    17801001XX   
##  [9871] 17801001XX    1230100401    1230100401    1710200101    1706300501   
##  [9876] 1060100301    1780100112    1780100112    1750102612    1780101703   
##  [9881] 1080100104    1480203001    1480501702    1480400502    1480400502   
##  [9886] 3161000105    1100400101    1480403301    1702021301    1620300201   
##  [9891] 1830506401    1230400201    1230400201    12301010XX    1750100201   
##  [9896] 1830202405    3162300203    2282300303    1830300701    1706338702   
##  [9901] 17094XXXXX    10901XXXXX    10901XXXXX    10901XXXXX040 689XXXXXXX   
##  [9906] 2310901006    1210600201    1431300101    3160700205    1830204802   
##  [9911] 3210505801    1480500401    2294200718    1210506401    1210506401   
##  [9916] 1830200405    1700634503    1210506601    1702304442    199XXXXXXX009
##  [9921] 199XXXXXXX009 183XXXXXXX    183XXXXXXX    148XXXXXXX    148XXXXXXX   
##  [9926] 148XXXXXXX    148XXXXXXX    1470100101    1721348401    1780100101   
##  [9931] 1780100101    1706306901    3160800309    1230501503    1480400601   
##  [9936] 1830200501    1830200501    14806001XX    14806001XX    1780207001   
##  [9941] 1480401001    1480401001    31610028XX    3160803603    17023004XX   
##  [9946] 17023004XX    17023044XX    1090100803    1830204504    1480400501   
##  [9951] 1480400501    1782000301    231XXXXXXX    299XXXXXXX013 199XXXXXXX010
##  [9956] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 1830500301    14802XXXXX   
##  [9961] 14801001XX    16501XXXXX    2280400203    2280400203    1710200102   
##  [9966] 2294200602    1480403201    3160904501    32109XXXXX    1750500701   
##  [9971] 1610500202    1610500202    1610500202    16204XXXXX    16204XXXXX   
##  [9976] 16204XXXXX    1709201502    30701001XX    1090100704    1480401901   
##  [9981] 1480401502    1060800301    1060800301    17039XXXXX    1090101601   
##  [9986] 1120100301    1120100301    11004001XX    11004001XX    11201004XX   
##  [9991] 110XXXXXXX    2302001801    18302XXXXX    1706306501    1480600103   
##  [9996] 1480600103    1480600401    1480600401    1480401501    1480401501   
## [10001] 123XXXXXXX    17204002XX    12105012XX    31608XXXXX    1230100402   
## [10006] 69302004XX    1750600601    1480402507    1750102501    18303XXXXX   
## [10011] 1709441801    1480500403    1710200103    1710200103    3161202002   
## [10016] 1750400301    1750400301    1100400102    1830509201    1480400101   
## [10021] 1480400101    199XXXXXXX053 1090101001    17608010XX    3070800101   
## [10026] 1480400803    1480400803    1480403401    1830201102    1830201102   
## [10031] 17102001XX    17102001XX    17063XXXXX    1750102610    30703001XX   
## [10036] 12106XXXXX    17710001XX    17011026XX    1750300507    1702021301   
## [10041] 17603XXXXX    17023XXXXX    1702222101    1702807101    17037XXXXX   
## [10046] 199XXXXXXX012 17038XXXXX    183XXXXXXX    17809XXXXX    17501023XX018
## [10051] 17041XXXXX    1210501203    17002042XX    17036XXXXX    17506XXXXX   
## [10056] 14703004XX    1750101403    1210501204    1702304308    1750300402   
## [10061] 17023044XX    1750102406    13116XXXXX    1750102603    199XXXXXXX010
## [10066] 16501XXXXX    1750101503    228XXXXXXX    14701013XX    199XXXXXXX013
## [10071] 3210200229    17023047XX    17039XXXXX    17023231XX    1702313401   
## [10076] 110XXXXXXX    14102XXXXX    199XXXXXXX054 1750102501    17032XXXXX   
## [10081] 17407001XX    1750100102    17033XXXXX    1702317901    22901001XX   
## [10086] 175XXXXXXX    1750102610    1750102605    1750102605    1750102605   
## [10091] 1750102605    1750102605    1750102605    1750102601    1750102601   
## [10096] 1750102601    1750102601    1750100101    1750300404    1750300404   
## [10101] 1750300404    1750300904    1750300904    1750300904    1750300904   
## [10106] 1480500408    1750102612    1750102612    1750102612    1750102612   
## [10111] 1750102612    1750102612    1750300507    1750300507    1750300507   
## [10116] 1750102404    1750102404    1750300505    1750300505    1750300505   
## [10121] 1750300505    1750300505    1080200401    1080200401    14805004XX034
## [10126] 1702300413    1702300405    1750100201    1750100201    17037XXXXX   
## [10131] 32102XXXXX026 17039060XX    1750100104    1210600201    1210506401   
## [10136] 17501023XX018 1750102301    1750300402    1750300402    17023004XX   
## [10141] 1750600302    1750102401    1750102401    1750300906    1750102603   
## [10146] 199XXXXXXX010 17503XXXXX    17503XXXXX    228XXXXXXX    32109XXXXX   
## [10151] 1750102602    22801001XX    17039XXXXX    12105012XX    199XXXXXXX054
## [10156] 199XXXXXXX054 1750300905    1750102501    1750102501    1750102501   
## [10161] 1750102501    1750102501    1750102608    1750102608    1750300903   
## [10166] 1750300903    1750400301    1750400301    1750400301    1750400301   
## [10171] 1750400301    1750400301    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [10176] 175XXXXXXX    175XXXXXXX    175XXXXXXX    32105XXXXX036 1750101001   
## [10181] 1750101001    1750102610    1750102610    1750102610    1750102610   
## [10186] 1750102610    1750102610    12106XXXXX    17710001XX    1700116701   
## [10191] 1702309901    1311600102    17603XXXXX    17023XXXXX    316XXXXXXX   
## [10196] 121XXXXXXX020 1702222101    1702807101    17037XXXXX    32102XXXXX026
## [10201] 1211100201    17038XXXXX    1701916502    1707700201    17501023XX018
## [10206] 2280100112    1311606801    17002042XX    17036XXXXX    11001XXXXX   
## [10211] 17506XXXXX    1210503801    1750101403    1210501204    1750300402   
## [10216] 17023044XX    1750102406    1750600302    1750102603    1703202702   
## [10221] 231XXXXXXX    199XXXXXXX010 17503XXXXX    22801016XX    16501XXXXX   
## [10226] 1750101503    22801019XX    22801001XX    14309011XX    17039XXXXX   
## [10231] 110XXXXXXX    31616XXXXX    10802XXXXX    11002XXXXX    17023043XX   
## [10236] 14102XXXXX    17015XXXXX    1750102501    3070800603    1705013201   
## [10241] 17033184XX    18304XXXXX    1702317901    22901001XX    175XXXXXXX   
## [10246] 32105XXXXX036 1750102610    1750102605    699XXXXXXX    17710001XX   
## [10251] 1750102612    17023XXXXX    1702807101    17038XXXXX    17041XXXXX   
## [10256] 17002042XX    1750101403    2311114001    1750102406    231XXXXXXX   
## [10261] 199XXXXXXX010 17503XXXXX    1220200101    17046036XX    16501XXXXX   
## [10266] 1750101503    1750102602    17065XXXXX    17047XXXXX    694XXXXXXX   
## [10271] 1750102501    17032XXXXX    17407001XX    17402XXXXX    1750400301   
## [10276] 22901001XX    175XXXXXXX    1750101001    17063XXXXX    1750102610   
## [10281] 17710001XX    1702021301    1703926101    1750100201    32104001XX   
## [10286] 32102XXXXX026 183XXXXXXX    17002042XX    11001XXXXX    17023004XX   
## [10291] 1750102401    13116XXXXX    231XXXXXXX    199XXXXXXX010 1703710601   
## [10296] 16501XXXXX    228XXXXXXX    110XXXXXXX    1703919103    12105012XX   
## [10301] 17039033XX    10804007XX    17407001XX    17041007XX    175XXXXXXX   
## [10306] 1705013202    1750102605    1750102605    1750102605    1750102605   
## [10311] 17023048XX    1480500406    3210501003    1750102601    1750102601   
## [10316] 1750102601    1750300404    1750300404    1750300904    1750300904   
## [10321] 17710001XX    1480500408    1750102612    1750102612    1750102612   
## [10326] 1750102612    1750102612    1750102612    1750102612    1750102404   
## [10331] 1750102404    1080201003    1750300505    1750300505    1080200401   
## [10336] 17023XXXXX    1750100201    316XXXXXXX    17037XXXXX    17037XXXXX   
## [10341] 17037XXXXX    2280100123    1702300414    32102XXXXX026 32102XXXXX026
## [10346] 1210600201    1210506401    1750102301    307XXXXXXX    3210603301   
## [10351] 14805004XX    14805004XX    17023004XX    17023004XX    1750600302   
## [10356] 1750102401    1709244002    231XXXXXXX    299XXXXXXX013 199XXXXXXX010
## [10361] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 649XXXXXXX   
## [10366] 228XXXXXXX    228XXXXXXX    228XXXXXXX    32109XXXXX    32109XXXXX   
## [10371] 1210601503    22801XXXXX027 1750101509    1210504201    1480501701   
## [10376] 3160806702    3210400102    1709201502    22801001XX    22801001XX   
## [10381] 22801001XX    1580200101    17039XXXXX    17039XXXXX    110XXXXXXX   
## [10386] 12105012XX    12105012XX    14102XXXXX    199XXXXXXX054 1060800201   
## [10391] 1750102501    1750102501    1750102501    1750102501    1750102501   
## [10396] 17032XXXXX    1703620919    1480403302    1750100102    30706002XX   
## [10401] 2301900206    1750400301    1750400301    1750400301    1750400301   
## [10406] 1480204001    17077XXXXX    22901001XX    175XXXXXXX    175XXXXXXX   
## [10411] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [10416] 32105XXXXX036 32105XXXXX036 32105XXXXX036 1750101001    1750101511   
## [10421] 1290100304    1750102610    1750102610    1750102610    1750102610   
## [10426] 1750102610    1750102605    2280100103    1700116701    1750102612   
## [10431] 1750300507    1750300505    2280100112    2311114001    1750102406   
## [10436] 1750102603    199XXXXXXX010 22801016XX    228XXXXXXX    694XXXXXXX   
## [10441] 1750102501    12106050XX    1750300903    1750400301    22901001XX   
## [10446] 1750102610    1210600208    1703616301    1702300405    3161003801   
## [10451] 1750100201    316XXXXXXX    1702807101    1703756501    17037038XX   
## [10456] 15802001XX    1750100104    689XXXXXXX    3070202301    183XXXXXXX   
## [10461] 14704XXXXX    307XXXXXXX    2290100116    17002042XX    17036XXXXX   
## [10466] 17023044XX    3210502301    1210602005    3162403901    231XXXXXXX   
## [10471] 299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 16501XXXXX    32109XXXXX   
## [10476] 1090300406    1100100510    1210506702    1750101509    3210400102   
## [10481] 199XXXXXXX013 22801001XX    1703719402    3160803003    1707027003   
## [10486] 1700240505    1703701604    17023047XX    110XXXXXXX    199XXXXXXX054
## [10491] 16302XXXXX    1750102501    10804007XX    17032027XX    1210501303   
## [10496] 1480500405    1750400301    17016XXXXX    17608010XX    1750102610   
## [10501] 30703001XX    1750102605    1750102605    1750102605    1750102605   
## [10506] 1750102605    31604071XX    1750300904    1750300904    1750300904   
## [10511] 1750300904    17710001XX    1700116701    17405206XX    1702329101   
## [10516] 1750102612    1750102612    1750102612    1750102612    1750102612   
## [10521] 1750102612    1750102612    1750300505    1750300505    1750300505   
## [10526] 1750300505    1750300505    1750300505    1750300505    2311100401   
## [10531] 17603XXXXX    17023XXXXX    1210502301    1750100201    316XXXXXXX   
## [10536] 121XXXXXXX020 1702222101    1702807101    32104001XX    14313XXXXX   
## [10541] 32102XXXXX026 2280101606    1701916502    183XXXXXXX    14704XXXXX   
## [10546] 17501023XX018 17000XXXXX    2280100112    17095XXXXX    17041XXXXX   
## [10551] 17321XXXXX023 3161003202    17002XXXXX    17506XXXXX    14703004XX   
## [10556] 1750101403    1211200303    2311114001    1290200402    61841007XX   
## [10561] 1750102406    13116XXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [10566] 399XXXXXXX016 17503XXXXX    22801016XX    1220200101    17046036XX   
## [10571] 1702632701    16501XXXXX    1750101503    14701013XX    32109XXXXX   
## [10576] 22801001XX    170XXXXXXX    17035XXXXX    17039XXXXX    17023231XX   
## [10581] 1702313401    1210502901    110XXXXXXX    12105012XX    17023043XX   
## [10586] 31608XXXXX    17406330XX    14102XXXXX    694XXXXXXX    69302004XX   
## [10591] 22807XXXXX    199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1750101401   
## [10596] 31611041XX    1060800201    1060800201    1060800201    17015XXXXX   
## [10601] 16302XXXXX    1750102501    3160700811    22915XXXXX    17032XXXXX   
## [10606] 1750102608    1750102608    17407001XX    1705013201    22501XXXXX   
## [10611] 12106050XX    1750300903    1750300903    17402XXXXX    1750400301   
## [10616] 1750400301    1750400301    1750400301    1750400301    1750400301   
## [10621] 1750400301    17033184XX    17077XXXXX    1702317901    22901001XX   
## [10626] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    12111002XX   
## [10631] 17063XXXXX    1750102610    1750102610    1750102610    1750102610   
## [10636] 1750102610    1750102610    1750102610    199XXXXXXX010 1480401601   
## [10641] 1480401601    1210501106    16102003XX    16102003XX    1830201401   
## [10646] 1830201401    1950100103    1210501103    1950100101    17092XXXXX   
## [10651] 17092XXXXX    1709253501    1480500406    3210501003    3210501003   
## [10656] 12305015XX    1830200801    1400211501    1780701403    1750102601   
## [10661] 1750102601    1750102601    1750100101    1750100101    1750100101   
## [10666] 1702326801    1760301104    1480400202    1480400202    1830200201   
## [10671] 1830200201    1210500105    1210500105    1702300401    1750100205   
## [10676] 1750100205    1210502403    1702700301    1702700301    17801001XX   
## [10681] 1230100401    17802020XX    1710200101    1231400701    17710001XX   
## [10686] 1780100112    1780100112    1703626303    1750102612    1750601201   
## [10691] 1709441601    1709441601    1760300401    1480501702    1480400502   
## [10696] 1480403301    1210501107    1702021301    1702021301    1210600207   
## [10701] 14805004XX034 1702300413    1230400201    1230400201    1702300405   
## [10706] 1750100201    1750100201    1750100201    1750100201    1750100201   
## [10711] 1400200201    1830202405    17037XXXXX    17037XXXXX    1400201601   
## [10716] 199XXXXXXX012 199XXXXXXX012 17039060XX    10901XXXXX    1711500401   
## [10721] 1210600201    1830204802    1480500401    1210506401    1210506401   
## [10726] 1830200405    1230400301    1210506601    1231200102    1210506602   
## [10731] 199XXXXXXX009 199XXXXXXX009 183XXXXXXX    183XXXXXXX    183XXXXXXX   
## [10736] 1480404101    1400200102    148XXXXXXX    148XXXXXXX    148XXXXXXX   
## [10741] 1470100101    1703923508    17321XXXXX023 1780100101    1702300415   
## [10746] 1830200501    1830200501    14806001XX    14806001XX    14806XXXXX   
## [10751] 1709201906    1709201906    1709201906    199XXXXXXX007 199XXXXXXX007
## [10756] 17036XXXXX    17802XXXXX    17802XXXXX    1480401001    1480401001   
## [10761] 14805004XX    1709201903    17023004XX    17023044XX    1620100101   
## [10766] 1830200802    1580200105    10201XXXXX    1703906002    1750600302   
## [10771] 1750600302    1702307202    1480400501    1750102401    1750102401   
## [10776] 1750102401    3210400105    1709441701    1709441701    1709441701   
## [10781] 1709201902    1709201902    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [10786] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [10791] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 14802XXXXX   
## [10796] 228XXXXXXX    1480500407    1480500407    2280400203    3210501001   
## [10801] 1480403201    1709446601    1480400211    1830200202    1210500107   
## [10806] 1210500107    1702300406    1702300406    1780100109    1780100109   
## [10811] 1703922001    1480501701    1480501701    3210400102    1709201502   
## [10816] 1709201502    1709201502    199XXXXXXX008 1090100704    1090100704   
## [10821] 1090100704    1580200101    1580200101    1480401502    17039XXXXX   
## [10826] 17039XXXXX    1230100909    11004001XX    11004001XX    110XXXXXXX   
## [10831] 110XXXXXXX    110XXXXXXX    1480400802    1703919103    1703919103   
## [10836] 1400201801    1702300411    1480600103    1210501210    1480600401   
## [10841] 1480600401    1480600401    1703620705    1780800401    1480401501   
## [10846] 1480401501    17204002XX    12105012XX    12105012XX    17023043XX   
## [10851] 17023043XX    17801XXXXX    17801XXXXX    1703935301    1230100402   
## [10856] 1480500402    3210506001    199XXXXXXX054 199XXXXXXX054 1400210001   
## [10861] 1480500404    1750600601    1750600601    1750102501    17505XXXXX   
## [10866] 17032027XX    1210501303    1709441801    1480500405    1210501305   
## [10871] 1210501305    1480403302    1480403302    1480500403    1703710606   
## [10876] 1702700302    1709448001    1750400301    1480204001    1400200701   
## [10881] 175XXXXXXX    175XXXXXXX    1830509201    1709447001    32105XXXXX036
## [10886] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 1400209701   
## [10891] 1750101511    1400233301    1210503104    1480403401    1780100103   
## [10896] 1830201102    1830201102    17102001XX    1830202402    1750102610   
## [10901] 1780100104    1780100104    1750102605    1750102605    1750102605   
## [10906] 1750102605    1750102605    1750102605    1750102605    1750102605   
## [10911] 1610200301    1610200301    16102003XX    16102003XX    16102003XX   
## [10916] 1210501104    17023048XX    17023048XX    1830201401    1830201401   
## [10921] 1950100103    10903XXXXX    10903XXXXX    1950100101    1950100101   
## [10926] 1950100101    1090500601    1703903302    1480500406    3210501003   
## [10931] 12305015XX    1090101403    1750102601    1750102601    1750102601   
## [10936] 1750102601    1750102601    1750100101    1750100101    1750100101   
## [10941] 1750100101    1480400202    1480400202    1830200201    1830200201   
## [10946] 1210500105    1702300401    1702300401    1750100205    1702700301   
## [10951] 1702700301    1702700301    17801001XX    17801001XX    17801001XX   
## [10956] 1750300404    1750300404    1750300404    1750300404    1750300404   
## [10961] 1750300404    1750300404    1230100401    1470200201    1750300904   
## [10966] 1750300904    1750300904    1750300904    1710200101    1703900803   
## [10971] 1703900803    1231400701    1706300501    3161100303    2130500101   
## [10976] 17710001XX    17710001XX    17710001XX    1060100301    1703620918   
## [10981] 1780100112    1780100112    3164000501    1060600603    1060600603   
## [10986] 1060600603    1060600603    1060600603    1750102612    1750102612   
## [10991] 1750102612    1750102612    1750102612    1750102612    1750102612   
## [10996] 1750102612    1750102612    1090101401    1090101401    1709637301   
## [11001] 1750300507    1750300507    1750300507    1750300507    1750300507   
## [11006] 1750300507    1750300507    1750300507    1750300507    1750300507   
## [11011] 1750601201    1750601201    1703906302    1703906302    1950100102   
## [11016] 1950100102    1780101703    1780101703    1080100104    1080100104   
## [11021] 1703900801    1703900801    1700206113    1100400105    2280203101   
## [11026] 2280203101    1760300401    1760300401    1702300402    1480400502   
## [11031] 1750300505    1750300505    1750300505    1750300505    1750300505   
## [11036] 1750300505    1750300505    1750300505    1750300505    3161000105   
## [11041] 1080200401    1080200401    1080200401    1080200401    1080200401   
## [11046] 1080200401    1080200401    1080200401    1080200401    1080200401   
## [11051] 1080200401    1480403301    1480403301    1702021301    1702021301   
## [11056] 1050200201    1050200201    1050200201    1703716607    1703716607   
## [11061] 1703926101    1703926101    1703926101    1090600901    1480400801   
## [11066] 1830506401    1100400186    17603XXXXX    17603XXXXX    14805004XX034
## [11071] 1702300413    1230400201    2280100117    2280100117    17023XXXXX   
## [11076] 17023XXXXX    17012XXXXX    1703745702    10801XXXXX    321XXXXXXX   
## [11081] 1750100201    1750100201    1750100201    316XXXXXXX    316XXXXXXX   
## [11086] 121XXXXXXX020 121XXXXXXX020 17002061XX    3161300102    3210200202   
## [11091] 3210200202    1830202405    1703906006    1703906006    1702807101   
## [11096] 1702807101    1702807101    1702807101    1702807101    1702807101   
## [11101] 1702807101    1100700801    3162300203    1480201001    3210900507   
## [11106] 1703900802    1703900802    3070100101    2282300303    1830300701   
## [11111] 1830300701    32104001XX    32104001XX    32104001XX    1703903305   
## [11116] 14313XXXXX    17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
## [11121] 17037XXXXX    1060403601    1100400110    32102XXXXX026 32102XXXXX026
## [11126] 1520400203    2280101701    2280101701    2280101701    17039060XX   
## [11131] 17039060XX    1950100106    121XXXXXXX019 10901XXXXX    10901XXXXX   
## [11136] 10901XXXXX040 31615002XX    1700204201    1700204201    1700204201   
## [11141] 2310901006    1750500501    1750500501    1750500501    1750500501   
## [11146] 1750500501    1750500501    1750500501    1750500501    1750500501   
## [11151] 1750500501    1210600201    1210600201    1431300101    1431300101   
## [11156] 3160700205    1830204802    1480500401    1480500401    2294200718   
## [11161] 2294200718    1210506401    1210506401    1830200405    1700634503   
## [11166] 1210506601    1702304442    1702304442    199XXXXXXX009 199XXXXXXX009
## [11171] 183XXXXXXX    183XXXXXXX    183XXXXXXX    1480400602    14804006XX   
## [11176] 14804006XX    1830500302    17501023XX018 17501023XX018 148XXXXXXX   
## [11181] 148XXXXXXX    148XXXXXXX    148XXXXXXX    1470100101    307XXXXXXX   
## [11186] 307XXXXXXX    2280203001    1703923508    1703923508    17321XXXXX023
## [11191] 1780100101    1780100101    21302007XX    3160800309    1060800701   
## [11196] 1060800701    1702304801    1480400601    1480400601    1721201002   
## [11201] 2311109001    1830200501    1830200501    1090100201    1090100201   
## [11206] 14806001XX    1901000201    3161102001    199XXXXXXX007 17002042XX   
## [11211] 17002042XX    17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX   
## [11216] 17036XXXXX    17036XXXXX    17036XXXXX    1090100801    1090100801   
## [11221] 1090100801    1090100801    17802XXXXX    17802XXXXX    17802XXXXX   
## [11226] 1480401001    1480401001    14805004XX    14805004XX    14805004XX   
## [11231] 10803XXXXX    10803XXXXX    3210902401    1760800302    2280100125   
## [11236] 1750300402    1750300402    1750601202    17023004XX    17023004XX   
## [11241] 17023044XX    3161102002    1620100101    1620100101    1620100101   
## [11246] 1580200105    1090101801    1090101801    1090101702    1090101702   
## [11251] 1703906002    1703906002    1703906002    1750600302    1750600302   
## [11256] 1750600302    1090100803    1090100803    1702307202    1702307202   
## [11261] 18301XXXXX    18301XXXXX    1830204504    1480400501    14804005XX   
## [11266] 1750102401    1750102401    1750102401    13116XXXXX    229XXXXXXX   
## [11271] 229XXXXXXX    1750300906    1750300906    1750300906    1750300906   
## [11276] 1750300906    1750300906    1060800203    1090101602    1090101602   
## [11281] 1100400111    1510300401    1090100804    1090100804    17501XXXXX   
## [11286] 17501XXXXX    17501XXXXX    17501XXXXX    1210501217    231XXXXXXX   
## [11291] 231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX    299XXXXXXX013
## [11296] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013
## [11301] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [11306] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016
## [11311] 399XXXXXXX016 399XXXXXXX016 649XXXXXXX    17503XXXXX    17503XXXXX   
## [11316] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
## [11321] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    1703710601   
## [11326] 1703710601    1702300408    1610500201    1610500201    2291504101   
## [11331] 1830500301    1830500301    19501001XX    19501001XX    14306XXXXX   
## [11336] 14306XXXXX    16501XXXXX    16501XXXXX    16501XXXXX    30702002XX   
## [11341] 3210902402    228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX   
## [11346] 228XXXXXXX    14701XXXXX    2280400203    2280400203    3210501001   
## [11351] 3210501001    2294200602    2294200602    1480403201    1080100302   
## [11356] 1080100302    1900800201    1080201011    1080201011    1080201011   
## [11361] 32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX    32109XXXXX   
## [11366] 1780101902    1750500701    1750500701    1750500701    1750500701   
## [11371] 1750500701    1750500701    1750500701    1750500701    1750500701   
## [11376] 1750500701    1520100102    1520100102    1610500202    1610500202   
## [11381] 1750102602    1750102602    3160700801    22812XXXXX046 22901008XX   
## [11386] 22901008XX    17039008XX    1703922001    17039191XX    17039191XX   
## [11391] 17039191XX    1706505506    1706505506    1480501701    3210400102   
## [11396] 1709201502    199XXXXXXX008 22801001XX    22801001XX    30701001XX   
## [11401] 17040075XX    1090100704    1090100704    1090100704    1580200101   
## [11406] 1750100601    1750100601    1750100601    1480401502    17023047XX   
## [11411] 1480403202    1060800301    1060800301    1060800301    1060800301   
## [11416] 1060800301    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
## [11421] 1090101601    1090101601    1090101601    23111004XX    1480403203   
## [11426] 1480403203    3161100301    3160800105    1706306601    11004001XX   
## [11431] 11004001XX    11004001XX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [11436] 1706008301    1780200403    1480400802    1480400802    1703900807   
## [11441] 1703900807    1703919103    1703919103    1780100902    10802XXXXX   
## [11446] 10802XXXXX    10802XXXXX    10802XXXXX    1706306501    14804028XX   
## [11451] 1750501701    1480600103    1480600401    1480600401    1703620705   
## [11456] 1703620705    1703907601    1480401501    1480401501    1703929301   
## [11461] 1830300704    1830300704    1703927702    1703927702    17204002XX   
## [11466] 1100400106    12105012XX    17039033XX    17039033XX    17039033XX   
## [11471] 2280202101    2280202101    17501002XX    17801XXXXX    17801XXXXX   
## [11476] 17801XXXXX    17801XXXXX    17813012XX    1020100101    1230100402   
## [11481] 17006345XX    17006345XX    1480500402    12105011XX    199XXXXXXX054
## [11486] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [11491] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1703903307   
## [11496] 1703707001    1060800201    1060800201    1060800201    1060800201   
## [11501] 1060800201    1060800201    1060800201    1060800201    1060800201   
## [11506] 1060800201    1060800201    1950100105    1080201017    1080201017   
## [11511] 1080201017    1480500404    1750600601    1750600601    1750600601   
## [11516] 16302XXXXX    1620100401    1620100401    1750102501    1750102501   
## [11521] 1750102501    1750102501    1750102501    1750102501    16105XXXXX   
## [11526] 16105XXXXX    3161100601    1080300501    1080300501    1080300501   
## [11531] 1080300501    1080400713    1080400713    10804007XX    10804007XX   
## [11536] 10804007XX    17505XXXXX    17505XXXXX    1750500101    31616003XX   
## [11541] 18303XXXXX    18303XXXXX    3161202005    18303057XX    1480403302   
## [11546] 1750102608    1750102608    1750102608    1703710606    2280100131   
## [11551] 2280101601    2312100501    2312100501    1101001501    22901XXXXX   
## [11556] 1610200302    1610200302    1100400104    1700634501    1710200103   
## [11561] 1710200103    1721335202    17213352XX    1080400715    11005XXXXX   
## [11566] 6930400701    1610100102    3161100105    11701XXXXX    17402XXXXX   
## [11571] 1704100701    17041007XX    17041007XX    1750400301    1750400301   
## [11576] 1750400301    1750400301    1750400301    1750400301    1750400301   
## [11581] 1750400301    1750400301    1750400301    1750400301    1480204001   
## [11586] 18303081XX    1100400102    1100400102    1060600601    1060600601   
## [11591] 1060600601    1060600601    1060600601    1060600601    19301XXXXX   
## [11596] 18304XXXXX    1080401103    1080401103    11101002XX    19010XXXXX   
## [11601] 19010XXXXX    1780200302    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [11606] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [11611] 175XXXXXXX    175XXXXXXX    1830509201    1480400101    1210501105   
## [11616] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 3210400113   
## [11621] 2311119501    1760800309    1750101001    1750101001    1750101001   
## [11626] 1750101001    1830301701    1830301701    17037457XX    2314300102   
## [11631] 2314300102    1704149903    1211200112    1700204202    1700204202   
## [11636] 1700204202    1480400803    1480400803    1480400803    1703903303   
## [11641] 1703903303    1480403401    1830201102    1830201102    17102001XX   
## [11646] 17102001XX    17063XXXXX    17063XXXXX    1700505801    1700505801   
## [11651] 1700505801    1700505801    1750102610    1750102610    1750102610   
## [11656] 1750102610    1750102610    1750102610    1750102610    1750102610   
## [11661] 1750102610    1702304806    1702304806    1702304806    1830202404   
## [11666] 1470300406    1702304431    17710001XX    1750102612    1750102604   
## [11671] 19001XXXXX    17023XXXXX    2290100108    1750101508    121XXXXXXX020
## [11676] 1702807101    199XXXXXXX012 17041XXXXX    17002042XX    17036XXXXX   
## [11681] 1750101506    1703202733    1750102401    231XXXXXXX    299XXXXXXX013
## [11686] 199XXXXXXX010 399XXXXXXX016 1700204229    17046XXXXX    16501XXXXX   
## [11691] 1703202717    32109XXXXX    17065XXXXX    199XXXXXXX013 17039XXXXX   
## [11696] 1703214001    1700204225    17501015XX    199XXXXXXX054 1703202734   
## [11701] 1750102501    17032XXXXX    17001025XX    16111XXXXX    30706002XX   
## [11706] 1290200401    19010XXXXX    175XXXXXXX    1703222501    1750101001   
## [11711] 17063XXXXX    1700204009    1750102610    1703202801    17710001XX   
## [11716] 2311100401    17023XXXXX    1702222101    1211100201    17038XXXXX   
## [11721] 1470100801    2291500501    1702304405    17041XXXXX    1702315101   
## [11726] 1311606801    2280100120    17002042XX    17036XXXXX    1703910501   
## [11731] 1703202713    1702311412    199XXXXXXX010 17046036XX    16501XXXXX   
## [11736] 1750101503    17065XXXXX    3210200229    17039XXXXX    17023231XX   
## [11741] 10802XXXXX    12105012XX    17023043XX    14102XXXXX    17032027XX   
## [11746] 17407001XX    17033XXXXX    175XXXXXXX    1703933005    16102003XX   
## [11751] 1830201401    1950100103    1950100101    12305015XX    1750100101   
## [11756] 1750100101    1750100101    1702326801    1760301104    1480400202   
## [11761] 1480400202    1830200201    1830200201    1210500105    1210500105   
## [11766] 1702300401    1702300401    1750100205    1750100205    1750100205   
## [11771] 1702700301    1702700301    17801001XX    17802020XX    1703900803   
## [11776] 17710001XX    17710001XX    1703620918    1170100501    1703626303   
## [11781] 1210505901    1703906302    1780101703    1703900801    1760300401   
## [11786] 1210501107    1702021301    1702021301    1703919101    1620300201   
## [11791] 1703926101    1120300103    1780200307    14805004XX034 1702300413   
## [11796] 1230400201    17023XXXXX    17023XXXXX    1750100201    1750100201   
## [11801] 1750100201    121XXXXXXX020 1703906006    1703900802    1830300701   
## [11806] 1830300701    32104001XX    17037XXXXX    17037XXXXX    1702300414   
## [11811] 32102XXXXX026 17039060XX    17039060XX    1210600201    1210600201   
## [11816] 1830204802    1480500401    1210506401    1210506401    1210506401   
## [11821] 1210506601    1210506601    1702304442    199XXXXXXX009 183XXXXXXX   
## [11826] 183XXXXXXX    14704XXXXX    17501023XX018 1470100101    1703923508   
## [11831] 17321XXXXX023 17321XXXXX023 1830200501    199XXXXXXX007 17002042XX   
## [11836] 17802XXXXX    17802XXXXX    1480401001    1210501204    17023004XX   
## [11841] 17023044XX    17023044XX    1620100101    1620100101    1620100101   
## [11846] 1580200105    1732116201    1703906002    1703906002    1703906002   
## [11851] 1750600302    1702307202    1707700302    1750102401    1750102401   
## [11856] 1750102401    1300100601    3210400105    1510300401    17501XXXXX   
## [11861] 1210501217    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [11866] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 1703710601    1702300408   
## [11871] 3161000112    16501XXXXX    16501XXXXX    3210501001    32109XXXXX   
## [11876] 17039008XX    199XXXXXXX008 1090100704    1090100704    1090100704   
## [11881] 1210501102    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
## [11886] 11004001XX    110XXXXXXX    110XXXXXXX    110XXXXXXX    1480400802   
## [11891] 1703900807    1703919103    1210503101    1210501210    1480600401   
## [11896] 1703620705    1480401501    17204002XX    12105012XX    12105012XX   
## [11901] 12105012XX    17039033XX    17023043XX    17801XXXXX    1703935301   
## [11906] 14102XXXXX    30702018XX    1480500402    12105011XX    199XXXXXXX054
## [11911] 199XXXXXXX054 199XXXXXXX054 1950100105    1480500404    1750600601   
## [11916] 16302XXXXX    1620100401    1750102501    1750102501    17505XXXXX   
## [11921] 17032027XX    1210600212    1210501305    1703710606    1703710606   
## [11926] 1700634501    1170100105    11701XXXXX    17041007XX    17041007XX   
## [11931] 19010XXXXX    175XXXXXXX    1830509201    1410204208    1210503104   
## [11936] 1480403401    1480403401    1830201102    1830201102    1830202404   
## [11941] 1709400101    1702304605    1705013202    1705013202    1480401601   
## [11946] 1480401601    16102003XX    16102003XX    16102003XX    16102003XX   
## [11951] 16102003XX    16102003XX    16102003XX    16102003XX    17023048XX   
## [11956] 17023048XX    1830201401    1830201401    1950100103    12106XXXXX   
## [11961] 12106XXXXX    1950100101    1100400132    2302012303    1709201501   
## [11966] 699XXXXXXX    1210600206    1480500406    3210501003    12305015XX   
## [11971] 12305015XX    12305015XX    1400211501    1400211501    1750100101   
## [11976] 1750100101    1702326801    1702326801    1702326801    1480400202   
## [11981] 1480400202    1480400202    1830200201    1830200201    1830200201   
## [11986] 1210500105    1210500105    1702300401    1750100205    1750100205   
## [11991] 1750100205    1702700301    1702700301    1702700301    1702700301   
## [11996] 17801001XX    17801001XX    1750300404    1230100401    1210504202   
## [12001] 1710200101    1231400701    17710001XX    17710001XX    17710001XX   
## [12006] 17710001XX    17710001XX    1780100112    1780100112    1480500408   
## [12011] 1630200301    1703626303    1703626303    1750102612    1750102612   
## [12016] 1210505901    1709441601    1701300701    3160407101    1704007501   
## [12021] 1480203001    1480203001    1760300401    1760300401    1480501702   
## [12026] 2302001802    1480400502    1750100207    1750300505    1080200401   
## [12031] 1480403301    1702021301    1702021301    1702021301    1702021301   
## [12036] 16203XXXXX    1300100501    1300100501    17030XXXXX    17030XXXXX   
## [12041] 17030XXXXX    17030XXXXX    17030XXXXX    17030XXXXX    1480400801   
## [12046] 2302001803    17603XXXXX    1703001001    14805004XX034 1702300413   
## [12051] 1230400201    1230400201    1230400201    17023XXXXX    17023XXXXX   
## [12056] 1702300405    1230100907    1750100201    1750100201    1750100201   
## [12061] 1750100201    1750100201    1750100201    1750100201    1230100903   
## [12066] 1230100903    316XXXXXXX    121XXXXXXX020 121XXXXXXX020 1702222101   
## [12071] 1702222101    1230100908    1400200201    1830202405    1702807101   
## [12076] 14313XXXXX    14313XXXXX    14313XXXXX    2280400201    17037XXXXX   
## [12081] 17037XXXXX    17037XXXXX    17094XXXXX    1400201601    1702300414   
## [12086] 31607008XX    15802XXXXX    32102XXXXX026 32102XXXXX026 32102XXXXX026
## [12091] 14002XXXXX    14002XXXXX    14002XXXXX    2280101701    17039060XX   
## [12096] 10901XXXXX    1100400201    17115024XX    17115024XX    17038XXXXX   
## [12101] 1210600201    1210600201    1210600201    1431300101    1830204802   
## [12106] 1210506401    1210506401    1830200405    1230400301    1210506601   
## [12111] 1210506601    199XXXXXXX009 199XXXXXXX009 183XXXXXXX    183XXXXXXX   
## [12116] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
## [12121] 183XXXXXXX    14804006XX    1400200102    14002001XX    17501023XX018
## [12126] 17501023XX018 148XXXXXXX    148XXXXXXX    148XXXXXXX    1470100101   
## [12131] 1470100101    307XXXXXXX    2302012304    17041XXXXX    17041XXXXX   
## [12136] 17321XXXXX023 17321XXXXX023 2302007005    1780100101    1780100101   
## [12141] 1480400601    1702300415    1830200501    1830200501    1830200501   
## [12146] 1830200501    14806001XX    14806001XX    14806001XX    14806XXXXX   
## [12151] 14806XXXXX    14806XXXXX    1780207001    1709201906    17002042XX   
## [12156] 17002042XX    17002042XX    17002XXXXX    17002XXXXX    17036XXXXX   
## [12161] 17036XXXXX    17036XXXXX    17802XXXXX    17802XXXXX    1480401001   
## [12166] 1480401001    1480401001    2312300101    14805004XX    2280400208   
## [12171] 2280400207    3161200102    17501014XX    17023004XX    17023004XX   
## [12176] 17023004XX    17023004XX    17023044XX    17023044XX    17023044XX   
## [12181] 17023044XX    3161102002    3210505803    1210501301    61841007XX   
## [12186] 1620100101    1620100101    1830200802    1580200105    10201XXXXX   
## [12191] 13208XXXXX    13208XXXXX    13208XXXXX    1703906002    1703906002   
## [12196] 1750600302    1750600302    1750600302    1750600302    1702307202   
## [12201] 1702307202    1480400501    1750102401    13116XXXXX    13116XXXXX   
## [12206] 1300100601    1480400604    1510300401    1510300401    1709244002   
## [12211] 1782000301    1709441701    17501XXXXX    17501XXXXX    231XXXXXXX   
## [12216] 231XXXXXXX    231XXXXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [12221] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [12226] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [12231] 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 1230100905    1703710601   
## [12236] 3161000112    14802XXXXX    2280403702    16501XXXXX    16501XXXXX   
## [12241] 16501XXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX   
## [12246] 1480401201    3210500301    1480500407    2280400203    2280400203   
## [12251] 2280400203    3210501001    1710200102    32109XXXXX    32109XXXXX   
## [12256] 1780701402    1610500202    1610500202    16204XXXXX    16204XXXXX   
## [12261] 1480400211    1480400211    1830200202    1210500107    1210500107   
## [12266] 1210500107    1702300406    1702300406    1780100109    1780100109   
## [12271] 1720400204    1470200701    22804002XX    1480501701    1709244001   
## [12276] 1709244001    1709201502    1709201502    1709201502    1709201502   
## [12281] 1705700701    199XXXXXXX008 1090100704    1230100902    1230100902   
## [12286] 1230100902    1480401901    1480401901    1480401901    17027XXXXX   
## [12291] 1210501102    17035169XX    17039XXXXX    17039XXXXX    17039XXXXX   
## [12296] 17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX    1120100301   
## [12301] 1230400303    1230400303    11004001XX    11004001XX    110XXXXXXX   
## [12306] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [12311] 1480201401    1480400802    2302001801    2302001801    2302012306   
## [12316] 1400201801    14002018XX    1480600103    1480600103    1210501210   
## [12321] 1210501210    1480600401    1480600401    17608XXXXX    1780800401   
## [12326] 1780800401    1480401202    1480401501    1480401501    1703929301   
## [12331] 123XXXXXXX    123XXXXXXX    123XXXXXXX    17204002XX    17204002XX   
## [12336] 12105012XX    12105012XX    12105012XX    17023043XX    17023043XX   
## [12341] 31608XXXXX    3211400102    17801XXXXX    17801XXXXX    17801XXXXX   
## [12346] 17801XXXXX    17801XXXXX    17801XXXXX    17801XXXXX    22823006XX   
## [12351] 14102XXXXX    14102XXXXX    14102XXXXX    14102XXXXX    14102XXXXX   
## [12356] 31610XXXXX    31610XXXXX    30702018XX    1230100402    69302004XX   
## [12361] 69302004XX    1480500402    199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [12366] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1780107901    1400210001   
## [12371] 1400210001    1480500404    1750600601    1750600601    1250203001   
## [12376] 1780800101    1750102501    1750102501    12304XXXXX030 17505XXXXX   
## [12381] 17032027XX    17032027XX    17032XXXXX    17032XXXXX    17032XXXXX   
## [12386] 1750500101    1750500101    1650100204    1650100204    1230100906   
## [12391] 1230100906    1210501303    1709441801    1480500405    18303057XX   
## [12396] 1210501305    1480403302    1480403302    1480500403    2302007001   
## [12401] 1710200103    1750100102    11701XXXXX    2302007002    31612020XX   
## [12406] 17041007XX    1750400301    1750400301    1480204001    23121145XX   
## [12411] 17077XXXXX    17077XXXXX    1500100101    1500100101    19010XXXXX   
## [12416] 19010XXXXX    19010XXXXX    22901001XX    175XXXXXXX    175XXXXXXX   
## [12421] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [12426] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    1830509201   
## [12431] 1480400101    1210501105    199XXXXXXX053 32105XXXXX036 32105XXXXX036
## [12436] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
## [12441] 32105XXXXX036 32105XXXXX036 1231200101    17608010XX    1750101511   
## [12446] 17037457XX    17037457XX    17037457XX    1704149903    1480400803   
## [12451] 12312001XX    1480403401    1480600104    1480600104    1830201102   
## [12456] 1830201102    17102001XX    17102001XX    17102001XX    1750102610   
## [12461] 1702304806    1830202404    3160806607    1750102605    17710001XX   
## [12466] 1750102612    17011026XX    1750300507    1700204233    1750300505   
## [12471] 17023XXXXX    17096373XX    121XXXXXXX020 1702807101    1750101202   
## [12476] 17038XXXXX    17041XXXXX    17002XXXXX    1750300402    1750102406   
## [12481] 231XXXXXXX    199XXXXXXX010 17503XXXXX    1750101503    228XXXXXXX   
## [12486] 32109XXXXX    17027XXXXX    17039XXXXX    17501015XX    199XXXXXXX054
## [12491] 1750300905    1750102501    17032027XX    1750100102    1750300903   
## [12496] 1750400301    17077XXXXX    175XXXXXXX    1750101001    1750102610   
## [12501] 199XXXXXXX010 1750102605    1750102612    17011026XX    1750300505   
## [12506] 17023XXXXX    1750100201    1702807101    14313XXXXX    17002042XX   
## [12511] 199XXXXXXX010 17503XXXXX    32109XXXXX    199XXXXXXX054 1750102501   
## [12516] 22915XXXXX    2290100205    22901001XX    1750101001    1750102610   
## [12521] 1702329101    2290100108    1750100201    1702807101    1210600201   
## [12526] 1210506401    14704XXXXX    17041XXXXX    17002042XX    17036XXXXX   
## [12531] 14805004XX    17023004XX    1750600302    299XXXXXXX013 199XXXXXXX010
## [12536] 199XXXXXXX010 14701XXXXX    17065XXXXX    17039XXXXX    12105012XX   
## [12541] 17032027XX    16111XXXXX    30706002XX    17402XXXXX    19010XXXXX   
## [12546] 175XXXXXXX    175XXXXXXX    1750101001    1750102605    1750102601   
## [12551] 1750100101    1750300404    1750300904    1750102612    1750102604   
## [12556] 1080201003    1750300505    1702807101    14704XXXXX    1703703908   
## [12561] 1750102401    299XXXXXXX013 199XXXXXXX010 17503XXXXX    1070300901   
## [12566] 17501015XX    199XXXXXXX054 1750102501    17032027XX    30706002XX   
## [12571] 1750400301    1080201703    175XXXXXXX    1750101001    1750102610   
## [12576] 1750102605    1750102605    1480500406    3210501003    1750300404   
## [12581] 1750300404    1750300904    1470300413    17710001XX    1480500408   
## [12586] 1702329101    1750102612    1750102612    1750102612    1703202724   
## [12591] 1750102604    1750300505    1750300505    1702304426    17023XXXXX   
## [12596] 2290100108    1750101508    1750100201    1702807101    1700211502   
## [12601] 1706300801    17037XXXXX    1702300414    32102XXXXX026 1210600201   
## [12606] 1210506401    17002042XX    14805004XX    17023004XX    1750101506   
## [12611] 1750600302    1750102401    1750300906    199XXXXXXX010 199XXXXXXX010
## [12616] 17503XXXXX    228XXXXXXX    14701XXXXX    1070300901    32109XXXXX   
## [12621] 17065XXXXX    3210400102    22801001XX    17039XXXXX    1700204225   
## [12626] 12105012XX    17023043XX    17501015XX    199XXXXXXX054 1060800201   
## [12631] 1750102501    1750102501    1750102501    17032XXXXX    1703202722   
## [12636] 30706002XX    1750400301    1480204001    175XXXXXXX    175XXXXXXX   
## [12641] 32105XXXXX036 1750101001    1750101001    1750102610    1750102610   
## [12646] 1750102610    199XXXXXXX010 1750102605    699XXXXXXX    1750102612   
## [12651] 1750300507    1750300505    689XXXXXXX    299XXXXXXX013 199XXXXXXX010
## [12656] 399XXXXXXX016 199XXXXXXX054 1750102501    1750300903    1750400301   
## [12661] 175XXXXXXX    1750102610    1705013202    1750300404    1750300904   
## [12666] 17710001XX    1750102612    1750300505    1703926101    121XXXXXXX020
## [12671] 1702304429    17037XXXXX    14704XXXXX    17501023XX018 17002042XX   
## [12676] 17002XXXXX    17036XXXXX    14703004XX    17023044XX    1702307202   
## [12681] 1750102401    299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 17039008XX   
## [12686] 17039XXXXX    1702313401    17023043XX    199XXXXXXX054 1750102501   
## [12691] 1750400301    17077XXXXX    19010XXXXX    175XXXXXXX    1750101001   
## [12696] 1750101511    1750102610    1700204240    17710001XX    1702304411   
## [12701] 17011026XX    1702309901    1703323010    1703620707    2311100401   
## [12706] 1706505611    1702304408    1740200802    1650104302    1700204274   
## [12711] 1700204255    1700204269    17023XXXXX    121XXXXXXX020 1702222101   
## [12716] 1700204235    1703202750    1704603611    1700211511    199XXXXXXX012
## [12721] 1750101202    1702323102    17038XXXXX    1703202753    2291500501   
## [12726] 17000XXXXX    1410200606    1702304405    1702315101    1703933001   
## [12731] 1700204219    1771000107    1706543701    2280100120    17002XXXXX   
## [12736] 17036XXXXX    1703922406    14703004XX    1470101308    1703202745   
## [12741] 1703818001    1750101403    1702304308    1750101504    1750300402   
## [12746] 1703926601    1750102406    1703910501    1830101805    13116XXXXX   
## [12751] 1750102603    1702311412    199XXXXXXX010 1220200101    1703620703   
## [12756] 17046036XX    1750101503    1702323104    1771000104    32109XXXXX   
## [12761] 1700204257    1703817223    1702311402    1703600201    17065XXXXX   
## [12766] 1700211504    199XXXXXXX013 22801001XX    3210200229    1771000103   
## [12771] 1703817215    17039XXXXX    17023231XX    1702313401    1703318416   
## [12776] 1700200101    1700220805    1703209801    1611101102    199XXXXXXX054
## [12781] 1100503407    1702300101    1703620904    1760300901    1701523304   
## [12786] 1703817207    1704603612    1700204284    1703817216    17032XXXXX   
## [12791] 1703817226    1702304701    1703930001    1740200416    17405XXXXX   
## [12796] 1703817202    2280101601    17407001XX    1780900302    1700220802   
## [12801] 1700204285    17402XXXXX    1702323101    17004089XX    17033XXXXX   
## [12806] 1703817206    1702317901    19010XXXXX    1703620702    175XXXXXXX   
## [12811] 1703202742    1703933006    32105XXXXX036 1700204277    1211100202   
## [12816] 1700204273    17063XXXXX    1700255701    1706600704    1700211509   
## [12821] 1703933005    1703817225    1702311408    1704118101    1702300201   
## [12826] 1702304605    1705013202    1750102605    1750102605    1702309003   
## [12831] 17023048XX    1703906010    1750100101    1702326801    1703817204   
## [12836] 1750300404    17710001XX    1580200502    1703626303    1750102612   
## [12841] 1750102612    1750102612    1703620704    1750300507    1750300507   
## [12846] 1703906302    1760300401    1750300505    1750300505    1080200401   
## [12851] 1702021301    1703745705    1703716607    1703926101    1300100501   
## [12856] 1210503002    17023XXXXX    1703745702    1750100201    1702222101   
## [12861] 1702807101    3162300203    14313XXXXX    1510200103    17037XXXXX   
## [12866] 31607008XX    32102XXXXX026 2280101701    199XXXXXXX012 17039060XX   
## [12871] 1700204234    1700204201    1210600201    1210506401    183XXXXXXX   
## [12876] 17501023XX018 307XXXXXXX    1707700109    1060800701    17002042XX   
## [12881] 17002XXXXX    17036XXXXX    1704603613    11001XXXXX    1090100801   
## [12886] 17802XXXXX    14703004XX    10803XXXXX    1750300402    1750300402   
## [12891] 17023004XX    1620100101    1703906002    1750600302    1703745701   
## [12896] 1702307202    1707700302    1750102401    1750300906    1210501217   
## [12901] 231XXXXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016
## [12906] 14306XXXXX    16501XXXXX    30702002XX    228XXXXXXX    14701XXXXX   
## [12911] 32109XXXXX    22901008XX    17039191XX    1760800310    1750100601   
## [12916] 17023047XX    17039XXXXX    19002XXXXX    110XXXXXXX    1703900807   
## [12921] 1210501210    1703927702    17039033XX    11002XXXXX    17023043XX   
## [12926] 17801XXXXX    14102XXXXX    1480500402    199XXXXXXX054 199XXXXXXX054
## [12931] 199XXXXXXX054 1750300905    1060800201    1750600601    1750102501   
## [12936] 1750102501    22915XXXXX    10804007XX    17032027XX    2280100131   
## [12941] 1700634501    1750300903    1750300903    17402XXXXX    1750400301   
## [12946] 1750400301    1750400301    17059051XX    17016XXXXX    18304XXXXX   
## [12951] 19010XXXXX    175XXXXXXX    32105XXXXX036 30742004XX    1750101001   
## [12956] 1750101511    17037457XX    1704149903    1211200112    1290100304   
## [12961] 1700204202    17063XXXXX    1750102610    1750102610    1750102610   
## [12966] 1750102601    1750100101    1702300401    1750100205    1703906302   
## [12971] 1703926101    10801003XX    1750100201    1703906006    3210900507   
## [12976] 32104001XX    32102XXXXX026 10901XXXXX    1210600201    1431300101   
## [12981] 3160700205    1480500401    2294200718    1210506401    1210506601   
## [12986] 183XXXXXXX    1650100102    17501023XX018 1470100101    1703923508   
## [12991] 1702304801    32109024XX    1750102401    299XXXXXXX013 199XXXXXXX010
## [12996] 399XXXXXXX016 2294200602    17040075XX    110XXXXXXX    1210501210   
## [13001] 1703907601    1703929301    17501002XX    17801XXXXX    17006345XX   
## [13006] 16302XXXXX    10804007XX    2312100501    17041007XX    175XXXXXXX   
## [13011] 1750102605    1750102605    1480500406    1750102601    17710001XX   
## [13016] 1750102612    1750102612    1750102612    1750102612    1750300507   
## [13021] 1750300507    6940100303    1750300505    1750300505    17023XXXXX   
## [13026] 199XXXXXXX012 17038XXXXX    17501023XX018 17041251XX    17002XXXXX   
## [13031] 1750101403    17501014XX    1750300402    1750300402    1750102406   
## [13036] 1750102603    231XXXXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [13041] 17503XXXXX    17503XXXXX    17503XXXXX    32109XXXXX    1480501701   
## [13046] 3210400102    1709201502    1709201502    1580200101    6941400201   
## [13051] 110XXXXXXX    6940100302    694XXXXXXX    199XXXXXXX054 199XXXXXXX054
## [13056] 199XXXXXXX054 199XXXXXXX054 1750102501    1750102501    17032027XX   
## [13061] 17032XXXXX    1750102608    1750102608    17407001XX    1750300903   
## [13066] 1750300903    1750400301    1750400301    1750400301    1750400301   
## [13071] 1480204001    22901001XX    175XXXXXXX    175XXXXXXX    1750101001   
## [13076] 6940100305    1750102610    1750102610    1750102610    1750102610   
## [13081] 1702304605    1705013202    1750102605    3210501003    1750102601   
## [13086] 1750100101    1702326801    17710001XX    1480500408    1703626303   
## [13091] 1750102612    1703745705    1703716607    1300100501    1210503002   
## [13096] 17023XXXXX    121XXXXXXX020 1702300414    31607008XX    32102XXXXX026
## [13101] 1700204234    1210600201    1431300101    1707700109    17036XXXXX   
## [13106] 17023044XX    1750600302    1703745701    1707700302    231XXXXXXX   
## [13111] 299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 17503XXXXX    16501XXXXX   
## [13116] 32109XXXXX    17039191XX    22801001XX    17023047XX    17039XXXXX   
## [13121] 110XXXXXXX    1707700401    12105012XX    17023043XX    14102XXXXX   
## [13126] 199XXXXXXX054 1750102501    17032027XX    1750400301    17077XXXXX   
## [13131] 18304XXXXX    19010XXXXX    22901001XX    175XXXXXXX    32105XXXXX036
## [13136] 17037457XX    1704149903    1211200112    1750102610    17710001XX   
## [13141] 1700116701    17603XXXXX    17023XXXXX    121XXXXXXX020 32104001XX   
## [13146] 17037XXXXX    32102XXXXX026 17000XXXXX    17041251XX    3161003202   
## [13151] 17002042XX    17036XXXXX    17501014XX    2311114001    17023044XX   
## [13156] 1750600302    13116XXXXX    231XXXXXXX    199XXXXXXX010 1702632701   
## [13161] 16501XXXXX    228XXXXXXX    17035169XX    110XXXXXXX    17023043XX   
## [13166] 14102XXXXX    17501015XX    199XXXXXXX054 17015XXXXX    1750102501   
## [13171] 22915XXXXX    17032027XX    17032XXXXX    17407001XX    17033184XX   
## [13176] 17077XXXXX    22901001XX    175XXXXXXX    12111002XX    199XXXXXXX010
## [13181] 30706002XX    1750100101    1702300401    1750100205    1480403301   
## [13186] 1703926101    1750100201    316XXXXXXX    3210200202    1100700801   
## [13191] 3210900507    1703900802    1830300701    1210600201    1431300101   
## [13196] 3160700205    1830204802    1480500401    1210506401    1700634503   
## [13201] 1210506601    1650100102    1470100101    1703923508    17321XXXXX023
## [13206] 1721201002    17802XXXXX    32109024XX    17023004XX    1620100101   
## [13211] 199XXXXXXX010 399XXXXXXX016 3161000112    16501XXXXX    17040075XX   
## [13216] 1090100704    1480403202    1706008301    1210501210    1703929301   
## [13221] 1703927702    17039033XX    1703707001    16302XXXXX    10804007XX   
## [13226] 2250100102    3161100105    17041007XX    1830509201    32105XXXXX036
## [13231] 1480403401    30703001XX    1750102605    2280100103    1750102612   
## [13236] 1750300507    3070300113    1750300505    316XXXXXXX    307XXXXXXX   
## [13241] 199XXXXXXX010 17503XXXXX    1750102602    694XXXXXXX    199XXXXXXX054
## [13246] 1750102501    1750300903    1750400301    1750102610    321XXXXXXX   
## [13251] 199XXXXXXX010 22901001XX    23020123XX    1750102605    1750102605   
## [13256] 16102003XX    17092XXXXX    17092XXXXX    1100400132    2302012303   
## [13261] 1709201501    1709201501    1709201501    1750100101    1702700301   
## [13266] 1702700301    11004002XX    1750102612    1750102612    1750300507   
## [13271] 1750300507    1703912601    1703912601    1780101703    1480203001   
## [13276] 1480203001    1480203001    1750300505    1750300505    1080200401   
## [13281] 1080200401    1702021301    1702021301    1050200502    1703707009   
## [13286] 3210400112    1703001001    1120300103    1760600104    1780200307   
## [13291] 14805004XX034 14805004XX034 1702300413    2290100201    17023XXXXX   
## [13296] 1703910701    23143001XX    1750100201    1750100201    1702807101   
## [13301] 1702807101    1080201020    17037XXXXX    17094XXXXX    31607008XX   
## [13306] 31607008XX    32102XXXXX026 32102XXXXX026 17039264XX    17039264XX   
## [13311] 199XXXXXXX012 1950100106    31615002XX    1080201016    1100400201   
## [13316] 17038XXXXX    17038XXXXX    1703710801    1703710801    17321XXXXX023
## [13321] 1090100201    14806001XX    14806001XX    14806001XX    17002XXXXX   
## [13326] 17002XXXXX    17036XXXXX    17036XXXXX    17802XXXXX    17506XXXXX   
## [13331] 1320801601    1750300402    17023004XX    1620100101    1620100101   
## [13336] 1750102406    23020070XX    23020XXXXX    23020XXXXX    1580200105   
## [13341] 2282907301    13208XXXXX    1702307202    17501XXXXX    231XXXXXXX   
## [13346] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [13351] 399XXXXXXX016 399XXXXXXX016 17503XXXXX    17503XXXXX    14801001XX   
## [13356] 14801001XX    2294200502    1830305702    1830305702    16501XXXXX   
## [13361] 1100400203    1750101503    2290100805    32109XXXXX    32109XXXXX   
## [13366] 32109XXXXX    1750500701    1750500701    1610500202    1610500202   
## [13371] 1703922001    1709201502    1709201502    1709201502    1709201502   
## [13376] 1705700701    22801001XX    3070300111    14309011XX    17039XXXXX   
## [13381] 17039XXXXX    11004XXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [13386] 110XXXXXXX    1703920301    1703920301    2302012302    1703929301   
## [13391] 1703911802    1703911802    12105012XX    17039033XX    17801XXXXX   
## [13396] 14102XXXXX    17501015XX    3210506001    199XXXXXXX054 199XXXXXXX054
## [13401] 199XXXXXXX054 1080402304    1060800201    1060800201    1750600601   
## [13406] 1750600601    1750102501    1750102501    22915XXXXX    1480100101   
## [13411] 1480100101    1080400713    17505XXXXX    17032XXXXX    17032XXXXX   
## [13416] 1750500101    1210600212    1210501305    1210501305    1750102608   
## [13421] 1750102608    1703710606    1703710606    2290100806    1750300903   
## [13426] 1709201910    2302007002    2302007002    1750400301    1750400301   
## [13431] 17033XXXXX    1060600601    1703718603    18304XXXXX    18304XXXXX   
## [13436] 1080401103    175XXXXXXX    175XXXXXXX    32105XXXXX036 32105XXXXX036
## [13441] 2314300102    1830305701    1703927701    1703922401    1210503104   
## [13446] 1480600104    1480600104    1700505801    1750102610    1750102610   
## [13451] 1702304806    1702304806    1709400101    1750102605    1750102605   
## [13456] 1750102605    1750102605    1750102605    1750102605    1750102605   
## [13461] 1750102605    1750102605    1750102605    1210501106    1210501106   
## [13466] 1610200301    16102003XX    16102003XX    16102003XX    16102003XX   
## [13471] 16102003XX    16102003XX    16102003XX    17023048XX    17023048XX   
## [13476] 1830201401    1830201401    1950100103    1431300104    2294200701   
## [13481] 1090300401    1950100101    19501XXXXX    17092XXXXX    17092XXXXX   
## [13486] 1709253501    1100400132    1100400132    2302012303    1709201501   
## [13491] 1709201501    699XXXXXXX    699XXXXXXX    699XXXXXXX    699XXXXXXX   
## [13496] 1100400168    1480500406    3210501003    12305015XX    12305015XX   
## [13501] 1750102601    1750102601    1750102601    1750100101    1750100101   
## [13506] 1760301104    1480400202    1480400202    1830200201    1830200201   
## [13511] 1210500105    1210500105    1750100205    1750100205    1750100205   
## [13516] 1702700301    1702700301    1702700301    1702700301    17801001XX   
## [13521] 17801001XX    2310901003    1750300404    1750300404    1750300404   
## [13526] 1750300404    1470200201    1470200201    17802020XX    1750300904   
## [13531] 1750300904    1750300904    1750300904    1750300904    1750300904   
## [13536] 1710200101    1710200101    1703900803    1703900803    1703900803   
## [13541] 1231400701    1231400701    2130500101    17710001XX    17710001XX   
## [13546] 17710001XX    1060100301    1060100301    1703620918    1780100112   
## [13551] 1780100112    1580200502    1480500408    1480500408    1703626303   
## [13556] 1060600603    1060600603    1060600603    1060600603    1060600603   
## [13561] 1750102612    1750102612    1750102612    1750102612    1750102612   
## [13566] 1750102612    1750102612    1750102612    1750102612    1750102612   
## [13571] 1750102612    1090101401    1709637301    1709637301    1709637301   
## [13576] 1750300507    1750300507    1750300507    1750300507    1750601201   
## [13581] 1750601201    1750601201    1703906302    1703906302    1703906302   
## [13586] 1780101703    1780101703    1780101703    1780101703    1780101703   
## [13591] 1780101703    1950100107    1709441601    1750102604    1080100104   
## [13596] 1080100104    1703900801    1703900801    1100400105    2280203101   
## [13601] 1480203001    1480203001    1480203001    1480203001    1760300401   
## [13606] 1480400502    1480400502    1750300505    1750300505    1750300505   
## [13611] 1750300505    1750300505    1750300505    1750300505    3161000105   
## [13616] 1080200401    1080200401    1080200401    1080200401    1080200401   
## [13621] 1080200401    1080200401    1080200401    1080200401    1080200401   
## [13626] 1080200401    1100400101    1480403301    1480403301    1480403301   
## [13631] 1702021301    1702021301    1702021301    1760801502    1050200201   
## [13636] 16203XXXXX    16203XXXXX    1703745705    1703926101    1703926101   
## [13641] 1703926101    1480400801    1830506401    1830506401    17603XXXXX   
## [13646] 17603XXXXX    17603XXXXX    1703707009    3210400112    3210400112   
## [13651] 14805004XX034 14805004XX034 1702300413    1230400201    2280100117   
## [13656] 2280100117    2280100117    17023XXXXX    17023XXXXX    17023XXXXX   
## [13661] 17023XXXXX    10801XXXXX    10801003XX    10801003XX    321XXXXXXX   
## [13666] 321XXXXXXX    23143001XX    1709100301    112XXXXXXX    112XXXXXXX   
## [13671] 1750100201    1750100201    316XXXXXXX    316XXXXXXX    316XXXXXXX   
## [13676] 316XXXXXXX    121XXXXXXX020 121XXXXXXX020 121XXXXXXX020 1700206101   
## [13681] 3210200202    1830202405    1703906006    1703906006    1703906006   
## [13686] 1702807101    1702807101    1702807101    3162300203    3162300203   
## [13691] 3210900507    1703900802    1703900802    1703900802    3070100101   
## [13696] 2281201810    2281201810    2282300303    2282300303    1830300701   
## [13701] 1830300701    1830300701    2290100804    32104001XX    32104001XX   
## [13706] 17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
## [13711] 17094XXXXX    1100400110    32102XXXXX026 32102XXXXX026 32102XXXXX026
## [13716] 32102XXXXX026 32102XXXXX026 2280101701    2280101701    2280101701   
## [13721] 2280101701    199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012
## [13726] 17039060XX    17039060XX    17039060XX    1950100106    1100801007   
## [13731] 10901XXXXX    10901XXXXX    10901XXXXX    31615002XX    31615002XX   
## [13736] 1700204201    1700204201    1700204201    11007XXXXX    11007XXXXX   
## [13741] 689XXXXXXX    689XXXXXXX    2310901006    17115024XX    1750500501   
## [13746] 1750500501    1210600201    1210600201    1210600201    1771000101   
## [13751] 1431300101    1431300101    1431300101    3160700205    3160700205   
## [13756] 1830204802    1830204802    3210505801    3210505801    1480500401   
## [13761] 1480500401    1480500401    2294200718    2294200718    2294200718   
## [13766] 1210506401    1210506401    1210506401    1830200405    1700634503   
## [13771] 1700634503    1700634503    1210506601    1210506601    199XXXXXXX009
## [13776] 199XXXXXXX009 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
## [13781] 183XXXXXXX    183XXXXXXX    1782400201    1480400602    14804006XX   
## [13786] 14804006XX    14804006XX    1830500302    17501023XX018 17501023XX018
## [13791] 17501023XX018 17501023XX018 17501023XX018 148XXXXXXX    148XXXXXXX   
## [13796] 148XXXXXXX    148XXXXXXX    148XXXXXXX    1470100101    1470100101   
## [13801] 307XXXXXXX    307XXXXXXX    2280203001    1703923508    1703923508   
## [13806] 1703923508    17321XXXXX023 17321XXXXX023 1780100101    3160800309   
## [13811] 1701640002    1702304801    1702304801    1702304801    1480400601   
## [13816] 1480400601    3210603301    1721201002    1721201002    2311109001   
## [13821] 1830200501    1830200501    1090100201    14806001XX    14806001XX   
## [13826] 14806001XX    14806001XX    1709201906    1901000201    1901000201   
## [13831] 3161102001    3161102001    199XXXXXXX007 199XXXXXXX007 17002042XX   
## [13836] 17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX   
## [13841] 17002XXXXX    17036XXXXX    2280101902    1090100801    1090100801   
## [13846] 17802XXXXX    17802XXXXX    17802XXXXX    17802XXXXX    1480401001   
## [13851] 1480401001    17506XXXXX    14805004XX    10803XXXXX    10803XXXXX   
## [13856] 10803XXXXX    10803XXXXX    10803XXXXX    10803XXXXX    1709201903   
## [13861] 1760800302    2280100125    1750300402    1750300402    17023004XX   
## [13866] 17023004XX    17023004XX    17023004XX    2282907302    17023044XX   
## [13871] 1620100101    1620100101    1620100101    1620100101    1580200105   
## [13876] 1090101801    1090101702    13208XXXXX    10901010XX    1703906002   
## [13881] 1703906002    1703906002    1703906002    1750600302    1750600302   
## [13886] 1750600302    1090100803    1702307202    1702307202    1702307202   
## [13891] 18301XXXXX    1830204504    1707700302    1480400501    1480400501   
## [13896] 1090100202    1750102401    1750102401    1750102401    1750102401   
## [13901] 229XXXXXXX    229XXXXXXX    1310702201    1310702201    1750300906   
## [13906] 1750300906    1750300906    1750300906    1480400604    1060800203   
## [13911] 3210400105    1100400111    1709244002    1709441701    17501XXXXX   
## [13916] 17501XXXXX    17501XXXXX    1100400183    1210501217    10608002XX   
## [13921] 1709201902    231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX   
## [13926] 231XXXXXXX    231XXXXXXX    231XXXXXXX    231XXXXXXX    299XXXXXXX013
## [13931] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013
## [13936] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [13941] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [13946] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016
## [13951] 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016
## [13956] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
## [13961] 17503XXXXX    17503XXXXX    17503XXXXX    1703710601    1703710601   
## [13966] 1703710601    1520400202    2314308802    1430600701    3161000112   
## [13971] 2311109002    1610500201    1750300901    1830500301    1830500301   
## [13976] 1830500301    18305003XX    19501001XX    19501001XX    19501001XX   
## [13981] 14306XXXXX    14306XXXXX    1080100106    16501XXXXX    16501XXXXX   
## [13986] 16501XXXXX    16501XXXXX    30702002XX    228XXXXXXX    228XXXXXXX   
## [13991] 228XXXXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX    14701XXXXX   
## [13996] 2280400203    2280400203    1900200612    3210501001    3210501001   
## [14001] 2294200602    2294200602    2294200602    1709446601    32109XXXXX   
## [14006] 32109XXXXX    32109XXXXX    32109XXXXX    1750500701    1750500701   
## [14011] 1610500202    1610500202    3160700801    3160700801    22901008XX   
## [14016] 22901008XX    17039008XX    17039008XX    17039191XX    1480501701   
## [14021] 1709244001    1709244001    3210400102    1709201502    1709201502   
## [14026] 1709201502    1709201502    1709201502    1709201502    1705700701   
## [14031] 199XXXXXXX008 199XXXXXXX013 22801001XX    30701001XX    17040075XX   
## [14036] 17040075XX    1090100704    1090100704    1090100704    1090100704   
## [14041] 1580200101    1580200101    1480401502    17023047XX    17023047XX   
## [14046] 1480403202    1480403202    1060800301    1060800301    1060800301   
## [14051] 1060800301    1060800301    1060800301    1060800301    1060800301   
## [14056] 1060800301    17039XXXXX    17039XXXXX    17039XXXXX    17039XXXXX   
## [14061] 17039XXXXX    17039XXXXX    17039XXXXX    1090101601    1090101601   
## [14066] 23111004XX    1480403203    1480403203    1480403203    3161100301   
## [14071] 3161100301    2312114501    1120100301    11004001XX    11004001XX   
## [14076] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [14081] 110XXXXXXX    110XXXXXXX    31616XXXXX    1706008301    1706008301   
## [14086] 1480400802    1704100702    1703900807    1703900807    1703919103   
## [14091] 1703919103    10802XXXXX    10802XXXXX    10802XXXXX    10802XXXXX   
## [14096] 10802XXXXX    14804028XX    1480600103    1480600103    1210501210   
## [14101] 1210501210    1480600401    1480600401    1750300907    1750300907   
## [14106] 1703620705    1703620705    1703620705    17608XXXXX    17608XXXXX   
## [14111] 17608XXXXX    17608XXXXX    1703907601    1703907601    1090500602   
## [14116] 1480401501    1480401501    1703929301    1703929301    1703929301   
## [14121] 123XXXXXXX    123XXXXXXX    1703927702    1703927702    1703927702   
## [14126] 17204002XX    17204002XX    17204002XX    1100400106    12105012XX   
## [14131] 12105012XX    12105012XX    12105012XX    12105012XX    17039033XX   
## [14136] 17039033XX    1080300506    1080300506    31608XXXXX    31608XXXXX   
## [14141] 2280202101    2280202101    17801XXXXX    17801XXXXX    17801XXXXX   
## [14146] 17801XXXXX    17801XXXXX    17813012XX    1703935301    694XXXXXXX   
## [14151] 694XXXXXXX    17006345XX    1480500402    3210506001    12105011XX   
## [14156] 12105011XX    1100400107    199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [14161] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [14166] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [14171] 1750300905    1750300905    1060800201    1060800201    1060800201   
## [14176] 1060800201    1060800201    1060800201    1060800201    1060800201   
## [14181] 1060800201    1060800201    1060800201    1950100105    1080201017   
## [14186] 1080201017    1080201017    1480500404    1750600601    1750600601   
## [14191] 1750600601    1750600601    16302XXXXX    16302XXXXX    1750102501   
## [14196] 1750102501    1750102501    1750102501    1750102501    1750102501   
## [14201] 1750102501    1750102501    1750102501    1750102501    16105XXXXX   
## [14206] 1100400109    1080100301    1480100101    1080300501    1080300501   
## [14211] 1080300501    1080300501    1080400713    10804007XX    10804007XX   
## [14216] 10804007XX    17505XXXXX    17505XXXXX    17505XXXXX    17505XXXXX   
## [14221] 17505XXXXX    17505XXXXX    17505XXXXX    17032027XX    31616003XX   
## [14226] 18303XXXXX    1709441801    1480403302    1750102608    1750102608   
## [14231] 1480500403    1480500403    1703710606    1703710606    2280100131   
## [14236] 1480400504    2312100501    2312100501    1610200302    2250100102   
## [14241] 2250100102    1100400104    1700634501    1710200103    11005XXXXX   
## [14246] 11005XXXXX    1610100102    1750300903    1750300903    1750300903   
## [14251] 1750300903    2280203102    2280203102    3161100105    3161100105   
## [14256] 11701XXXXX    1704100701    1704100701    17041007XX    17041007XX   
## [14261] 17041007XX    1750400301    1750400301    1750400301    1750400301   
## [14266] 1750400301    1750400301    1750400301    1750400301    1750400301   
## [14271] 1750400301    1750400301    1750400301    1750400301    1480204001   
## [14276] 1100400102    1480402801    17077XXXXX    1060600601    1060600601   
## [14281] 1060600601    1060600601    1060600601    1060600601    10606006XX   
## [14286] 10606006XX    1080201703    17016XXXXX    1080401103    1080401103   
## [14291] 1080401103    1080401103    1080401103    11101002XX    19010XXXXX   
## [14296] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [14301] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [14306] 175XXXXXXX    1830509201    1830509201    1480400101    199XXXXXXX053
## [14311] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
## [14316] 32105XXXXX036 32105XXXXX036 1090101001    1090101001    1760800309   
## [14321] 1750101001    1750101001    1750101001    1750101001    1830301701   
## [14326] 1830301701    1830301701    17037457XX    2314300102    2314300102   
## [14331] 1704149903    1830305701    3070800101    1480400803    1480400803   
## [14336] 1703903303    1703903303    1100400125    1480403401    1830205003   
## [14341] 1830201102    1830201102    17102001XX    17102001XX    17063XXXXX   
## [14346] 17063XXXXX    1700505801    1700505801    1700505801    1700505801   
## [14351] 1700505801    1700505801    1709201904    1709243002    1750102610   
## [14356] 1750102610    1750102610    1750102610    1750102610    1750102610   
## [14361] 1750102610    1750102610    1750102610    1750102610    1750102610   
## [14366] 1702304806    1830202404    1750102605    1750102612    1750300507   
## [14371] 1750300505    1080200401    17023XXXXX    121XXXXXXX020 32102XXXXX026
## [14376] 199XXXXXXX012 17501023XX018 10803XXXXX    1750101504    1750300402   
## [14381] 1750102406    1750102603    17501XXXXX    299XXXXXXX013 199XXXXXXX010
## [14386] 399XXXXXXX016 17503XXXXX    1750101503    1080201011    14102XXXXX   
## [14391] 694XXXXXXX    199XXXXXXX054 1060800201    1080201017    1750102501   
## [14396] 1750101505    1750300903    1750400301    10606006XX    1750101001   
## [14401] 1750102610    1750102605    1830201401    1950100103    2294200701   
## [14406] 3160801404    1750102601    1480400202    1830200201    1210500105   
## [14411] 1750100205    17801001XX    1230100401    1750102612    3161000105   
## [14416] 1080200401    1230400201    199XXXXXXX009 1830200501    1480401001   
## [14421] 3160803603    1782000301    399XXXXXXX016 2280400203    3210501001   
## [14426] 30701001XX    1090100704    1060800301    2312114501    11004001XX   
## [14431] 1480600401    1480401501    69302004XX    1060800201    1480500404   
## [14436] 1750400301    3070800101    1480400803    1830201102    17102001XX   
## [14441] 1830202404    199XXXXXXX010 1750101503    199XXXXXXX054 199XXXXXXX010
## [14446] 1750101503    199XXXXXXX054 1750102605    1760301102    2280102201   
## [14451] 17710001XX    1080200401    1702021301    17023XXXXX    17037XXXXX   
## [14456] 17002042XX    17036XXXXX    1750600302    231XXXXXXX    199XXXXXXX010
## [14461] 16501XXXXX    22801001XX    14102XXXXX    17501015XX    199XXXXXXX054
## [14466] 1750102501    17032XXXXX    17001025XX    2280100133    1290200401   
## [14471] 1703402901    1750101001    2281200302    1750102610    199XXXXXXX010
## [14476] 1830201401    1950100101    12305015XX    1750102601    1480400202   
## [14481] 1830200201    1210500105    1702300401    1750100205    17801001XX   
## [14486] 1230100401    1710200101    1480400502    3161000105    1480403301   
## [14491] 1830506401    1230400201    12301010XX    1830202405    3162300203   
## [14496] 1830300701    32102XXXXX026 14002XXXXX    2310901006    3160700205   
## [14501] 1830204802    1480500401    2294200718    1210506401    1830200405   
## [14506] 1230400301    1210506601    1231200102    199XXXXXXX009 183XXXXXXX   
## [14511] 1400200102    148XXXXXXX    1470100101    1480400601    1721201002   
## [14516] 1780207001    1480401001    1830204504    1480400501    1782000301   
## [14521] 299XXXXXXX013 399XXXXXXX016 1830500301    2280400203    2294200602   
## [14526] 1480403201    22804002XX    1090100704    1480401502    1060800301   
## [14531] 1230100909    11004001XX    1400201801    1480600401    1480401501   
## [14536] 123XXXXXXX    17204002XX    1230100402    199XXXXXXX054 3161202006   
## [14541] 1500100101    1830509201    1480400101    32105XXXXX036 1231200101   
## [14546] 1480403401    1830201102    1750102605    1750102601    1702300401   
## [14551] 1750100205    17710001XX    1703926101    199XXXXXXX012 1480500401   
## [14556] 17501023XX018 1703923508    1702304801    1901000201    17002042XX   
## [14561] 17802XXXXX    17023044XX    1750102401    13116XXXXX    299XXXXXXX013
## [14566] 199XXXXXXX010 399XXXXXXX016 16501XXXXX    17039008XX    17039191XX   
## [14571] 11004001XX    1703927702    12105012XX    17501002XX    17801XXXXX   
## [14576] 199XXXXXXX054 1750102501    17407001XX    17041007XX    1750400301   
## [14581] 1703903303    30703001XX    1480401601    1750102605    1750102605   
## [14586] 1750102605    1750102605    1750102605    1750102605    1750102605   
## [14591] 1750102605    1750102605    1750102605    1750102605    1750102605   
## [14596] 1750102605    1750102605    3210501003    1750102601    1750102601   
## [14601] 1750102601    1750102601    1750102601    1750102601    1750300404   
## [14606] 1750300404    1750300404    1750300404    1750300404    1750300404   
## [14611] 1750300904    1750300904    1750300904    1750300904    1750300904   
## [14616] 1750300904    17710001XX    1700116701    1750102612    1750102612   
## [14621] 1750102612    1750102612    1750102612    1750102612    1750102612   
## [14626] 1750102612    1750102612    1750102612    1750102612    1750102612   
## [14631] 1750102612    1750300507    1750300507    1750300507    1750300507   
## [14636] 1750300507    1750300507    1750300507    1750300507    1750300507   
## [14641] 1702309901    1703933004    1703755301    3160407101    1750300505   
## [14646] 1750300505    1750300505    1750300505    1750300505    1750300505   
## [14651] 1750300505    1750300505    1750300505    1750300505    1750300505   
## [14656] 1750300505    1750300505    1080200401    1080200401    1080200401   
## [14661] 1080200401    1080200401    1080200401    2311100401    1780200301   
## [14666] 1703202716    17603XXXXX    321XXXXXXX    1210505803    1750100201   
## [14671] 316XXXXXXX    121XXXXXXX020 1702222101    1702807101    32104001XX   
## [14676] 32104001XX    32104001XX    32104001XX    17037XXXXX    32102XXXXX026
## [14681] 1430901102    1211100201    19009004XX    183XXXXXXX    1650100102   
## [14686] 14704XXXXX    1707700201    17501023XX018 17501023XX018 307XXXXXXX   
## [14691] 2280100112    17041251XX    1703318405    1702304801    1311606801   
## [14696] 17002042XX    1702304308    1750101504    1750300402    1750300402   
## [14701] 1750300402    1750300402    1750300402    1750300402    1750300402   
## [14706] 2311114001    17023044XX    1750101512    1210600202    3161102002   
## [14711] 2291500104    3210505803    3161101701    1702300403    1702304307   
## [14716] 1080402901    3210502301    1750102406    1750102406    2280100109   
## [14721] 1750600302    2290100101    1750102603    1750102603    1750102603   
## [14726] 1750102603    1750102603    1750102603    231XXXXXXX    199XXXXXXX010
## [14731] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [14736] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [14741] 199XXXXXXX010 399XXXXXXX016 17503XXXXX    17503XXXXX    17503XXXXX   
## [14746] 17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX    17503XXXXX   
## [14751] 17503XXXXX    22801016XX    1703702801    1220200101    1702632701   
## [14756] 1400202502    1750101503    228XXXXXXX    1900800201    1080201011   
## [14761] 1080201011    32109XXXXX    1750500701    1750102602    1750102602   
## [14766] 1750102602    1750102602    3160700801    1760802001    1470200701   
## [14771] 17065XXXXX    17039XXXXX    110XXXXXXX    1701102605    1210503101   
## [14776] 2280100130    17023043XX    14102XXXXX    694XXXXXXX    69302004XX   
## [14781] 17501015XX    3210506001    199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [14786] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [14791] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [14796] 199XXXXXXX054 199XXXXXXX054 1060800201    1060800201    1060800201   
## [14801] 1060800201    1060800201    1060800201    1060800201    1060800201   
## [14806] 1080201017    1080201017    1080201017    1080201017    1080201017   
## [14811] 1080201017    1080201017    17015XXXXX    1703756101    1760300901   
## [14816] 1703919115    1210504901    1750102501    1750102501    1750102501   
## [14821] 1750102501    1750102501    1750102501    1750102501    1750102501   
## [14826] 1750102501    1750102501    1750102501    1750102501    1750102501   
## [14831] 17032XXXXX    1750102608    1750102608    1750102608    1750102608   
## [14836] 1750102608    2280104302    1750300903    1750300903    1750300903   
## [14841] 1750300903    1750300903    1750300903    1750300903    1750400301   
## [14846] 1750400301    1750400301    1750400301    1750400301    1750400301   
## [14851] 1750400301    1750400301    1750400301    1750400301    1750400301   
## [14856] 1750400301    1750400301    1750400301    1750400301    17016XXXXX   
## [14861] 1702317901    1703817217    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [14866] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [14871] 175XXXXXXX    175XXXXXXX    1703202742    1750101001    1750101001   
## [14876] 3210505901    1703730305    1750102610    1750102610    1750102610   
## [14881] 1750102610    1750102610    1750102610    1750102610    1750102610   
## [14886] 1750102610    1750102610    1750102610    1750102610    1750102610   
## [14891] 3160806607    1750102605    17023048XX    17710001XX    1750102612   
## [14896] 1750300507    1750300505    1080200401    17023XXXXX    1702222101   
## [14901] 17038XXXXX    17501023XX018 17000XXXXX    17041XXXXX    17002042XX   
## [14906] 14703004XX    1830700101    1750101403    3210400111    1750300402   
## [14911] 1750102406    199XXXXXXX010 17503XXXXX    16501XXXXX    1080201011   
## [14916] 32109XXXXX    2290100106    22801001XX    170XXXXXXX    110XXXXXXX   
## [14921] 12105012XX    14102XXXXX    694XXXXXXX    17501015XX    199XXXXXXX054
## [14926] 1750300905    1060800201    1080201017    1750102501    1704603612   
## [14931] 17407001XX    1750300903    17402XXXXX    1750400301    17033184XX   
## [14936] 175XXXXXXX    1211100202    12111002XX    17063XXXXX    1750102610   
## [14941] 1750102605    1750102605    12106XXXXX    12106XXXXX    699XXXXXXX   
## [14946] 699XXXXXXX    2280100103    2280100103    17710001XX    17710001XX   
## [14951] 1700116701    1700116701    1702329101    1702329101    1750102612   
## [14956] 1750102612    17011026XX    17011026XX    3210400702    3210400702   
## [14961] 1750300507    1750300507    1702309901    1702309901    1702342501   
## [14966] 1702342501    3160407101    3160407101    1750300505    1750300505   
## [14971] 2311100401    2311100401    17603XXXXX    17023XXXXX    17023XXXXX   
## [14976] 32104001XX    32104001XX    17037XXXXX    17037XXXXX    31607008XX   
## [14981] 31607008XX    32102XXXXX026 32102XXXXX026 1430901102    1430901102   
## [14986] 1211100201    1211100201    14106064XX    14106064XX    1701916502   
## [14991] 1701916502    2291500501    2291500501    17501023XX018 17501023XX018
## [14996] 2280100112    2280100112    3161003202    3161003202    2280100120   
## [15001] 2280100120    17002XXXXX    17002XXXXX    31610028XX    31610028XX   
## [15006] 1830700101    1830700101    1750101403    1750101403    17501014XX   
## [15011] 17501014XX    1702304308    1702304308    1750300402    1750300402   
## [15016] 2311114001    2311114001    61841007XX    61841007XX    1750102406   
## [15021] 1750102406    1750600302    1750600302    13116XXXXX    13116XXXXX   
## [15026] 1750102603    1750102603    231XXXXXXX    231XXXXXXX    199XXXXXXX010
## [15031] 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 22801016XX    22801016XX   
## [15036] 17033230XX    17033230XX    16501XXXXX    16501XXXXX    32109XXXXX   
## [15041] 32109XXXXX    22801001XX    22801001XX    110XXXXXXX    110XXXXXXX   
## [15046] 12105012XX    12105012XX    31608XXXXX    31608XXXXX    14102XXXXX   
## [15051] 14102XXXXX    17501015XX    17501015XX    22807XXXXX    22807XXXXX   
## [15056] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 31611041XX    31611041XX   
## [15061] 1750300905    17015XXXXX    17015XXXXX    1760300901    1760300901   
## [15066] 1750102501    1750102501    17032XXXXX    17032XXXXX    1750102608   
## [15071] 1750102608    225XXXXXXX    225XXXXXXX    1750300903    1750300903   
## [15076] 1750400301    1750400301    17033184XX    17033184XX    17077XXXXX   
## [15081] 17077XXXXX    18304XXXXX    18304XXXXX    1702317901    1702317901   
## [15086] 175XXXXXXX    2280100128    2280100128    1750102610    1750102610   
## [15091] 321XXXXXXX    231XXXXXXX    199XXXXXXX010 228XXXXXXX    22901001XX   
## [15096] 175XXXXXXX    1750102610    1703210102    1702304605    1705013202   
## [15101] 1750102605    1703906010    1750102601    1750100101    1702326801   
## [15106] 1703817204    1750300404    17710001XX    1703626303    1750102612   
## [15111] 1703906302    1750300505    1703745705    1703926101    17023XXXXX   
## [15116] 1703745702    1750100201    121XXXXXXX020 1702807101    1703906011   
## [15121] 1702304429    32102XXXXX026 17039060XX    1210600201    1431300101   
## [15126] 14704XXXXX    17501023XX018 1707700109    17002042XX    14703004XX   
## [15131] 10803XXXXX    17023004XX    1703906002    1750600302    1707700302   
## [15136] 1750102401    17501XXXXX    1210501217    231XXXXXXX    299XXXXXXX013
## [15141] 199XXXXXXX010 399XXXXXXX016 17503XXXXX    16501XXXXX    14701XXXXX   
## [15146] 17039008XX    17039191XX    22801001XX    17039XXXXX    1702313401   
## [15151] 110XXXXXXX    1703900807    1210501210    14102XXXXX    199XXXXXXX054
## [15156] 1703707001    1060800201    1080201017    1750102501    17032027XX   
## [15161] 18303XXXXX    1703620919    17405XXXXX    1830700102    1750400301   
## [15166] 17077XXXXX    19010XXXXX    22901001XX    175XXXXXXX    1750101511   
## [15171] 17037457XX    1704149903    1211200112    1290100304    1750102610   
## [15176] 17710001XX    1750102612    14704XXXXX    199XXXXXXX010 1702313401   
## [15181] 199XXXXXXX054 1750102501    175XXXXXXX    1750101001    1750102610   
## [15186] 1750102605    1750102612    1750300507    1750300505    299XXXXXXX013
## [15191] 199XXXXXXX010 399XXXXXXX016 694XXXXXXX    1750102501    17032XXXXX   
## [15196] 1750300903    1750400301    175XXXXXXX    1750102610    1750102605   
## [15201] 1750100101    1750300404    2280102201    1750300904    1750102612   
## [15206] 1750102604    1080201003    1750300505    1080200401    1080201018   
## [15211] 2290100108    121XXXXXXX020 199XXXXXXX012 17501023XX018 10803XXXXX   
## [15216] 17023044XX    1750101506    1750300906    1060800203    10608002XX   
## [15221] 199XXXXXXX010 17503XXXXX    1070300901    22801001XX    23111004XX   
## [15226] 1750101515    199XXXXXXX054 1060800201    1750102501    10804007XX   
## [15231] 30706002XX    1750400301    10606006XX    1080201703    175XXXXXXX   
## [15236] 32105XXXXX036 1750101001    1750102610    1750102605    1090300401   
## [15241] 1750102601    1750100101    17710001XX    1080100104    1704007501   
## [15246] 2280203101    1702021301    1703926101    1703700921    2280100117   
## [15251] 10801003XX    321XXXXXXX    1750100201    3210200202    1703906006   
## [15256] 1702807101    3210900507    1703900802    3070100101    1830300701   
## [15261] 32104001XX    17037XXXXX    2280101701    10901XXXXX    1210600201   
## [15266] 1431300101    3160700205    1480500401    2294200718    1210506401   
## [15271] 183XXXXXXX    1650100102    17501023XX018 1470100101    1703923508   
## [15276] 1702304801    1480400601    1721201002    1901000201    3161102001   
## [15281] 17002042XX    17002XXXXX    17802XXXXX    32109024XX    17023004XX   
## [15286] 1620100101    1702307202    1750102401    1090100701    299XXXXXXX013
## [15291] 199XXXXXXX010 399XXXXXXX016 1703710601    3161000112    2311109002   
## [15296] 19501001XX    16501XXXXX    2294200602    22901008XX    17040075XX   
## [15301] 1750100601    17039XXXXX    110XXXXXXX    1704100702    1703919103   
## [15306] 1703907601    1703929301    1703927702    12105012XX    17039033XX   
## [15311] 17801XXXXX    17006345XX    12105011XX    1703707001    1750600601   
## [15316] 16302XXXXX    10804007XX    2280101601    1704100701    17041007XX   
## [15321] 1750400301    175XXXXXXX    1830509201    1750102605    10903XXXXX   
## [15326] 1750102601    1750100101    1702300401    1750100205    17710001XX   
## [15331] 1703906302    1480403301    1702021301    1703926101    1703700921   
## [15336] 2280100117    1750100201    3210200202    1703906006    3210900507   
## [15341] 1830300701    2290100804    32104001XX    2280101701    1700204201   
## [15346] 1210600201    1431300101    3160700205    1830204802    1480500401   
## [15351] 2294200718    1210506401    1210506601    183XXXXXXX    17501023XX018
## [15356] 1470100101    1703923508    17321XXXXX023 3160800311    1480400601   
## [15361] 17002042XX    17002XXXXX    17802XXXXX    61841007XX    1620100101   
## [15366] 1703906002    1702307202    1750102401    13116XXXXX    231XXXXXXX   
## [15371] 199XXXXXXX010 399XXXXXXX016 1703710601    1702300408    3161000112   
## [15376] 19501001XX    16501XXXXX    228XXXXXXX    2294200602    17040075XX   
## [15381] 17039XXXXX    110XXXXXXX    1704100702    1703919103    1703907601   
## [15386] 1703929301    17039033XX    17801XXXXX    17006345XX    12105011XX   
## [15391] 1703707001    16302XXXXX    10804007XX    3161100105    1704100701   
## [15396] 1750400301    1830509201    31611XXXXX    1480403401    1750300505   
## [15401] 2290100108    199XXXXXXX010 17503XXXXX    30706002XX    1750102610   
## [15406] 1750102605    1750102612    1750300507    1750300505    199XXXXXXX010
## [15411] 1750102501    1750300903    1750400301    175XXXXXXX    1750102610   
## [15416] 1470300406    17710001XX    1750102604    19001XXXXX    17002040XX   
## [15421] 17023XXXXX    2290100108    121XXXXXXX020 1702807101    17041XXXXX   
## [15426] 17002042XX    17036XXXXX    1706316401    1750102401    199XXXXXXX010
## [15431] 399XXXXXXX016 14701XXXXX    17065XXXXX    17039XXXXX    17501015XX   
## [15436] 1750102501    17032XXXXX    16111XXXXX    30706002XX    17402XXXXX   
## [15441] 19010XXXXX    175XXXXXXX    1750101001    1750102610    1709243004   
## [15446] 13111008XX    1709446602    1702304605    1480401601    16102003XX   
## [15451] 16102003XX    16102003XX    16102003XX    17023048XX    1830201401   
## [15456] 1709253501    1100400132    1709201501    699XXXXXXX    1210600206   
## [15461] 1480500406    12305015XX    1750100101    1702326801    1702326801   
## [15466] 1210500105    1702300401    1750100205    1702700301    1702700301   
## [15471] 17801001XX    17801001XX    1210501309    1702905102    2281201801   
## [15476] 1510402101    17710001XX    17710001XX    1060100301    1780100112   
## [15481] 1480500408    1630200301    1480600106    1090101401    1210505901   
## [15486] 1709637301    1620400701    1709441601    1480203001    1480203001   
## [15491] 1760300401    1760300401    1480501702    1750100207    1750300505   
## [15496] 1480403301    1780200301    1702021301    1702021301    1702021301   
## [15501] 1702021301    1620300201    1300100501    17030XXXXX    17030XXXXX   
## [15506] 17030XXXXX    1480400801    17603XXXXX    1703001001    14805004XX034
## [15511] 1702300413    1230400201    1620100801    17023XXXXX    17096373XX   
## [15516] 1702300405    1750100201    1750100201    1750100201    1750100201   
## [15521] 121XXXXXXX020 121XXXXXXX020 1702222101    1400200201    1480201001   
## [15526] 1100500326    1760801002    17037XXXXX    17094XXXXX    1702300414   
## [15531] 32102XXXXX026 32102XXXXX026 1170100102    15204002XX    2280101701   
## [15536] 17039060XX    1100400201    17038XXXXX    1210600201    1210600201   
## [15541] 1830204802    1210506401    1210506601    199XXXXXXX009 199XXXXXXX009
## [15546] 14804006XX    1400200102    17501023XX018 17506002XX    148XXXXXXX   
## [15551] 148XXXXXXX    1470100101    1120300101    17041XXXXX    17321XXXXX023
## [15556] 1400201602    32114XXXXX    1702300415    14806001XX    14806XXXXX   
## [15561] 1709201906    17002042XX    17002XXXXX    17036XXXXX    1700505802   
## [15566] 17501014XX    17023004XX    17023004XX    17023044XX    17023044XX   
## [15571] 17023044XX    1620100101    1620100101    1620100101    3210502301   
## [15576] 3210502301    23020XXXXX    1620101102    1090101801    13208XXXXX   
## [15581] 13208XXXXX    1703906002    1703906002    1750600302    1750600302   
## [15586] 1702307202    13116XXXXX    1709244002    1709441701    1709441701   
## [15591] 17501XXXXX    1709201902    1709201902    231XXXXXXX    231XXXXXXX   
## [15596] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [15601] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016
## [15606] 1100400202    1702300408    3161000112    14802XXXXX    14801001XX   
## [15611] 16501XXXXX    16501XXXXX    16501XXXXX    228XXXXXXX    228XXXXXXX   
## [15616] 1620101101    2280400203    32109XXXXX    1520100102    1610500202   
## [15621] 16204XXXXX    17039008XX    1480501701    1709201502    1709201502   
## [15626] 1709201502    1709201502    1709201502    1705700701    1705700701   
## [15631] 1705700701    17040075XX    1090100704    1090100704    1580200101   
## [15636] 1210501102    1060800301    17039XXXXX    17039XXXXX    17039XXXXX   
## [15641] 17039XXXXX    17039XXXXX    11201004XX    110XXXXXXX    110XXXXXXX   
## [15646] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    1480201401   
## [15651] 1704100702    1400201801    1210501210    1480600401    1703028602   
## [15656] 1760800101    17608XXXXX    17608XXXXX    1480401501    1610501301   
## [15661] 12105012XX    12105012XX    12105012XX    17023043XX    1780200803   
## [15666] 17801XXXXX    14102XXXXX    14102XXXXX    694XXXXXXX    30702018XX   
## [15671] 1480500402    12105011XX    199XXXXXXX054 199XXXXXXX054 1060800201   
## [15676] 1400210001    1400204301    1750500901    1750600601    1750600601   
## [15681] 1703919115    1760801004    1750102701    1620400201    17505XXXXX   
## [15686] 17032027XX    17032XXXXX    1750500101    1750500101    1650100128   
## [15691] 1210501303    1709441801    1210501305    1480403302    1480403302   
## [15696] 1480500403    1520100103    1620400102    1080400709    691XXXXXXX   
## [15701] 1170100105    1750100102    1709201910    11701XXXXX    17041007XX   
## [15706] 1750400301    1480204001    1707030504    1100400102    1480603001   
## [15711] 1060600601    1080401103    19010XXXXX    22901001XX    175XXXXXXX   
## [15716] 175XXXXXXX    175XXXXXXX    1830509201    32105XXXXX036 32105XXXXX036
## [15721] 32105XXXXX036 32105XXXXX036 1900901801    1750101001    17608010XX   
## [15726] 3210505901    1750101511    17037457XX    17037457XX    1211200112   
## [15731] 1702301127    1760801005    1480403401    1480600104    17102001XX   
## [15736] 1750102610    1702304806    1830202404    1709446602    1702304605   
## [15741] 1705013202    1705013202    1480401601    1480401601    1750102605   
## [15746] 1210501106    16102003XX    16102003XX    16102003XX    16102003XX   
## [15751] 16102003XX    16102003XX    16102003XX    16102003XX    16102003XX   
## [15756] 16102003XX    1830201401    1830201401    1950100103    12106XXXXX   
## [15761] 12106XXXXX    12106XXXXX    17092XXXXX    17092XXXXX    1709253501   
## [15766] 1709253501    1709253501    1709201501    1210600206    1480500406   
## [15771] 12305015XX    12305015XX    12305015XX    1780701403    1750100101   
## [15776] 1750100101    1750100101    1702326801    1702326801    1760301104   
## [15781] 1480400202    1480400202    1830200201    1830200201    1210500105   
## [15786] 1210500105    1702300401    1750100205    1750100205    1750100205   
## [15791] 1702700301    1702700301    17801001XX    17801001XX    1750300404   
## [15796] 1230100401    1470200201    17802020XX    1210504202    1750300904   
## [15801] 17710001XX    17710001XX    17710001XX    17710001XX    1480500408   
## [15806] 1480500408    1630200301    1703626303    1703626303    1750102612   
## [15811] 1750102612    1210505901    1709441601    1701300701    1760300401   
## [15816] 1760300401    1480501702    1702300402    1750300505    1750300505   
## [15821] 1480403301    1702021301    1702021301    1702021301    1702021301   
## [15826] 1702021301    1709244801    1300100501    17030XXXXX    17030XXXXX   
## [15831] 17030XXXXX    17603XXXXX    17603XXXXX    17603XXXXX    1703001001   
## [15836] 14805004XX034 1702300413    1230400201    1230400201    1230400201   
## [15841] 17023XXXXX    17023XXXXX    17096373XX    1702300405    1230100907   
## [15846] 1750100201    1750100201    1750100201    1750100201    1750100201   
## [15851] 1750100201    1750100201    1750100201    1230100903    121XXXXXXX020
## [15856] 121XXXXXXX020 121XXXXXXX020 121XXXXXXX020 121XXXXXXX020 121XXXXXXX020
## [15861] 1702222101    1230100908    2282300303    2282300303    14313XXXXX   
## [15866] 14313XXXXX    14313XXXXX    17037XXXXX    17037XXXXX    17037XXXXX   
## [15871] 1702300414    1702300414    32102XXXXX026 32102XXXXX026 32102XXXXX026
## [15876] 32102XXXXX026 32102XXXXX026 14002XXXXX    14002XXXXX    14002XXXXX   
## [15881] 1230502901    2280101701    199XXXXXXX012 199XXXXXXX012 199XXXXXXX012
## [15886] 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012
## [15891] 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012 199XXXXXXX012
## [15896] 17039060XX    1950100106    10901XXXXX    1750100104    1711500401   
## [15901] 1320803002    1210600201    1210600201    1210600201    1480500401   
## [15906] 1210506401    1210506401    1830200405    1230400301    1210506601   
## [15911] 1210506601    199XXXXXXX009 199XXXXXXX009 183XXXXXXX    183XXXXXXX   
## [15916] 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
## [15921] 183XXXXXXX    183XXXXXXX    14804006XX    1400200102    1400200102   
## [15926] 17501023XX018 17501023XX018 148XXXXXXX    148XXXXXXX    148XXXXXXX   
## [15931] 148XXXXXXX    148XXXXXXX    148XXXXXXX    17041XXXXX    17041XXXXX   
## [15936] 17321XXXXX023 17321XXXXX023 17321XXXXX023 32114XXXXX    1702300415   
## [15941] 13112XXXXX    1830200501    1830200501    1830200501    1830200501   
## [15946] 1830200501    14806001XX    14806XXXXX    14806XXXXX    1709201906   
## [15951] 1709201906    17002042XX    17002042XX    17002042XX    17002042XX   
## [15956] 17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX    17002XXXXX   
## [15961] 17036XXXXX    17036XXXXX    17036XXXXX    17036XXXXX    17036XXXXX   
## [15966] 17802XXXXX    17802XXXXX    1480401001    1480401001    14805004XX   
## [15971] 1709201903    1709201903    17501014XX    17501014XX    1750300402   
## [15976] 17023004XX    17023004XX    17023004XX    17023004XX    17023044XX   
## [15981] 17023044XX    17023044XX    17023044XX    1702300403    1210501301   
## [15986] 1620100101    1620100101    1620100101    1709400901    1830200802   
## [15991] 1830200802    1580200105    13208XXXXX    13208XXXXX    13208XXXXX   
## [15996] 1703906002    1703906002    1750600302    1750600302    1750600302   
## [16001] 1750600302    1702307202    1480400501    1750102401    1750102401   
## [16006] 13116XXXXX    13116XXXXX    1300100601    1480200601    3210400105   
## [16011] 1510300401    1510300401    1510300401    1709244002    1709441701   
## [16016] 1709441701    1709441701    1709441701    17501XXXXX    17501XXXXX   
## [16021] 17501XXXXX    17501XXXXX    1709201902    1709201902    231XXXXXXX   
## [16026] 231XXXXXXX    299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013
## [16031] 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 299XXXXXXX013 199XXXXXXX010
## [16036] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [16041] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [16046] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [16051] 199XXXXXXX010 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016
## [16056] 399XXXXXXX016 399XXXXXXX016 3161000112    14802XXXXX    16501XXXXX   
## [16061] 16501XXXXX    16501XXXXX    228XXXXXXX    228XXXXXXX    228XXXXXXX   
## [16066] 228XXXXXXX    1480401201    1480500407    2280400203    2280400203   
## [16071] 3210501001    1480403201    1711501202    32109XXXXX    32109XXXXX   
## [16076] 1780701402    1610500202    16204XXXXX    1480400211    1480400211   
## [16081] 1830200202    1830200202    1210500107    1210500107    1702300406   
## [16086] 1702300406    1780100109    1780100109    1720400204    1470200701   
## [16091] 22804002XX    1480501701    1709244001    1709201502    1709201502   
## [16096] 1709201502    1705700701    199XXXXXXX013 199XXXXXXX013 199XXXXXXX013
## [16101] 199XXXXXXX013 1580200101    1230100902    1480401901    1480401901   
## [16106] 1210501102    17035169XX    17039034XX    17039XXXXX    17039XXXXX   
## [16111] 17039XXXXX    17039XXXXX    17039XXXXX    11004001XX    11004001XX   
## [16116] 110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [16121] 110XXXXXXX    1480201401    1480400802    2302001801    2302001801   
## [16126] 14002018XX    1210501210    1210501210    1480600401    1480600401   
## [16131] 1480600401    17608XXXXX    1780800401    1780800401    1480401202   
## [16136] 1480401501    1480401501    123XXXXXXX    123XXXXXXX    17204002XX   
## [16141] 12105012XX    12105012XX    12105012XX    12105012XX    17023043XX   
## [16146] 17023043XX    17023043XX    31608XXXXX    17813012XX    1703935301   
## [16151] 14102XXXXX    14102XXXXX    14102XXXXX    14102XXXXX    1020100101   
## [16156] 31610XXXXX    69302004XX    1480500402    199XXXXXXX054 199XXXXXXX054
## [16161] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054
## [16166] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1950100105   
## [16171] 1400210001    1480500404    1760300901    1750600601    1250203001   
## [16176] 1750102501    1750102501    1705700703    12304XXXXX030 17032027XX   
## [16181] 17032XXXXX    17032XXXXX    17032XXXXX    1750500101    1750500101   
## [16186] 1230100906    1210501303    1709441801    1480500405    18303057XX   
## [16191] 1210501305    1480403302    1480403302    1709448001    1709252901   
## [16196] 1709201910    11701XXXXX    1830804606    17041007XX    1750400301   
## [16201] 1750400301    1750400301    17077XXXXX    17077XXXXX    1500100101   
## [16206] 19010XXXXX    19010XXXXX    22901001XX    22901001XX    22901001XX   
## [16211] 22901001XX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [16216] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [16221] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
## [16226] 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036 32105XXXXX036
## [16231] 32105XXXXX036 32105XXXXX036 32105XXXXX036 17608010XX    1750101511   
## [16236] 17037457XX    17037457XX    1704149903    1480400803    12312001XX   
## [16241] 12312001XX    1480403401    1480403401    1480600104    1830205003   
## [16246] 1830201102    17102001XX    17102001XX    1830202402    1750102610   
## [16251] 1750102610    1830202404    3160806607    17710001XX    1210504001   
## [16256] 2311100401    17023XXXXX    1702222101    1702807101    17038XXXXX   
## [16261] 1470100801    17501023XX018 17041XXXXX    1702315101    17002XXXXX   
## [16266] 17036XXXXX    1703922406    17506XXXXX    14703004XX    1750101403   
## [16271] 1210501204    1750101504    1750102406    1703910501    1750102603   
## [16276] 199XXXXXXX010 17503XXXXX    1220200101    17046036XX    16501XXXXX   
## [16281] 1750101503    1700204257    1702311402    17065XXXXX    3210200229   
## [16286] 1703817215    17035XXXXX    17023231XX    12105012XX    17023043XX   
## [16291] 14102XXXXX    17501015XX    199XXXXXXX054 17032XXXXX    1703930001   
## [16296] 1703817202    17407001XX    12106050XX    17033XXXXX    1702317901   
## [16301] 1703933006    12111002XX    1706600704    1703933005    1702342201   
## [16306] 1709345201    1750102605    1750102605    1750102605    1750102605   
## [16311] 1750102605    1750102605    16102003XX    1830201401    1830201401   
## [16316] 10903XXXXX    1950100101    1831000201    32109001XX    17092XXXXX   
## [16321] 17092XXXXX    1100400132    2302012303    1709201501    1709201501   
## [16326] 699XXXXXXX    1100400168    1480500406    3210501003    12305015XX   
## [16331] 1750102601    1750100101    1480400202    1480400202    1830200201   
## [16336] 1830200201    1210500105    1702300401    1750100205    1702700301   
## [16341] 17801001XX    17801001XX    1750300404    1230100401    1710200101   
## [16346] 1231400701    1750102612    1750102612    1750102612    1750102612   
## [16351] 1750102612    1090101401    1709637301    1750300507    1750300507   
## [16356] 1750300507    1750601201    1703906302    1703906302    1703906302   
## [16361] 1780101703    1950100107    1709441601    1703900801    1100400105   
## [16366] 1480203001    1480203001    1480400502    1480400502    1750300505   
## [16371] 1750300505    3161000105    1080200401    1080200401    1080200401   
## [16376] 1080200401    1080200401    1080200401    1100400101    1480403301   
## [16381] 1702021301    1620300201    1830506401    17603XXXXX    1230400201   
## [16386] 10801XXXXX    10801003XX    1709100301    1750100201    316XXXXXXX   
## [16391] 121XXXXXXX020 1830202405    1702807101    3162300203    2281201810   
## [16396] 2282300303    1830300701    32104001XX    23019XXXXX    17094XXXXX   
## [16401] 17094XXXXX    1100400110    31607008XX    32102XXXXX026 1100400216   
## [16406] 2314300109    10901XXXXX    10901XXXXX    10901XXXXX040 1080103004   
## [16411] 1700204201    2310901006    1750500501    1750500501    1750500501   
## [16416] 1750500501    1210600201    1210600201    1431300101    3160700205   
## [16421] 1830204802    3210505801    1480500401    2294200718    1210506401   
## [16426] 1210506401    1830200405    1700634503    1230400301    1210506601   
## [16431] 199XXXXXXX009 183XXXXXXX    183XXXXXXX    183XXXXXXX    183XXXXXXX   
## [16436] 1830500302    17501023XX018 148XXXXXXX    1470100101    1703923508   
## [16441] 2302012304    3160800309    1090101005    1480400601    3210603301   
## [16446] 1721201002    2311109001    1830200501    1830200501    14806001XX   
## [16451] 14806001XX    14806001XX    1780207001    1709201906    1901000201   
## [16456] 3161102001    199XXXXXXX007 199XXXXXXX007 17036XXXXX    1090100801   
## [16461] 17802XXXXX    1480401001    1480401001    14805004XX    1709201903   
## [16466] 1750300402    1750300402    17023004XX    61841007XX    61841007XX   
## [16471] 1620100101    1100400212    23020018XX    23020XXXXX    23020XXXXX   
## [16476] 1090101801    1090101702    13208XXXXX    1750600302    1090100803   
## [16481] 1702307202    18301XXXXX    1830204504    1480400501    1750102401   
## [16486] 1090101602    1100400111    1709244002    1782000301    1709441701   
## [16491] 1210501217    10608002XX    1709201902    231XXXXXXX    231XXXXXXX   
## [16496] 231XXXXXXX    299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [16501] 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 17503XXXXX   
## [16506] 17503XXXXX    17503XXXXX    1703710601    1830500301    19501001XX   
## [16511] 14802XXXXX    14801001XX    14801001XX    16501XXXXX    16501XXXXX   
## [16516] 228XXXXXXX    1320803201    2280400203    2280400203    3161107501   
## [16521] 2294200602    1480403201    1100400188    1080100302    32109XXXXX   
## [16526] 1750500701    1610500202    3160700801    1709243001    22901008XX   
## [16531] 22901008XX    22804002XX    1709200702    1480501701    1709244001   
## [16536] 3160806702    3210400102    1709201502    1709201502    199XXXXXXX008
## [16541] 30701001XX    1090100704    1709441702    1580200101    1480401502   
## [16546] 17023047XX    1060800301    1060800301    17039XXXXX    1090101601   
## [16551] 23111004XX    1480403203    3160800105    1120100301    11004001XX   
## [16556] 11004001XX    11201004XX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [16561] 1780200403    2302001801    1780100902    2302012302    14804028XX   
## [16566] 1480600103    1100400131    1210501210    1480600401    1090500602   
## [16571] 1480401501    1480401501    3161700601    1830300704    17204002XX   
## [16576] 1100400106    12105012XX    1080300506    1080300506    1080300506   
## [16581] 31608XXXXX    14102XXXXX    14102XXXXX    1230100402    69302004XX   
## [16586] 3210506001    12105011XX    1100400107    199XXXXXXX054 199XXXXXXX054
## [16591] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1060800201   
## [16596] 1060800201    1060800201    1060800201    1060800201    1060800201   
## [16601] 1750600601    1750600601    16302XXXXX    1100400109    1080100301   
## [16606] 1480100101    1080400713    31616003XX    3161202005    1709441801   
## [16611] 1480403302    1750102608    2314300113    2312100501    1780108003   
## [16616] 1100400104    691XXXXXXX    1100400103    1080400715    1120200101   
## [16621] 1709252901    1704100701    2301900206    1750400301    1750400301   
## [16626] 1750400301    1750400301    1750400301    1750400301    1480204001   
## [16631] 1100400102    10606006XX    1080401103    1780200302    175XXXXXXX   
## [16636] 175XXXXXXX    175XXXXXXX    175XXXXXXX    1830509201    1480400101   
## [16641] 1480400101    1100400112    199XXXXXXX053 32105XXXXX036 1090101001   
## [16646] 2311119501    31611XXXXX    1750101001    1750101001    1830301701   
## [16651] 2314300102    3070800101    1100400125    1480403401    1480600104   
## [16656] 1830201102    1830201102    17102001XX    17102001XX    17063XXXXX   
## [16661] 1700505801    1709243002    1750102610    1750102610    1750102610   
## [16666] 1750102610    1702304806    30703001XX    30703001XX    1480401601   
## [16671] 1750102605    1750102605    1750102605    1750102605    1750102605   
## [16676] 1750102605    1750102605    1210501106    1210501106    17023048XX   
## [16681] 17023048XX    17023048XX    1830201401    1950100103    1950100103   
## [16686] 1431300104    3160700803    3160700803    1210501801    1210501801   
## [16691] 1760301102    1760301102    2294200701    3160801404    3160801404   
## [16696] 1210501103    1210501103    1210501103    1210501103    17092XXXXX   
## [16701] 1709253501    2302012303    1709201501    1709201501    1230101005   
## [16706] 1830200801    1830200801    1780701403    3161600502    1750101507   
## [16711] 1750101507    3160803002    3160803002    1750102601    1750102601   
## [16716] 1750102601    1750100101    1750100101    1480400202    1703703804   
## [16721] 1703703804    1701600104    1701600104    1830200201    1210500105   
## [16726] 1750100205    1210502403    1210502403    1702304604    1470101208   
## [16731] 1470101208    19002006XX    17801001XX    2310901003    1750300404   
## [16736] 1230100401    2280102201    17802020XX    1080204001    1080204001   
## [16741] 1630201302    3161202001    1210504202    1210504202    1750300904   
## [16746] 1470300406    1702304815    1702304431    17710001XX    17710001XX   
## [16751] 1760801504    3162300402    18308046XX    1580200502    1702329101   
## [16756] 1702329101    1060600603    1750102612    1750102612    1750102612   
## [16761] 1750102612    1750102612    1750102612    1750102612    17011026XX   
## [16766] 1760801503    1703721002    1703721002    1700204001    1750300507   
## [16771] 1780100132    1700208102    1700208102    1750102404    1750102404   
## [16776] 2311005001    1780101703    1780101703    1709441601    1750102604   
## [16781] 1750102604    1080201009    1080201003    1080201003    3160407116   
## [16786] 3160407116    2311101202    2311101202    1750300505    1750300505   
## [16791] 2294900103    3161000105    1702304426    1702304426    1080200401   
## [16796] 1080200401    1080200401    1210501107    1702021301    1702021301   
## [16801] 1780100110    1780100110    1080300509    2020200101    2020200101   
## [16806] 1080400707    1080201018    1080201018    3161103702    17603XXXXX   
## [16811] 17603XXXXX    17603XXXXX    1781303001    1781303001    3160803001   
## [16816] 1830804603    1830804603    1210501302    1210501302    1706333102   
## [16821] 1210600207    1210600207    1780100115    1780100115    2290100108   
## [16826] 1780100116    1780100116    1230100907    1230100907    1750100201   
## [16831] 1750100201    1750100201    1230100903    316XXXXXXX    316XXXXXXX   
## [16836] 316XXXXXXX    316XXXXXXX    121XXXXXXX020 1702222101    1702222101   
## [16841] 1230100908    1230100908    1702807101    1702807101    1702807101   
## [16846] 1100702402    22823XXXXX    1702304429    1702304429    17094XXXXX   
## [16851] 1706325002    31607008XX    31607008XX    1830205902    1780100147   
## [16856] 1520400203    10901XXXXX    10901XXXXX    10901XXXXX    1830204503   
## [16861] 1830204503    2310901004    2310901004    1080201016    1080400703   
## [16866] 1080400703    1750100104    17038XXXXX    1830200415    1830200415   
## [16871] 1750500501    1750500501    1750500501    1230401201    1080201025   
## [16876] 1080201025    199XXXXXXX009 183XXXXXXX    183XXXXXXX    183XXXXXXX   
## [16881] 183XXXXXXX    1650100102    1650100102    1830201404    1702304703   
## [16886] 1702304703    1830804607    17501023XX018 148XXXXXXX    148XXXXXXX   
## [16891] 148XXXXXXX    1700204004    307XXXXXXX    307XXXXXXX    307XXXXXXX   
## [16896] 22959001XX    1700522002    17041XXXXX    17041XXXXX    2314300114   
## [16901] 1701640002    1701640002    1060800701    1060800701    1702304801   
## [16906] 1702304801    2311109001    1703210001    1170100115    1830200501   
## [16911] 1830200501    14806001XX    14806XXXXX    14806XXXXX    1709201906   
## [16916] 1703202728    1701600102    1701600102    199XXXXXXX007 17002042XX   
## [16921] 17002XXXXX    17002XXXXX    17002XXXXX    17036XXXXX    1703703908   
## [16926] 1210502404    1480401001    10303XXXXX    10303XXXXX    10303XXXXX   
## [16931] 14703004XX    10803XXXXX    1210501108    1210501108    1706316401   
## [16936] 6560100102    6560100102    1709201903    3160803603    1750300402   
## [16941] 17023044XX    17023044XX    61841007XX    61841007XX    2310901007   
## [16946] 3210502301    1750102406    1780702902    23020018XX    23020018XX   
## [16951] 1750101506    1750101506    1290100302    1290100302    1703202733   
## [16956] 13208XXXXX    1750600302    1750600302    1080202701    1080202701   
## [16961] 1702304811    1780700501    1780700501    1100400160    1750102401   
## [16966] 1750102401    1750102401    1060800203    1060800203    3210400105   
## [16971] 3210400105    1702304814    1702304610    1709441701    10608002XX   
## [16976] 10608002XX    1709201902    231XXXXXXX    231XXXXXXX    231XXXXXXX   
## [16981] 231XXXXXXX    199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [16986] 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 399XXXXXXX016 649XXXXXXX   
## [16991] 17503XXXXX    17503XXXXX    17046036XX    16501XXXXX    16501XXXXX   
## [16996] 16501XXXXX    1703202717    228XXXXXXX    228XXXXXXX    228XXXXXXX   
## [17001] 1480500407    1480500407    2280100101    2280100101    1703703907   
## [17006] 2280100105    2280100105    2280400203    1900200612    3161107501   
## [17011] 3161107501    1703202725    3210501001    3210501001    2280100122   
## [17016] 2280100122    1070300901    1711501202    3160904501    2280400204   
## [17021] 2280400204    1701600103    1709446601    32109XXXXX    32109XXXXX   
## [17026] 32109XXXXX    32109XXXXX    1480500412    1750500701    1750500701   
## [17031] 3160701102    1520100102    1520100102    1520100102    3210400103   
## [17036] 3210400103    1704700303    1750102602    1750102602    1750102602   
## [17041] 1480400211    3160700801    3160700801    3161808901    1830200202   
## [17046] 1830200202    1210500107    1210500107    31612005XX    1702300406   
## [17051] 1702300406    3161105502    1780100109    1780100109    1760301105   
## [17056] 3161600701    2310901008    2310901008    2282802806    12301009XX   
## [17061] 1830204901    1830204901    1830800902    1480401301    1480401301   
## [17066] 17065XXXXX    1709244001    1709201502    1709201502    30701001XX   
## [17071] 1830201001    1830201001    1090100704    1090100704    1090100704   
## [17076] 1090100704    1703603201    1703603201    1703936701    1230100902   
## [17081] 1230100902    17027XXXXX    1060800301    17039XXXXX    1702313401   
## [17086] 1230400303    11004001XX    110XXXXXXX    110XXXXXXX    110XXXXXXX   
## [17091] 110XXXXXXX    2314300112    2314300112    1703741101    1703741101   
## [17096] 1700204228    1480400802    1700204225    1703919103    1703919103   
## [17101] 1210503101    2280100119    1830201103    1830201103    3210603305   
## [17106] 1700204221    2282802801    2282802801    1830204301    1830204301   
## [17111] 1702300411    1210501210    1210501210    2282900603    2282900603   
## [17116] 1780800401    1780800401    1480401501    3161700601    3161700601   
## [17121] 1060200501    1701735702    1701735702    1703701605    1703701605   
## [17126] 1080201001    1080201001    17204002XX    17023043XX    17023043XX   
## [17131] 1080300506    31608XXXXX    1700204006    17801XXXXX    17801XXXXX   
## [17136] 17813XXXXX    17813XXXXX    17813XXXXX    1703935301    14102XXXXX   
## [17141] 17047XXXXX    694XXXXXXX    694XXXXXXX    694XXXXXXX    31610XXXXX   
## [17146] 31610XXXXX    31610XXXXX    69302004XX    69302004XX    69302004XX   
## [17151] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1703910201   
## [17156] 1703910201    1060800201    1060800201    1060800201    1060800201   
## [17161] 1780107901    1703202734    1080201017    1480500404    1480500404   
## [17166] 16302XXXXX    1620100401    1750102501    1750102501    1750102501   
## [17171] 1750102501    1750102501    1750102501    1750102501    1750102501   
## [17176] 1750102501    22915XXXXX    12304XXXXX030 12304XXXXX030 1080300501   
## [17181] 17032027XX    17032XXXXX    17032XXXXX    1700204230    1230100906   
## [17186] 1709441801    17405XXXXX    17405XXXXX    1700204223    1080201021   
## [17191] 1080201021    1709448001    1780100122    1703736301    1703736301   
## [17196] 2280400202    1120100401    1120100401    1703701609    1703701609   
## [17201] 1703701614    1703701614    16111XXXXX    691XXXXXXX    691XXXXXXX   
## [17206] 1830204804    3161202002    225XXXXXXX    1700600602    1700600602   
## [17211] 1700600602    1750300903    11701XXXXX    1830804606    1830804606   
## [17216] 17402XXXXX    1750400301    1750400301    1750400301    1750400301   
## [17221] 23121145XX    1706324301    1060600601    1060600601    1060600601   
## [17226] 1060600601    10606006XX    10606006XX    1080201703    1080201703   
## [17231] 17016XXXXX    19301XXXXX    1080401103    1080401103    17092448XX   
## [17236] 19010XXXXX    19010XXXXX    19010XXXXX    1703402901    22901001XX   
## [17241] 175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX    175XXXXXXX   
## [17246] 175XXXXXXX    1480400101    32105XXXXX036 32105XXXXX036 32105XXXXX036
## [17251] 32105XXXXX036 1703222501    1750101001    1750101001    1750101001   
## [17256] 1700204236    3160806601    30709003XX    1703714701    1703714701   
## [17261] 1480400803    1480400803    1703603001    1650100121    1700600603   
## [17266] 1700600603    1170100109    1703710803    1780100103    1780100103   
## [17271] 1830506402    1830205003    1830205003    1830201102    17102001XX   
## [17276] 1700505801    1709201904    1700204224    1700204009    1709243002   
## [17281] 1830202402    1750102610    1750102610    1750102610    1750102610   
## [17286] 1750102610    1750102610    1750102610    1750102610    1702304806   
## [17291] 1830202404    1780100104    1780100104    1703202801    1100400118   
## [17296] 1750102605    1750102605    3074200701    17092XXXXX    17092XXXXX   
## [17301] 1100400132    1709201501    1709201501    699XXXXXXX    1210600206   
## [17306] 1090300404    1431300102    1703707003    1480500406    1210502402   
## [17311] 2282900601    1700225901    3210501003    1720900602    1750102601   
## [17316] 1750100101    1750300904    18308046XX    11004002XX    11004002XX   
## [17321] 1750102612    1750102612    1703721002    1780101703    1780101703   
## [17326] 1480203001    1480203001    1750300505    1750300505    1080200401   
## [17331] 1080200401    1080200401    1702021301    1760801502    1480400801   
## [17336] 1720820201    1707027002    1100100509    1750100201    316XXXXXXX   
## [17341] 1702807101    1702807101    17094XXXXX    17094XXXXX    199XXXXXXX012
## [17346] 10901XXXXX    31615002XX    1750500501    1750500501    1750500501   
## [17351] 14806001XX    14806001XX    14806001XX    14806001XX    10803XXXXX   
## [17356] 3072300201    23020070XX    1703709601    17037039XX    1750600302   
## [17361] 299XXXXXXX013 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010 199XXXXXXX010
## [17366] 399XXXXXXX016 1210602003    17503XXXXX    17503XXXXX    14801001XX   
## [17371] 16501XXXXX    1080400712    1520100102    1702328301    1480501701   
## [17376] 3160806702    1709201502    1709201502    1709201502    1709201502   
## [17381] 1709201502    1709201502    1709201502    199XXXXXXX013 1580200101   
## [17386] 1120300102    1060800301    11004XXXXX    110XXXXXXX    110XXXXXXX   
## [17391] 110XXXXXXX    110XXXXXXX    1703919103    2302012302    10802XXXXX   
## [17396] 3161000108    3161102104    1060200501    2280100132    14102XXXXX   
## [17401] 199XXXXXXX054 199XXXXXXX054 199XXXXXXX054 1060800201    1060800201   
## [17406] 1060800201    1703903301    1480403302    1750102608    2302007001   
## [17411] 2314300113    1703701617    2302007002    1750400301    1750400301   
## [17416] 1750400301    1060600601    17016XXXXX    1080401103    175XXXXXXX   
## [17421] 175XXXXXXX    1703703802    1700505801    1750102610    1750102610   
## [17426] 1750102605    1750102605    1750102605    1750102605    1750102605   
## [17431] 3210501003    1750102612    1750102612    1750102612    1750102612   
## [17436] 1750102612    1750102612    1750102612    1750300507    1750300507   
## [17441] 1750102404    1750102404    1750300505    1750300505    1750300505   
## [17446] 1750300505    1080200401    1080200401    1080200401    1702300405   
## [17451] 1750100201    1750100201    17037XXXXX    1702300414    32102XXXXX026
## [17456] 14805004XX    1750600302    231XXXXXXX    299XXXXXXX013 199XXXXXXX010
## [17461] 199XXXXXXX010 199XXXXXXX010 399XXXXXXX016 228XXXXXXX    32109XXXXX   
## [17466] 22801001XX    17039XXXXX    12105012XX    694XXXXXXX    199XXXXXXX054
## [17471] 199XXXXXXX054 199XXXXXXX054 1060800201    1750102501    1750102501   
## [17476] 1750102501    1750102608    1750300903    1750400301    1750400301   
## [17481] 1750400301    1750400301    1750400301    175XXXXXXX    175XXXXXXX   
## [17486] 175XXXXXXX    175XXXXXXX    175XXXXXXX    32105XXXXX036 1750102610   
## [17491] 1750102610    1750102610    1750102610    1750102610    1750102610   
## [17496] 1750102610    1750102605    17023048XX    31604001XX    1210601501   
## [17501] 1750100101    1480400202    1702304604    1750300404    1210504202   
## [17506] 1750300904    17710001XX    1702329101    1750102612    1750102612   
## [17511] 1750102612    1750102404    1750102404    1750102604    2311101202   
## [17516] 1750300505    1080200401    1702021301    17023XXXXX    2290100108   
## [17521] 1750100201    1702807101    1702807101    1700102510    32104001XX   
## [17526] 199XXXXXXX012 1750100104    183XXXXXXX    1650100102    17501023XX018
## [17531] 17002042XX    17002XXXXX    17036XXXXX    17603011XX    17023044XX   
## [17536] 1750101506    1750600302    1650100112    1750102401    1750300906   
## [17541] 3160700802    231XXXXXXX    199XXXXXXX010 399XXXXXXX016 17503XXXXX   
## [17546] 17046XXXXX    32109XXXXX    199XXXXXXX013 22801001XX    17023047XX   
## [17551] 17039XXXXX    110XXXXXXX    10802XXXXX    1210501210    1080300506   
## [17556] 14102XXXXX    1750101515    199XXXXXXX054 1060800201    1750102501   
## [17561] 1750102501    1750102501    17032XXXXX    3161003201    30706002XX   
## [17566] 1750400301    175XXXXXXX    175XXXXXXX    31611XXXXX    1750101001   
## [17571] 17037016XX    1703703802    1750102610    1750102610    1750102610   
## [17576] 1703202801    1750102605    1750102612    1750300507    1750300505   
## [17581] 321XXXXXXX    229XXXXXXX    231XXXXXXX    199XXXXXXX010 399XXXXXXX016
## [17586] 228XXXXXXX    1750102501    1750400301    175XXXXXXX    1750102610   
## [17591] 231XXXXXXX    199XXXXXXX010 32109XXXXX    694XXXXXXX    22901001XX   
## [17596] 299XXXXXXX013 199XXXXXXX010 399XXXXXXX016 2290119701    17710001XX   
## [17601] 17012XXXXX    121XXXXXXX020 1702222101    32102XXXXX026 199XXXXXXX012
## [17606] 17038XXXXX    17501023XX018 17000XXXXX    17002XXXXX    17036XXXXX   
## [17611] 1830700101    1750101403    1210501204    1750101504    1750300402   
## [17616] 17023004XX    17023044XX    1750102406    1750102603    231XXXXXXX   
## [17621] 399XXXXXXX016 16501XXXXX    1750101503    32109XXXXX    199XXXXXXX013
## [17626] 22801001XX    110XXXXXXX    2290100113    14102XXXXX    694XXXXXXX   
## [17631] 199XXXXXXX054 1750102501    17032XXXXX    1750400301    17033XXXXX   
## [17636] 175XXXXXXX    1750102610    1750102601    1750100101    1703906302   
## [17641] 1703926101    1703906006    3210900507    32104001XX    32102XXXXX026
## [17646] 10901XXXXX    1210600201    1431300101    1480500401    2294200718   
## [17651] 1210506401    1700634503    183XXXXXXX    1650100102    17501023XX018
## [17656] 1470100101    1703923508    1702304801    1750102401    199XXXXXXX010
## [17661] 399XXXXXXX016 1702300408    2294200602    17040075XX    110XXXXXXX   
## [17666] 1210501210    1703907601    1703929301    17501002XX    17801XXXXX   
## [17671] 16302XXXXX    2312100501    1704100701    12106XXXXX    17710001XX   
## [17676] 17023XXXXX    121XXXXXXX020 17038XXXXX    17041XXXXX    17002XXXXX   
## [17681] 199XXXXXXX010 399XXXXXXX016 17503XXXXX    16501XXXXX    17065XXXXX   
## [17686] 12105012XX    17501015XX    199XXXXXXX054 17032XXXXX    17407001XX   
## [17691] 22901001XX    175XXXXXXX   
## 1553 Levels: 1020100101 1020100201 10201XXXXX 1030300603 ... 699XXXXXXX
```

```r
as.factor(fisheries$fao_major_fishing_area)
```

```
##     [1] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##    [25] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##    [49] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##    [73] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##    [97] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##   [121] 37 37 37 37 37 37 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77
##   [145] 77 77 77 77 77 77 77 77 77 77 77 77 77 77 47 47 47 47 47 47 47 47 47 47
##   [169] 47 47 47 47 47 34 47 47 47 34 47 34 47 47 47 47 47 47 47 34 47 34 47 47
##   [193] 34 47 34 34 47 47 47 47 47 34 47 34 34 47 34 47 34 47 47 47 47 47 47 47
##   [217] 34 47 47 34 47 34 47 47 34 47 47 34 47 47 34 47 47 47 47 34 47 34 47 47
##   [241] 47 47 47 47 47 47 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
##   [265] 31 31 31 31 31 31 31 48 41 41 41 41 41 48 48 41 48 88 88 41 41 41 41 41
##   [289] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 48 48 88 41 41 41 41 41 41
##   [313] 41 41 41 41 41 41 41 41 34 41 41 88 34 41 41 88 41 41 41 48 88 48 48 41
##   [337] 48 41 48 48 41 41 48 41 41 88 88 41 88 41 41 34 41 48 41 41 41 41 48 41
##   [361] 41 41 48 41 88 41 41 41 41 88 48 41 88 41 41 41 41 41 41 48 41 41 41 41
##   [385] 48 41 41 41 41 48 41 41 41 41 41 41 48 41 41 41 41 41 41 34 41 88 41 48
##   [409] 41 41 41 31 31 31 31 31 58 57 81 71 81 57 71 57 81 57 58 58 58 58 58 58
##   [433] 57 81 71 41 41 57 81 57 81 57 57 71 57 71 58 58 57 81 71 81 57 58 57 81
##   [457] 58 57 81 57 57 81 71 57 81 71 57 81 71 81 58 57 81 71 57 81 58 57 81 71
##   [481] 57 81 71 58 58 58 57 71 57 81 71 57 81 57 81 71 57 81 71 58 81 57 57 81
##   [505] 71 81 57 81 58 58 57 57 81 71 57 81 57 81 71 57 81 71 58 57 81 57 58 58
##   [529] 58 58 57 81 57 81 71 58 57 81 71 58 57 81 71 41 58 57 81 71 58 57 81 71
##   [553] 71 58 57 71 57 81 57 81 71 57 81 71 58 57 81 71 81 58 58 57 81 71 57 81
##   [577] 58 57 81 41 41 41 58 81 57 81 71 57 81 71 57 81 71 41 57 81 57 81 58 57
##   [601] 81 71 41 58 57 81 71 57 81 71 58 58 57 57 81 57 57 81 71 57 81 57 81 71
##   [625] 58 58 57 81 71 58 57 81 71 57 81 71 57 81 71 57 81 71 71 57 81 71 57 81
##   [649] 57 81 71 58 57 81 71 58 81 57 81 71 57 81 58 41 57 81 71 57 81 71 58 57
##   [673] 81 58 58 57 81 71 57 81 71 41 57 71 58 57 81 58 58 57 71 57 81 57 81 71
##   [697] 58 58 57 81 71 57 81 71 57 71 57 81 71 58 57 81 71 57 81 71 81 31 31 31
##   [721] 34 31 31 31 31 34 31 31 31 31 31 51 51 51 51 51 51 51 51 51 51 51 51 51
##   [745] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##   [769] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##   [793] 51 57 57 57 57 57 57 57 57 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
##   [817] 31 31 31 31 31 31 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##   [841] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##   [865] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 34 34 41 31 57 51 71 87 41
##   [889] 41 41 31 34 34 34 34 41 31 57 51 77 87 71 34 31 57 51 71 77 87 31 34 34
##   [913] 41 31 57 51 71 34 41 31 51 71 87 34 31 87 34 87 34 34 34 34 34 87 34 34
##   [937] 51 34 34 41 31 34 41 31 57 51 41 31 57 51 34 34 34 31 87 34 41 41 41 34
##   [961] 31 41 34 41 34 34 31 57 51 34 41 31 57 51 34 31 57 51 77 87 71 41 57 51
##   [985] 57 51 71 31 34 41 31 57 51 71 41 34 57 51 77 34 31 87 57 51 34 41 31 57
##  [1009] 51 77 87 71 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [1033] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [1057] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [1081] 31 31 31 31 31 31 31 77 87 31 77 87 31 31 31 31 31 31 31 31 31 31 31 31
##  [1105] 31 31 31 31 31 31 31 31 77 87 31 31 31 31 31 77 87 31 31 31 77 87 31 31
##  [1129] 31 37 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41
##  [1153] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41
##  [1177] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41
##  [1201] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41
##  [1225] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41
##  [1249] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 51 51 51 51 51 51
##  [1273] 51 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 71 71 71 71 71
##  [1297] 71 71 71 34 21 41 21 41 41 41 34 47 37 21 27 21 27 27 21 34 27 27 21 37
##  [1321] 21 34 27 21 27 27 37 37 27 27 21 34 47 37 34 41 41 47 47 27 21 34 47 87
##  [1345] 34 47 87 27 41 27 37 37 51 34 47 41 51 34 51 37 34 47 87 34 37 37 27 34
##  [1369] 27 37 37 37 41 21 27 34 37 34 37 37 37 37 48 41 48 41 51 27 21 51 51 34
##  [1393] 51 47 48 47 34 47 34 47 37 34 34 21 41 41 27 51 37 34 27 47 41 51 37 67
##  [1417] 87 27 47 27 37 37 51 37 67 27 21 21 34 67 41 41 41 48 41 21 34 37 37 41
##  [1441] 37 34 27 48 21 37 51 37 41 41 67 34 47 41 37 67 21 51 37 34 87 21 51 47
##  [1465] 34 48 51 37 48 87 47 47 41 37 37 37 37 48 37 47 37 51 47 51 34 41 51 37
##  [1489] 34 47 87 87 34 37 87 21 34 27 27 34 34 27 34 34 34 34 47 34 34 34 34 34
##  [1513] 34 34 27 47 34 34 34 34 34 47 41 71 71 71 71 71 71 47 34 34 34 34 34 34
##  [1537] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [1561] 34 34 34 34 34 34 67 67 21 77 67 81 21 21 21 21 21 21 21 21 67 21 21 21
##  [1585] 21 21 21 21 21 21 21 21 21 21 77 87 77 87 21 21 67 21 21 67 67 21 67 67
##  [1609] 67 21 21 67 21 21 21 21 21 67 34 21 21 21 67 21 67 21 67 67 21 21 21 21
##  [1633] 67 67 67 67 67 67 67 21 21 21 21 67 67 21 21 21 67 21 67 21 21 67 21 21
##  [1657] 21 21 67 21 67 21 67 21 21 21 34 21 77 87 67 21 21 21 67 67 21 21 77 87
##  [1681] 21 21 21 21 21 21 34 21 77 87 21 31 34 34 34 27 27 27 27 27 27 27 27 27
##  [1705] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##  [1729] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##  [1753] 27 27 27 27 27 27 27 27 87 87 41 87 87 48 88 48 58 88 87 87 41 87 87 87
##  [1777] 48 58 48 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87
##  [1801] 87 87 87 87 87 87 48 34 87 48 87 87 87 87 87 87 87 87 48 58 88 48 87 87
##  [1825] 48 87 87 87 87 48 41 87 87 48 34 41 88 87 87 87 48 88 87 87 34 87 87 87
##  [1849] 87 87 41 87 48 47 41 88 87 34 87 87 87 87 41 87 87 34 48 41 58 88 87 87
##  [1873] 87 87 87 87 87 87 87 87 87 87 87 48 87 41 87 41 87 87 87 48 87 87 87 87
##  [1897] 87 87 87 87 87 34 61 61 34 27 47 41 31 57 51 77 61 87 81 71 51 81 41 34
##  [1921] 27 37 34 27 47 41 34 47 41 34 34 27 47 41 31 57 51 77 61 87 81 71 57 51
##  [1945] 77 61 87 81 71 34 47 41 31 57 51 77 61 87 81 71 34 27 47 41 31 57 51 77
##  [1969] 61 87 81 71 61 51 61 61 87 34 61 87 34 47 61 34 34 47 61 61 61 34 34 61
##  [1993] 34 34 61 61 61 61 61 34 34 34 34 61 61 61 61 87 61 61 47 34 61 61 34 47
##  [2017] 41 31 57 51 77 61 87 81 71 61 34 57 51 77 61 87 81 71 61 34 61 57 51 77
##  [2041] 87 81 71 34 47 61 51 81 51 81 61 61 51 81 34 34 47 61 34 61 34 61 61 34
##  [2065] 47 57 51 71 34 47 41 57 51 77 61 87 81 71 34 61 61 34 77 61 71 51 61 57
##  [2089] 61 61 57 51 77 61 87 81 71 34 27 47 41 31 57 51 77 61 87 81 71 61 34 61
##  [2113] 34 27 47 41 57 51 61 34 51 77 61 34 61 34 27 47 41 31 57 51 77 61 87 81
##  [2137] 71 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61 61
##  [2161] 61 61 61 61 61 61 61 61 61 61 61 61 61 87 77 87 77 87 87 31 31 87 31 87
##  [2185] 87 87 31 87 87 87 87 87 31 87 31 31 87 87 87 31 31 31 31 31 87 31 87 31
##  [2209] 87 31 87 31 87 31 31 87 31 87 87 87 87 87 31 87 87 31 87 31 31 77 87 31
##  [2233] 87 87 31 31 87 31 87 31 87 31 87 31 87 31 87 87 87 87 31 77 87 31 34 51
##  [2257] 51 34 51 51 51 34 51 34 34 34 34 34 34 51 34 51 51 34 51 34 34 51 34 51
##  [2281] 51 34 34 34 51 34 51 51 51 34 51 34 51 34 51 34 51 34 47 47 47 34 47 34
##  [2305] 47 47 47 34 47 34 47 34 34 47 34 34 47 47 34 34 34 34 34 34 34 34 34 34
##  [2329] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 47 34 34
##  [2353] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 77 87 81 71 57
##  [2377] 51 77 81 71 77 71 51 77 81 71 51 51 51 77 77 77 71 77 77 77 77 77 77 77
##  [2401] 51 51 77 77 77 81 71 77 71 77 81 71 51 51 77 51 77 81 71 77 81 71 51 77
##  [2425] 81 71 77 31 77 87 77 31 77 31 77 77 31 77 77 77 31 77 77 31 77 77 77 77
##  [2449] 31 77 31 77 77 77 31 77 77 87 31 77 77 77 31 77 77 31 77 77 77 87 77 37
##  [2473] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [2497] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [2521] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [2545] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [2569] 37 37 37 37 37 37 34 31 87 21 21 21 21 47 47 87 41 41 21 31 47 21 21 21
##  [2593] 21 21 21 34 31 31 34 31 47 34 31 87 31 31 34 47 31 47 31 47 47 21 31 34
##  [2617] 31 87 34 47 87 31 31 47 87 31 47 47 21 34 34 34 21 87 34 87 41 87 31 21
##  [2641] 21 47 31 34 47 31 21 47 34 34 31 47 31 47 34 47 34 31 21 34 87 31 31 47
##  [2665] 31 34 47 41 31 87 31 31 31 47 31 21 21 21 47 87 31 87 21 31 34 47 31 87
##  [2689] 21 31 31 21 41 34 21 47 31 41 31 34 34 41 31 87 34 21 34 31 87 47 34 47
##  [2713] 41 31 87 87 47 47 31 31 21 34 31 34 21 47 31 87 87 21 21 21 34 31 21 31
##  [2737] 34 31 34 34 31 31 34 31 34 37 37 37 37 37 37 77 87 37 37 37 37 37 37 34
##  [2761] 37 37 34 37 37 37 37 37 37 37 37 34 37 37 37 34 37 37 37 37 37 37 37 37
##  [2785] 37 37 34 34 37 37 37 34 37 37 34 34 37 37 37 37 37 34 37 37 37 34 37 37
##  [2809] 37 37 34 37 37 37 37 37 37 37 34 37 37 37 37 37 77 87 37 37 37 37 37 34
##  [2833] 37 77 34 37 37 37 37 77 87 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [2857] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [2881] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [2905] 34 34 34 34 27 27 27 27 27 27 27 21 27 27 27 27 27 21 27 27 21 27 27 27
##  [2929] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##  [2953] 27 27 27 27 27 27 27 27 27 27 27 27 21 27 27 21 27 27 27 27 27 27 27 27
##  [2977] 27 21 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##  [3001] 27 27 27 27 27 27 27 27 27 27 27 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [3025] 51 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
##  [3049] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
##  [3073] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 77 87 87 87 87 77 87 71
##  [3097] 87 71 77 87 87 71 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87
##  [3121] 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87
##  [3145] 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 77 87 71 87 87 87 87 87 87
##  [3169] 87 77 87 87 87 87 87 87 87 77 87 87 87 87 87 87 77 87 71 87 37 37 51 37
##  [3193] 37 37 37 51 51 37 51 37 51 51 37 51 51 51 37 37 37 51 37 37 51 51 37 51
##  [3217] 37 51 51 51 51 51 51 37 37 51 37 51 37 34 51 37 51 37 51 37 37 51 51 37
##  [3241] 51 34 51 37 51 51 51 51 37 37 51 37 37 51 37 51 51 51 37 51 37 51 51 51
##  [3265] 51 37 37 51 37 51 51 51 37 37 51 77 71 71 71 77 77 77 77 77 77 77 77 77
##  [3289] 77 77 77 77 71 77 77 77 77 77 71 77 34 34 34 34 34 34 34 34 34 34 34 34
##  [3313] 34 34 34 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [3337] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [3361] 51 51 51 51 21 34 47 27 21 21 27 41 41 41 41 34 47 34 47 27 21 21 27 21
##  [3385] 27 27 21 27 21 27 21 27 41 27 34 47 27 21 27 47 34 47 27 27 34 47 34 47
##  [3409] 47 27 21 47 87 34 47 41 87 27 47 27 34 47 27 34 34 21 27 34 27 34 27 27
##  [3433] 27 27 21 34 21 27 34 41 27 81 27 21 27 41 34 47 34 47 27 21 34 34 47 34
##  [3457] 47 34 47 34 41 34 27 34 41 47 34 47 41 87 34 34 27 21 21 34 41 27 77 87
##  [3481] 41 41 41 41 34 41 34 27 27 27 27 21 41 47 41 21 27 27 27 21 34 27 21 27
##  [3505] 27 21 34 47 47 41 27 27 34 34 41 77 21 34 47 87 47 41 41 27 21 27 34 47
##  [3529] 34 27 34 47 41 87 27 34 34 47 27 27 21 27 21 21 27 21 34 21 51 51 51 51
##  [3553] 51 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41
##  [3577] 41 41 41 41 41 41 41 41 41 41 27 27 21 27 27 27 27 21 27 21 27 27 27 27
##  [3601] 21 27 21 27 27 27 27 27 27 27 21 27 27 87 87 27 27 27 27 27 27 27 27 21
##  [3625] 27 21 27 27 27 21 27 21 27 27 21 27 21 27 27 27 27 27 21 27 27 27 27 21
##  [3649] 27 27 27 21 27 27 27 27 27 21 27 27 27 21 27 21 27 21 27 27 27 27 27 27
##  [3673] 27 21 27 21 27 27 21 27 21 27 71 71 71 71 71 71 71 71 71 71 71 71 71 71
##  [3697] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
##  [3721] 71 71 71 71 71 71 71 71 71 71 71 71 27 27 27 27 27 27 27 27 27 27 27 27
##  [3745] 27 27 27 27 58 34 27 51 37 27 37 27 27 21 21 27 37 37 27 41 41 27 37 37
##  [3769] 27 27 37 27 37 27 21 27 21 27 21 27 37 27 21 37 27 37 27 21 27 27 27 27
##  [3793] 37 27 27 34 27 57 51 77 87 27 27 27 27 27 37 27 31 27 27 37 27 58 27 34
##  [3817] 27 27 27 51 37 27 27 37 27 51 27 37 27 37 27 37 27 47 47 27 37 27 27 27
##  [3841] 27 27 27 37 34 27 37 27 37 27 37 37 27 27 37 27 37 27 27 27 27 27 37 27
##  [3865] 37 37 27 37 27 37 34 27 37 27 37 37 27 27 48 27 37 34 27 27 37 27 37 47
##  [3889] 27 37 27 27 37 27 27 34 27 37 37 27 37 27 37 27 37 37 27 37 27 37 34 27
##  [3913] 37 27 27 37 27 27 37 27 21 27 21 37 37 27 34 27 51 37 27 37 27 37 27 37
##  [3937] 27 37 27 37 37 27 27 37 37 27 37 27 37 27 37 27 21 27 21 58 27 37 58 27
##  [3961] 27 37 27 37 27 27 27 37 27 21 34 48 34 27 37 27 27 47 37 47 27 27 37 34
##  [3985] 27 27 27 27 27 34 27 37 27 37 21 27 27 27 48 58 27 37 58 27 21 37 27 37
##  [4009] 34 47 41 51 37 27 37 27 27 37 27 37 37 37 37 27 37 27 37 34 27 37 27 27
##  [4033] 27 27 37 37 34 27 37 27 21 27 21 27 37 27 27 27 27 27 27 27 37 34 27 37
##  [4057] 37 41 41 41 58 27 27 27 37 27 37 41 27 37 27 27 37 27 34 27 47 37 27 27
##  [4081] 27 37 27 27 27 27 21 27 58 47 41 58 37 37 27 37 27 37 58 27 37 27 37 27
##  [4105] 27 37 27 21 27 37 27 27 27 37 27 37 27 34 27 37 27 27 37 27 27 27 27 27
##  [4129] 37 27 27 51 37 27 51 27 37 27 37 34 27 31 57 51 37 77 87 27 27 37 27 27
##  [4153] 37 51 37 27 37 27 48 41 47 27 37 27 37 27 37 27 37 27 27 27 37 27 27 27
##  [4177] 27 37 37 27 37 41 37 27 27 37 27 37 27 51 37 27 37 27 27 37 27 34 27 37
##  [4201] 27 37 27 27 27 58 34 27 37 27 27 37 27 27 27 21 27 37 27 37 27 37 21 27
##  [4225] 21 21 27 37 27 37 34 27 31 57 51 77 87 31 31 31 31 31 31 31 31 31 31 31
##  [4249] 31 31 31 31 31 31 31 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77
##  [4273] 77 77 77 77 77 77 77 77 77 77 77 77 77 77 51 51 51 34 34 34 34 34 34 34
##  [4297] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [4321] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [4345] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [4369] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 51 34 34 51 81 37 47 81
##  [4393] 81 34 51 37 51 87 47 47 87 34 47 87 51 51 34 37 34 37 37 81 37 81 34 51
##  [4417] 34 51 34 51 34 47 34 51 34 51 47 34 47 51 37 87 81 37 34 37 34 37 34 47
##  [4441] 51 37 51 37 81 34 51 51 37 34 51 37 51 47 87 81 37 37 51 34 51 81 34 47
##  [4465] 81 81 34 37 34 34 67 21 34 27 21 21 51 48 41 48 48 27 41 41 27 21 67 27
##  [4489] 34 21 27 21 27 21 27 21 34 27 27 21 21 47 27 21 27 21 27 27 21 47 51 27
##  [4513] 51 48 27 34 27 47 48 41 27 21 34 27 27 21 34 21 51 27 41 47 47 27 21 34
##  [4537] 41 27 34 87 34 27 47 41 87 27 27 27 27 27 27 27 34 47 51 48 41 27 34 27
##  [4561] 87 34 27 27 47 27 21 67 27 27 21 34 27 27 27 27 27 34 27 27 27 27 27 34
##  [4585] 27 21 34 27 21 47 67 27 34 27 21 41 27 27 27 27 21 27 41 34 34 27 51 34
##  [4609] 47 51 27 47 27 21 34 48 41 34 47 51 34 51 34 47 47 27 51 34 47 27 34 47
##  [4633] 27 27 27 21 34 21 27 48 34 48 27 34 27 48 34 47 41 51 67 87 27 27 27 41
##  [4657] 34 27 67 27 21 27 21 27 27 48 34 27 67 67 67 67 34 41 41 48 21 51 27 21
##  [4681] 41 41 27 27 27 21 34 27 47 51 27 27 21 48 34 47 41 21 47 27 21 41 27 21
##  [4705] 34 27 21 34 67 27 21 27 27 21 34 47 51 34 47 27 67 21 34 51 27 34 27 34
##  [4729] 41 21 34 27 47 51 34 47 51 48 87 47 48 41 48 27 27 48 27 27 27 51 34 27
##  [4753] 47 51 27 27 21 27 48 34 27 47 67 34 34 47 21 47 27 27 21 27 21 48 48 34
##  [4777] 34 34 47 41 34 34 34 34 34 34 34 34 34 34 34 34 34 47 47 87 34 47 87 34
##  [4801] 87 34 34 34 34 34 47 34 47 34 34 34 34 34 34 34 34 34 34 34 34 47 34 34
##  [4825] 47 34 34 34 34 34 47 87 34 34 34 34 47 34 34 47 34 34 47 34 47 34 34 47
##  [4849] 34 47 34 34 47 34 34 34 34 34 34 34 34 34 34 34 47 34 34 34 34 37 37 41
##  [4873] 34 37 34 37 37 37 34 37 37 34 37 34 37 34 37 34 37 34 34 37 34 37 34 37
##  [4897] 37 34 37 37 34 37 34 37 34 37 37 37 34 37 34 37 37 34 37 37 34 37 37 37
##  [4921] 37 37 37 34 37 37 34 37 34 34 37 34 37 37 34 34 37 34 37 34 37 37 37 37
##  [4945] 34 37 34 37 34 37 34 37 34 37 34 37 41 34 37 34 37 37 34 37 34 37 37 34
##  [4969] 34 37 34 37 34 37 37 34 37 37 37 34 37 34 37 37 34 37 37 34 37 34 34 37
##  [4993] 37 34 37 21 27 21 27 27 21 27 21 27 21 27 21 27 27 21 27 21 27 27 21 27
##  [5017] 27 27 21 27 21 27 21 27 21 27 21 27 21 27 21 21 27 21 27 21 27 27 21 27
##  [5041] 27 21 27 21 21 27 21 27 21 27 21 27 21 27 21 31 31 31 31 31 31 31 31 31
##  [5065] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
##  [5089] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 71 71
##  [5113] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 34 34 77
##  [5137] 87 77 31 77 31 77 77 34 77 77 31 77 31 77 77 77 31 77 31 77 77 34 77 87
##  [5161] 31 77 77 87 31 77 77 34 77 87 77 34 57 51 34 34 34 34 34 57 51 51 51 57
##  [5185] 51 34 34 34 34 34 34 34 34 34 57 51 34 34 34 34 57 51 34 34 34 34 34 34
##  [5209] 34 34 57 51 57 51 57 51 51 57 51 57 51 34 34 34 34 57 51 34 34 34 34 34
##  [5233] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [5257] 34 34 34 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 47 41 41 47
##  [5281] 77 87 47 31 34 47 34 34 47 34 34 57 34 34 31 77 31 77 34 47 41 31 77 31
##  [5305] 77 57 34 21 21 34 47 41 41 41 34 31 77 41 34 47 41 31 41 47 57 77 87 41
##  [5329] 31 47 57 41 77 77 87 71 34 47 31 77 47 77 87 21 27 47 31 27 27 27 27 27
##  [5353] 21 27 27 21 27 27 27 27 21 27 27 27 27 27 27 27 31 27 27 27 27 27 47 27
##  [5377] 21 27 47 27 27 47 21 27 27 27 27 27 27 21 27 27 27 27 21 27 27 27 21 27
##  [5401] 27 21 34 47 47 27 27 27 47 27 47 27 27 21 27 27 27 27 27 27 27 27 27 27
##  [5425] 27 27 47 27 27 27 27 27 34 47 27 27 27 47 27 27 27 27 27 27 47 27 27 27
##  [5449] 27 27 21 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57
##  [5473] 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57
##  [5497] 51 57 51 57 51 57 51 58 57 51 58 57 51 57 51 57 51 57 51 57 51 57 51 57
##  [5521] 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57
##  [5545] 51 57 51 57 51 57 51 57 51 57 51 57 51 57 51 57 57 57 71 57 71 57 71 57
##  [5569] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 71 57 71
##  [5593] 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71
##  [5617] 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71
##  [5641] 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71
##  [5665] 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71
##  [5689] 57 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
##  [5713] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 57 71 57 71
##  [5737] 57 71 57 71 57 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
##  [5761] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 57 71 57 71 57 71 57 71 51 51
##  [5785] 51 51 57 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [5809] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 57 51
##  [5833] 51 51 51 51 51 51 51 51 51 51 51 51 57 51 47 47 47 51 51 51 51 51 47 51
##  [5857] 51 51 47 51 51 51 27 27 27 21 21 21 27 27 27 27 34 21 27 21 27 21 27 27
##  [5881] 27 21 27 27 21 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 21 27 27 27
##  [5905] 21 27 34 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 34 27 27 27 27
##  [5929] 27 27 27 34 27 27 27 27 21 27 21 34 27 27 27 27 21 27 27 27 27 21 27 27
##  [5953] 27 27 27 27 21 27 27 34 27 27 27 27 34 27 27 27 27 34 21 27 27 27 27 34
##  [5977] 27 27 27 34 27 27 21 27 27 27 27 27 27 27 27 27 27 34 27 27 27 27 27 27
##  [6001] 27 27 27 27 27 27 27 27 27 34 27 27 27 21 27 27 21 27 27 21 27 34 27 27
##  [6025] 27 27 27 27 27 21 27 27 27 21 27 27 34 27 27 27 21 27 27 27 27 21 27 27
##  [6049] 27 21 27 27 21 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
##  [6073] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 41 37
##  [6097] 37 47 51 37 47 47 37 37 37 51 37 47 47 47 37 37 47 37 37 37 37 37 37 37
##  [6121] 47 37 37 37 37 51 37 37 37 37 51 47 47 37 47 37 37 34 47 41 51 37 37 37
##  [6145] 47 37 51 37 41 37 47 37 37 37 51 37 37 37 47 37 51 37 37 51 47 37 37 37
##  [6169] 37 47 41 47 37 51 37 21 47 41 37 47 41 37 37 21 21 21 27 27 21 37 21 34
##  [6193] 57 51 37 37 37 37 37 47 34 47 37 41 51 34 34 47 41 31 51 37 37 34 37 37
##  [6217] 34 37 37 34 37 37 34 27 31 51 37 34 47 41 51 37 34 34 27 47 31 51 37 37
##  [6241] 41 51 21 37 21 37 34 37 37 37 37 37 34 27 37 37 37 37 37 21 34 21 47 41
##  [6265] 31 51 37 37 51 37 37 34 37 41 51 37 37 37 37 47 41 51 34 47 41 51 37 34
##  [6289] 37 34 37 34 47 51 37 37 34 47 37 37 21 34 37 34 21 47 41 31 51 37 34 27
##  [6313] 47 41 31 51 37 34 21 47 41 31 51 37 37 37 37 37 37 34 27 47 51 21 21 37
##  [6337] 27 47 41 51 34 37 47 37 41 37 37 37 37 34 47 41 51 27 21 34 47 41 51 37
##  [6361] 37 21 37 41 41 37 37 21 37 37 37 34 47 41 37 37 37 34 47 41 51 37 21 34
##  [6385] 47 41 51 37 21 31 37 37 57 51 37 37 37 37 37 47 51 37 37 37 21 37 34 27
##  [6409] 37 37 37 47 41 51 37 47 41 51 34 51 37 37 34 27 47 41 31 51 37 34 47 37
##  [6433] 57 51 31 31 31 31 31 31 67 61 67 61 34 27 21 47 41 31 58 57 51 37 77 67
##  [6457] 61 87 81 71 51 61 41 31 77 67 61 81 71 21 48 58 48 48 48 58 51 77 61 87
##  [6481] 41 41 27 21 87 81 67 34 27 21 47 41 31 37 21 27 21 21 27 21 34 27 27 21
##  [6505] 21 27 21 34 21 47 41 31 21 34 27 21 47 41 31 27 34 34 47 57 51 61 81 61
##  [6529] 71 34 34 27 21 47 41 31 57 51 77 67 61 87 81 71 34 47 57 51 77 67 61 87
##  [6553] 81 71 48 48 47 58 34 47 81 81 34 27 21 47 41 31 57 51 77 61 87 81 71 27
##  [6577] 61 87 81 41 57 51 87 81 47 47 47 21 48 87 61 34 47 41 77 67 61 87 71 61
##  [6601] 67 61 61 61 57 77 67 61 87 81 71 51 61 34 47 41 31 51 61 81 71 48 34 34
##  [6625] 47 57 51 61 71 61 71 61 34 47 41 51 77 61 87 81 61 27 21 34 27 21 47 41
##  [6649] 31 51 77 67 61 81 71 61 67 61 71 34 47 31 57 77 61 81 71 34 27 21 47 41
##  [6673] 51 77 87 81 61 61 48 41 57 51 61 81 57 21 48 58 48 58 27 21 34 27 47 41
##  [6697] 31 57 51 87 81 34 21 47 41 57 51 61 31 34 27 47 27 21 34 61 61 48 61 51
##  [6721] 57 51 77 67 61 87 81 71 51 81 61 61 61 61 71 61 61 61 61 61 61 71 61 61
##  [6745] 34 47 57 51 87 81 77 87 67 61 67 61 61 48 34 61 71 34 31 21 61 48 58 61
##  [6769] 48 58 34 41 51 67 61 34 21 61 81 48 34 27 47 41 31 58 57 51 37 77 67 61
##  [6793] 87 81 71 34 27 47 31 51 81 67 61 61 27 47 31 57 51 77 67 61 81 71 77 67
##  [6817] 61 67 21 21 48 34 47 41 67 61 87 71 61 77 67 61 87 81 71 67 61 67 61 67
##  [6841] 61 77 67 77 67 61 61 61 61 61 71 77 61 34 47 41 41 48 47 41 58 27 21 34
##  [6865] 47 51 81 34 41 31 87 41 61 34 27 47 41 31 57 51 61 87 81 71 61 61 58 81
##  [6889] 61 47 61 61 47 67 61 21 77 67 61 27 21 34 77 67 61 21 61 57 51 71 41 27
##  [6913] 34 27 21 47 41 31 57 51 37 77 67 61 87 81 71 57 51 21 61 81 71 34 47 41
##  [6937] 31 57 51 77 67 61 87 81 71 61 34 47 51 81 61 48 41 81 47 41 57 51 87 81
##  [6961] 71 48 21 57 51 77 67 61 87 81 71 48 34 27 21 47 41 31 57 51 37 77 67 61
##  [6985] 87 81 71 41 67 61 81 61 48 47 51 61 34 47 41 57 51 37 77 67 61 87 81 71
##  [7009] 48 58 48 34 27 21 47 31 57 51 77 67 61 81 71 61 81 47 67 61 41 58 21 21
##  [7033] 61 48 67 61 34 27 21 47 41 31 57 51 77 67 61 87 81 71 61 51 51 51 51 51
##  [7057] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [7081] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 71 71 71 71 71 71 71 71 71 71
##  [7105] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 61 34 34 61 61 61 34
##  [7129] 61 34 34 61 34 61 61 88 61 34 61 67 61 34 27 21 47 41 31 57 51 37 77 67
##  [7153] 61 87 81 71 34 47 41 51 61 81 71 57 51 61 81 71 21 61 47 41 88 48 48 58
##  [7177] 88 61 41 41 61 67 34 47 31 37 21 21 21 34 21 41 31 37 34 41 31 34 81 61
##  [7201] 61 34 34 47 34 27 47 41 31 57 51 77 67 61 87 81 71 34 47 57 51 77 67 61
##  [7225] 87 81 71 47 48 58 88 61 48 88 34 81 81 34 47 41 31 57 51 77 61 87 81 71
##  [7249] 34 47 41 61 81 47 34 61 41 61 81 47 47 87 61 34 47 41 51 77 61 87 71 61
##  [7273] 34 31 81 61 61 41 51 87 81 71 34 21 47 41 31 57 51 37 77 61 87 81 71 34
##  [7297] 41 87 77 34 47 31 57 51 61 81 71 61 34 61 21 58 88 61 61 51 71 34 21 34
##  [7321] 21 47 41 31 51 67 61 87 81 71 61 61 34 34 47 41 57 51 77 61 87 81 71 61
##  [7345] 61 61 81 61 21 48 41 58 88 77 61 81 88 21 47 57 51 81 71 34 61 34 47 51
##  [7369] 61 34 41 31 57 51 77 87 81 71 34 47 41 61 61 61 57 51 77 87 81 71 34 47
##  [7393] 51 81 34 41 31 51 61 61 61 61 61 61 61 61 61 61 61 61 34 47 57 51 81 87
##  [7417] 88 61 48 47 61 61 61 48 61 47 61 34 41 31 57 51 77 87 81 71 61 41 48 34
##  [7441] 47 31 57 51 61 81 71 34 41 31 57 51 61 71 48 34 27 47 41 31 57 51 37 77
##  [7465] 67 61 87 81 71 34 21 41 31 51 61 87 81 71 61 34 47 41 31 57 51 37 77 61
##  [7489] 87 81 71 58 88 34 88 34 47 41 31 57 51 37 77 61 87 81 71 34 47 41 31 57
##  [7513] 51 77 67 61 87 81 71 47 61 81 77 67 61 71 67 61 61 67 61 77 61 61 77 67
##  [7537] 61 77 87 34 41 87 48 47 41 58 57 51 88 47 41 31 41 81 88 34 47 41 31 57
##  [7561] 51 77 61 87 81 71 34 51 61 81 71 21 88 48 34 47 41 31 57 51 37 88 77 67
##  [7585] 61 87 81 71 34 88 34 41 81 61 47 34 47 41 77 67 61 81 71 61 41 57 51 81
##  [7609] 71 48 34 27 47 41 31 57 51 37 77 61 87 81 71 61 61 21 61 47 81 61 34 47
##  [7633] 41 31 57 51 77 67 61 87 81 71 88 34 51 34 48 47 41 47 57 51 81 41 81 61
##  [7657] 57 51 77 61 87 81 71 34 34 27 21 47 41 31 57 51 37 77 67 61 87 81 71 41
##  [7681] 61 34 47 51 71 61 34 61 34 41 31 57 51 77 61 87 81 71 34 47 51 34 27 47
##  [7705] 41 31 57 51 37 77 67 61 87 81 71 34 27 21 47 41 31 57 51 77 67 61 81 71
##  [7729] 47 47 34 34 47 61 58 88 21 61 61 34 27 21 47 41 31 57 51 77 67 61 87 81
##  [7753] 71 21 61 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [7777] 51 51 34 34 21 21 41 41 41 21 34 47 34 47 27 21 27 21 27 27 21 34 47 27
##  [7801] 21 27 27 34 47 27 34 27 34 47 34 41 47 47 27 21 34 47 41 87 34 47 87 34
##  [7825] 87 27 34 27 47 27 34 27 21 27 34 27 27 34 27 27 27 21 27 34 41 27 81 27
##  [7849] 21 41 21 34 47 34 47 27 21 34 34 34 47 34 47 34 47 34 34 34 41 47 34 27
##  [7873] 47 41 87 34 34 27 21 21 34 27 34 41 41 47 34 47 21 47 41 21 27 41 34 27
##  [7897] 21 27 21 27 34 47 34 27 34 47 27 27 34 34 27 47 27 21 27 34 47 87 41 27
##  [7921] 34 47 34 87 27 27 34 47 41 87 81 27 34 34 47 27 27 27 21 34 37 37 37 37
##  [7945] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 34 34 34 34 34 34 34 34
##  [7969] 34 34 34 87 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [7993] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [8017] 34 34 34 34 34 87 34 34 34 34 34 34 34 34 34 34 34 34 34 87 27 37 37 37
##  [8041] 34 37 37 37 34 37 37 37 37 37 37 37 34 37 34 34 37 37 37 37 37 37 37 34
##  [8065] 34 37 37 37 34 37 34 34 37 34 37 34 37 37 37 37 37 37 37 37 37 37 37 27
##  [8089] 37 37 37 34 34 34 34 34 34 47 87 34 87 21 21 47 41 41 21 27 34 47 34 47
##  [8113] 27 21 21 27 21 27 27 21 34 47 27 21 27 27 27 34 34 34 47 27 47 34 27 34
##  [8137] 27 34 47 34 34 34 34 41 47 47 27 21 47 87 34 47 77 87 27 27 34 47 27 34
##  [8161] 34 47 27 34 34 27 27 21 34 27 34 27 27 27 27 27 21 34 27 27 27 34 47 41
##  [8185] 27 27 81 27 21 41 87 34 47 34 47 27 21 34 34 41 34 47 34 34 47 47 34 47
##  [8209] 34 27 34 27 34 41 47 34 34 34 47 41 51 77 87 34 34 31 51 34 27 21 21 34
##  [8233] 77 41 41 34 34 47 27 27 21 27 34 47 41 21 41 27 27 21 27 34 27 21 34 27
##  [8257] 34 27 21 27 34 47 27 34 34 47 27 27 34 47 27 21 27 34 47 47 87 47 41 87
##  [8281] 34 27 47 34 47 51 87 27 34 34 27 47 41 77 87 81 27 34 34 47 27 21 34 21
##  [8305] 21 34 21 57 51 57 51 51 57 51 51 51 51 51 51 51 51 51 51 51 57 51 51 51
##  [8329] 51 57 51 51 51 51 57 51 57 51 51 51 57 51 57 71 57 71 57 71 57 71 57 71
##  [8353] 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71
##  [8377] 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 57 71 57
##  [8401] 71 57 71 57 71 57 71 57 57 71 57 71 57 71 57 71 57 71 57 71 71 57 71 57
##  [8425] 71 71 57 71 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
##  [8449] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
##  [8473] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
##  [8497] 71 71 57 71 57 71 57 71 57 71 57 71 51 51 51 51 51 51 51 51 51 51 51 51
##  [8521] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [8545] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [8569] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 34 37 37 37 37 37 37 37 37 37
##  [8593] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [8617] 37 37 37 37 37 37 37 37 71 71 71 71 71 34 71 71 71 71 71 71 71 31 31 31
##  [8641] 31 31 31 31 31 31 31 31 31 31 31 31 31 34 34 34 34 34 34 34 34 34 34 34
##  [8665] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [8689] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [8713] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
##  [8737] 34 34 34 34 34 34 34 34 34 34 51 51 51 51 51 51 51 51 51 51 51 51 51 51
##  [8761] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 57 51 51 51 51 51 57
##  [8785] 51 51 51 51 57 51 77 77 77 31 77 31 31 31 77 77 31 31 31 21 21 31 31 31
##  [8809] 31 31 77 31 77 31 31 77 87 71 31 77 77 31 31 31 31 31 77 77 31 77 31 77
##  [8833] 77 77 31 77 31 31 77 31 77 31 31 77 31 31 31 77 31 77 31 77 31 77 77 87
##  [8857] 31 77 21 31 77 31 77 31 77 31 77 31 31 77 31 77 31 77 31 31 77 31 77 31
##  [8881] 31 77 77 31 31 31 21 31 77 77 31 77 77 77 31 31 77 31 77 31 77 77 31 31
##  [8905] 31 77 21 31 31 77 77 77 77 77 77 77 77 77 77 77 77 77 31 77 31 77 31 31
##  [8929] 31 77 21 77 31 77 31 31 31 77 31 77 77 77 31 77 31 77 21 77 31 77 87 71
##  [8953] 31 77 31 77 31 77 31 77 31 77 31 77 31 31 77 31 77 31 77 77 31 77 31 31
##  [8977] 77 31 31 77 77 77 31 77 87 71 77 31 71 71 71 71 71 71 71 71 71 71 71 71
##  [9001] 71 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
##  [9025] 37 37 31 34 37 34 37 34 37 34 37 34 34 37 34 34 37 34 34 37 34 34 37 34
##  [9049] 37 34 37 34 37 37 34 37 34 37 34 37 34 37 37 34 37 34 37 34 37 34 37 34
##  [9073] 37 34 37 34 34 37 34 37 34 37 34 37 34 34 37 34 37 34 37 34 37 34 37 34
##  [9097] 34 34 37 34 37 34 37 34 37 37 37 34 37 34 34 37 34 37 34 37 34 37 34 37
##  [9121] 34 37 34 37 34 37 34 37 34 37 34 37 34 34 34 37 34 37 34 37 34 37 34 37
##  [9145] 34 37 34 34 37 34 37 34 37 34 34 37 34 34 34 37 34 37 34 37 34 37 34 37
##  [9169] 34 37 34 37 34 37 34 37 34 37 37 34 51 51 51 51 51 51 51 51 51 51 51 51
##  [9193] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 57 57 57 57 57 58
##  [9217] 47 47 58 41 41 47 47 47 47 58 47 47 47 47 47 47 47 47 47 58 47 47 58 58
##  [9241] 58 47 47 47 47 47 47 47 41 47 58 47 47 47 47 47 47 47 41 41 41 58 47 41
##  [9265] 47 47 41 58 47 47 47 47 47 47 47 47 41 47 47 47 47 41 47 47 47 47 47 47
##  [9289] 47 58 47 71 71 71 71 71 71 71 71 71 27 21 27 27 41 27 27 27 34 34 27 27
##  [9313] 27 27 27 21 34 27 27 27 34 34 27 34 27 34 27 27 27 27 27 34 34 27 27 87
##  [9337] 34 87 27 27 27 27 27 27 27 34 27 27 34 27 27 27 27 27 27 34 27 27 34 27
##  [9361] 27 27 21 27 27 34 27 27 27 27 27 27 27 27 34 27 27 34 34 34 27 34 27 34
##  [9385] 27 27 34 21 27 34 34 27 87 34 27 34 27 27 27 27 27 27 41 41 27 27 27 27
##  [9409] 34 27 27 27 27 27 27 27 34 34 27 27 27 34 34 27 34 34 34 27 27 27 27 27
##  [9433] 27 87 27 27 27 34 34 27 27 27 27 27 27 27 27 27 34 27 34 27 27 27 34 34
##  [9457] 31 31 34 31 31 34 31 34 31 31 34 31 31 31 34 31 71 71 71 71 71 71 71 71
##  [9481] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 81 81 71 81 81 81
##  [9505] 88 81 88 48 88 48 58 88 81 81 81 81 81 81 81 81 88 81 81 71 81 81 81 81
##  [9529] 81 88 48 88 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81
##  [9553] 58 88 81 81 81 81 81 81 81 88 81 81 81 81 81 81 81 81 81 81 81 81 81 81
##  [9577] 81 81 48 58 88 81 88 81 81 81 81 88 81 81 81 81 81 81 81 81 81 81 41 81
##  [9601] 81 88 81 88 81 81 81 81 81 81 81 81 81 88 81 81 81 81 81 81 81 81 81 48
##  [9625] 41 58 88 81 81 81 81 81 88 81 88 81 88 48 41 88 81 81 81 88 81 88 81 81
##  [9649] 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 81 71 81 81 81 81 81 88
##  [9673] 81 81 81 81 81 81 81 81 81 81 88 81 81 81 88 81 81 81 81 81 81 81 81 81
##  [9697] 81 71 81 81 81 58 88 81 81 71 77 87 77 87 31 31 31 31 77 77 77 77 77 31
##  [9721] 77 31 77 31 31 31 31 77 31 77 87 77 77 31 77 77 31 77 31 77 31 77 77 31
##  [9745] 77 31 77 31 77 31 77 87 31 77 31 77 77 31 77 77 31 77 77 87 31 34 34 34
##  [9769] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 47
##  [9793] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 77
##  [9817] 77 77 77 77 77 77 77 77 77 77 81 71 71 71 71 71 71 71 71 71 71 71 71 71
##  [9841] 71 71 71 71 71 71 27 34 47 51 81 27 21 27 88 48 88 27 27 34 27 27 21 27
##  [9865] 21 27 27 27 27 27 21 27 21 27 27 27 27 21 34 27 27 88 81 27 21 27 27 27
##  [9889] 34 27 27 27 21 27 34 27 27 27 27 27 88 27 21 27 27 27 27 27 27 27 27 27
##  [9913] 27 34 27 27 27 27 34 27 21 27 21 27 21 47 81 27 81 27 21 27 27 27 27 27
##  [9937] 21 48 88 27 27 21 27 27 34 81 34 27 27 27 21 27 27 27 34 51 81 27 27 27
##  [9961] 88 27 27 21 27 27 27 21 34 47 47 51 81 47 51 81 88 27 27 27 27 27 21 34
##  [9985] 27 27 21 27 21 27 88 27 27 27 27 21 27 21 27 21 27 27 34 27 27 27 81 27
## [10009] 34 27 48 81 27 21 21 34 47 27 27 27 21 27 27 81 27 27 21 27 27 21 27 21
## [10033] 27 34 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [10057] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [10081] 51 51 51 51 51 51 51 34 47 57 51 37 87 34 27 31 37 37 34 41 31 34 47 41
## [10105] 31 34 34 27 57 51 77 87 34 57 51 77 87 34 41 31 57 51 57 51 47 47 87 34
## [10129] 87 34 34 47 87 34 34 51 34 57 51 34 34 34 37 34 51 34 57 51 34 34 77 34
## [10153] 34 34 57 51 51 34 57 51 77 87 57 51 57 51 34 47 31 57 51 37 34 57 51 37
## [10177] 77 87 34 57 51 34 31 57 51 77 87 51 51 51 51 51 51 51 51 51 51 51 51 51
## [10201] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [10225] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 71
## [10249] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [10273] 71 71 71 71 71 71 71 71 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [10297] 37 37 37 37 37 37 37 37 37 34 34 27 47 31 77 41 41 34 31 37 34 31 41 31
## [10321] 34 34 34 27 47 41 31 77 87 77 87 34 41 31 34 34 34 77 34 47 77 77 34 34
## [10345] 47 34 34 34 77 41 34 47 34 47 34 34 41 77 77 34 47 41 77 77 77 34 47 77
## [10369] 34 47 77 77 77 77 41 41 41 41 34 47 77 41 34 47 41 34 47 34 77 34 34 47
## [10393] 41 77 87 77 34 41 87 77 41 34 47 41 31 41 34 31 34 27 47 41 31 77 87 34
## [10417] 47 77 31 34 34 34 41 31 77 87 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [10441] 71 71 71 71 71 71 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87
## [10465] 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87 87
## [10489] 87 87 87 87 87 87 87 87 87 87 87 87 71 47 41 31 57 51 71 34 47 41 31 71
## [10513] 71 71 71 34 47 41 31 57 51 71 34 47 41 31 57 51 71 71 71 71 71 71 71 71
## [10537] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [10561] 71 71 57 51 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [10585] 71 71 71 71 71 71 71 57 51 71 71 71 34 41 31 71 71 71 71 71 71 57 51 71
## [10609] 71 71 71 57 51 71 34 47 41 31 57 51 71 71 71 71 71 34 47 31 71 71 71 34
## [10633] 47 41 31 57 51 71 81 67 61 21 34 47 27 21 21 21 27 48 41 88 41 48 41 27
## [10657] 67 27 67 34 21 41 34 47 31 34 21 27 21 27 21 27 21 27 27 21 21 34 47 27
## [10681] 27 21 27 27 34 27 21 34 34 27 48 41 47 81 27 27 21 34 21 77 47 47 27 21
## [10705] 87 34 47 51 77 87 27 27 34 47 27 47 81 34 21 27 34 27 27 34 27 27 27 27
## [10729] 27 41 27 21 27 21 67 27 27 27 41 31 27 27 27 27 57 27 21 48 41 81 48 41
## [10753] 58 27 21 34 27 47 27 21 34 48 34 34 47 67 47 27 47 34 47 34 27 34 41 31
## [10777] 21 48 41 58 48 58 48 34 47 41 31 57 88 77 67 61 87 81 41 47 77 67 21 21
## [10801] 27 48 67 67 77 67 77 67 77 67 47 41 87 41 48 41 58 27 27 21 67 41 81 27
## [10825] 34 47 27 27 21 48 47 41 21 21 31 27 21 27 31 48 27 21 34 67 27 21 27 34
## [10849] 47 34 47 77 67 21 27 34 41 27 47 27 21 34 47 34 47 34 87 48 87 47 51 41
## [10873] 81 81 47 87 48 21 41 27 34 41 27 58 34 47 41 67 81 27 34 27 47 27 67 27
## [10897] 21 21 67 34 77 67 34 27 21 47 41 57 51 81 34 27 34 27 47 27 34 41 27 21
## [10921] 21 27 47 34 27 21 27 27 41 41 27 27 34 27 47 41 37 34 27 47 41 27 21 27
## [10945] 21 27 34 27 27 34 27 47 34 27 21 34 27 21 47 41 31 37 27 27 34 27 47 41
## [10969] 27 34 27 27 27 27 27 34 27 51 27 34 27 21 27 34 27 47 41 87 34 27 21 47
## [10993] 41 31 51 87 81 34 27 27 34 27 21 47 41 31 57 51 87 81 34 27 34 27 34 27
## [11017] 34 27 34 27 34 27 27 27 34 27 34 47 27 27 34 27 21 47 41 31 57 51 87 27
## [11041] 34 27 21 47 41 31 57 51 37 87 81 34 27 34 27 34 27 47 34 47 34 27 47 27
## [11065] 41 27 47 27 41 47 47 21 34 27 34 27 34 34 47 34 34 27 47 34 27 34 27 21
## [11089] 27 34 27 27 34 27 34 27 47 41 57 51 87 27 27 27 27 34 27 27 27 34 27 34
## [11113] 27 21 27 47 34 27 47 51 37 34 27 34 47 27 34 27 47 34 27 47 27 34 27 27
## [11137] 27 34 27 47 27 34 27 21 47 41 31 57 51 87 81 34 27 34 27 27 27 34 27 34
## [11161] 27 34 27 27 27 27 27 47 27 21 34 27 21 27 34 27 27 34 27 34 27 21 47 27
## [11185] 34 27 34 34 27 27 27 21 27 27 34 41 27 34 27 27 27 27 21 27 21 41 27 27
## [11209] 27 34 27 34 27 47 41 34 27 47 34 27 21 51 34 27 47 27 21 34 27 41 57 51
## [11233] 27 27 51 57 51 27 34 47 34 27 34 27 47 47 34 27 34 27 34 27 47 34 27 47
## [11257] 34 27 34 27 34 27 27 27 27 34 27 41 51 47 51 34 27 21 47 41 31 34 34 27
## [11281] 27 27 34 27 34 27 41 51 34 34 27 47 41 51 34 27 47 41 51 37 34 47 41 31
## [11305] 57 51 37 87 81 34 27 47 27 34 27 21 47 41 31 57 51 37 87 81 34 27 27 27
## [11329] 47 27 34 27 34 27 34 27 34 27 21 27 27 34 27 41 51 37 34 27 21 27 21 34
## [11353] 27 27 34 27 27 34 41 51 34 27 47 31 51 27 34 27 21 47 41 31 57 51 37 87
## [11377] 34 27 27 47 87 81 27 27 34 27 34 47 34 27 47 34 27 41 41 41 27 27 51 27
## [11401] 27 27 21 47 41 34 27 37 27 34 27 34 27 21 41 51 34 27 47 51 34 27 37 27
## [11425] 34 27 27 27 27 34 27 21 34 47 41 27 27 27 21 34 47 34 27 27 34 47 41 51
## [11449] 27 27 34 21 27 21 34 27 34 27 21 27 34 27 34 27 27 27 34 34 27 47 34 27
## [11473] 27 34 27 47 31 21 27 27 34 27 34 27 34 27 21 47 41 31 57 51 37 87 27 34
## [11497] 34 27 21 47 41 31 57 51 37 87 81 34 34 41 51 21 34 27 47 27 34 27 34 27
## [11521] 21 47 41 51 34 27 27 34 27 47 41 34 27 34 27 41 34 47 47 27 34 27 27 47
## [11545] 41 47 41 51 47 34 51 34 27 27 51 34 27 27 27 27 21 27 27 27 27 27 34 27
## [11569] 27 34 27 34 27 34 27 21 47 41 31 57 51 37 87 81 41 27 34 27 34 27 41 57
## [11593] 51 37 27 34 34 27 27 34 27 27 34 27 21 47 41 31 57 51 37 87 27 27 27 34
## [11617] 27 47 51 27 27 47 34 27 41 51 34 27 34 34 47 34 34 34 27 47 34 27 21 27
## [11641] 37 27 27 21 27 21 34 27 34 27 47 51 34 27 21 47 41 31 57 51 87 47 57 51
## [11665] 21 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
## [11689] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
## [11713] 31 31 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [11737] 51 51 51 51 51 51 51 51 51 51 51 51 51 34 21 21 27 21 34 47 37 34 21 27
## [11761] 21 27 21 27 21 34 27 27 21 37 34 47 21 21 34 34 51 34 37 34 37 34 47 34
## [11785] 34 21 34 37 34 34 34 47 47 47 47 21 34 51 34 47 51 27 34 34 34 37 34 34
## [11809] 47 34 34 34 47 34 37 37 27 34 27 37 27 37 34 21 34 37 34 34 37 34 47 37
## [11833] 21 21 34 27 47 21 51 34 34 51 34 27 47 47 37 34 27 47 34 34 34 34 21 47
## [11857] 47 21 34 51 34 37 34 27 47 51 37 37 34 37 37 34 37 21 34 34 21 27 21 37
## [11881] 37 34 27 47 51 21 34 47 37 21 34 34 51 34 21 34 27 21 27 47 51 34 51 47
## [11905] 21 34 37 34 37 34 47 51 34 21 47 37 34 34 51 47 34 47 47 47 51 34 37 37
## [11929] 34 37 34 51 37 47 47 27 37 27 21 21 88 34 34 47 67 61 34 27 21 47 41 31
## [11953] 51 61 34 81 27 21 21 47 61 27 88 48 88 61 41 41 41 27 21 81 27 37 34 47
## [11977] 34 47 77 18 27 21 27 21 67 27 21 27 34 27 21 34 27 47 81 27 21 34 27 31
## [12001] 27 27 34 47 51 81 71 27 21 47 37 34 47 34 61 37 48 47 61 37 48 88 34 47
## [12025] 81 61 27 81 34 34 27 34 47 51 37 61 34 47 34 47 51 61 87 81 41 61 27 47
## [12049] 47 47 27 21 61 34 47 87 61 34 27 47 51 67 61 87 67 61 61 47 77 47 51 61
## [12073] 37 27 61 47 41 51 61 34 47 51 88 27 47 61 41 34 47 51 27 37 61 34 51 21
## [12097] 48 27 61 51 34 27 37 27 27 34 37 27 27 27 37 27 21 34 27 21 47 37 67 61
## [12121] 81 34 37 27 34 47 18 61 81 34 37 61 48 34 51 37 61 61 27 21 27 81 18 27
## [12145] 21 61 48 41 88 67 61 81 27 58 34 51 61 51 71 34 47 61 34 47 18 27 21 61
## [12169] 34 61 61 61 51 34 47 51 37 34 47 77 71 61 61 61 61 34 47 61 47 27 48 34
## [12193] 27 34 47 34 47 31 61 34 47 27 34 51 71 47 21 34 61 41 27 48 47 71 41 67
## [12217] 61 48 34 47 41 31 51 37 88 77 67 61 87 81 71 67 61 61 27 37 61 61 34 37
## [12241] 61 31 51 37 61 27 61 67 27 21 61 21 27 34 61 61 27 81 61 81 67 61 61 27
## [12265] 67 61 77 67 67 61 61 61 61 41 48 41 48 41 58 88 47 21 37 27 67 61 18 27
## [12289] 61 61 37 71 34 27 47 51 37 81 71 27 27 37 27 21 48 47 41 51 37 61 81 21
## [12313] 27 61 61 27 37 27 21 34 31 27 21 41 67 61 61 27 21 47 18 67 61 27 21 47
## [12337] 51 71 47 71 27 61 27 41 37 67 61 81 71 61 34 47 51 81 71 27 61 37 27 27
## [12361] 61 34 34 27 47 51 37 61 61 27 37 21 27 81 61 61 34 61 61 47 34 61 51 77
## [12385] 71 47 81 37 61 67 61 87 48 87 47 47 41 81 81 41 27 51 37 48 61 37 34 61
## [12409] 41 61 34 47 27 37 34 47 81 51 34 27 21 47 41 51 77 61 87 81 71 27 27 27
## [12433] 27 34 27 47 51 77 61 87 81 71 27 81 34 34 47 51 47 21 27 37 48 88 27 21
## [12457] 27 21 61 34 47 21 61 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [12481] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 31 47 47 47
## [12505] 47 47 47 47 47 47 47 47 47 47 47 47 47 47 47 47 31 31 34 31 34 34 31 31
## [12529] 31 31 34 34 34 31 34 31 31 31 34 34 31 31 31 31 31 34 31 31 31 31 31 31
## [12553] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 34
## [12577] 31 41 41 34 31 31 31 31 34 31 34 31 87 31 31 34 31 31 31 31 31 34 31 31
## [12601] 31 34 34 34 34 34 31 34 34 31 34 31 31 34 31 31 34 31 31 34 31 41 34 34
## [12625] 31 34 31 31 31 31 34 31 87 31 31 31 31 41 34 31 34 34 31 34 31 87 31 77
## [12649] 77 77 77 77 77 77 77 77 77 77 77 77 77 77 34 34 34 34 34 34 34 34 34 34
## [12673] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [12697] 34 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [12721] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [12745] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [12769] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [12793] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [12817] 51 51 51 51 51 51 51 51 51 34 34 57 51 34 34 34 34 34 34 34 34 34 34 34
## [12841] 57 51 34 57 51 34 34 34 51 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [12865] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [12889] 57 51 34 34 34 34 34 34 34 34 34 34 34 34 57 51 34 34 34 34 34 34 34 34
## [12913] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 57 51 51 34 34 34 51
## [12937] 34 34 34 34 34 57 51 34 34 57 51 34 34 34 34 34 34 34 34 34 34 34 34 34
## [12961] 34 34 34 57 51 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [12985] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [13009] 37 37 57 51 41 47 51 34 47 57 51 57 51 51 57 51 51 51 51 51 51 51 51 51
## [13033] 57 51 51 51 51 41 57 51 34 57 51 51 41 41 41 51 41 51 41 51 51 34 47 57
## [13057] 51 57 51 51 51 57 51 51 57 51 34 47 57 51 41 51 34 51 51 51 34 47 57 51
## [13081] 34 34 34 41 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [13105] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [13129] 34 34 34 34 34 34 34 34 34 34 34 71 71 71 71 71 71 71 71 71 71 71 71 71
## [13153] 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [13177] 71 71 71 31 31 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [13201] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [13225] 37 37 37 37 37 37 37 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [13249] 71 51 51 51 58 47 51 47 48 88 58 58 48 58 88 47 47 58 58 47 51 47 51 47
## [13273] 51 47 48 58 88 47 51 47 51 47 51 47 47 47 47 47 51 47 47 51 47 47 51 47
## [13297] 51 47 51 47 51 47 51 88 47 51 47 51 47 51 47 47 47 51 58 47 51 47 51 47
## [13321] 58 48 58 88 47 51 47 51 51 51 47 51 51 47 51 51 58 48 58 47 51 51 47 51
## [13345] 51 51 48 47 58 51 47 51 47 51 58 88 51 47 51 47 58 51 51 47 58 51 47 51
## [13369] 47 51 47 48 47 58 88 47 51 47 51 47 51 58 48 47 58 88 47 51 58 47 47 51
## [13393] 47 47 51 47 51 58 47 58 51 47 47 51 47 51 47 51 51 58 88 47 47 47 51 47
## [13417] 47 47 51 47 51 47 51 47 51 58 48 58 47 51 51 47 51 47 51 47 47 51 47 51
## [13441] 47 47 47 47 47 58 88 47 47 51 47 51 88 34 27 47 41 31 57 51 37 87 81 27
## [13465] 21 27 34 27 21 47 41 51 37 34 41 27 21 21 21 21 27 27 51 48 41 48 58 88
## [13489] 48 58 88 34 27 47 37 27 41 41 27 37 34 27 37 34 37 21 27 21 27 21 27 21
## [13513] 27 21 37 34 27 47 37 27 21 21 34 47 41 31 27 37 21 34 21 47 41 31 37 27
## [13537] 21 34 27 37 27 21 27 34 27 51 34 37 34 27 21 34 34 47 34 34 27 31 37 87
## [13561] 34 27 21 47 41 31 57 51 77 87 71 27 27 21 37 47 57 51 81 34 27 21 34 27
## [13585] 37 34 27 47 41 51 37 41 48 31 27 37 34 27 27 37 48 21 58 88 34 27 37 34
## [13609] 27 41 31 57 51 81 27 34 27 21 47 41 31 57 51 37 87 81 27 34 27 37 34 27
## [13633] 37 47 21 47 51 34 34 27 37 41 27 37 27 41 51 27 47 51 47 51 47 21 34 27
## [13657] 37 34 27 37 87 27 27 37 34 37 51 41 34 27 34 47 34 27 41 37 34 27 37 27
## [13681] 27 27 34 27 37 34 41 37 27 37 34 34 27 37 37 27 37 27 37 34 27 37 37 27
## [13705] 37 34 27 47 41 37 48 27 34 27 47 51 37 34 27 47 37 34 47 51 37 34 27 47
## [13729] 47 27 27 21 37 27 37 34 27 37 27 37 27 37 27 21 27 21 34 27 37 37 34 27
## [13753] 37 27 37 27 37 27 37 34 27 37 34 27 37 34 27 37 27 34 27 37 27 37 27 21
## [13777] 34 27 21 41 51 37 37 27 34 27 37 27 34 27 31 51 37 34 27 47 41 37 27 37
## [13801] 34 37 37 34 27 37 27 37 27 27 21 27 21 37 27 37 41 27 37 27 27 21 21 48
## [13825] 41 58 88 48 27 37 27 37 27 21 34 34 27 47 41 51 37 27 34 27 37 34 27 47
## [13849] 37 27 21 27 41 34 41 31 57 51 87 48 27 51 57 51 34 27 51 37 51 41 34 27
## [13873] 47 37 47 81 27 48 27 34 27 47 37 34 47 37 27 34 27 37 27 27 34 27 21 27
## [13897] 34 27 21 37 27 47 34 27 34 47 41 31 21 21 21 27 41 48 27 41 37 34 34 21
## [13921] 48 34 27 21 47 41 57 51 37 34 27 47 41 51 37 87 48 34 47 41 31 57 51 37
## [13945] 88 77 61 87 81 34 27 21 47 51 37 34 47 41 31 57 51 77 87 34 27 37 27 37
## [13969] 37 37 37 21 37 34 27 37 27 34 27 37 34 27 27 34 27 47 37 37 34 27 47 41
## [13993] 51 37 34 27 21 21 27 21 34 27 37 48 27 47 51 37 21 37 27 51 27 37 34 27
## [14017] 34 37 34 41 48 41 41 48 47 41 58 88 87 47 27 34 27 27 27 37 27 21 47 37
## [14041] 41 81 27 34 37 27 37 34 27 21 47 41 31 51 37 87 34 27 47 41 51 37 87 27
## [14065] 21 27 34 27 37 27 37 21 27 27 21 48 34 47 41 58 37 87 37 27 37 21 37 34
## [14089] 47 27 37 47 41 57 51 87 21 27 21 34 47 27 21 34 27 34 27 37 34 27 51 37
## [14113] 27 37 27 27 21 34 27 37 27 37 34 27 37 27 21 37 27 34 27 47 51 37 34 27
## [14137] 34 41 27 37 34 47 34 27 47 41 37 21 21 27 37 37 34 41 27 37 27 34 21 47
## [14161] 41 31 57 51 37 77 61 87 81 71 57 51 34 27 21 47 41 31 57 51 37 87 81 34
## [14185] 34 31 77 21 34 27 47 37 27 37 34 27 47 31 57 51 37 77 87 71 27 27 27 88
## [14209] 34 27 47 41 27 34 27 37 34 27 47 41 31 57 51 34 27 34 48 41 57 51 41 81
## [14233] 47 51 34 27 27 37 27 27 37 27 27 21 27 37 34 47 57 51 81 34 47 27 37 27
## [14257] 27 37 34 27 37 34 27 21 47 41 31 57 51 37 77 61 87 81 41 27 21 47 34 27
## [14281] 21 41 37 87 34 27 27 34 34 27 47 41 37 27 34 34 27 21 47 41 31 51 37 77
## [14305] 61 87 27 37 27 27 34 27 21 47 41 51 37 27 37 47 34 47 31 51 34 27 37 34
## [14329] 34 47 34 47 27 27 21 27 37 27 27 21 27 21 27 21 27 37 34 27 21 41 51 37
## [14353] 48 48 34 27 21 47 41 31 57 51 77 87 71 81 21 57 57 57 57 57 57 57 57 57
## [14377] 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57 57
## [14401] 57 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21
## [14425] 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 21 51 51 51 51 51 51 31
## [14449] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
## [14473] 31 31 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
## [14497] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
## [14521] 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27 27
## [14545] 27 27 27 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [14569] 37 37 37 37 37 37 37 37 37 37 37 37 37 61 61 34 27 21 47 41 31 57 51 77
## [14593] 67 61 87 81 71 41 34 27 21 41 31 37 34 27 21 47 41 31 34 27 21 47 41 31
## [14617] 61 61 34 27 21 47 41 31 57 51 77 61 87 81 71 34 47 57 51 77 61 87 81 71
## [14641] 61 61 61 61 34 27 21 47 41 31 57 51 77 61 87 81 71 34 47 41 31 57 51 61
## [14665] 61 61 61 61 61 61 61 61 61 61 57 51 61 71 61 61 61 61 61 61 61 61 61 61
## [14689] 71 61 61 61 61 61 61 61 61 61 57 51 77 61 87 81 71 61 61 61 61 61 61 61
## [14713] 61 61 61 61 87 61 71 61 61 61 57 51 77 61 81 71 61 34 47 41 31 57 51 77
## [14737] 67 61 87 81 71 61 34 27 41 31 57 51 61 81 71 61 61 61 61 61 61 61 61 77
## [14761] 71 61 61 77 61 81 71 61 61 61 61 61 61 61 61 61 61 61 61 61 61 41 34 27
## [14785] 21 47 41 31 57 51 37 77 67 61 87 81 71 34 47 41 31 57 51 77 71 34 47 41
## [14809] 57 51 77 71 61 61 61 61 61 34 27 21 47 41 31 57 51 77 61 87 81 71 61 47
## [14833] 41 57 51 81 61 57 51 77 61 87 81 71 34 27 21 47 41 31 57 51 37 77 67 61
## [14857] 87 81 71 61 61 61 34 27 21 47 41 31 57 51 61 71 61 57 61 81 61 34 27 21
## [14881] 47 41 31 57 51 77 61 87 81 71 61 51 51 51 51 51 51 51 51 51 51 51 51 51
## [14905] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [14929] 51 51 51 51 51 51 51 51 51 51 51 51 57 51 57 71 57 71 57 71 57 71 57 71
## [14953] 57 71 57 51 57 71 57 71 57 51 57 71 57 71 57 71 57 51 57 71 57 57 71 57
## [14977] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
## [15001] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 51 57 71 57 71 57 71 57 71 57
## [15025] 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57 71 57
## [15049] 71 57 71 57 71 57 71 57 51 71 57 71 51 57 71 57 71 57 51 57 71 57 51 57
## [15073] 71 57 51 57 51 57 71 57 71 57 71 57 71 51 57 71 57 51 57 57 57 57 57 57
## [15097] 57 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [15121] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [15145] 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34 34
## [15169] 34 34 34 34 34 34 34 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77 77
## [15193] 77 77 77 77 77 77 77 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
## [15217] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 37 37
## [15241] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [15265] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [15289] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [15313] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [15337] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [15361] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [15385] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 31 31 31 31 31 31 71 71 71
## [15409] 71 71 71 71 71 71 71 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
## [15433] 31 31 31 31 31 31 31 31 31 31 31 31 48 48 88 34 61 47 57 51 81 34 21 48
## [15457] 88 88 37 41 41 81 34 34 47 27 27 27 34 81 27 21 81 81 37 81 34 51 81 27
## [15481] 47 37 41 81 37 81 81 48 41 88 34 47 81 81 34 27 81 34 47 51 37 34 34 57
## [15505] 51 87 41 57 81 47 47 27 81 47 51 87 34 47 51 87 34 81 51 37 81 37 81 34
## [15529] 88 34 34 51 37 81 34 51 88 51 34 37 37 34 37 27 21 34 37 34 81 41 81 37
## [15553] 81 34 37 37 61 81 41 81 58 51 51 34 81 51 34 51 34 47 51 34 47 81 77 87
## [15577] 88 81 81 34 51 34 47 34 51 34 51 41 48 58 47 48 58 41 81 37 34 47 41 58
## [15601] 51 37 87 81 37 88 37 37 88 88 34 37 81 51 37 81 21 34 81 81 81 34 41 48
## [15625] 41 58 57 88 47 51 81 37 37 81 81 37 81 34 47 51 37 81 81 47 41 58 51 37
## [15649] 81 81 37 37 34 27 81 81 47 51 27 81 34 47 51 47 81 81 34 51 88 37 34 37
## [15673] 51 81 81 37 37 81 34 81 81 81 81 81 47 34 51 47 81 37 87 48 47 41 81 81
## [15697] 88 81 81 88 37 51 88 37 37 81 41 81 37 81 81 81 51 51 34 51 81 37 34 47
## [15721] 41 51 81 34 81 81 34 34 51 34 81 81 37 88 21 34 81 21 58 34 34 47 67 61
## [15745] 34 21 27 21 47 57 51 77 61 87 81 71 27 21 21 47 57 61 48 41 48 58 88 58
## [15769] 41 41 27 21 81 67 34 47 37 34 47 21 27 21 27 21 27 21 27 27 21 37 34 47
## [15793] 27 21 34 27 21 21 31 34 34 47 51 81 34 47 37 34 47 34 47 37 48 47 34 47
## [15817] 81 41 34 51 27 34 21 47 51 37 58 34 34 57 51 57 51 71 47 47 47 27 21 61
## [15841] 34 47 51 87 61 34 47 41 31 77 61 87 71 61 34 47 61 87 81 71 34 61 27 37
## [15865] 34 47 51 34 47 51 34 47 34 47 51 87 71 27 37 61 61 34 34 47 41 31 57 51
## [15889] 37 77 67 61 87 81 71 51 47 21 87 27 48 34 27 37 27 34 27 27 27 27 37 27
## [15913] 21 34 21 47 41 31 51 37 67 61 34 27 37 34 47 47 41 51 37 61 81 34 51 27
## [15937] 37 61 61 81 47 18 27 21 67 61 41 67 61 48 58 34 47 31 51 34 47 57 51 71
## [15961] 34 47 31 77 67 34 47 27 21 34 48 41 57 51 51 34 47 51 37 34 47 51 71 61
## [15985] 61 34 47 51 58 67 61 47 48 51 88 34 47 34 47 51 71 34 27 34 47 51 71 47
## [16009] 61 21 34 27 47 41 48 41 58 88 34 47 51 71 48 58 51 37 34 27 47 41 57 37
## [16033] 67 61 18 48 34 47 41 31 58 57 51 37 88 77 67 61 87 81 71 21 47 77 67 61
## [16057] 81 37 61 34 47 37 34 31 51 71 27 67 27 21 21 27 21 34 47 61 81 81 67 61
## [16081] 67 61 67 61 77 67 67 61 61 61 61 41 48 48 41 58 51 34 47 51 37 81 61 27
## [16105] 61 37 71 31 34 27 47 51 71 27 21 34 47 41 51 37 71 81 21 67 61 37 34 31
## [16129] 18 27 21 51 67 61 61 27 21 27 61 21 47 57 51 71 47 57 71 27 21 21 34 47
## [16153] 51 71 27 61 61 34 34 27 47 57 51 37 77 61 87 81 71 34 37 21 51 27 61 34
## [16177] 47 61 61 34 47 51 71 47 81 61 87 48 87 47 47 41 81 58 58 58 37 21 37 34
## [16201] 47 51 34 47 27 34 47 47 51 87 71 34 47 57 51 77 67 61 87 71 34 27 21 47
## [16225] 41 31 57 51 67 61 87 81 71 81 34 34 47 47 21 27 61 27 37 58 21 21 27 21
## [16249] 67 34 47 21 61 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [16273] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [16297] 51 51 51 51 51 51 51 51 51 48 34 27 47 41 57 51 27 27 21 27 27 48 48 48
## [16321] 88 48 48 48 88 27 27 41 41 27 27 34 27 21 27 21 27 27 27 27 27 21 34 27
## [16345] 27 27 34 47 41 57 51 27 27 34 27 47 27 34 27 47 27 41 48 27 27 48 88 27
## [16369] 21 57 51 27 34 27 47 41 57 51 27 27 34 27 27 41 27 27 27 41 34 27 27 27
## [16393] 34 27 27 27 27 27 27 48 88 27 27 27 48 27 27 21 27 48 27 27 34 47 41 51
## [16417] 34 27 27 27 27 27 27 27 34 27 27 27 27 27 27 27 21 41 51 27 34 41 27 27
## [16441] 48 27 27 27 41 27 27 27 21 48 41 88 27 48 27 27 27 21 34 27 27 27 21 34
## [16465] 48 57 51 34 48 41 27 88 48 48 41 27 27 48 34 27 34 48 27 27 34 27 27 41
## [16489] 27 48 34 34 48 34 27 41 27 48 34 47 41 57 51 27 41 57 51 34 27 34 27 48
## [16513] 88 34 27 27 48 27 21 27 27 27 27 27 27 51 27 27 48 34 27 27 41 41 48 41
## [16537] 41 48 41 27 27 27 41 41 27 34 48 27 27 27 27 27 27 27 27 21 27 48 41 88
## [16561] 27 27 27 48 27 27 27 34 27 27 27 21 27 27 27 27 34 34 47 41 27 34 51 27
## [16585] 27 48 27 27 48 34 47 41 57 51 34 27 47 41 57 51 34 27 27 27 27 48 27 27
## [16609] 27 48 41 51 41 27 27 27 88 27 27 27 48 27 41 34 27 47 41 57 51 41 27 27
## [16633] 27 27 34 27 57 51 27 27 21 27 27 27 27 27 27 57 51 27 34 27 27 27 48 27
## [16657] 21 27 21 27 27 48 34 47 57 51 51 77 67 67 27 21 31 77 67 81 71 21 31 21
## [16681] 31 77 21 21 31 21 21 31 21 31 21 31 21 21 31 21 31 77 67 48 48 48 48 88
## [16705] 67 77 67 67 21 21 31 21 31 27 21 31 21 31 21 21 31 21 31 21 21 21 21 31
## [16729] 31 21 31 31 21 21 31 21 31 21 21 31 21 21 21 31 21 31 31 31 31 77 31 67
## [16753] 31 31 31 77 77 27 21 31 77 67 87 71 31 31 21 31 31 77 67 21 31 77 87 31
## [16777] 21 31 48 21 31 31 21 31 21 31 21 31 21 77 67 21 21 31 21 77 67 21 21 31
## [16801] 77 67 31 77 67 77 21 31 67 21 31 77 77 67 31 77 67 77 67 77 77 67 77 67
## [16825] 31 77 67 77 67 31 77 67 67 21 31 77 67 31 21 31 77 67 21 31 77 21 77 21
## [16849] 31 48 21 21 67 67 67 21 21 31 67 77 67 77 67 21 21 31 77 77 77 67 21 31
## [16873] 77 67 21 31 21 21 31 77 67 31 77 67 21 31 21 21 21 31 77 31 31 77 67 67
## [16897] 77 31 77 31 21 31 21 77 21 31 21 77 67 21 67 88 77 67 48 31 21 31 21 31
## [16921] 21 31 77 31 31 31 21 21 77 67 21 77 21 31 31 21 31 48 21 77 31 77 21 31
## [16945] 21 77 77 67 77 67 21 31 21 31 31 48 21 31 21 31 31 77 67 21 34 21 31 21
## [16969] 31 21 31 31 31 48 21 77 48 21 31 77 67 48 31 77 67 21 31 77 67 21 31 77
## [16993] 31 21 31 77 31 31 77 67 77 67 21 31 21 21 31 21 21 21 31 31 21 31 21 31
## [17017] 21 21 21 77 67 77 48 21 31 77 67 21 31 77 67 21 31 77 77 67 77 77 67 71
## [17041] 67 77 67 67 77 67 77 67 67 77 67 67 77 67 77 67 77 67 77 67 77 67 67 77
## [17065] 67 77 48 48 88 21 77 67 21 31 77 67 21 31 31 77 67 77 21 31 77 21 21 48
## [17089] 31 77 67 21 31 21 31 31 21 31 21 31 77 31 77 67 67 31 21 31 77 67 21 21
## [17113] 31 21 31 77 67 21 21 67 21 21 31 21 31 21 31 21 31 77 31 31 31 77 67 21
## [17137] 77 67 21 31 77 21 77 67 31 77 67 21 77 67 21 31 77 67 21 31 21 31 77 67
## [17161] 67 31 21 21 31 77 21 34 21 47 31 77 67 87 81 71 31 77 67 21 77 31 77 31
## [17185] 67 48 21 31 31 21 31 48 67 21 31 67 77 67 21 31 21 31 77 21 77 67 21 21
## [17209] 21 31 67 77 21 21 31 77 21 31 77 67 67 21 21 31 77 67 21 77 21 31 31 21
## [17233] 77 67 48 21 31 77 31 77 21 31 77 67 87 71 21 21 31 77 67 31 21 31 77 31
## [17257] 67 21 77 67 21 31 31 31 21 31 67 77 77 67 21 21 31 21 21 31 48 31 31 48
## [17281] 67 34 21 31 77 67 87 81 71 77 21 77 67 31 58 41 51 41 41 88 88 58 88 88
## [17305] 41 41 41 41 41 41 41 41 41 41 41 41 41 41 58 88 41 51 41 47 41 48 88 41
## [17329] 87 41 51 87 41 47 41 41 41 41 41 41 41 87 48 88 41 41 41 41 51 87 48 41
## [17353] 58 88 41 41 48 41 41 41 41 47 41 51 88 41 41 41 51 88 41 41 41 41 41 41
## [17377] 48 47 41 58 57 51 88 41 41 41 41 88 48 41 58 88 41 48 41 41 41 41 41 41
## [17401] 48 41 51 41 51 87 41 41 41 41 41 41 48 41 51 87 41 41 41 41 87 41 41 41
## [17425] 51 34 41 31 57 71 41 34 41 31 57 77 87 71 34 71 77 87 41 31 57 71 34 41
## [17449] 31 87 34 87 34 34 34 34 34 71 71 34 57 71 71 34 34 34 34 34 71 34 41 31
## [17473] 34 77 87 71 47 71 34 41 31 57 71 34 41 31 77 87 34 34 41 31 57 77 87 71
## [17497] 31 31 31 31 31 21 31 31 31 31 31 31 31 77 87 77 87 31 31 31 31 31 31 31
## [17521] 31 31 87 31 31 31 87 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31
## [17545] 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 77 87 31 31 31 31 31 77
## [17569] 31 31 31 31 31 77 87 31 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71 71
## [17593] 71 71 71 34 34 34 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [17617] 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51 37 37 37
## [17641] 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37 37
## [17665] 37 37 37 37 37 37 37 37 37 51 51 51 51 51 51 51 51 51 51 51 51 51 51 51
## [17689] 51 51 51 51
## Levels: 18 21 27 31 34 37 41 47 48 51 57 58 61 67 71 77 81 87 88
```


We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy<- fisheries %>%
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
table(fisheries_tidy$country)
```

```
## 
##                   Albania                   Algeria            American Samoa 
##                       934                      1561                       556 
##                    Angola                  Anguilla       Antigua and Barbuda 
##                      2119                       129                       356 
##                 Argentina                     Aruba                 Australia 
##                      3403                       172                      8183 
##                   Bahamas                   Bahrain                Bangladesh 
##                       423                      1169                       169 
##                  Barbados                   Belgium                    Belize 
##                       795                      2530                      1075 
##                     Benin                   Bermuda  Bonaire/S.Eustatius/Saba 
##                      1419                       846                         4 
##    Bosnia and Herzegovina                    Brazil  British Indian Ocean Ter 
##                        21                      4784                        97 
##    British Virgin Islands         Brunei Darussalam                  Bulgaria 
##                       332                       186                      1596 
##          C<f4>te d'Ivoire                Cabo Verde                  Cambodia 
##                      1859                       462                       238 
##                  Cameroon                    Canada            Cayman Islands 
##                      1340                      5099                        84 
##           Channel Islands                     Chile                     China 
##                      1313                      3878                      2801 
##      China, Hong Kong SAR          China, Macao SAR                  Colombia 
##                      1782                       206                      2710 
##                   Comoros   Congo, Dem. Rep. of the        Congo, Republic of 
##                       965                       484                      1527 
##              Cook Islands                Costa Rica                   Croatia 
##                       810                      1171                       947 
##                      Cuba                Cura<e7>ao                    Cyprus 
##                      2981                        18                      1703 
##                   Denmark                  Djibouti                  Dominica 
##                      3741                       352                       213 
##        Dominican Republic                   Ecuador                     Egypt 
##                      1958                      1595                      2467 
##               El Salvador         Equatorial Guinea                   Eritrea 
##                       620                       551                       653 
##                   Estonia                  Ethiopia    Falkland Is.(Malvinas) 
##                      1088                       129                       502 
##             Faroe Islands         Fiji, Republic of                   Finland 
##                      2283                      1798                       706 
##                    France             French Guiana          French Polynesia 
##                     10639                       231                       672 
##      French Southern Terr                     Gabon                    Gambia 
##                       139                      1089                      1214 
##                   Georgia                   Germany                     Ghana 
##                       428                      4813                      2462 
##                 Gibraltar                    Greece                 Greenland 
##                        61                      4091                      1311 
##                   Grenada                Guadeloupe                      Guam 
##                      1635                       372                       520 
##                 Guatemala                    Guinea              GuineaBissau 
##                       622                       697                       634 
##                    Guyana                     Haiti                  Honduras 
##                       251                       204                       842 
##                   Iceland                     India                 Indonesia 
##                      2346                      5588                      9274 
##    Iran (Islamic Rep. of)                      Iraq                   Ireland 
##                      1210                       150                      3235 
##               Isle of Man                    Israel                     Italy 
##                       952                      1359                      4567 
##                   Jamaica                     Japan                    Jordan 
##                       149                     15429                       226 
##                     Kenya                  Kiribati  Korea, Dem. People's Rep 
##                       958                       875                       210 
##        Korea, Republic of                    Kuwait                    Latvia 
##                     10824                       805                      1101 
##                   Lebanon                   Liberia                     Libya 
##                       614                      1514                       578 
##                 Lithuania                Madagascar                  Malaysia 
##                      1274                      1008                      6963 
##                  Maldives                     Malta          Marshall Islands 
##                       487                      2156                       292 
##                Martinique                Mauritania                 Mauritius 
##                       672                      1501                       991 
##                   Mayotte                    Mexico Micronesia, Fed.States of 
##                       194                      6202                       413 
##                    Monaco                Montenegro                Montserrat 
##                        43                       168                        63 
##                   Morocco                Mozambique                   Myanmar 
##                      4758                       434                       117 
##                   Namibia                     Nauru               Netherlands 
##                       905                       150                      2944 
##      Netherlands Antilles             New Caledonia               New Zealand 
##                       338                       789                      4594 
##                 Nicaragua                   Nigeria                      Niue 
##                       904                      1479                       145 
##            Norfolk Island      Northern Mariana Is.                    Norway 
##                        41                       488                      3747 
##                      Oman                 Other nei                  Pakistan 
##                      1086                      1556                      2166 
##                     Palau   Palestine, Occupied Tr.                    Panama 
##                       636                       429                      1773 
##          Papua New Guinea                      Peru               Philippines 
##                       686                      2767                      4548 
##          Pitcairn Islands                    Poland                  Portugal 
##                        63                      2553                     11570 
##               Puerto Rico                     Qatar                R<e9>union 
##                       918                       941                       736 
##                   Romania        Russian Federation       Saint Barth<e9>lemy 
##                      1738                      4736                         6 
##              Saint Helena     Saint Kitts and Nevis               Saint Lucia 
##                       609                       397                       558 
##  Saint Vincent/Grenadines               SaintMartin                     Samoa 
##                       715                         6                       386 
##     Sao Tome and Principe              Saudi Arabia                   Senegal 
##                      1035                      2200                      2988 
##     Serbia and Montenegro                Seychelles              Sierra Leone 
##                       516                      1142                      1526 
##                 Singapore              Sint Maarten                  Slovenia 
##                      1937                         4                       644 
##           Solomon Islands                   Somalia              South Africa 
##                       505                       141                      3881 
##                     Spain                 Sri Lanka   St. Pierre and Miquelon 
##                     17482                      1351                      1038 
##                     Sudan            Sudan (former)                  Suriname 
##                         3                        90                       234 
##    Svalbard and Jan Mayen                    Sweden      Syrian Arab Republic 
##                        41                      3115                       793 
##  Taiwan Province of China  Tanzania, United Rep. of                  Thailand 
##                      9927                      1277                      4843 
##                TimorLeste                      Togo                   Tokelau 
##                        98                      1723                       102 
##                     Tonga       Trinidad and Tobago                   Tunisia 
##                       403                       923                      3019 
##                    Turkey      Turks and Caicos Is.                    Tuvalu 
##                      3326                       193                       162 
##                   Ukraine        Un. Sov. Soc. Rep.      United Arab Emirates 
##                      1823                      7084                      1801 
##            United Kingdom  United States of America                   Uruguay 
##                      6577                     18080                      2134 
##         US Virgin Islands                   Vanuatu   Venezuela, Boliv Rep of 
##                       348                       789                      3409 
##                  Viet Nam     Wallis and Futuna Is.                     Yemen 
##                       405                       128                      1278 
##            Yugoslavia SFR                  Zanzibar 
##                      1383                       247
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_focus<-fisheries_tidy%>%
  select(country,isscaap_taxonomic_group, asfis_species_name,asfis_species_number, year, catch)
fisheries_focus
```

```
## # A tibble: 376,771 x 6
##    country isscaap_taxonomic_group asfis_species_n~ asfis_species_n~  year catch
##    <chr>   <chr>                   <chr>            <chr>            <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1995    NA
##  2 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1996    53
##  3 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1997    20
##  4 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1998    31
##  5 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        1999    30
##  6 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2000    30
##  7 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2001    16
##  8 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2002    79
##  9 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2003     1
## 10 Albania Sharks, rays, chimaeras Squatinidae      10903XXXXX        2004     4
## # ... with 376,761 more rows
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_focus %>%
summarize(n_species=n_distinct(asfis_species_name))
```

```
## # A tibble: 1 x 1
##   n_species
##       <int>
## 1      1546
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>%
  select(country,catch,year) %>%
  filter(year ==2000) %>%
  arrange(desc(catch))
```

```
## # A tibble: 8,793 x 3
##    country                  catch  year
##    <chr>                    <dbl> <dbl>
##  1 China                     9068  2000
##  2 Peru                      5717  2000
##  3 Russian Federation        5065  2000
##  4 Viet Nam                  4945  2000
##  5 Chile                     4299  2000
##  6 China                     3288  2000
##  7 China                     2782  2000
##  8 United States of America  2438  2000
##  9 China                     1234  2000
## 10 Philippines                999  2000
## # ... with 8,783 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy %>%
  select(country,catch,year, asfis_species_name) %>%
  filter(between(year,1990,2000)) %>%
  filter(asfis_species_name =="Sardina pilchardus") %>%
  arrange(desc(catch))
```

```
## # A tibble: 336 x 4
##    country            catch  year asfis_species_name
##    <chr>              <dbl> <dbl> <chr>             
##  1 Morocco              947  1994 Sardina pilchardus
##  2 Morocco              925  1996 Sardina pilchardus
##  3 Spain                912  1996 Sardina pilchardus
##  4 Morocco              859  2000 Sardina pilchardus
##  5 Morocco              845  1990 Sardina pilchardus
##  6 Morocco              827  1991 Sardina pilchardus
##  7 Morocco              723  1998 Sardina pilchardus
##  8 Morocco              710  1993 Sardina pilchardus
##  9 Russian Federation   627  1992 Sardina pilchardus
## 10 Russian Federation   579  1991 Sardina pilchardus
## # ... with 326 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy %>%
  select(country,catch,year, asfis_species_name) %>%
  filter(between(year,2008,2012)) %>%
  filter(asfis_species_name =="Cephalopoda") %>%
  arrange(desc(catch))
```

```
## # A tibble: 80 x 4
##    country catch  year asfis_species_name
##    <chr>   <dbl> <dbl> <chr>             
##  1 India      94  2011 Cephalopoda       
##  2 India      93  2010 Cephalopoda       
##  3 India      88  2012 Cephalopoda       
##  4 China      86  2008 Cephalopoda       
##  5 China      74  2010 Cephalopoda       
##  6 Italy      66  2012 Cephalopoda       
##  7 India      62  2009 Cephalopoda       
##  8 India      61  2009 Cephalopoda       
##  9 India      60  2010 Cephalopoda       
## 10 Spain      57  2008 Cephalopoda       
## # ... with 70 more rows
```



9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fisheries_tidy %>%
  select(catch,year, asfis_species_name) %>%
  filter(between(year,2008,2012)) %>%
  arrange(desc(catch))
```

```
## # A tibble: 51,014 x 3
##    catch  year asfis_species_name   
##    <dbl> <dbl> <chr>                
##  1  9806  2010 Osteichthyes         
##  2  9613  2012 Osteichthyes         
##  3  8898  2009 Osteichthyes         
##  4  8221  2011 Trichiurus lepturus  
##  5  8188  2012 Theragra chalcogramma
##  6  7981  2008 Engraulis ringens    
##  7  7873  2008 Clupea harengus      
##  8  7250  2009 Clupea harengus      
##  9  6880  2012 Engraulis ringens    
## 10  6841  2010 Trichiurus lepturus  
## # ... with 51,004 more rows
```

10. Use the data to do at least one analysis of your choice.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
