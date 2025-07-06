# -Final-Capstone-Project

 Dynamic Pricing for Urban Parking Lots

This project implements a “dynamic pricing system for urban parking lots” using real-time occupancy data streams.  
It simulates live streaming from historical data, applies a demand-based pricing model, and visualizes daily pricing trends through an interactive dashboard.

 Table of Contents
 
-Tech Stack
- Architecture flow
- Architecture Diagram
- how to run
- overview
- dataset
- models
- visualization
- Prerequisites

Tech Stack


Technology	Purpose                                   
Python	Programming language
Pathway (`pw`)	Real-time data stream processing
Pandas	Data preprocessing
Scikit-learn	Label encoding
Bokeh	Interactive plotting
Panel	Interactive plotting
Matplotlib(optional)	Exploratory plots

 Architecture

 Flow:

1️  Preprocessing
- Load `dataset.csv`
- Combine `LastUpdatedDate` & `LastUpdatedTime` → `Timestamp`
- Encode categorical columns
- Sort by `Timestamp`
- Save as `parking_stream.csv`

2️  Stream Processing
- Use `pw.demo.replay_csv()` to simulate real-time stream
- Define schema (`ParkingSchema`)
- Parse timestamps & extract day-level info

3️  Pricing Model
- Aggregate occupancy data daily
- Compute dynamic price using demand-based formula

4️  Visualization
- Display aggregated prices & trends on a web dashboard with Bokeh & Panel


5 Architecture Diagram

          +------------------+
          |   dataset.csv    |
          +------------------+
                   |
                   v
        +---------------------------+
        | Preprocessing (Pandas)   |
        | - Timestamp creation     |
        | - Encode categorical     |
        | - Save as CSV            |
        +---------------------------+
                   |
                   v
        +---------------------------+
        | Pathway Streaming         |
        | - Simulate live stream    |
        | - Schema definition       |
        | - Parse timestamp & day   |
        +---------------------------+
                   |
                   v
        +---------------------------+
        | Pricing Model             |
        | - Daily aggregation       |
        | - Demand-based pricing   |
        +---------------------------+
                   |
                   v
        +---------------------------+
        | Dashboard                 |
        | - Bokeh + Panel plot      |
        | - Web UI: Price vs Time   |
        +---------------------------+


6 how to run

   - you can run on google colab


7  Overview

Urban parking spaces are a scarce and highly demanded resource. Static pricing often leads to overcrowding or under-utilization of parking lots.

This project implements an intelligent, real-time, data-driven pricing engine for 14 parking spaces, using real-time data streams, economic theory, and custom ML models (built from scratch with only numpy, pandas, and pathway).

 We implement two pricing models:

 - Model 1: Baseline Linear Pricing
 - Model 2: Demand-based Pricing

8  Dataset
We use a simulated dataset covering 14 parking lots, over 73 days, with 18 time points per day (every 30 mins from 8:00 AM to 4:30 PM).

- Each record includes:

  - Location: Latitude, Longitude

  - Lot Features: Capacity, Occupancy, Queue length

  - Vehicle: Type (car, bike, truck)

   - Environment: Traffic congestion, Special day flag


9 Models

- Model 1: Baseline Linear Model
  - Objective:
Price adjusts linearly with occupancy — as the lot fills up, the price increases proportionally.

P(t+1) = P(t) + α × (Occupancy / Capacity)
​
  - p(t)— Current price
  - p(t+1)— Next price
 - α — Scaling factor (learning rate for price adjustment)
  - Occupancy — Current number of vehicles in the lot
  - Capacity — Maximum number of vehicles the lot can hold


- Characteristics:
  
  1.Simple, interpretable
  2.Only depends on occupancy
  3. Serves as a benchmark model

-Model 2: Demand-based Pricing
  - Objective:
Price adjusts based on a composite demand score, incorporating multiple real-world factors beyond occupancy.

- Demand Function:
Demand = α × (Occupancy / Capacity) + β × QueueLength − γ × TrafficLevel + δ × IsSpecialDay + ε × VehicleTypeWeight



- Pricing based on Demand:
P(t) = BasePrice × (1 + λ × NormalizedDemand)

    - BasePrice — Starting price (e.g., $10)
    - NormalizedDemand — Scaled demand value to keep price smooth and bounded
    - λ — Demand sensitivity factor
    - QueueLength — Number of vehicles waiting
    - TrafficLevel — Nearby traffic congestion level
    - IsSpecialDay — Indicator for holidays or events
    - VehicleTypeWeight — Weight based on type of incoming vehicle (e.g., car, bike, truck)


- Demand is normalized to keep prices smooth & bounded.

Characteristics:

  1. More intelligent
  2.Considers queue, traffic, events, and vehicle type
  3. Produces smooth, realistic price adjustments

10 Visualizations:

   1.Real-time line plots of daily prices for each of the 14 lots

   2.Red dots at each time point for clarity

   3.Tabs for each parking lot 


11  Prerequisites
 
1 Python 3.8+  
2 Install dependencies:
```bash
pip install pandas numpy pathway bokeh panel  ```bash

