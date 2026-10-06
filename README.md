# Ola Ride Analytics Dashboard

An interactive 5-page dashboard analysing 20,407 Ola ride bookings (Bengaluru, July 2024): ride volume, vehicle performance, revenue, cancellations and ratings.

**Live demo:** enable GitHub Pages for this repo (Settings -> Pages -> main branch) and open the link, or just open `index.html` in a browser.

## Dataset
20,407 bookings, 20 columns (status, vehicle type, pickup/drop, booking value, payment method, cancellation reasons, ratings). Cleaning: dropped the corrupted `Vehicle Images` column, converted "null" text to blanks, checked duplicate Booking_IDs (none), revenue counted on successful rides only.

## Pages
- **Overall:** bookings, success rate, cancellation rate, revenue, status split, daily revenue trend
- **Vehicle Type:** revenue, bookings, distance and success rate for each of the 7 vehicle types
- **Revenue:** payment methods, daily distance, average booking value, top 10 customers
- **Cancellation:** customer vs driver cancellations with reasons
- **Rating:** driver and customer ratings by vehicle type
- Filters: day range and vehicle type

## Tools
Python (pandas) for cleaning and aggregation, HTML/JavaScript, Chart.js

## Key insights
- 62.0% of bookings completed, 28.1% cancelled (17.9% by drivers, 10.2% by customers); 9.9% end in "Driver Not Found"
- Revenue from completed rides: INR 6,900,234
- Top customer cancel reason: driver not moving towards pickup; top driver cancel reason: personal and car related issue
- Cash (55%) and UPI (40%) dominate payments

## Screenshots
![Overall](screenshots/overall.png)
![Vehicle](screenshots/vehicle.png)
![Revenue](screenshots/revenue.png)
![Cancellation](screenshots/cancel.png)
![Rating](screenshots/rating.png)
