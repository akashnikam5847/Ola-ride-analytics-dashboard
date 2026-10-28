# Ola Ride Analytics Dashboard (Power BI)

An interactive Power BI dashboard analysing **20,407 Ola ride bookings (Bengaluru, July 2024)**: booking outcomes, revenue by vehicle type, cancellation reasons and payment behaviour.

![Dashboard](screenshots/dashboard.png)

## Business questions answered
- How many bookings are completed vs cancelled, and who cancels more: drivers or customers?
- Which vehicle types earn the most revenue?
- Why do rides get cancelled?
- How do customers pay?
- Is demand steady across days and weeks?

## Dataset
`data/Bookings-20000-Rows.csv`: 20,407 bookings, 20 columns (date, booking status, vehicle type, pickup/drop, booking value, payment method, cancellation reasons, ratings).

## Data preparation (Power Query)
- Removed the corrupted `Vehicle Images` column
- Converted the text "null" to real blanks
- Set correct data types (date, whole number, decimal)
- Checked duplicate `Booking_ID` values (none found)
- Added `Week of Month` (Week 1 to 4) for the week slicer
- Built a separate `CancelReasons` table (customer and driver reasons stacked)
- Revenue is counted on **successful rides only**

Full script: [`docs/power_query.m`](docs/power_query.m)

## Data model
`Bookings` (1) ---> (*) `CancelReasons` on `Booking_ID`

## Key DAX measures
| Measure | Purpose |
|---|---|
| Total Bookings | Distinct count of Booking_ID |
| Success Rate | Completed / Total |
| Cancellation Rate | Cancelled / Total |
| Total Revenue | Sum of Booking_Value for successful rides |
| Driver / Customer Cancel Rate | Split of cancellations |
| Revenue Share % | Vehicle revenue / total revenue |
| Payment Share % | Payment method / completed rides |

All measures: [`docs/dax_measures.md`](docs/dax_measures.md)

## Dashboard features
- 4 KPI cards: Total Bookings, Success Rate, Total Revenue, Cancellation Rate
- Daily completed vs cancelled trend
- Booking outcome donut
- Revenue by vehicle type
- Cancellation reasons (customer vs driver)
- Payment method mix
- Slicers: Vehicle Type and Week of Month
- Custom dark theme: [`theme/ola_dark_theme.json`](theme/ola_dark_theme.json)

## Key insights
- **62.0%** of bookings completed; **28.1%** cancelled (drivers 17.9%, customers 10.2%); **9.9%** ended in "Driver Not Found"
- Revenue from completed rides: **INR 69,00,234**
- Demand is flat day to day. Busiest day was 22 July (656 completed + cancelled bookings)
- Prime Sedan leads revenue with INR 10,56,843 (15.3%); other vehicle types earn almost equally
- Top customer cancel reason: driver not moving towards pickup. Top driver cancel reason: personal and car-related issue (1,263 cases)
- Cash (54.8%) and UPI (40.4%) make up 95.2% of paid rides

## Tools
Power BI Desktop (Power Query, DAX), Excel/CSV

## Files
```
Ola-Ride-Analytics-PowerBI/
|-- Ola_Ride_Analytics.pbix
|-- data/Bookings-20000-Rows.csv
|-- screenshots/dashboard.png
|-- theme/ola_dark_theme.json
|-- docs/power_query.m
|-- docs/dax_measures.md
|-- docs/build_guide.md
`-- README.md
```

## How to open
1. Download the repository
2. Open `Ola_Ride_Analytics.pbix` in Power BI Desktop
3. If asked, update the CSV path under Transform data > Data source settings

## Author
Rushikesh Tarmale | Operations Executive | Aspiring Data Analyst
