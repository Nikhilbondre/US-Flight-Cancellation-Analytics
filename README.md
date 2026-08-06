# US Flight Delay & Cancellation Analytics Dashboard

An end-to-end Power BI analytics project examining US domestic flight 
performance from 2019–2023 — covering delay trends, root causes, 
airline rankings, and airport-level performance.

**Page1**
<img width="1375" height="770" alt="Screenshot 2026-08-06 232330" src="https://github.com/user-attachments/assets/66666185-ab90-4d3e-a285-8117f383d5d7" />

## Dataset
- **Source:** Kaggle — US Flight Delay Dataset
- **Size:** ~1.05M flight records
- **Time period:** 2019–2023
- **Granularity:** Individual flight level
- **Key fields:** Airline, Origin, Destination, Scheduled/Actual times, 
  Delay minutes by cause (Carrier, Weather, NAS, Late Aircraft, Security), 
  Cancellation status, Distance

Files in this repo:
- `data/raw_flights.csv` — original unprocessed data
- `data/cleaned_flights.csv` — cleaned dataset used in the model

## Tools Used
- **Power BI Desktop** — data modeling, DAX, visualization
- **Power Query** — data cleaning and transformation
- **DAX** — custom measures

## Data Cleaning Process
Performed in Power Query before loading into the model:
- Removed redundant and unused columns to streamline the dataset
- Standardized inconsistent airline name formatting across records
- Handled missing/null values in delay and cancellation fields
- Corrected data types for date, time, and numeric fields
- Verified no duplicate flight records remained after cleaning
- Reviewed extreme/outlier delay values for data quality

## DAX Measures
Key measures built for this dashboard:

```
Total Flights = COUNTROWS(Flights)

Avg Arrival Delay = AVERAGE(Flights[ArrDelay])

Cancellation Rate = DIVIDE(CALCULATE(COUNTROWS(Flights), Flights[Cancelled] = 1), [Total Flights])
Flight On Time % = DIVIDE(CALCULATE(COUNTROWS(Flights), Flights[ArrDelay] <= 15), [Total Flights])

Delay per Flight = DIVIDE( [Total Delay Minutes], [Total Flights])

Total Delay Minutes = SUM(Flights[CarrierDelay]) + SUM(Flights[WeatherDelay]) + SUM(Flights[NASDelay]) + SUM(Flights[LateAircraftDelay]) + 
SUM(Flights[SecurityDelay])
```

**Page 1. Overview**

KPI summary (total flights, on-time %, avg delay, cancellation rate) with year-over-year trend lines for delay and cancellation rate.

2. Delay Causes

Breakdown of total delay minutes by cause (carrier, weather, NAS, late aircraft, security) per year, plus a share-of-total-delay donut chart and a delay-per-flight trend line.

3. Carrier Scorecard

Airline-level performance table and on-time % ranking, highlighting the worst-performing carriers on both delay and on-time rate.

4. Airport Performance

Origin airport delay and traffic volume analysis, highlight the worst-performing major airport.


