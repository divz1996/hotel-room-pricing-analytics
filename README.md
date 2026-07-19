# Hotel Room Pricing Analytics

End-to-end hospitality analytics project focused on hotel room pricing, booking pattern analysis, demand forecasting, and Power BI dashboarding using multi-year reservation data.

## Project Overview

This project analyses multi-year hotel reservation data to optimise dynamic room pricing and improve revenue management for a Chennai-based hotel property with 200 rooms and 3 restaurants.[cite:1] Using data analytics and machine learning, the work aims to predict optimal room rates, uncover demand patterns across sources and seasons, and support decision-making through an interactive Power BI dashboard.[cite:1][cite:2]

## Business Problem

Dynamic pricing is critical for hotels because room rates must respond to demand, seasonality, and booking behaviour to maximise both occupancy and revenue. The specific business problem addressed here is optimising room rates for the hotel **“Raintree – Anna Salai”** using historical reservation data for fiscal years 2018 and 2019.[cite:1] The project was commissioned to:

- Predict the optimal room rate that maximises revenue per room night.
- Track booking patterns in near real time to understand demand trends by source, room type and period.
- Provide actionable insights on pricing and channel strategy.

## Objectives

- Build a predictive model to estimate room rates based on reservation-level features.[cite:1]
- Analyse booking behaviour by source, room type, continent and time period.
- Design an interactive Power BI dashboard to monitor reservations, rates and booking mix.
- Recommend pricing and data quality improvements to increase revenue realisation.

## Dataset

The core dataset consists of daily reservation-level records for fiscal years 2018 and 2019, with 10 primary fields:[cite:1]

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

The data preparation workflow transforms raw ERP exports into an analytical dataset suitable for modeling and dashboarding:[cite:1]

- **Room type grouping** – 14 ERP room types are grouped into business-friendly categories: Deluxe, Club Room, Studio and Suite, based on similar pricing behaviour.[cite:1]
- **Geographic aggregation** – Guests from 118 countries are grouped into continents (Africa, Asia, Australia, Europe, North America, South America, United Nations) for segment-level analysis.[cite:1]
- **Missing value treatment** – Null values in booking source are dropped; null values in continent are replaced with India where appropriate; records with room rates equal to 0 are removed.[cite:1]
- **New feature: Duration** – Length of stay in days is calculated from arrival and departure dates.[cite:1]
- **Encoding categorical variables** – Room type, source, and continent are encoded for use in machine learning models.[cite:1]
- **Outlier treatment** – Outliers in duration and booking time are capped at 4 days and 36 days respectively, and log transformation is applied to room rates to improve distributional properties.[cite:1]

## Exploratory Data Analysis

Exploratory analysis highlights key patterns in booking volumes and pricing.[cite:1]

### Booking Volume and Seasonality

- Fiscal years 2018 and 2019 both show higher reservation counts in Q1 and Q4, with relatively lower activity in Q2 and Q3, indicating seasonal peaks at the start and end of the year.[cite:1]
- Quarterly reservation counts (sample):  
  - 2018 – Q1: 12,017; Q2: 10,728; Q3: 10,675; Q4: 10,855.[cite:1]  
  - 2019 – Q1: 12,935; Q2: 10,652; Q3: 10,821; Q4: 12,270.[cite:1]

### Source Performance

Booking sources contribute very differently to overall volume:[cite:1]

| Source                 | Reservations |
|------------------------|-------------:|
| Company Sales Team     | 37,908[cite:1] |
| Online Aggregators     | 32,220[cite:1] |
| Travel Agency – USA    | 5,188[cite:1] |
| Travel Agency – Europe | 1,674[cite:1] |
| Others                 | 14,261[cite:1] |

### Room Rate by Room Type

Average realised room rates vary materially across room types:[cite:1]

| Room Type  | Avg Room Rate (INR) |
|-----------|---------------------:|
| Deluxe    | 4,945[cite:1]        |
| Club Room | 5,430[cite:1]        |
| Studio    | 4,846[cite:1]        |
| Suite     | 8,192[cite:1]        |

Notably, Studio rooms – considered a higher-end category – realise lower average rates than Club Rooms, signalling a potential misalignment in pricing or positioning.[cite:1]

## Model Development

The modeling workflow focuses on predicting room rates using reservation-level features.[cite:1]

### Approach

- Train/test split of the prepared analytical dataset.
- Baseline **Linear Regression** model fitted to estimate room rates.[cite:1]
- Model refinement attempts via cross-validation (K-Fold) and LASSO regularisation.[cite:1]
- Additional experiments with **Decision Tree** and **Random Forest** models, including hyperparameter tuning.[cite:1]

### Performance

- The linear regression model achieved an RMSE of 17.90% and an R-squared of 14.17%.[cite:1]
- Decision Tree model RMSE was around 955 even after grid-search-based hyperparameter tuning.[cite:1]
- Random Forest model reached an out-of-bag (OOB) score of 0.39.[cite:1]

