# Data Note

This repository does **not** include raw CSV data files.

## Dataset and Scope

This project uses the official **2017 Yellow Taxi Trip Data** from NYC Open Data.

Useful source links:

- [NYC 2017 Yellow Taxi Trip Data Open Data landing page](https://data.cityofnewyork.us/Transportation/2017-Yellow-Taxi-Trip-Data/biws-g3hs/about_data)
- [Socrata CSV/API endpoint used in the code](https://data.cityofnewyork.us/resource/biws-g3hs.csv)

The notebook and exported script pull a manageable sample directly from the official CSV endpoint instead of relying on local course files.

## Fields Pulled First

The code first requests these fields:

- `vendorid`
- `tpep_pickup_datetime`
- `tpep_dropoff_datetime`
- `passenger_count`
- `trip_distance`
- `ratecodeid`
- `pulocationid`
- `dolocationid`
- `payment_type`
- `fare_amount`
- `tip_amount`
- `tolls_amount`
- `total_amount`

## Working Data Used in This Project

The stored notebook outputs show:

- public-data sample pull: **180,000 rows**
- filtered modeling sample: **116,748 credit-card trips**
- raw API fields pulled first: **13**
- final modeling inputs before one-hot encoding: **21**
- positive class share: about **52.7 percent generous-tip trips**

The code pulls monthly chunks from 2017, with 15,000 rows requested per month.

## Why Credit-Card Trips Only

The final model represents the filtered **credit-card trip subset**, not all taxi trips.

This is important because credit-card tips are recorded in the trip table more consistently than cash tips. Limiting the analysis to credit-card trips makes the target more reliable, but it also narrows the scope of the result.

## Reproducibility Notes

- Reruns require internet access and availability of the NYC Open Data API.
- The code includes an optional Socrata app-token field if retrieval is slow or rate-limited.
- The repository does not include the full 2017 taxi table.
- The result should not be described as performance on all NYC taxi trips.
