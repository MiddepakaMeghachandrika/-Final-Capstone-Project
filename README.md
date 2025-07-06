# -Final-Capstone-Project

 Dynamic Pricing for Urban Parking Lots

This project implements a “dynamic pricing system for urban parking lots” using real-time occupancy data streams.  
It simulates live streaming from historical data, applies a demand-based pricing model, and visualizes daily pricing trends through an interactive dashboard.

 Table of Contents
 
-Tech Stack
- Architecture flow
- Architecture Diagram
- how to run
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

7  Prerequisites
 
1 Python 3.8+  
2 Install dependencies:
```bash
pip install pathway pandas scikit-learn bokeh panel



Overview

Urban parking spaces are a scarce and highly demanded resource. Static pricing often leads to overcrowding or under-utilization of parking lots.

This project implements an intelligent, real-time, data-driven pricing engine for 14 parking spaces, using real-time data streams, economic theory, and custom ML models (built from scratch with only numpy, pandas, and pathway).

We implement two pricing models:

Model 1: Baseline Linear Pricing
 Model 2: Demand-based Pricing

 Dataset
We use a simulated dataset covering 14 parking lots, over 73 days, with 18 time points per day (every 30 mins from 8:00 AM to 4:30 PM).

Each record includes:

 Location: Latitude, Longitude

 Lot Features: Capacity, Occupancy, Queue length

 Vehicle: Type (car, bike, truck)

 Environment: Traffic congestion, Special day flag


Models

Model 1: Baseline Linear Model
 Objective:
Price adjusts linearly with occupancy — as the lot fills up, the price increases proportionally.

 Formula:
𝑃
𝑡
+
1
=
𝑃
𝑡
+
𝛼
⋅
(
Occupancy
Capacity
)
P 
t+1
​
 =P 
t
​
 +α⋅( 
Capacity
Occupancy
​
 )
where:

𝑃
𝑡
P 
t
​
 : price at time 
𝑡
t

𝛼
α: sensitivity constant

Occupancy
Capacity
Capacity
Occupancy
​
 : lot fill rate

 Characteristics:
 1.Simple, interpretable
 2.Only depends on occupancy
 3. Serves as a benchmark model

Model 2: Demand-based Pricing
 Objective:
Price adjusts based on a composite demand score, incorporating multiple real-world factors beyond occupancy.

 Demand Function:
Demand
=
𝛼
⋅
(
Occupancy
Capacity
)
+
𝛽
⋅
(
Queue Length
)
−
𝛾
⋅
(
Traffic
)
+
𝛿
⋅
(
Special Day
)
+
𝜀
⋅
(
Vehicle Type Weight
)
Demand=α⋅( 
Capacity
Occupancy
​
 )+β⋅(Queue Length)−γ⋅(Traffic)+δ⋅(Special Day)+ε⋅(Vehicle Type Weight)
where:

𝛼
,
𝛽
,
𝛾
,
𝛿
,
𝜀
α,β,γ,δ,ε: weights assigned to each factor

 Price Function:
𝑃
𝑡
=
𝑃
base
⋅
(
1
+
𝜆
⋅
Normalized Demand
)
P 
t
​
 =P 
base
​
 ⋅(1+λ⋅Normalized Demand)
where:

𝑃
base
P 
base
​
 : base price ($10)

𝜆
λ: scaling constant

Demand is normalized to keep prices smooth & bounded.

Characteristics:
1. More intelligent
2.Considers queue, traffic, events, and vehicle type
3. Produces smooth, realistic price adjustments

Visualizations
1.Real-time line plots of daily prices for each of the 14 lots

2.Red dots at each time point for clarity

3.Tabs for each parking lot to monitor individual
