🚗 Real-Time Dynamic Parking Pricing System
This project builds a real-time, demand-sensitive pricing model for parking spots using live data streams. It adjusts parking prices based on various parameters such as occupancy, traffic conditions, special events, and vehicle types.

📦 Tech Stack
Layer	Technologies Used
Programming	Python, Pathway
Data Handling	Pandas, NumPy
Visualization	Bokeh, Panel
Real-Time Engine	Pathway
Plot Rendering	Bokeh + Panel
Data Source	CSV Streaming (simulated real-time)

🧠 Key Features
⏱ Real-time simulation using Pathway.replay_csv

📊 Demand estimation model with custom feature weights

💰 Dynamic pricing computation based on normalized demand

📈 Interactive visualization using Bokeh & Panel

🔗 Event-based windowing and stream joins

🧮 Daily max aggregation and global normalization

✅ Clamped pricing within bounds (0.5x – 2x base)

🏗️ Architecture Flow
mermaid
Copy
Edit
graph TD
    A[CSV Input (parking_stream.csv)] --> B[Pathway Replay CSV]
    B --> C[Time Parsing & Feature Engineering]
    C --> D[Daily Tumbling Window]
    D --> E[Aggregation: Occupancy, Queue, Traffic, etc.]
    E --> F[Vehicle Type Weight Average]
    F --> G[Demand Estimation Formula]
    G --> H[Global Min/Max Demand Calculation]
    H --> I[Demand Normalization]
    I --> J[Raw Price Calculation]
    J --> K[Clamp Prices (0.5x - 2x)]
    K --> L[Bokeh Plotter Function]
    L --> M[Panel Layout Visualization]
    M --> N[Web App Visualization]
🧮 Demand & Pricing Formula
text
Copy
Edit
Demand Score =
    α * (Occupancy / Capacity)
  + β * QueueLength
  - γ * TrafficLevel
  + δ * IsSpecialDay
  + ε * MeanVehicleWeight

Price =
    base_price * (1 + λ * NormalizedDemand)

Final Price is clamped between [0.5x, 2x] of base_price
Where:

α, β, γ, δ, ε, λ are user-defined weights

base_price = 10.0
