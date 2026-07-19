# Hotel Room Pricing Analytics

End-to-end hospitality analytics project focused on hotel room pricing, booking pattern analysis, demand forecasting, and Power BI dashboarding using multi-year reservation data.

## Project Overview

This project analyses multi-year hotel reservation data to optimise dynamic room pricing and improve revenue management for a Chennai-based hotel property with 200 rooms and 3 restaurants. Using data analytics and machine learning, the work aims to predict optimal room rates, uncover demand patterns across sources and seasons, and support decision-making through an interactive Power BI dashboard.

## Business Problem

Dynamic pricing is critical for hotels because room rates must respond to demand, seasonality, and booking behaviour to maximise both occupancy and revenue. The specific business problem addressed here is optimising room rates for the hotel **“Raintree – Anna Salai”** using historical reservation data for fiscal years 2018 and 2019. The project was commissioned to:

- Predict the optimal room rate that maximises revenue per room night.
- Track booking patterns in near real time to understand demand trends by source, room type and period.
- Provide actionable insights on pricing and channel strategy.

## Objectives

- Build a predictive model to estimate room rates based on reservation-level features.
- Analyse booking behaviour by source, room type, continent and time period.
- Design an interactive Power BI dashboard to monitor reservations, rates and booking mix.
- Recommend pricing and data quality improvements to increase revenue realisation.

## Power BI Dashboards

### Hotel Pricing Overview

![Hotel pricing overview dashboard](dashboards/screenshots/your-overview-file.png)

This page summarises key KPIs including total reservations, room‑type mix, and booking sources, with slicers for date, source, and nation to support revenue management decisions.

### Room Rate and Source Mix

![Room rate and source mix dashboard](dashboards/screenshots/your-pricing-file.png)

This view compares average realised room rates across Deluxe, Club Room, Studio and Suite categories, and highlights contribution by core channels such as Company Sales Team and Online Aggregators.

### Trend and Seasonality Analysis

![Trend and seasonality dashboard](dashboards/screenshots/your-trend-file.png)

This dashboard tracks monthly arrival and reservation trends, surfaces seasonality patterns, and shows how booking sources and geographies contribute across the fiscal year.
## Dataset

The core dataset consists of daily reservation-level records for fiscal years 2018 and 2019, with 10 primary fields:

- **Name** – Guest name.
- **Reservation No** – Unique ERP-generated reservation identifier.
- **Room Type** – Room category for the booking.
- **Arrival Date** – Date of customer arrival.
- **Departure Date** – Date of customer departure.
- **Adults/Children** – Number of adults and children in the booking.
- **Nation** – Guest nationality.
- **Source** – Booking source/channel.
- **Room Rate** – Final agreed room rate.
- **Reservation Date** – Date the reservation was made.

Additional processed datasets capture time series of room rates and aggregated booking metrics.

## Data Preparation and Feature Engineering

The data preparation workflow transforms raw ERP exports into an analytical dataset suitable for modeling and dashboarding:

- **Room type grouping** – 14 ERP room types are grouped into business-friendly categories: Deluxe, Club Room, Studio and Suite, based on similar pricing behaviour.
- **Geographic aggregation** – Guests from 118 countries are grouped into continents (Africa, Asia, Australia, Europe, North America, South America, United Nations) for segment-level analysis.
- **Missing value treatment** – Null values in booking source are dropped; null values in continent are replaced with India where appropriate; records with room rates equal to 0 are removed.
- **New feature: Duration** – Length of stay in days is calculated from arrival and departure dates.
- **Encoding categorical variables** – Room type, source, and continent are encoded for use in machine learning models.
- **Outlier treatment** – Outliers in duration and booking time are capped at 4 days and 36 days respectively, and log transformation is applied to room rates to improve distributional properties.

## Exploratory Data Analysis

Exploratory analysis highlights key patterns in booking volumes and pricing.

### Booking Volume and Seasonality

- Fiscal years 2018 and 2019 both show higher reservation counts in Q1 and Q4, with relatively lower activity in Q2 and Q3, indicating seasonal peaks at the start and end of the year.
- Quarterly reservation counts (sample):
  - 2018 – Q1: 12,017; Q2: 10,728; Q3: 10,675; Q4: 10,855.
  - 2019 – Q1: 12,935; Q2: 10,652; Q3: 10,821; Q4: 12,270.

### Source Performance

Booking sources contribute very differently to overall volume:

| Source                 | Reservations |
|------------------------|-------------:|
| Company Sales Team     |       37,908 |
| Online Aggregators     |       32,220 |
| Travel Agency – USA    |        5,188 |
| Travel Agency – Europe |        1,674 |
| Others                 |       14,261 |

### Room Rate by Room Type

Average realised room rates vary materially across room types:

| Room Type | Avg Room Rate (INR) |
|-----------|---------------------:|
| Deluxe    |                4,945 |
| Club Room |                5,430 |
| Studio    |                4,846 |
| Suite     |                8,192 |

Notably, Studio rooms – considered a higher-end category – realise 
