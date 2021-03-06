# Analysis of NYC Bike Share Citi Bike Data
## by Minjian Wu


## Dataset

NYC Bike Share operates Citi Bike program and generates data regarding the program, including trip records, a real time feed of station status and monthly reports. The Citi Bike program data is exclusively generated by the operator NYC Bike Share, a limited liability corporation solely owned by Motivate. The dataset and documentation on the data can be found via this link https://www.citibikenyc.com/system-data.

The data includes (for each month of a year):
- Trip Duration in seconds
- Start Time and Date
- Stop Time and Date
- Start Station Name
- End Station Name
- Station ID
- Station Lat/Long
- Bike ID
- User Type (Customer = 24-hour pass or 3-day pass user; Subscriber = Annual Member)
- Gender (0 = unknown; 1 = male; 2 = female)
- Year of Birth

This data has been processed to remove trips that are taken by staff as they service and inspect the system, trips that are taken to/from any of the “test” stations, and any trips that were below 60 seconds in length (potentially false starts or users trying to re-dock a bike to ensure it's secure).

In this study, we are investigating the NYC bike share data in the year of 2020. Due to the volume of downloads I choose not to do it manually. Instead, I use Beautifulsoup and requests to parse the domain HTML (https://s3.amazonaws.com/tripdata/index.html), and then automate the downloading process with requests and zipfile and save the unziped spreadsheets to the working folder with Pandas' to_csv method.

The downloaded spreadsheets are read in and merged into one big dataframe that holds the record for the whole year. After that, I wrangle the dataframe - remove redundant information, remove any duplicated and NaN data, remove any apparent outliers, modify datatypes to suit, and create additional features for analyses later on.


## Summary of Findings

In exploring the cleaned data, I found that trip duration is right skewed with mode at around 500 seconds(~10 min). The spread of riders' age is slightly bimodal but generally right skewed with modes at around the 30s and the 50s. It makes sense for these two age groups to lead the bike hire counts as most people use a bike for work/exercise/grocery shopping etc. There are much more subscribers (Annual Member) than customers (24-hour pass or 3-day pass user). Subscribers are expected to be stably active and this means there should not be much randomness in bike rides data collected. About twice as many males than females use shared bikes, although this bias may be due to gender proportions in the population of NYC. In exploring the peak times for bike rides, I found that the peaks are during the summer months (as expected), with September being the busiest month. Although the number of daily bike rides almost flats out at high levels throughout August and September, there doesn't appear to be a particular pattern around the activities each day in a month. From a ridgeline plot, one could say that throughout 2020, the first half of each month has more bike riding activities than the second half, but the difference would only be marginal. But in general, there is no clear pattern of one day being busier / quieter than the rest. Within a day, bike rides usually peak at 8am and then around 5pm, with more people ride bikes in the afternoon, as bike activities drop slightly in the morning passing the peak time at 8 and pick up the pace gradually from lunchtime all the way towards late afternoon. This pattern seems to follow a typical work/social/home schedule and it is not affected by whether the day is in a warm/hot or cold month. It then follows that the peaks are likely related to people using bikes to commute between work and home. In terms of rider population, there are much more male subscribers than the other gender/user types. Male, aged between 25 and 35 are the population that ride bikes the most in the city. Either because of a larger population base or an age/gender preference, this age group within the males plays a big role in bike hiring. It then leads to the conclusion that there is a strong positive correlation between number of bike rides and a male gender, an age group of 25 to 35 and an annual membership.

Outside of the main variables of interest, I also computed the straight line distances between start and end stations. In exploring this data, I found the distances are right skewed with mode at around 1.2km. I also pin-pointed the most popular start and end stations on a map of NYC, and found that the top start and end stations share exactly the same locations, except that there are slightly different ranking orders of popularity. Since we had got rid of those trips that start and end at the same location (i.e. those with a straight line distance of zero) in data wrangling, the coincidence that most trips still start and end between the same stations indicates a true popularity for bikes at these locations - near parks and/or central. So if a company was to invest in putting more bikes or in setting up a snacks/drinks bar/mobile shop then these locations are ideal. In exploring the straight line distances vs. trip duration, I found that although longer distance journeys obviously would take a longer time, shorter distance journeys oftentimes also take a longer (than needed) time. This is likely attributed to riders making stops or taking a detour between the start and end points. In exploring this further to see the influence from age/gender/usertype, I found that younger people (under the age of 30) take more time on a bike ride, regardless of the start and end distances. Also there is a tendency for customers (who are on a 24-hr or 3-day pass) to spend longer times on a same distance trip than subscribers (who are on an annual membership). This makes sense because customers would wish to make most use of their limited-time passes. On the other hand, there is no tendency for women to spend more / less time on a ride than men other than due to speed of ride. Lastly, there is no differential pattern in distance vs time in relation to age, other than that older people are less likely to complete a trip in shorter times due to them riding at lower speeds.


## Key Insights for Presentation

For the presentation, I first introduce the dataset and then present two maps, each with the top 10 popular start and top 10 popular end stations pinned (with an interactive pop up to show the station ID). Then I moved on to present the most popular bike riding month in 2020, followed by the most popular day in a month, and the most popular time (hour) in a day. Lastly I presented the relationship for between-station distance vs trip duration against gender/user type and age.

The visualisations demonstrate that the most popular stations are located near parks or at a central location, and that most people ride in summer months, and in particular at around the morning peak at 8am and the afternoon peak at 5pm. Lastly, customers who are on a 24-hr or 3-day pass tend to spend more time on their bike rides, probably because they would like to make the most out of their limited-time passes.
