---
title: "Lab 4 Homework"
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

## Load the tidyverse

```r
library(tidyverse)
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe~
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent~
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino~
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini~
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"~
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli~
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu~
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt~
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", ~
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,~
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,~
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3~
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,~
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range~
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",~
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect~
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi~
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car~
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3~
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N~
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, ~
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA~
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20~
```

```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
homerange<-clean_names(homerange)
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
class(homerange$taxon)
```

```
## [1] "character"
```

```r
taxon<-as.factor(homerange$taxon)
```

```r
is.factor(taxon)
```

```
## [1] TRUE
```


```r
class(homerange$order)
```

```
## [1] "character"
```

```r
order<-as.factor(homerange$order)
```

```r
is.factor(order)
```

```
## [1] TRUE
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa<- select(homerange, taxon:species)
taxa
```

```
## # A tibble: 569 x 7
##    taxon         common_name             class        order family genus species
##    <chr>         <chr>                   <chr>        <chr> <chr>  <chr> <chr>  
##  1 lake fishes   american eel            actinoptery~ angu~ angui~ angu~ rostra~
##  2 river fishes  blacktail redhorse      actinoptery~ cypr~ catos~ moxo~ poecil~
##  3 river fishes  central stoneroller     actinoptery~ cypr~ cypri~ camp~ anomal~
##  4 river fishes  rosyside dace           actinoptery~ cypr~ cypri~ clin~ fundul~
##  5 river fishes  longnose dace           actinoptery~ cypr~ cypri~ rhin~ catara~
##  6 river fishes  muskellunge             actinoptery~ esoc~ esoci~ esox  masqui~
##  7 marine fishes pollack                 actinoptery~ gadi~ gadid~ poll~ pollac~
##  8 marine fishes saithe                  actinoptery~ gadi~ gadid~ poll~ virens 
##  9 marine fishes lined surgeonfish       actinoptery~ perc~ acant~ acan~ lineat~
## 10 marine fishes orangespine unicornfish actinoptery~ perc~ acant~ naso  litura~
## # ... with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(taxa$common_name)
```