These results suggest that the available features explain only part of the variability in room rates, and that incorporating richer drivers (e.g., competitor pricing, occupancy levels, marketing campaigns, events) would be necessary to materially improve predictive performance.

## Power BI Dashboard

An interactive Power BI dashboard complements the notebooks by visualising key metrics for pricing and demand analysis.[cite:2]

### Key Views

- **Room Rate by Room Type** – Donut chart showing average room rate across Deluxe, Club Room, Studio and Suite categories.
- **Room Rate by Source Group and Room Type** – Clustered bar chart comparing average room rate across booking sources for each room type.
- **Bookings by Source Group** – Donut chart showing mix of reservations by source group (Sales Team, Online Aggregators, Others, Travel Agencies).
- **Quarterly Reservations** – Bar chart of reservation counts by quarter and year.
- **Monthly Trend Analysis** – Line charts showing count of arrivals and reservations by month and year.
- **Consolidated Dashboard and Final Trend Analysis** – Multi-panel views combining KPIs (e.g., number of reservations, number of countries visited, room-type counts) with trend lines and source breakdowns.

Dashboard screenshots are available in the `dashboards/screenshots/` directory for quick visual inspection.

## Business Insights and Recommendations

The combined analysis and modeling effort led to several practical insights:[cite:1]

- **Seasonal peaks** – Demand is stronger in Q1 and Q4, suggesting opportunities for premium pricing, targeted promotions and capacity planning during these periods.[cite:1]
- **Source mix optimisation** – Company Sales Team and Online Aggregators together drive the bulk of reservations, but their realised rates differ by room type, indicating room for channel-specific pricing strategies.[cite:1]
- **Studio room pricing** – Studio rooms, despite being a higher category, realise lower average rates than Club Rooms and Deluxe rooms. The hotel should reassess Studio pricing, value communication, and bundling to capture more revenue per room night.[cite:1]
- **Data quality improvements** – Incomplete capture of critical fields such as number of adults/children and nationality limits deeper analysis; improving data capture processes will enhance future analytics and model performance.[cite:1]

Specific source-wise average rate comparisons highlight how revenue per room night varies by channel:[cite:1]

| Particulars              | Deluxe (INR) | Club Room (INR) | Studio (INR) | Suite (INR) |
|--------------------------|-------------:|----------------:|-------------:|------------:|
| Online Aggregators       | 4,825[cite:1] | 5,552[cite:1]   | 5,419[cite:1] | 8,316[cite:1] |
| Others                   | 4,960[cite:1] | 5,096[cite:1]   | 4,845[cite:1] | 6,655[cite:1] |
| Sales Team               | 5,128[cite:1] | 5,505[cite:1]   | 4,717[cite:1] | 8,443[cite:1] |
| Travel Agency – Europe   | 4,834[cite:1] | 5,345[cite:1]   | 5,716[cite:1] | 6,768[cite:1] |
| Travel Agency - USA      | 4,355[cite:1] | 4,853[cite:1]   | 4,688[cite:1] | 7,651[cite:1] |

## Repository Structure

The repository is organised to mirror the end-to-end analytics workflow:

```text
hotel-room-pricing-analytics/
├── README.md
├── .gitignore
├── data/
│   ├── raw/                  # Original ERP exports (year-wise reservation data)
│   └── processed/            # Cleaned/aggregated time-series datasets
├── notebooks/
│   ├── pricing_modeling.ipynb        # Data prep, EDA and pricing model development
│   └── time_series_forecasting.ipynb # Time-series analysis and forecasting
├── dashboards/
│   ├── hotel_pricing_dashboard.pbix  # Power BI report
│   └── screenshots/                  # Dashboard preview images
├── reports/
│   └── project_presentation.pdf      # Project presentation
└── docs/
    └── data_dictionary.md           # Field-level documentation
```

## Tools and Technologies

- Python and Jupyter Notebook for data preparation, exploratory analysis and modeling.
- Excel and CSV/Excel time-series workbooks for raw and intermediate data.
- Power BI for interactive dashboarding and visual analytics.
- Classical machine learning techniques including linear regression, decision tree, random forest, cross-validation and regularisation.[cite:1][cite:2]

## How to Navigate This Repo

- Start with `README.md` to understand the business context and key insights.
- Explore `docs/data_dictionary.md` for a detailed description of dataset fields.
- Open `notebooks/pricing_modeling.ipynb` to review data preparation, EDA and pricing model experiments.
- Open `notebooks/time_series_forecasting.ipynb` to see time-series analysis and forecasting.
- Review `data/raw/` and `data/processed/` to understand the raw inputs and analytical datasets.
- Open `dashboards/hotel_pricing_dashboard.pbix` in Power BI, or inspect images in `dashboards/screenshots/` for a quick visual tour.
- Refer to `reports/project_presentation.pdf` for a slide-based narrative of the project.
