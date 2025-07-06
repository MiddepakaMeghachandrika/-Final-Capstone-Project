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


