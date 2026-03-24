# Data Note

This repo does **not** include raw CSV files.

## Main source

This project uses the official **2017 Yellow Taxi Trip Data** from NYC Open Data.

Useful links (Copy the link address and paste it into a new tab):

- [NYC 2017 Yellow Taxi Trip Data Open Data landing page](https://data.cityofnewyork.us/Transportation/2017-Yellow-Taxi-Trip-Data/biws-g3hs/about_data)
- [Socrata CSV/API endpoint used in the code](https://data.cityofnewyork.us/resource/biws-g3hs.csv)

## Why I did not upload the dataset

I did not upload a local CSV for this repo because:

- the official dataset is public and already available online
- the full 2017 table is very large
- this project was designed to be reproducible directly from the official API
- the notebook and script already show the exact fields and pull method

## How the code reads the data

The notebook and script pull monthly chunks from the official CSV endpoint and keep these fields first:

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

## Working data used in this repo

This public version uses:

- a reproducible public-data slice of **180,000 rows**
- a filtered modeling sample of **116,748 credit-card trips**

## Important limit

The final model represents the filtered **credit-card subset**, not all taxi riders.

This matters because cash tips are not recorded as reliably in the trip table, so I limited the modeling data to credit-card trips for a more consistent target.