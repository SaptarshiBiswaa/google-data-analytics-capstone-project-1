# How casual vs annual member users interact differently with Cyclistic, a bike-share service? 
### (Aimed for devising marketing strategy for Cyclistic to convert casual riders into subscribed members)

![bike-chicago-AdobeStock_53728138-1024x680](https://github.com/user-attachments/assets/6338ea02-d6e9-4868-9dd5-662d123096eb)


## Background

Welcome to the Cyclistic bike-share analysis case study! In this project, I will be diving into the data of Cyclistic, a fictional bike-share company based in Chicago. This is the final capstone project in the Google Data Analytics Professional Certificate Course offered by Coursera. Imagining the position of a junior data analyst on the marketing team, my role is to help design a strategy to convert casual riders into annual members—an essential goal for Cyclistic's future success.

Cyclistic, founded in 2016, operates a fleet of over 5,800 bicycles across 692 stations throughout Chicago. The company stands out by offering a range of bikes, including traditional bicycles, reclining bikes, hand tricycles, and cargo bikes, making it accessible to a wide range of users, including those with disabilities. While the majority of riders use standard bikes, approximately 8% opt for assistive options. Cyclistic has seen success in attracting both leisure riders and commuters, with around 30% of users riding daily for work.

Cyclistic's marketing strategy so far relied mostly on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. However, Cyclistic's finance analysis team has suggested that customers who use single-ride or full-day passes, namely casual riders, are less profitable than annual members. The marketing team, led by Lily Moreno, is keen to understand how casual riders and annual members differ in their bike usage patterns and how these insights can inform a targeted strategy to convert casual riders into more profitable annual members. The key questions they want to answer,

* How do annual members and casual riders use Cyclistic bikes differently?

* Why would casual riders buy Cyclistic annual memberships?

* How can Cyclistic use digital media to influence casual riders to become members?

My role is to answer the first question and come-up with **3 recommendations** that can be enacted to boost subscription. On that goal, below I will analyze and present the ride-share data of Cyclistic during Jan to Dec 2020 to provide data-driven recommendations for its marketing team. The analysis is performed with the help of **Microsoft excel** for **data preparation, processing, visualization and insights**.


## Data source

We will study a [public data](https://divvy-tripdata.s3.amazonaws.com/index.html) made available by Motivate International Inc. (with [license](https://divvybikes.com/data-license-agreement)) and use the data between Jan to Dec 2020 to act as the trip history data of Cyclistic for that year. To ensure data privacy, riders' personal information such as credit card number has been scrubbed. This prevents us from examining certain depths of information such as which distinct ride passes belong to the same rider or, what are the home locations of riders.

## Brief description of the raw data

The data of the year 2020 is organized between 10 csv files, one for the interval Jan-Mar, and one each for rest of the months. Their names are formatted as YYYYMM-divvy-tripdata, except the file for the Jan-Mar trip history has name Divvy_Trips_2020_Q1. Within each file, there are 13 fields:

1. **ride_id**(categorical): Each trip is assigned a unique ride ID which is text valued.
2. **rideable_type**(categorical): The bike type used for the ride, takes value in {"docked_bike", "electric_bike", "classic_bike"}.
3. **started_at**(datetime): The trip start date and time.
4. **ended_at**(datetime): The trip end date and time.
5. **start_station_name**(categorical): Text valued name of the Cyclistic station where the trip started.
6. **start_station_id**(categorical): The ID of the start station, which corresponds to a unique identifier assigned to each Cyclistic station. This can be a number or, a text.
7. **end_station_name**(categorical): Name of the Cyclistic station where the trip ended.
8. **end_station_id**(categorical): ID of the trip end station.
9. **start_lat**(numeric): Latitude of the trip start location.
10. **start_lng**(numeric): Longitude of trip start location.
11. **end_lat**(numeric): Latitude of the trip end location.
12. **end_lng**(numeric): Longitude of the trip end location.
13. **member_casual**(categorical): The type of customer who took the ride, this can be either "member": Someone with annual subscription for the service or, "casual": A casual rider.

## Data processing:

The aggregated data consists of around 3.5 million rows, far surpassing the maximum 1,048,576 rows in an Excel worksheet. As a result, we process the data, as well as conduct part of the analysis separately within each data file. Then summarize each of them by building relevant pivot tables which are latter combined in a separate excel file for collective analysis.

### Cleaning measures: Each column is processed separately

* The $filter$ tool of Excel has proven particularly useful for this. By scrolling down the list of distinct entries shown by the filtering window under a column, we can identify if the latter contains any **invalid or, unwanted entries, blank cells** etc., and filter the respective rows for further processing.

    $\underline{Findings}$: The fields *ride_id*, *rideable_type*, *started_at*, *ended_at* and *member_casual* have no invalid entries. But, the other fields have some of the cells blank. Instead of erasing the corresponding rows entirely, we can leverage whatever pieces of information they contain.

* **Duplicates**: Each ride data is supposed to carry a unique *ride_id*. We find no duplicates for this field.

*  **Swapped values**: We find for some of the rows the entries of the *started_at* and *ended_at* fields are exchanged. This is corrected by using the $IF$ function of Excel to swap the entries if the time under *ended_at* is less than the *started_at* time.


### Added columns

We add the following columns derived from the existing data.

1. **ride duration**(time): Calculated by taking difference of the *ended_at* and *started_at* columns, and formatted as h:mm:ss.
2. **day of week**(categorical): The day of week when each ride started, denoted by a number between 1 to 7 with 1=Sunday and 7=Saturday.
3. **Month**(categorical): A number between 1 to 12 denoting the month of ride start date.
4. **2 hour groups**(categorical): The 24 hours of a day is divided into 12 groups each covering a 2 hours interval, such as the duration of 2 PM to 4 PM is denoted by 14:00:00 and so on. Each ride is assigned a group based on ride start time.
5. **4 hour groups**(categorical): A similar definition with 4 hours gap between groups.

## Data analysis and visualization

Excel is used to perform all the analysis and make the following charts. The rides taken throughout 2020 are distributed into various categories.

<img width="1042" alt="ride share charts 1 57 30 AM" src="https://github.com/user-attachments/assets/9282fee4-a632-466c-b1f4-530ed022edc8" />

<img width="664" alt="popular stations" src="https://github.com/user-attachments/assets/067d3f38-e6a6-4bab-b6f2-d1e7c1062b69" />

## PowerBI Dashboard (made using Power BI Service)

<img width="1298" alt="Screen Shot 2025-06-08 at 8 30 05 PM" src="https://github.com/user-attachments/assets/979fc493-1fee-4eae-8f3f-8a0f8446e73f" />


### Key trends in the data

1. (From E) Members constitute most of the rides.

2. (From A) Members make about same number of trips throughout the week with slight decline on weekends. Whereas, casual riders tend to use the ride-share mostly on weekends. Nevertheless, the total ride count of casual users stays below members' on each day of week, although it becomes almost matching on weekends.

3. (From B) The average ride length stays about uniform across each day of the week for both casual riders and members. However, casual riders, on average, use the service for a significantly longer duration than members.

4. (From F) Members typically use the ride service from morning until evening with a peak near afternoon, while casual riders tend to access it from noon till evening with peak usage during afternoon. The count of members' usage exceeds casual riders' almost throughout the day.

5. (From D) The Average ride duration of members remains about the same throughout the day, whereas the average usage length of casual riders peaks near late night while remaining about similar throughout the day. In any case, the ride duration of casual riders significantly exceeds the members'.

6. (From G) At an arbitrary end station casual riders are much more likely to visit than members over the year. The ride count of casual riders significantly outweight members' at many different end stations than the other way around. We don't see any such trend by considering the start stations.

7. (From C) During weekends both members and casual riders mostly use the ride from noon till evening. Compared to that, over weekdays some of weight from noon time is shifted towards morning hours which is much significant among member users and less so for casual riders.

8. For both members and casual users, almost all the top visited starting stations are also top listed as popular ending stations. We also see, members mostly visited stations which are close to amusement places, on the other hand, casual riders like to go to a wide variety of places close to banks, hospitals, hotels, restaurants and stores, apartment complexes etc.

### Summary of differences between members and casual riders

Aspect | Casual      | Member      |
-------| ----------- | ----------- |
$Ride\space length$ (each day or, over multiple time-frames) | Much longer (on average, **peaks at night**)     | Shorter     |
$Ride\space count$ (daily, hourly and total wise) | Smaller   | Larger (significantly in weekdays)      |
$${Preferred\space ride\space day}$$ | Weekends   | All over the week     |
$${Weekday\space most\space usage\space hours}$$ | Noon to evening | Morning to evening |
$${End\space station\space neighborhood\space types}$$| Wide-variety | Specific (mostly amusement) |

## Data-driven recommendations

Since the original pricing structure of Cyclistic is not specified I will also make assumptions or, suggestions about it in the following recommendations.

1. Since casual users typically use the ride service for much longer duration than members, and more so during off hours, setting up some kind of pricing structure based on duration and time of usage which becomes discounted and more flexible for annual members, would greatly encourage annual subsription among unsubscribed users. At the same time, the casual riders would find a compelling reason to become members.

2. Casual usage peaks a lot during weekends compared to weekdays, whereas members generally use the service almost uniformly across a week. Therefore, implementing a day specific non-uniform pricing for general usage and making it uniform for members would also incentivise the casual to member conversion.

3. As casual riders frequently travel to a wide-variety of places than members even after constituting a smaller fraction of the total ride count, it will also be effective to offer more flexibility of visit stations for members than casual users.


## Limitations in the data and rooms for expanded study

Here we enlist possible information not included in the above data which we belive would be able to deepen our understanding on the riders' behavior and help develop more accurate and effective strategies.

1. **Distinct riders**: As we already mentioned, some kind of personal information which would enable us to tag each ride to a distinct rider would be useful in multiple accounts. Firstly, we can identify the top casual users and make more targeted strategies. Secondly, this would allow us to make stats and find distributions of person based usage of the ride service which could reveal many more trends and generate ideas. Furthermore, we could also track conversion of casual users to members within the data and investigate the key driving forces.

2. **Home (or, office) address**: Along the same line having access to the home addresses of users would reveal further insights. For example, how often riders use the service to commute to and from home (office) vs between other places. We could then make membership discounts for travels to home (office), or, some useful places nearby.


3. **Multiple years**: Studying data across many years would also enable us to find trends in monthly or, quarterly usage of the service and make marketing strategies accordingly, such as, make some seasonal discount offerings, or, choose focused marketing zone based on seasons.


4. **Bike types**: In the above studied data of the year 2020, most of the months only had *docked bike* as the rideable type. The *electric bike* started appearing only from July and the *classic bike* was just introduced in end of the year, in December. It appears, the latter two bike types were first introduced in the latter part of 2020. Therefore, reliable trends regarding bike types will start becoming apparent by studying data of subsequent years.
