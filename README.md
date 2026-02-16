# HOTEL-OPERATION
Hotel Booking Demand Analysis: An end-to-end data analytics project exploring 119,000+ bookings to optimize hotel operations. Features analysis of cancellation drivers, revenue trends (ADR), seasonal demand patterns, and customer segmentation using Python-based statistical modeling and visualization.
Data Preparation and Cleaning
Time-Series Conversion: The script creates a unified arrival_date column by combining year, month, and day data.
Status Tracking: It converts reservation_status_date into a datetime format to track when booking statuses changed.
Structural Review: The df.info() command is used to inspect the dataset's columns and data types.
 Booking Distribution Analysis
Segmentation Analysis: The script performs a grouped analysis of bookings by hotel type, arrival_date_month, and market_segment.
Distribution Mapping: It uses unstack() to create a pivot table (distribution map) of these segments for easier comparison.
Cancellation Trends
Lead Time Impact: Analysis of how the lead_time (days between booking and arrival) affects the is_canceled rate.
Visual Correlation: A scatter plot is generated to visualize whether longer lead times correlate with higher cancellation rates.
 Financial and Operational Metrics
Pricing Trends: Analysis of the Average Daily Rate (ADR) over time to identify seasonal pricing fluctuations.
Revenue Visualization: A line plot is used to display adr trends relative to the arrival_date.
Special Requests: The script calculates the frequency of total_of_special_requests and identifies the average number of requests based on booking changes.
