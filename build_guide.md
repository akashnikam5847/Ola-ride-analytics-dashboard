# Build Guide: Ola Ride Analytics in Power BI Desktop

Follow these steps in order. Total time: about 2 to 3 hours.

## 0. Before you start
- Power BI Desktop (Windows, free)
- `Bookings-20000-Rows.csv`
- Files from this repo: `docs/power_query.m`, `docs/dax_measures.md`, `theme/ola_dark_theme.json`

## 1. Load and clean data
1. Home > Get data > Blank query > Advanced Editor.
2. Paste **Query 1 (Bookings)** from `power_query.m`, fix the file path, Done. Rename the query `Bookings`.
3. Create a second blank query, paste **Query 2 (CancelReasons)**, rename it `CancelReasons`.
4. Check the column names in the preview match the script. Fix any that differ.
5. Close and Apply.

## 2. Check the numbers (do this before building any visual)
Add a Card with each measure and confirm: Total Bookings = 20,407, Success Rate = 62.0%, Total Revenue = 69,00,234, Cancellation Rate = 28.1%. If they don't match, the filter text in a measure or a column name is wrong.

## 3. Data model
Model view: drag `Bookings[Booking_ID]` to `CancelReasons[Booking_ID]`. Cardinality one-to-many, filter direction Single (Bookings filters CancelReasons).

## 4. Measures
Create a `_Measures` table and add every measure from `docs/dax_measures.md`.

## 5. Theme and page
1. View > Themes > Browse for themes > pick `theme/ola_dark_theme.json`.
2. View > Page view > Page size > Custom: width 1500, height 995.
3. Format page > Canvas background: black `#0B0B0C`.

## 6. Layout (approximate pixel positions on a 1500 x 995 canvas)

| Visual | Type | X | Y | W | H |
|---|---|---|---|---|---|
| Header title (text box) | Text box | 20 | 15 | 400 | 80 |
| Slicer 1: Vehicle Type | Slicer > Button slicer | 430 | 15 | 560 | 80 |
| Slicer 2: Week of Month | Slicer > Button slicer | 1005 | 15 | 475 | 80 |
| KPI: Total Bookings | Card | 20 | 110 | 350 | 85 |
| KPI: Success Rate | Card | 385 | 110 | 350 | 85 |
| KPI: Total Revenue | Card | 750 | 110 | 350 | 85 |
| KPI: Cancellation Rate | Card | 1115 | 110 | 365 | 85 |
| 1. Daily completed vs cancelled | Line chart (smoothed) | 20 | 210 | 980 | 370 |
| 2. Booking outcome | Donut chart | 1015 | 210 | 465 | 370 |
| 3. Revenue by vehicle | Clustered column | 20 | 595 | 490 | 380 |
| 4. Cancellation reasons | Clustered bar | 525 | 595 | 490 | 380 |
| 5. Payment method mix | Donut chart | 1030 | 595 | 450 | 380 |

Under each chart, add a text box (small, yellow left border line) with the matching `Insight - ...` measure.

## 7. Visual settings
- **Slicers:** Vehicle Type on `Bookings[Vehicle_Type]`, Week on `Bookings[Week of Month]`. Format: Button slicer, fill `#F5C242`, text black, rounded corners.
- **KPI cards:** Success Rate value colour green `#57B85F`, Cancellation Rate red `#D9534F`, Revenue yellow `#F5C242`.
- **Line chart:** axis `Bookings[Date]`, values `Completed Rides` and `Cancelled Rides`. Turn on smoothing.
- **Outcome donut:** legend `Bookings[Outcome]`, values `Total Bookings`. Colours: Completed green, Driver cancelled red, Customer cancelled orange, Driver not found grey.
- **Revenue by vehicle:** axis `Vehicle_Type`, values `Total Revenue`, yellow bars.
- **Cancellation reasons:** axis `CancelReasons[Reason]`, legend `CancelReasons[Cancelled By]`, values `Cancel Count`. Customer = blue, Driver = red.
- **Payment donut:** legend `Payment_Method`, values `Completed Rides`. Colours: Cash yellow, UPI green, Credit Card blue, Debit Card purple.

## 8. Export for GitHub
1. Save as `Ola_Ride_Analytics.pbix`.
2. Screenshot the report page (or File > Export > Export to PDF, then crop to PNG). Save as `screenshots/dashboard.png`.
3. Upload this folder structure to GitHub (see README, "Files").

## 9. Check before you push
- Slicers filter every visual (Format > Edit interactions)
- Numbers match step 2
- The CSV path note in the README is correct
- You can explain each DAX measure in an interview
