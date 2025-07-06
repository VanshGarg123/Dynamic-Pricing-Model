 # Real-Time Dynamic Parking Pricing System 🚗
This project builds a real-time, demand-sensitive pricing model for parking spots using live data streams. It adjusts parking prices based on various parameters such as occupancy, traffic conditions, special events, and vehicle types.


## Tech Stack 📦
| Layer            | Technologies                  |
|------------------|------------------------------|
| Programming      | Python, Pathway              |
| Data Handling    | Pandas, NumPy               |
| Visualization    | Bokeh, Panel                |
| Real-Time Engine | Pathway                    |
| Plot Rendering   | Bokeh + Panel              |
| Data Source      | CSV Streaming (simulated real-time) |



## Key Features 🧠
⏱ Real-time simulation using Pathway.replay_csv <br />
📊 Demand estimation model with custom feature weights <br />
💰 Dynamic pricing computation based on normalized demand <br />
📈 Interactive visualization using Bokeh & Panel <br />
🔗 Event-based windowing and stream joins <br />
🧮 Daily max aggregation and global normalization <br />
✅ Clamped pricing within bounds (0.5x – 2x base) <br />

## Architecture Flow 🏗️ 
graph TD
    A[CSV Input (parking_stream.csv)] --> B[Pathway Replay CSV] <br />
    B --> C[Time Parsing & Feature Engineering] <br />
    C --> D[Daily Tumbling Window] <br />
    D --> E[Aggregation: Occupancy, Queue, Traffic, etc.] <br />
    E --> F[Vehicle Type Weight Average] <br /> 
    F --> G[Demand Estimation Formula] <br />
    G --> H[Global Min/Max Demand Calculation] <br />
    H --> I[Demand Normalization] <br />
    I --> J[Raw Price Calculation] <br />
    J --> K[Clamp Prices (0.5x - 2x)] <br />
    K --> L[Bokeh Plotter Function] <br / >
    L --> M[Panel Layout Visualization] <br />
    M --> N[Web App Visualization] <br />
    
## Demand & Pricing Formula 🧮
$$
\text{DemandScore} = \alpha \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right) + \beta \cdot \text{QueueLength} - \gamma \cdot \text{TrafficLevel} + \delta \cdot \text{IsSpecialDay} + \varepsilon \cdot \text{MeanVehicleWeight}
$$

$$
\text{Price} = \text{Base price} \cdot \left( 1 + \lambda \cdot \text{NormalizedDemand} \right)
$$

Final Price is clamped between 0,5x-2x of base_price <br/>
Where: <br/>
α, β, γ, δ, ε, λ are user-defined weights <br/>
base_price = 10.0 <br/>
 
