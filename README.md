# Drone Network Analysis and Delay Prediction

Exercise:

It's July 26th in the year 2050. You are operating an international passenger transportation system with drones which are deployed in services around the world.
Your network consists of regional services within a country and global services which connect multiple countries. All your services are circular services, that is, they start and end at the same location. Once they're back at the start location, a new rotation starts. Changing from service A to service B at a station which both services call is always possible.\
The goal of this exercise is to analyze the current state of this network and to optimize it for the future.

## 1. Network analysis
1) How many drones are deployed in regional services in Europe?
2) How many station pairs are directly connected in the network (i.e. going from A to B without changing services)?
3) Which countries cannot be reached from Germany (including indirect connections)?
4) What's the fastest route from Utica in the US to Boumerdas in Algeria in the current network?
5) What's the average time it takes to get from a random station to another random station?
6) How would you improve this average time if you could set up an additional service?
7) Which station in your network would you consider the most important one?
8) If you could set up the network from scratch with the existing drones, what would you change?

## 2. Predicting on-time arrivals
1) Before starting the analysis, you ask your colleagues about their opinion on what influences the on-time arrival of a service. Which statement is correct?
   - “From my former experience as a pilot I can say that drones from 'Barber LLC', 'Sharp Ltd', and 'Freeman-Garrison' are very difficult to get to the destination on time.”
   - “The technology of drones is already so sophisticated that wind has no impact on the arrival time. “
   - “Services in Colombia are almost never on time because of the difficult climate close to the equator.”
   - “Customers pay much more for the global services. So I assume that these services have less delays.”
   - “The heavier the drone, the more expensive it is to do a speed up in order to catch up delays. Therefore the bigger drones will have more delays.”
2) What is the biggest driver of the arrival delay?
3) If your only goal is to bring your passengers to the destination on time, which drones would you replace with new ones?
4) Can you predict the delays of all station arrivals in the last days of July?
5) Which service will have the least delays in the last days of July?

## Data
### stations.csv
List of stations which are included in your services (i.e. you have permission for starting and landing there)
- continent: Continent on which station is located
- contry_code: Alpha 2 code of country of station
- lat_lng: Coordinates in decimal degrees
- major_city: Well-known city which is somehow in the vicinity of the station for easier reference
- station: Name of the station

### services.csv
List of stations which each service calls
- service_id: Id of service
- station: Name of the station
- type: Geographical scope of the service ('regional' or 'global')
- station_order: Order of the station in the rotation

### drones.csv
List of drones which are employed in your services
- drone_id: Id of drone
- service_id: Id of service in which the drone is used
- capacity_persons: Maximum number of persons which can be transported
- fuel_consumption_gm_per_mile: Grams of fuel which are necessary for flying one mile under standard conditions
- manufacturer: Manufacturer of drone
- max_altitude_ft: Maximum altitude in feet
- max_capacity_fuel_gm: Maximum capacity of the fuel tank
- min_capacity_fuel_gm: Fuel reserve in grams which needs to be exceeded at all times to ensure proper operation
- operating_speed_mph: Flying speed for optimal fuel consumption under standard conditions
- optimal_altitude_ft: Flying altitude for optimal fuel consumption under standard conditions

### schedules.csv
Schedules for every day in July 2050 for all of your services
- service_id: Id of service
- station_call_id: Id of a certain call (arrival and departure) at the station
- station: Name of station
- scheduled_arrival_datetime: Arrival date and time (UTC) at the station as planned
- scheduled_departure_datetime: Departure date and time (UTC) at the station as planned
- forecast_windspeed_kts: Most recent forecast of windspeed at the station in knots prior to departure at the previous station

### actuals.csv
Actual arrival and departure times for all days prior to July 26th, 2050
- service_id: Id of service
- station_call_id: Id of a certain call (arrival and departure) at the station
- station: Name of station
- scheduled_arrival_datetime: Arrival date and time (UTC) at the station as it actually happened
- scheduled_departure_datetime: Departure date and time (UTC) at the station as it actually happened
- actual_windspeed_kts: Actual windspeed at the station at the time of landing (arrival)
- arrival_delay_seconds: Deviation to the planned arrival time (positive numbers are delays)
- actual_fuel_consumption_gm_per_mile: Grams of fuel consumed between departing at the previous station and arriving at the current station