```
## 
##                         aardwolf                 Abert's squirrel 
##                                1                                1 
##                   Abert's towhee                Aesculapian snake 
##                                1                                1 
##   African brush-tailed porcupine            African bush elephant 
##                                1                                1 
##              allied rock-wallaby                  American badger 
##                                1                                1 
##                   American bison                     american eel 
##                                1                                1 
##         American gray flycatcher                 American kestrel 
##                                1                                1 
##                  American marten                    American pika 
##                                1                                1 
##            American red squirrel                American redstart 
##                                1                                1 
##            American tree sparrow          American yellow warbler 
##                                1                                1 
##            Anegada ground iguana          Angel island chuckwalla 
##                                1                                1 
##              antilopine kangaroo                       arctic fox 
##                                1                                1 
##           arctic ground squirrel                      Arctic hare 
##                                1                                1 
##                     arctic shrew                           argali 
##                                1                                1 
##                   Armenian viper                   Asian elephant 
##                                1                                1 
##                  atlantic salmon        atlantic sharpnose puffer 
##                                1                                1 
##               australian gregory           Bahamian Andros iguana 
##                                1                                1 
##                    ballan wrasse             banded ground-cuckoo 
##                                1                                1 
##                   banded sculpin       banner-tailed kangaroo rat 
##                                1                                1 
##                    barbary sheep                         barn owl 
##                                1                                1 
##                 barred sand bass                       bay dikier 
##                                1                                1 
##                     beech marten                     Bell's vireo 
##                                1                                1 
##                     bermuda chub                   Berwick's wren 
##                                1                                1 
##               bicolor damselfish                    bighorn sheep 
##                                1                                1 
##           black-capped chickadee               black-capped vireo 
##                                1                                1 
##              black-footed ferret            black-striped wallaby 
##                                1                                1 
##          black-tailed jackrabbit     black-throated green warbler 
##                                1                                1 
##                    black grouper                     black grouse 
##                                1                                1 
##                 black rhinoceros                   black rockfish 
##                                1                                1 
##                 black woodpecker             Blackburnian warbler 
##                                1                                1 
##                  blackear wrasse                    blackeye goby 
##                                1                                1 
##                       blacksnake               blacktail redhorse 
##                                1                                1 
##          blacktailed rattlesnake                Blanding's turtle 
##                                1                                1 
##                      blue iguana                    blue rockfish 
##                                1                                1 
##                  bluebanded goby                         bluegill 
##                                1                                1 
##                  bluehead wrasse            bluespine unicornfish 
##                                1                                1 
##        bluestreak cleaner wrasse                           bobcat 
##                                1                                1 
##                  Bonelli's eagle                     booted eagle 
##                                1                                1 
##                       boreal owl            Botta's pocket gopher 
##                                1                                1 
##              Brazilian porcupine        bridled nail-tail wallaby 
##                                1                                1 
##              broad-toothed mouse                broadheaded snake 
##                                1                                1 
##                 brown antechinus                      brown trout 
##                                1                                1 
##                  brown wood rail                         bushbuck 
##                                1                                1 
##        bushmanland tent tortoise             bushy-tailed woodrat 
##                                1                                1 
##             butlers garter snake                          cabezon 
##                                1                                1 
##       California ground squirrel            california sheepshead 
##                                1                                1 
##                  California vole                      Canada lynx 
##                                1                                1 
##                   Canada warbler                    canary damsel 
##                                1                                1 
##                    canyon towhee               cape dune mole rat 
##                                1                                1 
##                       cape genet                        cape hare 
##                                1                                1 
##                    cape mole rat                   cape porcupine 
##                                1                                1 
##                          caracal                         caracara 
##                                1                                1 
##               Carolina chickadee                    Carolina wren 
##                                1                                1 
##                              cat              central stoneroller 
##                                1                                1 
##                  Chacoan peccary                          chamois 
##                                1                                1 
##                checkered snapper                          cheetah 
##                                1                                1 
##                       cherubfish           chestnut-sided warbler 
##                                1                                1 
##            chevron butterflyfish                   chicken turtle 
##                                1                                1 
##                chinese pit viper                 chipping sparrow 
##                                1                                1 
##                           chital                   cinereus shrew 
##                                1                                1 
##                     clown wrasse                        coachwhip 
##                                1                                1 
##                 cocoa damselfish                 collared peccary 
##                                1                                1 
##                Colorado chipmunk        Columbian ground squirrel 
##                                1                                1 
##                           comber          common brushtail possum 
##                                1                                1 
##                   common buzzard                 common chaffinch 
##                                1                                1 
##                common chuckwalla                    common cuckoo 
##                                1                                1 
##            common dwarf mongoose                     common eland 
##                                1                                1 
##                 common firecrest                     common genet 
##                                1                                1 
##                    common linnet                  common mole rat 
##                                1                                1 
##                     common raven                  common redstart 
##                                1                                1 
##           common snapping turtle                  common wallaroo 
##                                1                                1 
##                    common wombat               common wood pigeon 
##                                1                                1 
##              common yellowthroat                    Cooper's hawk 
##                                1                                1 
##                  copper rockfish           copperbelly watersnake 
##                                1                                1 
##                       copperhead                    coral grouper 
##                                1                                1 
##                       coral hind                      coral trout 
##                                1                                1 
##                        corncrake                           coruro 
##                                1                                1 
##                     cotton mouse                      cottonmouth 
##                                1                                1 
##                           cougar                    crowned shrew 
##                                1                                1 
##                           culpeo                           cunner 
##                                1                                1 
##                  cutthroat trout               Cuvier's spiny rat 
##                                1                                1 
##      Dalh's toad-headed tortoise              Damaraland mole rat 
##                                1                                1 
##                       damselfish                 Dartford warbler 
##                                1                                1 
##                    desert iguana                  desert tortoise 
##                                1                                1 
##                   desert warthog                   desert woodrat 
##                                1                                1 
##             dusky-footed woodrat                    dusky grouper 
##                                1                                1 
##                     dusky grouse          dwarf fat-tailed jerboa 
##                                1                                1 
##                   dwarf hawkfish            east African mole rat 
##                                1                                1 
##                  eastern bettong                 eastern bluebird 
##                                1                                1 
##               eastern cottontail            eastern gray squirrel 
##                                1                                1 
##            Eastern grey kangaroo             eastern indigo snake 
##                                1                                1 
##                 eastern kingbird                Eastern kingsnake 
##                                1                                1 
##       Eastern long-necked turtle               eastern meadowlark 
##                                1                                1 
##                     eastern mole               Eastern mud turtle 
##                                1                                1 
##   Eastern spiny softshell turtle eastern triangular butterflyfish 
##                                1                                1 
##               eastern wood pewee               eastern worm snake 
##                                1                                1 
##                Egyptian mongoose                Egyptian tortoise 
##                                1                                1 
##                 Egyptian vulture       elegant fat-tailed opossum 
##                                1                                1 
##                   Ethiopian wolf               Eurasian eagle-owl 
##                                1                                1 
##                    Eurasian lynx               Eurasian pygmy owl 
##                                1                                1 
##             Eurasian sparrowhawk   Eurasian three-toed woodpecker 
##                                1                                1 
##             Eurasian treecreeper                    Eurasian wren 
##                                1                                1 
##                 Eurasian wryneck                   European bison 
##                                1                                1 
##        European green woodpecker                    European hare 
##                                1                                1 
##                European hedgehog                 European kestrel 
##                                1                                1 
##                    European mink                    European mole 
##                                1                                1 
##                European nightjar                European nuthatch 
##                                1                                1 
##             European pine marten             European pond turtle 
##                                1                                1 
##                  European rabbit                  European roller 
##                                1                                1 
##                 european seabass                   European serin 
##                                1                                1 
##             European turtle dove               European whipsnake 
##                                1                                1 
##                      fallow deer                     fer-de-lance 
##                                1                                1 
##                           ferret                       field vole 
##                                1                                1 
##                           fisher                            fossa 
##                                1                                1 
##         four-toed elephant shrew                     fox squirrel 
##                                1                                1 
##       Franklin's ground squirrel             G<fc>nther's dik-dik 
##                                1                                1 
##                          gadwall            Galapagos land iguana 
##                                1                                1 
##                   Geoffroy's cat              giant garter snakes 
##                                1                                1 
##                giant golden mole               giant kangaroo rat 
##                                1                                1 
##                      giant panda                   giant trevally 
##                                1                                1 
##                       gila trout                gilthead seabream 
##                                1                                1 
##                          giraffe                             goat 
##                                1                                1 
##                        goldcrest     golden-rumped elephant shrew 
##                                1                                1 
##                 golden bandicoot                     golden eagle 
##                                1                                1 
##                     gopher snake                  gopher tortoise 
##                                1                                1 
##              Grant's golden mole                      grass snake 
##                                1                                1 
##              grasshopper sparrow                     gray snapper 
##                                1                                1 
##                          graysby                   greasy grouper 
##                                1                                1 
##                    great bittern                 great horned owl 
##                                1                                1 
##            great plains ratsnake             great spotted cuckoo 
##                                1                                1 
##                   greater glider                   greater grison 
##                                1                                1 
##                     greater kudu          greater prairie-chicken 
##                                1                                1 
##                     greater rhea               greater roadrunner 
##                                1                                1 
##       greater white-footed shrew           grey-headed woodpecker 
##                                1                                1 
##                   grey partridge                        groundhog 
##                                1                                1 
##             half-banded seaperch                       hartebeest 
##                                1                                1 
##                   hazel dormouse                     hazel grouse 
##                                1                                1 
##                      hen harrier             High Mountain Lizard 
##                                1                                1 
##                    hognose snake                           hoopoe 
##                                1                                1 
##                            horse                       house wren 
##                                1                                1 
##                  humphead wrasse                     Iberian lynx 
##                                1                                1 
##                           impala               impressed tortoise 
##                                1                                1 
##                        inca dove         Indian crested porcupine 
##                                1                                1 
##               Indian desert jird                      Indian hare 
##                                1                                1 
##                   indigo bunting                     island mouse 
##                                1                                1 
##                           jaguar                       jaguarundi 
##                                1                                1 
##          japanese black rockfish              japanese shrimpgoby 
##                                1                                1 
##                Japanese squirrel                           kakapo 
##                                1                                1 
##                        kelp bass                        king rail 
##                                1                                1 
##                         kinkajou               Kirtland's warbler 
##                                1                                1 
##                          kit fox                      land mullet 
##                                1                                1 
##                    lanner falcon            large-headed rice rat 
##                                1                                1 
##               large indian civet                  largemouth bass 
##                                1                                1 
##                    least bittern                   least chipmunk 
##                                1                                1 
##                 least flycatcher                     least weasel 
##                                1                                1 
##                          leopard                      leopard cat 
##                                1                                1 
##                 leopard tortoise               lesser grey shrike 
##                                1                                1 
##                      lesser rhea                lined surgeonfish 
##                                1                                1 
##                       little owl                loggerhead shrike 
##                                1                                1 
##                long-clawed shrew              long-eared hedgehog 
##                                1                                1 
##                   long-eared owl              long-footed potoroo 
##                                1                                1 
##            long-snouted seahorse                  long-tailed tit 
##                                1                                1 
##               long-tailed weasel                  longear sunfish 
##                                1                                1 
##                  longfinned goby                    longnose dace 
##                                1                                1 
##         Lumholtz's tree-kangaroo                 magnolia warbler 
##                                1                                1 
##               Malagasy giant rat                      maned sloth 
##                                1                                1 
##                     maori wrasse                           margay 
##                                1                                1 
##                Marmora's warbler                   marsh mongoose 
##                                1                                1 
##                     marsh rabbit                        marsh tit 
##                                1                                1 
##                      meadow vole     mediterranean rainbow wrasse 
##                                1                                1 
##           mediterranean tortoise                melodious warbler 
##                                1                                1 
##              melon butterflyfish           Merriam's kangaroo rat 
##                                1                                1 
##       middle spotted woodpeckers         midget faded rattlesnake 
##                                1                                1 
##           midland painted turtle                        milksnake 
##                                1                                1 
##               Mojave rattlesnake                Montagu's harrier 
##                                1                                1 
##                     montane vole                      moon wrasse 
##                                1                                1 
##                            moose                  mottled sculpin 
##                                1                                1 
##                  mountain beaver                 mountain gazelle 
##                                1                                1 
##                    mountain goat                    mountain hare 
##                                1                                1 
##                 mourning warbler                        mule deer 
##                                1                                1 
##                      muskellunge                          muskrat 
##                                1                                1 
##                   mutton snapper                   naked mole rat 
##                                1                                1 
##              namaqua dwarf adder                   nassau grouper 
##                                1                                1 
##         North American porcupine              northern brown kiwi 
##                                1                                1 
##         Northern flying squirrel                 Northern goshawk 
##                                1                                1 
##      northern hairy-nosed wombat             northern mockingbird 
##                                1                                1 
##           Northern parl squirrel   Northern three-striped opossum 
##                                1                                1 
##              Northern watersnake                northern wheatear 
##                                1                                1 
##                     Oak titmouse                  ocean whitefish 
##                                1                                1 
##                           ocelot                            okapi 
##                                1                                1 
##          orangespine unicornfish               Ord's kangaroo rat 
##                                1                                1 
##                ornate box turtle                   ornate tinamou 
##                                1                                1 
##                          ostrich                         ovenbird 
##                                1                                1 
##                    oystercatcher                   painted comber 
##                                1                                1 
##                      pampas deer                  Patagonian mara 
##                                1                                1 
##                     peacock hind                 peregrine falcon 
##                                1                                1 
##             Peruvian plantcutter                   Peter's dukier 
##                                1                                1 
##                       pine snake                  plains viscacha 
##                                1                                1 
##                     plateau pika                          pollack 
##                                1                                1 
##                   prairie falcon                     prairie vole 
##                                1                                1 
##                        pronghorn             prothonotary warbler 
##                                1                                1 
##                             pudu                      pumpkinseed 
##                                1                                1 
##                     pygmy rabbit               quillback rockfish 
##                                1                                1 
##                            racer                    rainbow trout 
##                                1                                1 
##                red-backed shrike          red-crowned ant tanager 
##                                1                                1 
##                   red-eyed vireo              red-footed tortoise 
##                                1                                1 
##             red-legged pademelon             red-necked pademelon 
##                                1                                1 
##               red-necked wallaby              red-shouldered hawk 
##                                1                                1 
##                  red-tailed hawk         red-throated ant tanager 
##                                1                                1 
##            red-throated caracara                red bush squirrel 
##                                1                                1 
##                         red deer                      red grouper 
##                                1                                1 
##                         red hind                     red kangaroo 
##                                1                                1 
##                         red kite                         red moki 
##                                1                                1 
##                        red panda                     red squirrel 
##                                1                                1 
##               redbacked ratsnake               redband parrotfish 
##                                1                                1 
##                  redbanded perch                redfin parrotfish 
##                                1                                1 
##                    redlip blenny              redspotted hawkfish 
##                                1                                1 
##               redtail parrotfish                 Reeves's muntjac 
##                                1                                1 
##                         reindeer                   ringneck snake 
##                                1                                1 
##             rivulated parrotfish                        rock bass 
##                                1                                1 
##                    rock squirrel                         roe deer 
##                                1                                1 
##                       Roman mole                    rosyside dace 
##                                1                                1 
##            rufous elephant shrew                     Ruppel's fox 
##                                1                                1 
##          Russian steppe tortoise                       rusty goby 
##                                1                                1 
##                      sage grouse                           saithe 
##                                1                                1 
##                           salema         salt marsh harvest mouse 
##                                1                                1 
##             schoolmaster snapper                          sculpin 
##                                1                                1 
##                           serval               sharp-shinned hawk 
##                                1                                1 
##           short-toed snake eagle           Siberian brown lemming 
##                                1                                1 
##                Siberian chipmunk                  Siberian weasel 
##                                1                                1 
##                       sidewinder                        sika deer 
##                                1                                1 
##                 silvery mole rat                    slender shrew 
##                                1                                1 
##                    slippery dick                       sloth bear 
##                                1                                1 
##                  smallmouth bass                     snow leopard 
##                                1                                1 
##                    snowshoe hare                        snowy owl 
##                                1                                1 
##                  snubnosed viper          South American gray fox 
##                                1                                1 
##             southern bog lemming         Southern brown bandicoot 
##                                1                                1 
##         Southern flying squirrel       southern grasshopper mouse 
##                                1                                1 
##          Southern plains woodrat       southwestern carpet python 
##                                1                                1 
##                  spanish hogfish                     Spanish ibex 
##                                1                                1 
##              Spanish pond turtle              spectacled dormouse 
##                                1                                1 
##    Speke's hinge-backed tortoise                spiny tail lizard 
##                                1                                1 
##               spotted flycatcher          spotted ground squirrel 
##                                1                                1 
##               spotted nutcracker            spur-thighed tortoise 
##                                1                                1 
##                  star-nosed mole                         steenbok 
##                                1                                1 
##             steephead parrotfish           Stephen's kangaroo rat 
##                                1                                1 
##                  stinkpot turtle                            stoat 
##                                1                                1 
##             stoplight parrotfish         streaked fantail warbler 
##                                1                                1 
##        stripe-necked musk turtle          striped ground squirrel 
##                                1                                1 
##               striped parrotfish                  Swainson's hawk 
##                                1                                1 
##                     swamp rabbit                    swamp wallaby 
##                                1                                1 
##                        swift fox          Tahititan butterflyfish 
##                                1                                1 
##                        tawny owl                            tayra 
##                                1                                1 
##           teardrop butterflyfish                  Tenerife lizard 
##                                1                                1 
##   thick-tailed three-toed jerboa   thirteen-lined ground squirrel 
##                                1                                1 
##               thumbprint emperor                            tiger 
##                                1                                1 
##                      tiger quoll                tiger rattlesnake 
##                                1                                1 
##                      tiger snake               timber rattlesnake 
##                                1                                1 
##                 Tome's spiny rat           tooth-billed bowerbird 
##                                1                                1 
##              travancore tortoise         twin-spotted rattlesnake 
##                                1                                1 
##              twinspot damselfish                   Uinta chipmunk 
##                                1                                1 
##                     wards damsel                 water chevrotain 
##                                1                                1 
##                       water vole        Western Bonelli's warbler 
##                                1                                1 
##             western capercaillie              western diamondback 
##                                1                                1 
##            Western grey kangaroo               western meadowlard 
##                                1                                1 
##                    Western quoll                 western ratsnake 
##                                1                                1 
##          western red-backed vole               western worm snake 
##                                1                                1 
##           western yellow wagtail                         whinchat 
##                                1                                1 
##          white-backed woodpecker     White-bellied<U+00A0>nesomys 
##                                1                                1 
##                 white-eyed vireo             white-footed dunnart 
##                                1                                1 
##             white-lipped peccary                white-tailed deer 
##                                1                                1 
##            white-tailed mongoose                    white crappie 
##                                1                                1 
##                   white goatfish                 white rhinoceros 
##                                1                                1 
##                    white wagtail             whitesaddle goatfish 
##                                1                                1 
##              whitetail dascyllus                          wildcat 
##                                1                                1 
##                 willow ptarmigan                        wolverine 
##                                1                                1 
##                     wood lemming                       wood mouse 
##                                1                                1 
##                  woodchat shrike                    woodland vole 
##                                1                                1 
##                         woodlark                    worm pipefish 
##                                1                                1 
##                          wrentit            yellow-bellied marmot 
##                                1                                1 
##       yellow-blotched map turtle             yellow-breasted chat 
##                                1                                1 
##              yellow-necked mouse             yellow-pine chipmunk 
##                                1                                1 
##             yellow bellied racer                  yellow bullhead 
##                                1                                1 
##                  yellow mongoose                     yellow perch 
##                                1                                1 
##                   yellowfin hind                yellowhead wrasse 
##                                1                                1 
##               yellowtail snapper 
##                                1
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$trophic_guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivore<-filter(homerange,trophic_guild=="carnivore")
```

