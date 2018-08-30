------------------------------------------------------------------------

Introduction
============

As per consumer expenditure survey, on average household in united states spends 1/5th of total expenditure on transportation, making it the second largest expenditure category after housing. With fuel prices on the rise, an individual can save a huge amount in fuel expenditure by choosing a Fuel-Efficient Car. Analysis of EPA Green Guide data was carried out to help those in the market for a "Green Car" because of fuel costs and environmental impact. As per data, on average City/Highway Mileage for Green cars is much more, compared to the less Eco-Friendly cars.

| Green Car | City/Hwy Gas Mileage (Miles/Gallon) | City/Hwy CO2 Emissions (Grams/Mile) |
|-----------|-------------------------------------|-------------------------------------|
| No        | 21.8                                | 416.6                               |
| Yes       | 33.8                                | 256.4                               |

The data includes information about Vehicle make-n-model, Gas Mileage, CO2 Emission, Fuel Type, Transmission Type etc. by Vehicle Segment. Based on our analysis, we have learned that Gas Mileage depends on various factors such as: Engine Size in Liters, Number of Cylinder, Transmission Type & Fuel Type. Additionally, CO2 Emission is directly related to the amount of fuel consumed by car.

Further we have explored the data in detail to find answers to the questions such as: Is there a relationship between Engine Size and CO2 Emission? Which is better a Diesel or Gasoline Engine? Does Transmission type have an impact on Mileage? Which car is most fuel efficient and have least negative impact on environment within different vehicle segment?

------------------------------------------------------------------------

### Affect of Engine Size on Fuel-Economy/Gas-Mileage

The Size of the Engine (i.e. Engine's Capacity/Displacement) has a huge impact on Gas Mileage & CO2 Emissions. Usually, car with the small engine has better fuel economy as compared to a car with the large engine. A good example would be comparing the same Car Model, only differing in size of the engine:

| Car Model         | Engine Size(Liters) | Fuel Type | City/Hwy Gas Mileage (Miles/Gallon) | City/Hwy CO2 Emissions (Grams/Mile) |
|:------------------|---------------------|-----------|-------------------------------------|-------------------------------------|
| CHEVROLET Sonic 5 | 1.4                 | Gasoline  | 32                                  | 280                                 |
| CHEVROLET Sonic 5 | 1.8                 | Gasoline  | 29                                  | 306                                 |
| HYUNDAI Elantra   | 1.4                 | Gasoline  | 35                                  | 256                                 |
| HYUNDAI Elantra   | 1.6                 | Gasoline  | 29                                  | 305                                 |

**HYUNDAI ELANTRA** achieved mileage of 35 MPG from a 1.4-liter engine while it achieved mileage of only 29 MPG from a 1.6 liter engine, a difference of 6 more miles per gallon with a change in engine size.

*Figure 1: Relationship between Engine Size, Gas Mileage and CO2 Emission*

<img src="StoryTellingDocument_files/figure-markdown_github/unnamed-chunk-5-1.png" angle=90 style="display: block; margin: auto;" />

Engine Capacity determines the amount of fuel the engine burns. The larger the engine capacity, more likely it is to burn more fuel as it produces more power. Hence, the more fuel it uses per mile, the more CO2 it emits. Therefore, for maximum fuel efficiency, select a vehicle with engine capacity of less than or equal to 2 Liters.

------------------------------------------------------------------------

### Affect of Fuel & Transmission Type on Fuel-Economy/Gas-Mileage

On Average Diesel Cars give great mileage. As per the table below, Diesel Cars typically delivers approximately 20% better fuel economy than similar performing Gasoline Cars. However, diesel produces more pollutants , which have a negative impact on air pollution.

| Car Model       | Engine Size(Liters) | Fuel Type | Transmission Type | City/Hwy Gas Mileage (Miles/Gallon) | Air Pollution Score |
|:----------------|---------------------|-----------|-------------------|-------------------------------------|---------------------|
| CHEVROLET Cruze | 1.6                 | Diesel    | Man               | 37                                  | 3                   |
| CHEVROLET Cruze | 1.4                 | Gasoline  | Man               | 32                                  | 6                   |
| JAGUAR XE       | 2.0                 | Diesel    | SemiAuto          | 36                                  | 1                   |
| JAGUAR XE       | 2.0                 | Gasoline  | SemiAuto          | 28                                  | 7                   |

Air Pollution score ranges from 0 (Worst) to 10 (Best).

**JAGUAR XE** if powered by Diesel, is more Fuel-Efficienct than if powered by Gasoline. However, diesel emissions compared to gasoline emissions contribute much more to the Air Pollution as per the EPA score.

In terms of best fuel , the choice between diesel and gasoline doesn't seem to be straighforward. Therefore, before electing the car for high fuel efficiency , seek out for other factors as well such as transmission type. Car's transmission make sure that the right amount of power is distributed across car wheels to drive at a given speed.

*Figure 2: Relationship between "Fuel & Transmission Type" and "Gas-Mileage"*

<img src="StoryTellingDocument_files/figure-markdown_github/unnamed-chunk-7-1.png" angle=90 style="display: block; margin: auto;" />

CVT & Automated Manual transmission type provides more gas mileage than any other transmission type for gasoline cars. However, for diesel cars manual transmission would be more fuel-efficient than automatic or semi-automatic transmission.Now as we know diesel cars cause more pollution than gasoline cars, therefore, prefer gasoline cars with Continuously Variable transmission(CVT) or Automated Manual transmission to achieve high fuel efficiency and to conserve environment .

------------------------------------------------------------------------

### Most Fuel Efficient and Environmental Friendly Car Model within different Vehicle Segments

*Figure 3: Best Fuel Efficient Eco-Friendly Car*

<img src="StoryTellingDocument_files/figure-markdown_github/unnamed-chunk-8-1.png" angle=90 />

All the above listed cars are among the best environnmental performers and are powered by gasoline and have an engine capacity of less than or equal to 2 Liters.

These cars have less impact on environment and have high-fuel efficiency as well. As per the analysis:

1.  **TOYOTA Prius c** is the best Eco-Friendly Fuel Efficient Small Car.
2.  **HYUNDAI Ioniq Plug-in Hybrid** is the best Eco-Friendly Fuel Efficient Medium Size Car.
3.  **HYUNDAI Ioniq Blue** is the best Eco-Friendly Fuel Efficient Large Car.
4.  **KIA Niro FE** is the best Eco-Friendly Fuel Efficient Station Wagon.

We can conclude that Fuel-Efficient cars use less gasoline than other cars to travel the same distance ,hence less CO2 is released in the atmosphere. For purchasing Fuel-Efficient Car , ensure that the car's engine size is not large and it is powered by gasoline with either Continuous Variable Transmission or Automated Manual Transmission. Now based on the research, car buyers can navigate the green car marketplace to find the car that best suits their need for vehicle size.
