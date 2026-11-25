Content
This data set contains booking information for a city hotel and a resort hotel, and includes information such as when the booking was made, length of stay, the number of adults, children, and/or babies, and the number of available parking spaces, among other things.

All personally identifying information has been removed from the data.

Acknowledgements
The data is originally from the article Hotel Booking Demand Datasets, written by Nuno Antonio, Ana Almeida, and Luis Nunes for Data in Brief, Volume 22, February 2019.

The data was downloaded and cleaned by Thomas Mock and Antoine Bichat for #TidyTuesday during the week of February 11th, 2020.

## Data Cleaning Summary
The raw dataset (`data/raw/hotel_bookings.csv`) was audited and transformed using Power Query before building the dashboard:

- **Missing & Placeholder Values:** Replaced literal `"NULL"` strings in `agent` and `company` with `0` (representing direct bookings without an agency or corporate account) and imputed missing `country` values as `"Unknown"`.
- **Category Consolidation:** Merged `"Undefined"` entries in the `meal` column into `"SC"` (Self Catering), as both represent bookings without a meal package.
- **Invalid Records & Anomalies:** Filtered out invalid records with `0` total guests (`adults + children + babies = 0`) and flagged `0`-night stays with `0` ADR so they do not distort average daily rate calculations.
- **Duplicate Handling Decision:** **Retained exact duplicate rows.** Because the dataset lacks a unique booking or room ID, consecutive identical rows—particularly in the `Groups` and `Corporate` segments—represent multi-room block bookings rather than system errors. Keeping them ensures accurate room volume, occupancy, and revenue totals.
- **Date & Type Standardization:** Merged `arrival_date_day_of_month`, `arrival_date_month`, and `arrival_date_year` into a unified `arrival_date` column, and formatted `adr`, `lead_time`, and `reservation_status_date` to their proper numeric and date types.