```r
herbivore<-filter(homerange,trophic_guild=="herbivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
carnivore_mean<-select(carnivore, mean_hra_m2)
```

```r
mean(carnivore_mean$mean_hra_m2)
```

```
## [1] 13039918
```

```r
herbivore_mean<-select(herbivore, mean_hra_m2)
```

```r
mean(herbivore_mean$mean_hra_m2)
```

```
## [1] 34137012
```
**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer<-filter(homerange,family=="cervidae")
```

```r
colnames(deer)
```

```
##  [1] "taxon"                      "common_name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "n"                          "mean_mass_g"               
## [11] "log10_mass"                 "alternative_mass_reference"
## [13] "mean_hra_m2"                "log10_hra"                 
## [15] "hra_reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic_guild"              "dimension"                 
## [21] "preymass"                   "log10_preymass"            
## [23] "ppmr"                       "prey_size_reference"
```


```r
select(deer, mean_mass_g,log10_mass,family,genus,species)
```

```
## # A tibble: 12 x 5
##    mean_mass_g log10_mass family   genus      species    
##          <dbl>      <dbl> <chr>    <chr>      <chr>      
##  1     307227.       5.49 cervidae alces      alces      
##  2      62823.       4.80 cervidae axis       axis       
##  3      24050.       4.38 cervidae capreolus  capreolus  
##  4     234758.       5.37 cervidae cervus     elaphus    
##  5      29450.       4.47 cervidae cervus     nippon     
##  6      71450.       4.85 cervidae dama       dama       
##  7      13500.       4.13 cervidae muntiacus  reevesi    
##  8      53864.       4.73 cervidae odocoileus hemionus   
##  9      87884.       4.94 cervidae odocoileus virginianus
## 10      35000.       4.54 cervidae ozotoceros bezoarticus
## 11       7500.       3.88 cervidae pudu       puda       
## 12     102059.       5.01 cervidae rangifer   tarandus
```

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    



## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
