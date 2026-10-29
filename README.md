# Air Cargo Customer & Route Analysis in SQL

A MySQL project for an airline that wants to find its best customers for targeted offers, understand its routes for better aircraft planning, and produce ticket sales reports.

**Tools:** MySQL

## Business question

Which customers are worth targeting with offers, which routes and classes drive revenue, and how can routine reports be made fast and repeatable?

## What the queries answer

| Business question | SQL technique |
|---|---|
| Which customers have booked, and which booked with a specific airline brand? | `INNER JOIN` between customers and tickets |
| How many business-class passengers are there, and what revenue do they bring in? | Aggregation with `SUM` |
| Which customers travel Economy Plus? | Subquery |
| Has total revenue crossed the 10,000 target? | `IF` with an aggregate |
| What is the highest ticket price in each travel class? | Window function `MAX() OVER (PARTITION BY class_id)` |
| How much has each customer spent on each aircraft, with customer subtotals and a grand total? | `GROUP BY ... WITH ROLLUP` |
| What is the average distance and number of passengers per aircraft on routes flown more than once? | Common table expressions (CTEs) + joins |
| Which routes are longer than 2,000 miles? | Stored procedure |
| A reusable list of business-class customers by brand | View |
| How can route lookups run faster? | Index + `EXPLAIN` execution plan |
| How is a new analyst given database access? | `CREATE USER` / `GRANT` |

## Business value

- **Targeted offers:** customer-level spend totals and class/brand filters identify high-value travellers to receive promotions.
- **Aircraft planning:** route distance and passengers-per-aircraft help match aircraft to demand.
- **Faster reporting:** views, stored procedures and indexes turn one-off queries into repeatable reports.

## Files

| File | Contents |
|---|---|
| `Air-Cargo_Analysis.sql` | All queries, views, stored procedure and index |

The source data is not included in this repo.

<details>
<summary>Data dictionary</summary>

**customer:** customer details

| Column | Description |
|---|---|
| customer_id | Customer ID |
| first_name, last_name | Customer name |
| date_of_birth | Date of birth |
| gender | Gender |

**passengers_on_flights:** each passenger's trip

| Column | Description |
|---|---|
| aircraft_id | Aircraft ID |
| route_id | Route ID |
| customer_id | Customer ID |
| depart, arrival | Departure and arrival airports |
| seat_num | Seat number |
| class_id | Travel class |
| travel_date | Date of travel |
| flight_num | Flight number |

**ticket_details:** ticket purchases

| Column | Description |
|---|---|
| p_date | Purchase date |
| customer_id | Customer ID |
| aircraft_id | Aircraft ID |
| class_id | Travel class |
| no_of_tickets | Tickets purchased |
| a_code | Airport code |
| price_per_ticket | Price per ticket |
| brand | Airline brand |

**routes:** route details

| Column | Description |
|---|---|
| route_id | Route ID |
| flight_num | Flight number |
| origin_airport, destination_airport | Start and end airports |
| aircraft_id | Aircraft ID |
| distance_miles | Route distance in miles |

</details>
