-   [Objective of EDA](#objective-of-eda)
-   [Code File Basics](#code-file-basics)
    -   [Code Header](#code-header)
    -   [Clear Environment and Load packages](#clear-environment-and-load-packages)
-   [Load Data to begin EDA](#load-data-to-begin-eda)
    -   [Analyse the Structure & Summary of data](#analyse-the-structure-summary-of-data)
    -   [Analyse the Visual Summary of data](#analyse-the-visual-summary-of-data)
-   [Detailed EDA to examine the observations :](#detailed-eda-to-examine-the-observations)
    -   [How different variables are Correlated?](#how-different-variables-are-correlated)
    -   [Which is the most common fuel used in motor vehicles? How many bi-fuel models are listed?](#which-is-the-most-common-fuel-used-in-motor-vehicles-how-many-bi-fuel-models-are-listed)
    -   [How many different motor vehicle models are present across each class of vehicle?](#how-many-different-motor-vehicle-models-are-present-across-each-class-of-vehicle)
    -   [List of motor vehicle models those have both 2WD & 4WD vehicles .](#list-of-motor-vehicle-models-those-have-both-2wd-4wd-vehicles-.)
    -   [How many motor vehicle models are SmartWay certified?](#how-many-motor-vehicle-models-are-smartway-certified)
    -   [Are there any Zero Emission Vehicles? If yes, list their names.](#are-there-any-zero-emission-vehicles-if-yes-list-their-names.)
    -   [How Air Pollution Score & Greenhouse Gas Score distributed across various Motor Vehicle Models?](#how-air-pollution-score-greenhouse-gas-score-distributed-across-various-motor-vehicle-models)
    -   [What is the relationship between engine size and CO2 emission?](#what-is-the-relationship-between-engine-size-and-co2-emission)
    -   [What is the relationship between Fuel Economy and CO2 emission?](#what-is-the-relationship-between-fuel-economy-and-co2-emission)
    -   [What is the relationship between Vehicle Transmission Type & Fuel Economy?](#what-is-the-relationship-between-vehicle-transmission-type-fuel-economy)
    -   [Which Gasoline Vehicles get more than 40 MPG in the City?](#which-gasoline-vehicles-get-more-than-40-mpg-in-the-city)
    -   [Which Gasoline Vehicles get more than 40 MPG on the highway?](#which-gasoline-vehicles-get-more-than-40-mpg-on-the-highway)
    -   [Which vehicles get better fuel economy in city than on highway?](#which-vehicles-get-better-fuel-economy-in-city-than-on-highway)
    -   [Which vehicle manufacturer got EPA rating for more than 10 vehicle models?](#which-vehicle-manufacturer-got-epa-rating-for-more-than-10-vehicle-models)
    -   [Which Small Car is most Fuel-Efficient & Environment friendly?](#which-small-car-is-most-fuel-efficient-environment-friendly)
    -   [Which Medium Size Car is most Fuel-Efficient & Environment friendly?](#which-medium-size-car-is-most-fuel-efficient-environment-friendly)
    -   [Which Large Car is most Fuel-Efficient & Environment friendly?](#which-large-car-is-most-fuel-efficient-environment-friendly)
    -   [Which Station Wagon is most Fuel-Efficient & Environment friendly?](#which-station-wagon-is-most-fuel-efficient-environment-friendly)
    -   [Which is better a Diesel or Gasoline Engine?](#which-is-better-a-diesel-or-gasoline-engine)
    -   [What is the affect of Fuel & Transmission Type on Fuel-Economy/Gas-Mileage?](#what-is-the-affect-of-fuel-transmission-type-on-fuel-economygas-mileage)
    -   [Which is the most fuel-efficient car within each vehicle class? And what are their characteristics?](#which-is-the-most-fuel-efficient-car-within-each-vehicle-class-and-what-are-their-characteristics)

------------------------------------------------------------------------

Objective of EDA
----------------

-   Analyse data-set to summarize the main points
-   Examine the data to understand the underlying relationship between different variables
-   Detection of mistakes

Code File Basics
----------------

### Code Header

``` r
# Course: BUAN 5210
# Title: Final Project Technical Appendix 
# Purpose: Analyse "Environmental Protection Agency"" Green Vehicle data to determine which vehicle is more efficient and less polluting
```

### Clear Environment and Load packages

``` r
knitr::opts_chunk$set(echo = TRUE, tidy = TRUE)

# Clear working directory (remove all objects)
rm(list=ls(all=TRUE)) 

# Load packages
library(tidyverse)
library(gridExtra)
library(GGally)
library(knitr)
library(grid)
library(reshape)
library(reshape2)
```

Load Data to begin EDA
----------------------

``` r
# Import EPA Green Vehicle Data
EPA.GV.Data <- read.csv("EPA_Green_Vehicle.csv", header = TRUE)
```

### Analyse the Structure & Summary of data

``` r
# Structure of the dataset
str(EPA.GV.Data)
```

    ## 'data.frame':    2138 obs. of  23 variables:
    ##  $ Model               : Factor w/ 499 levels "ACURA ILX","ACURA MDX",..: 1 1 2 2 2 2 2 2 2 2 ...
    ##  $ Displ               : num  2.4 2.4 3.5 3.5 3.5 3.5 3.5 3.5 3.5 3.5 ...
    ##  $ Cyl                 : int  4 4 6 6 6 6 6 6 6 6 ...
    ##  $ Trans               : Factor w/ 27 levels "AMS-6","AMS-7",..: 3 3 27 27 27 27 27 27 27 27 ...
    ##  $ Drive               : Factor w/ 2 levels "2WD","4WD": 1 1 1 1 1 1 2 2 2 2 ...
    ##  $ Fuel.Type1          : Factor w/ 4 levels "Diesel","Electricity",..: 4 4 4 4 4 4 4 4 4 4 ...
    ##  $ Fuel.Type2          : Factor w/ 3 levels "","Electricity",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Cert.Region         : Factor w/ 2 levels "CA","FA": 1 2 1 1 2 2 1 1 2 2 ...
    ##  $ Stnd                : Factor w/ 21 levels "B5","L2","L2LEV160",..: 8 14 8 8 14 14 8 8 14 14 ...
    ##  $ Stnd.Description    : Factor w/ 21 levels "California LEV-II LEV",..: 9 15 9 9 15 15 9 9 15 15 ...
    ##  $ Underhood.ID        : Factor w/ 314 levels "JASXV06.0VHB",..: 151 151 154 154 154 154 154 154 154 154 ...
    ##  $ Veh.Class           : Factor w/ 10 levels "large car","midsize car",..: 5 5 6 6 6 6 6 6 6 6 ...
    ##  $ Air.Pollution.Score : int  3 3 3 3 3 3 3 3 3 3 ...
    ##  $ City.MPG.FT1        : int  25 25 19 20 19 20 18 19 18 19 ...
    ##  $ City.MPG.FT2        : int  NA NA NA NA NA NA NA NA NA NA ...
    ##  $ Hwy.MPG.FT1         : int  35 35 27 27 27 27 26 26 26 26 ...
    ##  $ Hwy.MPG.FT2         : int  NA NA NA NA NA NA NA NA NA NA ...
    ##  $ Cmb.MPG.FT1         : int  29 29 22 23 22 23 21 22 21 22 ...
    ##  $ Cmb.MPG.FT2         : int  NA NA NA NA NA NA NA NA NA NA ...
    ##  $ Greenhouse.Gas.Score: int  6 6 4 5 4 5 4 4 4 4 ...
    ##  $ SmartWay            : Factor w/ 3 levels "Elite","No","Yes": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ Comb.CO2.FT1        : int  309 309 404 390 404 390 424 404 424 404 ...
    ##  $ Comb.CO2.FT2        : int  NA NA NA NA NA NA NA NA NA NA ...

``` r
# Summary of the data set
summary(EPA.GV.Data)
```

    ##                     Model          Displ            Cyl        
    ##  FORD F150             :  42   Min.   :0.000   Min.   : 0.000  
    ##  CHEVROLET Silverado 15:  28   1st Qu.:2.000   1st Qu.: 4.000  
    ##  GMC Sierra 15         :  28   Median :2.800   Median : 6.000  
    ##  CHEVROLET Camaro      :  16   Mean   :3.024   Mean   : 5.483  
    ##  CHEVROLET Colorado    :  16   3rd Qu.:3.600   3rd Qu.: 6.000  
    ##  FORD F150 FFV         :  16   Max.   :8.000   Max.   :16.000  
    ##  (Other)               :1992                                   
    ##         Trans     Drive            Fuel.Type1         Fuel.Type2  
    ##  SemiAuto-8:428   2WD:1224   Diesel     :  46              :2018  
    ##  SemiAuto-6:370   4WD: 914   Electricity:   6   Electricity:  32  
    ##  Man-6     :223              Ethanol    :  88   Gas        :  88  
    ##  Auto-6    :140              Gasoline   :1998                     
    ##  AMS-7     :130                                                   
    ##  Auto-8    :125                                                   
    ##  (Other)   :722                                                   
    ##  Cert.Region        Stnd                       Stnd.Description
    ##  CA:1058     T3B125   :438   Federal Tier 3 Bin 125    :438    
    ##  FA:1080     L3ULEV125:281   California LEV-III ULEV125:281    
    ##              T3B70    :271   Federal Tier 3 Bin 70     :271    
    ##              L3ULEV70 :255   California LEV-III ULEV70 :255    
    ##              L3SULEV30:172   California LEV-III SULEV30:172    
    ##              T3B30    :163   Federal Tier 3 Bin 30     :163    
    ##              (Other)  :558   (Other)                   :558    
    ##        Underhood.ID         Veh.Class   Air.Pollution.Score
    ##  JPRXV03.0C91:  60   small car   :724   Min.   : 1.000     
    ##  JGMXT05.3384:  40   midsize car :350   1st Qu.: 3.000     
    ##  JBMXJ02.0B4X:  38   small SUV   :337   Median : 3.000     
    ##  JJLXJ03.0FSP:  32   large car   :209   Mean   : 3.982     
    ##  JBMXV03.0B58:  30   standard SUV:196   3rd Qu.: 5.000     
    ##  JMBXV04.0U2A:  26   pickup      :182   Max.   :10.000     
    ##  (Other)     :1912   (Other)     :140                      
    ##   City.MPG.FT1     City.MPG.FT2     Hwy.MPG.FT1      Hwy.MPG.FT2   
    ##  Min.   :  9.00   Min.   : 13.00   Min.   : 12.00   Min.   :17.00  
    ##  1st Qu.: 17.00   1st Qu.: 16.00   1st Qu.: 24.00   1st Qu.:22.00  
    ##  Median : 20.00   Median : 18.00   Median : 28.00   Median :24.00  
    ##  Mean   : 21.07   Mean   : 32.94   Mean   : 28.25   Mean   :37.08  
    ##  3rd Qu.: 24.00   3rd Qu.: 56.00   3rd Qu.: 32.00   3rd Qu.:57.25  
    ##  Max.   :150.00   Max.   :113.00   Max.   :122.00   Max.   :99.00  
    ##                   NA's   :2018                      NA's   :2018   
    ##   Cmb.MPG.FT1      Cmb.MPG.FT2     Greenhouse.Gas.Score  SmartWay   
    ##  Min.   : 10.00   Min.   : 14.00   Min.   : 1.000       Elite:  40  
    ##  1st Qu.: 19.00   1st Qu.: 19.00   1st Qu.: 3.000       No   :1839  
    ##  Median : 23.00   Median : 20.00   Median : 5.000       Yes  : 259  
    ##  Mean   : 23.71   Mean   : 34.34   Mean   : 4.725                   
    ##  3rd Qu.: 27.00   3rd Qu.: 56.75   3rd Qu.: 6.000                   
    ##  Max.   :136.00   Max.   :106.00   Max.   :10.000                   
    ##                   NA's   :2018                                      
    ##   Comb.CO2.FT1    Comb.CO2.FT2  
    ##  Min.   :  0.0   Min.   : 15.0  
    ##  1st Qu.:330.0   1st Qu.:241.8  
    ##  Median :387.0   Median :446.5  
    ##  Mean   :393.5   Mean   :378.6  
    ##  3rd Qu.:455.0   3rd Qu.:475.0  
    ##  Max.   :840.0   Max.   :614.0  
    ##                  NA's   :2018

Observations from glimpse/summary of data:

-   Ten variables are numerical/integer
    -   Maximum number of cylinder engine offered in a vehicle's is 16
    -   Biggest Engine Displacement has the capacity of 8 liters
    -   Air Pollution score & Greenhouse Gas Score ranges from 1(worst) to 10(best)
-   Eleven variables are factor
    -   Most vehicle use a 2- wheel drive layout
    -   10 different classification of vehicle size are present
    -   Gasoline is the most common used fuel
    -   Most of the vehicles certified in California
    -   Large number of vehicles are certified with **Federal Tier 3** emission standard
    -   Most of the vehicles are not SmartWay Certified

### Analyse the Visual Summary of data

``` r
# Visualize numerical variables (i.e. Displ, Cyl, City.MPG.FT1, Hwy.MPG.FT1,
# Cmb.MPG.FT1, Comb.CO2.FT1, Air.Pollution.Score and Greenhouse.Gas.Score)
# together

par(mfrow = c(3, 3))
hist(EPA.GV.Data$Displ, main = "Histogram of Engine Displacement")
hist(EPA.GV.Data$Cyl, main = "Histogram of Engine Cylinders")
hist(EPA.GV.Data$City.MPG.FT1, main = "Histogram of City Fuel Economy")
hist(EPA.GV.Data$Hwy.MPG.FT1, main = "Histogram of Highway Fuel Economy")
hist(EPA.GV.Data$Cmb.MPG.FT1, main = "Histogram of combined City/Highway Fuel Economy")
hist(EPA.GV.Data$Air.Pollution.Score, main = "Histogram of Air Pollution Score")
hist(EPA.GV.Data$Greenhouse.Gas.Score, main = "Histogram of Greenhouse Gas Score")
hist(EPA.GV.Data$Comb.CO2.FT1, main = "Histogram of combined City/Highway CO2 tailpipe emissions")
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-5-1.png)

Observations from visual summary of data:

-   Combined City/Highway CO2 tailpipe emissions have a normal distribution across the data
-   Air Pollution Score is between 3 and 5 for most vehicles
-   Greenhouse Gas Score is between 2 and 6 for most vehicles
-   City , Highway and Combined(i.e. City/Highway) Fuel economy have a right skewed distribution
-   Most vehicles have 4 or 6 engine cylinders
-   Most vehicles have an engine with a volume of 2 litres

------------------------------------------------------------------------

Detailed EDA to examine the observations :
------------------------------------------

### How different variables are Correlated?

``` r
EPA.GV.Data %>% select(Displ, Cyl, SmartWay, Air.Pollution.Score, Greenhouse.Gas.Score, 
    City.MPG.FT1, Hwy.MPG.FT1, Cmb.MPG.FT1, Comb.CO2.FT1) %>% ggpairs()
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-6-1.png)

**Findings:**

1.  Engine displacement & magnitude of CO2 emission have strong positive correlation.
2.  Greenhouse Gas score & fuel economy have strong positive correlation.
3.  Fuel economy & CO2 emission have strong negative correlation.
4.  Number of cylinders & engine displacement have strong linear relationship. As displacement is the total volume of all cylinders.

### Which is the most common fuel used in motor vehicles? How many bi-fuel models are listed?

``` r
# To find and visualize the most common fuel used in motor vehicles
F1 <- EPA.GV.Data %>% distinct(Model, Fuel.Type1) %>% group_by(Fuel.Type1) %>% 
    summarise(Count = n()) %>% ggplot(aes(x = reorder(Fuel.Type1, Count), y = Count, 
    fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    guides(fill = FALSE) + geom_text(aes(label = Count), size = 5, vjust = -0.1, 
    position = position_dodge(0.9)) + theme_classic() + ggtitle("Most Vehicles use Gasoline") + 
    xlab("Fuel Type") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 12), 
    axis.text = element_text(size = 10))

# To find and visualize the count of dual fuel motor vehicles
F2 <- EPA.GV.Data %>% filter(Fuel.Type2 %in% c("Electricity", "Gas")) %>% distinct(Model, 
    Fuel.Type1, Fuel.Type2) %>% mutate(Fuel.Type = paste(Fuel.Type1, "Or", Fuel.Type2)) %>% 
    group_by(Fuel.Type) %>% summarise(Count = n()) %>% ggplot(aes(x = reorder(Fuel.Type, 
    Count), y = Count, fill = Fuel.Type)) + geom_bar(stat = "identity", position = "dodge") + 
    guides(fill = FALSE) + geom_text(aes(label = Count), size = 5, vjust = -0.1, 
    position = position_dodge(0.9)) + theme_classic() + ggtitle("39 Dual Fuel vehicle Models") + 
    xlab("Fuel Type") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 12), 
    axis.text = element_text(size = 10))

grid.arrange(F1, F2, nrow = 1)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-7-1.png)

**Findings:**

1.  Gasoline is the most common fuel used in motor vehicles.
2.  3 motor vehicle models runs only on electricity.
3.  39 Bi-Fuel models are available. For dual fuel vehicles "Gasoline and Ethanol" are the conventional fuel & "Electricity and Gas" are the alternative fuel.
4.  Most of the Bi-Fuel models used "Ethanol Or Gas".

### How many different motor vehicle models are present across each class of vehicle?

``` r
# To find and visualize the total number of unique motor vehicle models are
# present across each class of vehicle
D1 <- EPA.GV.Data %>% distinct(Model, Veh.Class) %>% group_by(Veh.Class) %>% 
    summarise(Count = n()) %>% ggplot(aes(x = reorder(Veh.Class, Count), y = Count, 
    fill = Veh.Class)) + geom_bar(stat = "identity", position = "dodge") + guides(fill = FALSE) + 
    geom_text(aes(label = Count), size = 5, vjust = -0.1, position = position_dodge(0.9)) + 
    theme_classic() + ggtitle("Small Cars have 189 different car models") + 
    xlab("Vehicle Class") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 14, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 13), 
    axis.text = element_text(size = 10)) + theme(axis.text.x = element_text(angle = 20, 
    hjust = 1, vjust = 1))

# To find and visualize whether 2WD or 4WD layout is used across each class
# of vehicle
D2 <- EPA.GV.Data %>% distinct(Model, Veh.Class, Drive) %>% group_by(Veh.Class, 
    Drive) %>% summarise(Count = n()) %>% ggplot(aes(x = reorder(Veh.Class, 
    Count), y = Count, fill = Drive)) + geom_bar(stat = "identity", position = "dodge") + 
    geom_text(aes(label = Count), size = 5, vjust = -0.1, position = position_dodge(0.9)) + 
    theme_classic() + ggtitle("Most motor vehicles use a 2-wheel drive layout") + 
    xlab("Vehicle Class") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 14, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 13), 
    axis.text = element_text(size = 10)) + theme(axis.text.x = element_text(angle = 20, 
    hjust = 1, vjust = 1)) + theme(legend.position = c(0.15, 0.85)) + theme(legend.background = element_rect(fill = "white", 
    color = "black")) + guides(fill = guide_legend(title = "Wheel-Drive"))

grid.arrange(D1, D2, nrow = 1)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-8-1.png)

**Findings:**

1.  Small Cars have 189 different car models, however Van has only 2 models available.
2.  Most motor vehicles use a 2WD layout.
3.  Standard SUV, Small SUV & Station wagon have more 4WD models than 2WD models.
4.  Small cars have many variety of car models for both 2WD & 4WD vehicles.

### List of motor vehicle models those have both 2WD & 4WD vehicles .

``` r
#List of motor vehicle models those have both 2WD & 4WD vehicles
kable(
EPA.GV.Data %>%
  distinct(Model, Drive) %>%
  group_by(Model) %>%
  summarise(Count = n()) %>%
  filter(Count > 1) %>%
  select(Model) %>%
  head(10),
align = "l",
format = "html",
#caption = "Motor vehicle models available in both 2WD and 4WD layout ",
col.names = c("Motor Vehicle Model"))
```

<table>
<thead>
<tr>
<th style="text-align:left;">
Motor Vehicle Model
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
ACURA MDX
</td>
</tr>
<tr>
<td style="text-align:left;">
ACURA RDX
</td>
</tr>
<tr>
<td style="text-align:left;">
ACURA TLX
</td>
</tr>
<tr>
<td style="text-align:left;">
AUDI A3
</td>
</tr>
<tr>
<td style="text-align:left;">
AUDI A3 Cabriolet
</td>
</tr>
<tr>
<td style="text-align:left;">
AUDI A6
</td>
</tr>
<tr>
<td style="text-align:left;">
AUDI Q3
</td>
</tr>
<tr>
<td style="text-align:left;">
AUDI R8
</td>
</tr>
<tr>
<td style="text-align:left;">
AUDI R8 Spyder
</td>
</tr>
<tr>
<td style="text-align:left;">
BMW 320i
</td>
</tr>
</tbody>
</table>
122 Motor vehicle models are available in both 2WD and 4WD layout.

### How many motor vehicle models are SmartWay certified?

``` r
# To find and visualize the number of SmartWay certified vehicles

EPA.GV.Data %>% distinct(Model, SmartWay) %>% group_by(SmartWay) %>% summarise(Count = n()) %>% 
    ggplot(aes(x = reorder(SmartWay, Count), y = Count, fill = SmartWay)) + 
    geom_bar(stat = "identity", position = "dodge") + geom_text(aes(label = Count), 
    size = 5, vjust = -0.1, position = position_dodge(0.9)) + theme_classic() + 
    guides(fill = FALSE) + ggtitle("19 Motor Vehicles are among the best environmental performers") + 
    xlab("SmartWay Certified") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 12), 
    axis.text = element_text(size = 11))
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-10-1.png)

**Findings:**

1.  84 Motor vehicles are SmartWay Certified.
2.  SmartWay Elite certification is given to 19 Motor Vehicles.

### Are there any Zero Emission Vehicles? If yes, list their names.

``` r
kable(
EPA.GV.Data %>%
  filter(Stnd == "ZEV" ) %>%
  select(Model,Veh.Class,Fuel.Type1,Stnd.Description,Air.Pollution.Score,Greenhouse.Gas.Score,SmartWay),
align = "l",
#format = "html",
caption = "Zero Emission Electric Cars : Most environmentally friendly vehicle")
```

| Model                  | Veh.Class     | Fuel.Type1  | Stnd.Description | Air.Pollution.Score | Greenhouse.Gas.Score | SmartWay |
|:-----------------------|:--------------|:------------|:-----------------|:--------------------|:---------------------|:---------|
| FORD Focus Electric    | small car     | Electricity | California ZEV   | 10                  | 10                   | Elite    |
| HYUNDAI Ioniq Electric | midsize car   | Electricity | California ZEV   | 10                  | 10                   | Elite    |
| KIA Soul Electric      | station wagon | Electricity | California ZEV   | 10                  | 10                   | Elite    |

**Findings:**

1.  There are 3 zero emission vehicles, powered by electricity.

### How Air Pollution Score & Greenhouse Gas Score distributed across various Motor Vehicle Models?

``` r
# To visualize Air Pollution Score across various Motor Vehicle Models
E1 <- EPA.GV.Data %>% distinct(Model, Air.Pollution.Score) %>% group_by(Air.Pollution.Score) %>% 
    summarise(Count = n()) %>% ggplot(aes(x = reorder(Air.Pollution.Score, Count), 
    y = Count)) + geom_bar(stat = "identity", position = "dodge") + geom_text(aes(label = Count), 
    size = 5, vjust = -0.1, position = position_dodge(0.9)) + theme_classic() + 
    guides(fill = FALSE) + ggtitle("Most vehicles have Air Pollution Score of 3 ") + 
    xlab("Air Pollution Score") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 12), 
    axis.text = element_text(size = 11))

# To visualize Greenhouse Gas Score across various Motor Vehicle Models
E2 <- EPA.GV.Data %>% distinct(Model, Greenhouse.Gas.Score) %>% group_by(Greenhouse.Gas.Score) %>% 
    summarise(Count = n()) %>% ggplot(aes(x = reorder(Greenhouse.Gas.Score, 
    Count), y = Count)) + geom_bar(stat = "identity", position = "dodge") + 
    geom_text(aes(label = Count), size = 5, vjust = -0.1, position = position_dodge(0.9)) + 
    theme_classic() + guides(fill = FALSE) + ggtitle("Greenhouse Gas Score is\n less than 6 for most vehicles") + 
    xlab("Greenhouse Gas Score") + ylab("Count of motor vehicle models") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 12), 
    axis.text = element_text(size = 11))

grid.arrange(E1, E2, nrow = 1)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-12-1.png)

**Findings:**

1.  Air Pollution score is 10 only for 3 vehicles.
2.  Air Pollution score is less than equal to 5 for majority of vehicles.
3.  Greenhouse Gas Score is less than 6 for majority of vehicles.

### What is the relationship between engine size and CO2 emission?

``` r
# Relationship between engine size and CO2 emission for Cars
D1 <- EPA.GV.Data %>% filter(Veh.Class %in% c("large car", "small car", "midsize car", 
    "station wagon")) %>% group_by(Model, Displ, Veh.Class) %>% summarise(CO2.Emission = mean(Comb.CO2.FT1)) %>% 
    ggplot(aes(x = Displ, y = CO2.Emission, color = Veh.Class)) + geom_point() + 
    theme_light() + ggtitle("The larger the engine, the more Co2 it will produce") + 
    xlab("Engine Displacement(Liters)") + ylab("CO2 Emissions (Grams/Mile)") + 
    theme(plot.title = element_text(size = 13, face = "bold", hjust = 0.5)) + 
    theme(axis.title = element_text(size = 12), axis.text = element_text(size = 11)) + 
    theme(legend.position = c(0.77, 0.25)) + theme(legend.background = element_rect(fill = "white", 
    color = "black")) + labs(color = "Vehicle Class (Cars)")

# Relationship between engine size and CO2 emission for Trucks
D2 <- EPA.GV.Data %>% filter(Veh.Class %in% c("minivan", "pickup", "small SUV", 
    "standard SUV", "special purpose", "van")) %>% group_by(Model, Displ, Veh.Class) %>% 
    summarise(CO2.Emission = mean(Comb.CO2.FT1)) %>% ggplot(aes(x = Displ, y = CO2.Emission, 
    color = Veh.Class)) + geom_point() + theme_light() + ggtitle("Trucks emit more CO2 than Cars") + 
    xlab("Engine Displacement(Liters)") + ylab("CO2 Emissions (Grams/Mile)") + 
    theme(plot.title = element_text(size = 13, face = "bold", hjust = 0.5)) + 
    theme(axis.title = element_text(size = 12), axis.text = element_text(size = 11)) + 
    theme(legend.position = c(0.77, 0.25)) + theme(legend.background = element_rect(fill = "white", 
    color = "black")) + labs(color = "Vehicle Class (Trucks)")

grid.arrange(D1, D2, nrow = 1)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-13-1.png)

**Findings:**

1.  Co2 production is directly related to the amount of fuel the engine burns.
2.  Engine Displacement/Size of Engine & CO2 Emissions have strong positive linear relationship. The larger the engine , more likely it is to burn more fuel , hence more CO2 it will produce.
3.  Heavier Vehicles emit more CO2 than light-weight vehicles.
4.  Mostly all the vehicles under Truck category emits more than 300 grams CO2 per mile.

### What is the relationship between Fuel Economy and CO2 emission?

``` r
# Relationship between Fuel Economy and CO2 emission for Cars
FE1 <- EPA.GV.Data %>% filter(Veh.Class %in% c("large car", "small car", "midsize car", 
    "station wagon")) %>% group_by(Model, Displ, Veh.Class) %>% summarise(CO2.Emission = mean(Comb.CO2.FT1), 
    Cmb.Mileage = mean(Cmb.MPG.FT1)) %>% ggplot(aes(x = Cmb.Mileage, y = CO2.Emission, 
    color = Veh.Class)) + geom_point() + theme_light() + ggtitle("Higher the Fuel Economy, Lower the CO2 Emissions") + 
    xlab("Combine Fuel Economy (MPG)") + ylab("CO2 Emissions (Grams/Mile)") + 
    theme(plot.title = element_text(size = 13, face = "bold", hjust = 0.5)) + 
    theme(axis.title = element_text(size = 12), axis.text = element_text(size = 11)) + 
    theme(legend.position = c(0.77, 0.75)) + theme(legend.background = element_rect(fill = "white", 
    color = "black")) + labs(color = "Vehicle Class (Cars)")

# Relationship between Fuel Economy and CO2 emission for Trucks
FE2 <- EPA.GV.Data %>% filter(Veh.Class %in% c("minivan", "pickup", "small SUV", 
    "standard SUV", "special purpose", "van")) %>% group_by(Model, Displ, Veh.Class) %>% 
    summarise(CO2.Emission = mean(Comb.CO2.FT1), Cmb.Mileage = mean(Cmb.MPG.FT1)) %>% 
    ggplot(aes(x = Cmb.Mileage, y = CO2.Emission, color = Veh.Class)) + geom_point() + 
    theme_light() + ggtitle("Trucks have higher CO2 Emission than Cars") + xlab("Combine Fuel Economy (MPG)") + 
    ylab("CO2 Emissions (Grams/Mile)") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 12), 
    axis.text = element_text(size = 11)) + theme(legend.position = c(0.21, 0.22)) + 
    theme(legend.background = element_rect(fill = "white", color = "black")) + 
    labs(color = "Vehicle Class (Trucks)")

grid.arrange(FE1, FE2, nrow = 1)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-14-1.png)

**Findings:**

1.  Car with better gas mileage have low CO2 Emissions.
2.  Fuel Economy & CO2 Emissions have strong negative linear relationship. The lower the fuel economy , more likely it is to burn more fuel , hence more CO2 it will produce.
3.  Heavier Vehicles emit more CO2 than light-weight vehicles.
4.  Mostly all the vehicles under Truck category emits more than 300 grams CO2 per mile.

### What is the relationship between Vehicle Transmission Type & Fuel Economy?

``` r
# To Visualize the relationship between Fuel Economy & Transmission type
EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", "Num.Of.Gears"), 
    sep = "\\-") %>% ggplot(aes(x = Transmission.Type, y = Cmb.MPG.FT1, fill = "#4271AE")) + 
    geom_boxplot(color = "#1F3552") + scale_y_continuous(name = "Combined City/Highway Fuel Economy(MPG)", 
    breaks = seq(0, 140, 10)) + scale_x_discrete(name = "Transmission Type") + 
    theme_bw() + guides(fill = FALSE) + ggtitle("Vehicles with Continuously Variable Transmission(CVT) are more Fuel Efficient", 
    subtitle = "Fuel Economy by Transmission type")
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-15-1.png)

**Findings:**

1.  Vehicles with Continuously Variable Transmission(CVT) are more Fuel Efficient
2.  Automated Manual(i.e. AutoMan) has the most variation in Fuel Economy in comparision with other transmission types
3.  Very few vehicles have the combined mileage of more than 35 miles per gallon
4.  On average ,vehicles with Manual(i.e. Man) transmission achieved an MPG of 25 while vehicles with Automatic(i.e. Auto) transmission achieved an MPG of 18, a difference of 7 more miles per gallon.

### Which Gasoline Vehicles get more than 40 MPG in the City?

``` r
# To visualize the gasoline Vehicles that get more than 40 MPG in the City
EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", "Num.Of.Gears"), 
    sep = "\\-") %>% filter(Fuel.Type1 == "Gasoline", City.MPG.FT1 > 40) %>% 
    group_by(Model, Displ, Fuel.Type1) %>% summarise(City.MPG = mean(City.MPG.FT1)) %>% 
    arrange(desc(City.MPG)) %>% ggplot(aes(x = reorder(Model, desc(City.MPG)), 
    y = City.MPG)) + geom_bar(stat = "identity", position = "dodge") + geom_text(aes(label = City.MPG), 
    size = 4, vjust = -0.1, position = position_dodge(0.9)) + theme_classic() + 
    ggtitle("Gasoline Vehicles that get more than 40 MPG in the City") + xlab("Vehicle Make & Model") + 
    ylab("City Fuel Economy (MPG)") + theme(plot.title = element_text(size = 14, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 13), 
    axis.text = element_text(size = 10)) + theme(axis.text.x = element_text(angle = 50, 
    hjust = 1, vjust = 1))
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-16-1.png)

**Findings:**

1.  HYUNDAI Ioniq Blue is the most fuel efficient model in the market, rated at 57 MPG in the city.
2.  15 vehicle models rated at more than 40 MPG in the city.

### Which Gasoline Vehicles get more than 40 MPG on the highway?

``` r
# To visualize the gasoline Vehicles that get more than 40 MPG in the City
EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", "Num.Of.Gears"), 
    sep = "\\-") %>% filter(Fuel.Type1 == "Gasoline", Hwy.MPG.FT1 > 40) %>% 
    group_by(Model, Displ, Fuel.Type1) %>% summarise(Highway.MPG = mean(Hwy.MPG.FT1)) %>% 
    arrange(desc(Highway.MPG)) %>% ggplot(aes(x = reorder(Model, desc(Highway.MPG)), 
    y = Highway.MPG)) + geom_bar(stat = "identity", position = "dodge") + geom_text(aes(label = Highway.MPG), 
    size = 4, vjust = -0.1, position = position_dodge(0.9)) + theme_classic() + 
    ggtitle("Gasoline Vehicles that get more than 40 MPG on the Highway") + 
    xlab("Vehicle Make & Model") + ylab("Highway Fuel Economy (MPG)") + theme(plot.title = element_text(size = 14, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 13), 
    axis.text = element_text(size = 10)) + theme(axis.text.x = element_text(angle = 50, 
    hjust = 1, vjust = 1))
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-17-1.png)

**Findings:**

1.  HYUNDAI Ioniq Blue is the most fuel efficient model in the market, rated at 59 MPG on the highway.
2.  17 vehicle models rated at more than 40 MPG on the highway.

### Which vehicles get better fuel economy in city than on highway?

``` r
# List of vehicles that get better fuel economy in city than on highway
TBL <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", "Num.Of.Gears"), 
    sep = "\\-") %>% group_by(Model, Displ, Fuel.Type1, SmartWay, Greenhouse.Gas.Score, 
    Air.Pollution.Score) %>% summarise(City.MPG = mean(City.MPG.FT1), Highway.MPG = mean(Hwy.MPG.FT1)) %>% 
    filter(Highway.MPG < City.MPG, Fuel.Type1 != "Electricity") %>% mutate(MPG_Diff = City.MPG - 
    Highway.MPG) %>% filter(MPG_Diff > 1) %>% arrange(desc(MPG_Diff))

T1 <- TBL %>% select(Model, City.MPG) %>% mutate(City.Or.Highway = "City MPG")

T2 <- TBL %>% select(Model, Highway.MPG) %>% mutate(City.Or.Highway = "Highway MPG")

names(T1)[6] <- "MPG"
names(T2)[6] <- "MPG"

rbind.data.frame(T1, T2) %>% ggplot(aes(x = reorder(Model, MPG), y = MPG, fill = City.Or.Highway)) + 
    geom_bar(stat = "identity", position = "dodge") + geom_text(aes(label = MPG), 
    size = 4, hjust = 1.2, position = position_dodge(0.9)) + theme_classic() + 
    ggtitle("Vehicles that use the least gasoline in stop-n-go driving", subtitle = "Best City MPG") + 
    xlab("Vehicle Make & Model") + ylab("Fuel Economy (MPG)") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 0)) + theme(axis.title = element_text(size = 13), 
    axis.text = element_text(size = 11.5)) + guides(fill = guide_legend(title = "Fuel Economy")) + 
    scale_fill_manual(values = c("maroon1", "seagreen1")) + coord_flip()
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-18-1.png)

``` r
kable(TBL, align = "l", format = "html", caption = "Best vehicles for City Driving")
```

<table>
<caption>
Best vehicles for City Driving
</caption>
<thead>
<tr>
<th style="text-align:left;">
Model
</th>
<th style="text-align:left;">
Displ
</th>
<th style="text-align:left;">
Fuel.Type1
</th>
<th style="text-align:left;">
SmartWay
</th>
<th style="text-align:left;">
Greenhouse.Gas.Score
</th>
<th style="text-align:left;">
Air.Pollution.Score
</th>
<th style="text-align:left;">
City.MPG
</th>
<th style="text-align:left;">
Highway.MPG
</th>
<th style="text-align:left;">
MPG\_Diff
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
CHEVROLET Malibu
</td>
<td style="text-align:left;">
1.8
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
3
</td>
<td style="text-align:left;">
49
</td>
<td style="text-align:left;">
43
</td>
<td style="text-align:left;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
KIA Niro Touring
</td>
<td style="text-align:left;">
1.6
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
46
</td>
<td style="text-align:left;">
40
</td>
<td style="text-align:left;">
6
</td>
</tr>
<tr>
<td style="text-align:left;">
KIA Niro
</td>
<td style="text-align:left;">
1.6
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Elite
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
51
</td>
<td style="text-align:left;">
46
</td>
<td style="text-align:left;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
TOYOTA Prius c
</td>
<td style="text-align:left;">
1.5
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Elite
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
48
</td>
<td style="text-align:left;">
43
</td>
<td style="text-align:left;">
5
</td>
</tr>
<tr>
<td style="text-align:left;">
FORD C-MAX Hybrid
</td>
<td style="text-align:left;">
2.0
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
42
</td>
<td style="text-align:left;">
38
</td>
<td style="text-align:left;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
TOYOTA RAV4 Hybrid
</td>
<td style="text-align:left;">
2.5
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
34
</td>
<td style="text-align:left;">
30
</td>
<td style="text-align:left;">
4
</td>
</tr>
<tr>
<td style="text-align:left;">
KIA Niro FE
</td>
<td style="text-align:left;">
1.6
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Elite
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
52
</td>
<td style="text-align:left;">
49
</td>
<td style="text-align:left;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
LEXUS NX 300h
</td>
<td style="text-align:left;">
2.5
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
33
</td>
<td style="text-align:left;">
30
</td>
<td style="text-align:left;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
LINCOLN MKZ Hybrid
</td>
<td style="text-align:left;">
2.0
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
41
</td>
<td style="text-align:left;">
38
</td>
<td style="text-align:left;">
3
</td>
</tr>
<tr>
<td style="text-align:left;">
FORD Fusion Energi Plug-in Hybrid
</td>
<td style="text-align:left;">
2.0
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Elite
</td>
<td style="text-align:left;">
10
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
43
</td>
<td style="text-align:left;">
41
</td>
<td style="text-align:left;">
2
</td>
</tr>
<tr>
<td style="text-align:left;">
FORD Fusion Hybrid
</td>
<td style="text-align:left;">
2.0
</td>
<td style="text-align:left;">
Gasoline
</td>
<td style="text-align:left;">
Yes
</td>
<td style="text-align:left;">
9
</td>
<td style="text-align:left;">
7
</td>
<td style="text-align:left;">
43
</td>
<td style="text-align:left;">
41
</td>
<td style="text-align:left;">
2
</td>
</tr>
</tbody>
</table>
**Findings:**

1.  11 Vehicles get better mileage in City than on highway.
2.  "CHEVROLET Malibu" & "KIA Niro Touring" have difference of 6 MPG between City and highway mileage
3.  "KIA Niro" & "TOYOTA Pirus c" have difference of 5 MPG between City and highway mileage
4.  All the listed vehicles are SmartWay certified and have good GreenHouse Gas & Air Pollution score.

### Which vehicle manufacturer got EPA rating for more than 10 vehicle models?

``` r
EPA.GV.Data %>% separate(col = Model, into = c("Car.Brand", "Car.Model"), sep = "\\ ", 
    extra = "merge") %>% distinct(Car.Brand, Car.Model) %>% group_by(Car.Brand) %>% 
    summarise(Num.Of.CarModels = n()) %>% filter(Num.Of.CarModels > 10) %>% 
    arrange(desc(Num.Of.CarModels)) %>% ggplot(aes(x = reorder(Car.Brand, Num.Of.CarModels), 
    y = Num.Of.CarModels, fill = Car.Brand)) + geom_bar(stat = "identity", position = "dodge") + 
    geom_text(aes(label = Num.Of.CarModels), size = 5, vjust = -0.1, position = position_dodge(0.9)) + 
    theme_classic() + ggtitle("For 2018 model year: EPA rated 57 BMW Models") + 
    xlab("Vehicle Manufacturer") + ylab("Number Of Car Models") + theme(plot.title = element_text(size = 14, 
    face = "bold", hjust = 0.5)) + theme(axis.title = element_text(size = 13), 
    axis.text = element_text(size = 10)) + theme(axis.text.x = element_text(angle = 35, 
    hjust = 1, vjust = 1)) + guides(fill = FALSE)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-19-1.png)

**Findings:**

1.  In 2018, EPA rated more than 30 models for following manufacturers : BMW, MERCEDES-BENZ, PORSCHE, AUDI
2.  IN 2018, EPA rated more than 10 models for following 14 manufacturers : BMW, MERCEDES-BENZ, PORSCHE, AUDI, TOYOTA, FORD, CHEVROLET, MINI, KIA, HYUNDAI, VOLVO, LEXUS, NISSAN, VOLKSWAGEN

### Which Small Car is most Fuel-Efficient & Environment friendly?

``` r
# To Visualize the relationship between engine size, co2 emission and fuel
# economy
SmallCar1 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "small car", Fuel.Type1 != 
    "Electricity") %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% ggplot(aes(x = Displ, y = Combine.MPG)) + geom_point() + stat_smooth(method = lm, 
    se = FALSE, color = "dodgerblue3") + theme_classic() + theme(plot.title = element_text(size = 15, 
    face = "bold", hjust = 0.88)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + ggtitle("Larger the Engine, Lower the Mileage, Higher the CO2 Emissions") + 
    xlab("Engine Displacement (Size of Engine in Liters)") + ylab("Combined Fuel Economy (MPG)")

# To Visualize which transmission type is best
SmallCar2 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "small car", Fuel.Type1 %in% 
    c("Diesel", "Gasoline")) %>% filter(Transmission.Type %in% c("Auto", "Man", 
    "CVT")) %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% group_by(Transmission.Type, Fuel.Type1) %>% summarise(Avg_Combine.MPG = mean(Combine.MPG)) %>% 
    ggplot(aes(x = reorder(Transmission.Type, Avg_Combine.MPG), y = Avg_Combine.MPG, 
        fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    scale_y_continuous(limits = c(0, 40), breaks = seq(0, 40, 10)) + theme_classic() + 
    theme(plot.title = element_text(size = 15, face = "bold", hjust = 0.3)) + 
    theme(plot.subtitle = element_text(size = 13)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + scale_x_discrete(labels = c(Auto = "Automatic", 
    Man = "Manual", CVT = "CVT")) + scale_x_discrete(labels = c(CVT = expression(bold("CVT")), 
    parse = TRUE)) + theme(legend.title = element_text(size = 14, color = "black"), 
    legend.text = element_text(size = 13, color = "black")) + geom_text(aes(label = round(Avg_Combine.MPG, 
    0)), size = 6, vjust = 1, position = position_dodge(0.9)) + ggtitle("Gasoline Cars: CVT is the most Fuel-Efficient Transmission Type") + 
    xlab("Transmission Type") + ylab("Avg Gas Mileage (MPG)") + geom_rect(aes(xmin = 0, 
    xmax = 2.5, ymin = 0, ymax = 40), alpha = 0.1, fill = "white") + # geom_hline(yintercept = 30) +
guides(fill = guide_legend(title = "Fuel Type")) + scale_fill_manual(values = c("goldenrod1", 
    "dodgerblue3"))

# To Visualize the best car in the category
SmallCar3 <- rbind.data.frame((EPA.GV.Data %>% filter(Veh.Class == "small car", 
    Fuel.Type1 %in% c("Gasoline"), SmartWay != "No") %>% select(-Cert.Region, 
    -Stnd, -Stnd.Description, -Underhood.ID) %>% group_by(Model, Displ, Cyl, 
    Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG > 40)), (EPA.GV.Data %>% filter(Veh.Class == "small car", 
    Fuel.Type1 %in% c("Diesel"), SmartWay != "No") %>% select(-Cert.Region, 
    -Stnd, -Stnd.Description, -Underhood.ID) %>% group_by(Model, Displ, Cyl, 
    Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG > 36, Trans == "Auto-9"))) %>% ggplot(aes(x = reorder(Model, 
    desc(Combine.MPG)), y = Combine.MPG, fill = Fuel.Type1)) + geom_bar(stat = "identity", 
    position = "dodge") + theme_classic() + geom_text(aes(label = round(Combine.MPG, 
    0)), size = 6, hjust = 1.2, position = position_dodge(0.9)) + xlab("Vehicle Model & Make") + 
    ylab("Combined Fuel Economy (MPG)") + scale_y_continuous(limits = c(0, 50), 
    breaks = seq(0, 50, 10)) + theme(plot.title = element_text(size = 15, face = "bold", 
    hjust = 0)) + theme(plot.subtitle = element_text(size = 13)) + theme(axis.title.y = element_blank()) + 
    theme(axis.title.x = element_text(size = 15), axis.text = element_text(size = 13)) + 
    theme(legend.title = element_text(size = 14, color = "black"), legend.text = element_text(size = 13, 
        color = "black")) + guides(fill = guide_legend(title = "Fuel Type")) + 
    scale_fill_manual(values = c("goldenrod1", "dodgerblue3")) + scale_x_discrete(labels = c(`TOYOTA Prius c` = expression(bold("TOYOTA Prius c")), 
    parse = TRUE)) + ggtitle("TOYOTA Prius c: Best Fuel-Efficient Eco-Friendly Car") + 
    coord_flip()

grid.arrange(SmallCar1, SmallCar2, SmallCar3, nrow = 2)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-20-1.png)

**Findings:**

1.  TOYOTA Prius c is the most Fuel-Efficient & Environment friendly small car and have a mileage of more than 40 miles per gallon.
2.  Listed Gasoline Powered Cars are among the Best Environnmental Performers.

### Which Medium Size Car is most Fuel-Efficient & Environment friendly?

``` r
# To Visualize the relationship between engine size, co2 emission and fuel
# economy
MidsizeCar1 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "midsize car", Fuel.Type1 != 
    "Electricity") %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% ggplot(aes(x = Displ, y = Combine.MPG)) + geom_point() + stat_smooth(method = lm, 
    se = FALSE, color = "dodgerblue3") + theme_classic() + theme(plot.title = element_text(size = 15, 
    face = "bold", hjust = 0.88)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + ggtitle("Larger the Engine, Lower the Mileage, Higher the CO2 Emissions") + 
    xlab("Engine Displacement (Size of Engine in Liters)") + ylab("Combined Fuel Economy (MPG)")

# To Visualize which transmission type is best
MidsizeCar2 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "midsize car", Fuel.Type1 %in% 
    c("Diesel", "Gasoline")) %>% filter(!(Transmission.Type %in% c("AMS", "Auto", 
    "SCV", "SemiAuto"))) %>% select(-Cert.Region, -Stnd, -Stnd.Description, 
    -Num.Of.Gears, -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, 
    SmartWay, Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% 
    summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 0)) %>% group_by(Transmission.Type, 
    Fuel.Type1) %>% summarise(Avg_Combine.MPG = mean(Combine.MPG)) %>% ggplot(aes(x = reorder(Transmission.Type, 
    Avg_Combine.MPG), y = Avg_Combine.MPG, fill = Fuel.Type1)) + geom_bar(stat = "identity", 
    position = "dodge") + scale_y_continuous(limits = c(0, 40), breaks = seq(0, 
    40, 10)) + theme_classic() + theme(plot.title = element_text(size = 15, 
    face = "bold", hjust = 0.78)) + theme(plot.subtitle = element_text(size = 13)) + 
    theme(axis.title = element_text(size = 15), axis.text = element_text(size = 13)) + 
    theme(axis.title.y = element_text(margin = margin(t = 0, r = 10, b = 0, 
        l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + scale_x_discrete(labels = c(AutoMan = expression(bold("Automated Manual")), 
    Man = "Manual", CVT = expression(bold("CVT")))) + theme(legend.title = element_text(size = 14, 
    color = "black"), legend.text = element_text(size = 13, color = "black")) + 
    geom_text(aes(label = round(Avg_Combine.MPG, 0)), size = 6, vjust = 1, position = position_dodge(0.9)) + 
    ggtitle("Gasoline Cars : Automated Manual & CVT are the most\nFuel-Efficient Transmission Type") + 
    xlab("Transmission Type") + ylab("Avg Gas Mileage (MPG)") + geom_rect(aes(xmin = 0, 
    xmax = 1.5, ymin = 0, ymax = 40), alpha = 0.1, fill = "white") + # geom_hline(yintercept = 30) +
guides(fill = guide_legend(title = "Fuel Type")) + scale_fill_manual(values = c("goldenrod1", 
    "dodgerblue3"))

# To Visualize the best car in the category
MidsizeCar3 <- rbind.data.frame((EPA.GV.Data %>% filter(Veh.Class == "midsize car", 
    Fuel.Type1 %in% c("Gasoline"), SmartWay != "No") %>% select(-Cert.Region, 
    -Stnd, -Stnd.Description, -Underhood.ID) %>% group_by(Model, Displ, Cyl, 
    Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG > 45, Trans != "SCV-6")), (EPA.GV.Data %>% filter(Veh.Class == 
    "midsize car", Fuel.Type1 %in% c("Diesel"), SmartWay != "No") %>% select(-Cert.Region, 
    -Stnd, -Stnd.Description, -Underhood.ID) %>% group_by(Model, Displ, Cyl, 
    Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG >= 35, Trans != "Man-6"))) %>% ggplot(aes(x = reorder(Model, 
    desc(Combine.MPG)), y = Combine.MPG, fill = Fuel.Type1)) + geom_bar(stat = "identity", 
    position = "dodge") + theme_classic() + geom_text(aes(label = round(Combine.MPG, 
    0)), size = 6, hjust = 1.2, position = position_dodge(0.9)) + xlab("Vehicle Model & Make") + 
    ylab("Combined Fuel Economy (MPG)") + scale_y_continuous(limits = c(0, 60), 
    breaks = seq(0, 60, 10)) + theme(plot.title = element_text(size = 15, face = "bold", 
    hjust = 0.7)) + theme(plot.subtitle = element_text(size = 13)) + theme(axis.title.y = element_blank()) + 
    theme(axis.title.x = element_text(size = 15), axis.text = element_text(size = 13)) + 
    theme(legend.title = element_text(size = 14, color = "black"), legend.text = element_text(size = 13, 
        color = "black")) + guides(fill = guide_legend(title = "Fuel Type")) + 
    scale_fill_manual(values = c("goldenrod1", "dodgerblue3")) + scale_x_discrete(labels = c(`HYUNDAI Ioniq Plug-in Hybrid` = expression(bold("HYUNDAI Ioniq Plug-in Hybrid")), 
    parse = TRUE)) + ggtitle("HYUNDAI Ioniq Plug-in Hybrid: Best Fuel-Efficient Eco-Friendly Car") + 
    coord_flip()

grid.arrange(MidsizeCar1, MidsizeCar2, MidsizeCar3, nrow = 2)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-21-1.png)

**Findings:**

1.  HYUNDAI Ioniq Plug-in Hybrid is the most Fuel-Efficient & Environment friendly midsize car and have a mileage of &gt;50 miles per gallon.
2.  Listed Gasoline Powered Cars are among the Best Environnmental Performers.

### Which Large Car is most Fuel-Efficient & Environment friendly?

``` r
# To Visualize the relationship between engine size, co2 emission and fuel
# economy
LargeCar1 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "large car", Fuel.Type1 != 
    "Electricity") %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% ggplot(aes(x = Displ, y = Combine.MPG)) + geom_point() + stat_smooth(method = lm, 
    se = FALSE, color = "dodgerblue3") + theme_classic() + theme(plot.title = element_text(size = 15, 
    face = "bold", hjust = 0.88)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + ggtitle("Larger the Engine, Lower the Mileage, Higher the CO2 Emissions") + 
    xlab("Engine Displacement (Size of Engine in Liters)") + ylab("Combined Fuel Economy (MPG)")

# To Visualize which transmission type is best
LargeCar2 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "large car", Fuel.Type1 != 
    "Electricity") %>% filter(!(Transmission.Type %in% c("AMS", "Auto", "Man", 
    "SCV"))) %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% group_by(Transmission.Type, Fuel.Type1) %>% summarise(Avg_Combine.MPG = mean(Combine.MPG)) %>% 
    ggplot(aes(x = reorder(Transmission.Type, Avg_Combine.MPG), y = Avg_Combine.MPG, 
        fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    scale_y_continuous(limits = c(0, 40), breaks = seq(0, 40, 10)) + theme_classic() + 
    theme(plot.title = element_text(size = 15, face = "bold", hjust = 0.78)) + 
    theme(plot.subtitle = element_text(size = 13)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + scale_x_discrete(labels = c(AutoMan = expression(bold("Automated Manual")), 
    SemiAuto = "Semi Automatic", CVT = expression(bold("CVT")))) + theme(legend.title = element_text(size = 14, 
    color = "black"), legend.text = element_text(size = 13, color = "black")) + 
    geom_text(aes(label = round(Avg_Combine.MPG, 0)), size = 6, vjust = 1, position = position_dodge(0.9)) + 
    ggtitle("Gasoline Car : Automated Manual & CVT are the most\n Fuel-Efficient Transmission Type") + 
    xlab("Transmission Type") + ylab("Avg Gas Mileage (MPG)") + geom_rect(aes(xmin = 0, 
    xmax = 1.5, ymin = 0, ymax = 40), alpha = 0.1, fill = "white") + # geom_hline(yintercept = 28) +
guides(fill = guide_legend(title = "Fuel Type")) + scale_fill_manual(values = c("coral1", 
    "dodgerblue3"))

# To Visualize the best car in the category
LargeCar3 <- rbind.data.frame((EPA.GV.Data %>% filter(Veh.Class == "large car", 
    Fuel.Type1 %in% c("Gasoline"), SmartWay != "No") %>% select(-Cert.Region, 
    -Stnd, -Stnd.Description, -Underhood.ID) %>% group_by(Model, Displ, Cyl, 
    Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG > 35)), (EPA.GV.Data %>% filter(Veh.Class == "large car", 
    Fuel.Type1 %in% c("Ethanol")) %>% select(-Cert.Region, -Stnd, -Stnd.Description, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(max(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG > 16))) %>% ggplot(aes(x = reorder(Model, desc(Combine.MPG)), 
    y = Combine.MPG, fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    theme_classic() + geom_text(aes(label = round(Combine.MPG, 0)), size = 6, 
    hjust = 1.2, position = position_dodge(0.9)) + xlab("Vehicle Model & Make") + 
    ylab("Combined Fuel Economy (MPG)") + scale_y_continuous(limits = c(0, 60), 
    breaks = seq(0, 60, 10)) + theme(plot.title = element_text(size = 15, face = "bold", 
    hjust = 0.5)) + theme(plot.subtitle = element_text(size = 13)) + theme(axis.title.y = element_blank()) + 
    theme(axis.title.x = element_text(size = 15), axis.text = element_text(size = 13)) + 
    theme(legend.title = element_text(size = 14, color = "black"), legend.text = element_text(size = 13, 
        color = "black")) + guides(fill = guide_legend(title = "Fuel Type")) + 
    scale_fill_manual(values = c("coral1", "dodgerblue3")) + scale_x_discrete(labels = c(`HYUNDAI Ioniq Blue` = expression(bold("HYUNDAI Ioniq Blue")), 
    parse = TRUE)) + ggtitle("HYUNDAI Ioniq Blue: Best Fuel-Efficient Eco-Friendly Car") + 
    coord_flip()

grid.arrange(LargeCar1, LargeCar2, LargeCar3, nrow = 2)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-22-1.png)

**Findings:**

1.  HYUNDAI Ioniq Blue is the most Fuel-Efficient & Environment friendly large car and have a mileage of &gt;50 miles per gallon.
2.  Listed Gasoline Powered Cars are among the Best Environnmental Performers.

### Which Station Wagon is most Fuel-Efficient & Environment friendly?

``` r
# To Visualize the relationship between engine size, co2 emission and fuel
# economy
StationWagon1 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "station wagon", Fuel.Type1 != 
    "Electricity") %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% ggplot(aes(x = Displ, y = Combine.MPG)) + geom_point() + stat_smooth(method = lm, 
    se = FALSE, color = "dodgerblue3") + theme_classic() + theme(plot.title = element_text(size = 15, 
    face = "bold", hjust = 0.88)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + ggtitle("Larger the Engine, Lower the Mileage, Higher the CO2 Emissions") + 
    xlab("Engine Displacement (Size of Engine in Liters)") + ylab("Combined Fuel Economy (MPG)")

# To Visualize which transmission type is best
StationWagon2 <- EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", 
    "Num.Of.Gears"), sep = "\\-") %>% filter(Veh.Class == "station wagon", Fuel.Type1 %in% 
    c("Diesel", "Gasoline")) %>% filter(!(Transmission.Type %in% c("AMS", "Auto", 
    "Man", "SCV"))) %>% select(-Cert.Region, -Stnd, -Stnd.Description, -Num.Of.Gears, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Transmission.Type, SmartWay, 
    Fuel.Type1, Veh.Class, Air.Pollution.Score, Greenhouse.Gas.Score) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0)) %>% group_by(Transmission.Type, Fuel.Type1) %>% summarise(Avg_Combine.MPG = mean(Combine.MPG)) %>% 
    ggplot(aes(x = reorder(Transmission.Type, Avg_Combine.MPG), y = Avg_Combine.MPG, 
        fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    scale_y_continuous(limits = c(0, 40), breaks = seq(0, 40, 10)) + theme_classic() + 
    theme(plot.title = element_text(size = 15, face = "bold", hjust = 0)) + 
    theme(plot.subtitle = element_text(size = 13)) + theme(axis.title = element_text(size = 15), 
    axis.text = element_text(size = 13)) + theme(axis.title.y = element_text(margin = margin(t = 0, 
    r = 10, b = 0, l = 0))) + theme(axis.title.x = element_text(margin = margin(t = 12, 
    r = 0, b = 0, l = 0))) + scale_x_discrete(labels = c(AutoMan = expression(bold("Automated Manual")), 
    SemiAuto = "Semi Automatic", CVT = "CVT")) + theme(legend.title = element_text(size = 14, 
    color = "black"), legend.text = element_text(size = 13, color = "black")) + 
    geom_text(aes(label = round(Avg_Combine.MPG, 0)), size = 6, vjust = 1, position = position_dodge(0.9)) + 
    ggtitle("Gasoline Car : Automated Manual is the most\n Fuel-Efficient Transmission Type") + 
    xlab("Transmission Type") + ylab("Avg Gas Mileage (MPG)") + geom_rect(aes(xmin = 0, 
    xmax = 2.5, ymin = 0, ymax = 40), alpha = 0.1, fill = "white") + # geom_hline(yintercept = 28) +
guides(fill = guide_legend(title = "Fuel Type")) + scale_fill_manual(values = c("goldenrod1", 
    "dodgerblue3"))

# To Visualize the best car in the category
StationWagon3 <- rbind.data.frame((EPA.GV.Data %>% filter(Veh.Class == "station wagon", 
    Fuel.Type1 %in% c("Gasoline"), SmartWay != "No") %>% select(-Cert.Region, 
    -Stnd, -Stnd.Description, -Underhood.ID) %>% group_by(Model, Displ, Cyl, 
    Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG > 35)), (EPA.GV.Data %>% filter(Veh.Class == "station wagon", 
    Fuel.Type1 %in% c("Diesel")) %>% select(-Cert.Region, -Stnd, -Stnd.Description, 
    -Underhood.ID) %>% group_by(Model, Displ, Cyl, Fuel.Type1, Trans) %>% summarise(Combine.MPG = round(mean(Cmb.MPG.FT1), 
    0), Air.Pollution.Score = max(Air.Pollution.Score), Greenhouse.Gas.Score = max(Greenhouse.Gas.Score)) %>% 
    filter(Combine.MPG >= 34))) %>% ggplot(aes(x = reorder(Model, desc(Combine.MPG)), 
    y = Combine.MPG, fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    theme_classic() + geom_text(aes(label = round(Combine.MPG, 0)), size = 6, 
    hjust = 1.2, position = position_dodge(0.9)) + xlab("Vehicle Model & Make") + 
    ylab("Combined Fuel Economy (MPG)") + scale_y_continuous(limits = c(0, 60), 
    breaks = seq(0, 60, 10)) + theme(plot.title = element_text(size = 15, face = "bold", 
    hjust = 0)) + theme(plot.subtitle = element_text(size = 13)) + theme(axis.title.y = element_blank()) + 
    theme(axis.title.x = element_text(size = 15), axis.text = element_text(size = 13)) + 
    theme(legend.title = element_text(size = 14, color = "black"), legend.text = element_text(size = 13, 
        color = "black")) + guides(fill = guide_legend(title = "Fuel Type")) + 
    scale_fill_manual(values = c("goldenrod1", "dodgerblue3")) + scale_x_discrete(labels = c(`KIA Niro FE` = expression(bold("KIA Niro FE")), 
    parse = TRUE)) + ggtitle("KIA Niro FE: Best Fuel-Efficient Eco-Friendly Car") + 
    coord_flip()

grid.arrange(StationWagon1, StationWagon2, StationWagon3, nrow = 2)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-23-1.png)

**Findings:**

1.  HYUNDAI Ioniq Blue is the most Fuel-Efficient & Environment friendly station wagon and have a mileage of &gt;50 miles per gallon.
2.  Listed Gasoline Powered Cars are among the Best Environnmental Performers.

### Which is better a Diesel or Gasoline Engine?

``` r
# To Visualize whether Diesel is more efficient or Gasoline
FF1 <- EPA.GV.Data %>% filter(Fuel.Type1 != "Electricity") %>% filter(Veh.Class %in% 
    c("small car", "midsize car", "large car", "station wagon")) %>% group_by(Fuel.Type1) %>% 
    summarise(FuelEconomy = mean(Cmb.MPG.FT1)) %>% ggplot(aes(x = Fuel.Type1, 
    y = FuelEconomy, fill = Fuel.Type1)) + geom_bar(stat = "identity", position = "dodge") + 
    theme_classic() + ggtitle("Diesel Cars operate more efficiently than Gasoline Cars") + 
    xlab("Fuel Type") + ylab("Gas Mileage (Miles/Gallon)") + guides(fill = FALSE) + 
    theme(plot.title = element_text(size = 13, face = "bold", hjust = 0.5)) + 
    theme(axis.title = element_text(size = 12), axis.text = element_text(size = 11)) + 
    scale_fill_manual(values = c("goldenrod1", "coral1", "dodgerblue3"))

# To Visualize whether Disel Cars have more impact on Environment or
# Gasoline
FF2 <- EPA.GV.Data %>% filter(Fuel.Type1 != "Electricity") %>% filter(Veh.Class %in% 
    c("small car", "midsize car", "large car", "station wagon")) %>% group_by(Fuel.Type1) %>% 
    summarise(AirPollutionScore = mean(Air.Pollution.Score)) %>% ggplot(aes(x = Fuel.Type1, 
    y = AirPollutionScore, fill = Fuel.Type1)) + geom_bar(stat = "identity", 
    position = "dodge") + theme_classic() + ggtitle("Gasoline Cars are better than Disel Cars for Environment") + 
    xlab("Fuel Type") + ylab("Air Pollution Score") + theme(legend.position = c(0.14, 
    0.8)) + theme(plot.title = element_text(size = 13, face = "bold", hjust = 0.5)) + 
    theme(axis.title = element_text(size = 12), axis.text = element_text(size = 11)) + 
    scale_fill_manual(values = c("goldenrod1", "coral1", "dodgerblue3")) + guides(fill = guide_legend(title = "Fuel Type"))


grid.arrange(FF1, FF2, nrow = 1)
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-24-1.png)

**Findings:**

1.  Diesel Cars operate more efficiently than Gasoline Cars.
2.  Gasoline Cars have less negative impact on Environment in comparision with Diesel Cars.

### What is the affect of Fuel & Transmission Type on Fuel-Economy/Gas-Mileage?

``` r
# To Visualize the affect of transmission type on fuel economy
EPA.GV.Data %>% separate(col = Trans, into = c("Transmission.Type", "Num.Of.Gears"), 
    sep = "\\-") %>% filter(Veh.Class %in% c("small car", "midsize car", "large car", 
    "station wagon")) %>% filter(Fuel.Type1 %in% c("Gasoline", "Diesel"), !(Transmission.Type %in% 
    c("SCV", "AMS"))) %>% transform(newcol = paste(Fuel.Type1, Transmission.Type, 
    sep = "--")) %>% group_by(newcol) %>% summarise(FuelEconomy = mean(Cmb.MPG.FT1)) %>% 
    ggplot(aes(x = reorder(newcol, FuelEconomy), y = FuelEconomy, fill = newcol)) + 
    geom_bar(stat = "identity", position = "dodge") + theme_classic() + ggtitle("On Average which is the most Fuel-Efficient Environment Friendly Blend?", 
    subtitle = "Gasoline with Continuously Variable Transmission(CVT) Type") + 
    xlab("Fuel & Transmission Type") + ylab("Average Gas Mileage (Miles/Gallon)") + 
    guides(fill = FALSE) + geom_text(aes(label = round(FuelEconomy, 0)), size = 5, 
    hjust = 1.2, position = position_dodge(0.9), color = "white") + theme(plot.title = element_text(size = 13, 
    face = "bold", hjust = 1)) + theme(plot.subtitle = element_text(size = 11, 
    hjust = 0.5)) + theme(axis.title = element_text(size = 12), axis.text = element_text(size = 11)) + 
    scale_fill_manual(values = c("cyan3", "darkcyan", "lightgrey", "lightgrey", 
        "lightgrey", "navy", "lightgrey", "lightgrey")) + coord_flip()
```

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-25-1.png)

**Findings:**

1.  Gasoline powered cars with Continuously Variable Transmission(CVT) Type have highest fuel efficiency.
2.  For Diesel cars manual transmission would be more fuel-efficient than automatic or semi-automatic transmission.

### Which is the most fuel-efficient car within each vehicle class? And what are their characteristics?

![alt text]( https://github.com/SUMansi/EPA_GreenGuide/blob/master/EDA_Figure/unnamed-chunk-26-1.png)

| Model                        | Displ | Transmission.Type | Fuel.Type1 | Veh.Class     | SmartWay | FuelEconomy | CO2Emission | Greenhouse.Gas.Score | Air.Pollution.Score |
|:-----------------------------|:------|:------------------|:-----------|:--------------|:---------|:------------|:------------|:---------------------|:--------------------|
| CHEVROLET Volt               | 1.5   | CVT               | Gasoline   | small car     | Elite    | 42          | 51          | 10                   | 7                   |
| MITSUBISHI Mirage            | 1.2   | CVT               | Gasoline   | small car     | Yes      | 39          | 225         | 9                    | 5                   |
| TOYOTA Prius c               | 1.5   | CVT               | Gasoline   | small car     | Elite    | 46          | 193         | 10                   | 7                   |
| CHEVROLET Malibu             | 1.8   | CVT               | Gasoline   | midsize car   | Yes      | 46          | 194         | 10                   | 3                   |
| FORD Fusion Hybrid           | 2.0   | CVT               | Gasoline   | midsize car   | Yes      | 42          | 211         | 9                    | 7                   |
| HYUNDAI Ioniq Plug-in Hybrid | 1.6   | AutoMan           | Gasoline   | midsize car   | Elite    | 52          | 75          | 10                   | 7                   |
| FORD C-MAX Hybrid            | 2.0   | CVT               | Gasoline   | large car     | Yes      | 40          | 222         | 9                    | 7                   |
| HYUNDAI Ioniq                | 1.6   | AutoMan           | Gasoline   | large car     | Elite    | 55          | 163         | 10                   | 7                   |
| HYUNDAI Ioniq Blue           | 1.6   | AutoMan           | Gasoline   | large car     | Elite    | 58          | 154         | 10                   | 7                   |
| KIA Niro                     | 1.6   | AutoMan           | Gasoline   | station wagon | Elite    | 49          | 183         | 10                   | 7                   |
| KIA Niro FE                  | 1.6   | AutoMan           | Gasoline   | station wagon | Elite    | 50          | 177         | 10                   | 7                   |
| KIA Niro Touring             | 1.6   | AutoMan           | Gasoline   | station wagon | Yes      | 43          | 207         | 9                    | 7                   |
