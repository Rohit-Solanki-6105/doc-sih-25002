# Tourist Anomaly Detection – Model Report  

## Model Training Summary  
- **Algorithm**: Random Forest Classifier  
- **Features Used**:  
  - `phone_on` – Device status (1 = ON, 0 = OFF)  
  - `inactivity_mins` – Minutes of no movement  
  - `route_deviation_km` – Distance from planned route (km)  
  - `crime_index` – Normalized (0–1) from NCRB data  
  - `is_night` – Time indicator (1 = night, 0 = day)  

---

## Model Performance  

| Metric                           | Value       |  
|----------------------------------|-------------|  
| Accuracy                         | **92.50%**  |  
| Safe tourists correctly detected | 145 / 150   |  
| Unsafe tourists correctly detected | 120 / 130 |  

---

## Sample Predictions  

### Case 1 – Normal (Safe)  
**Input**  
```json
{
  "phone_on": 1,
  "inactivity_mins": 20,
  "route_deviation_km": 1.5,
  "crime_index": 0.2,
  "is_night": 0
}

Output - Tourist is SAFE

### Case 2 – Not Normal (Unsafe)  
**Input**
```json
 {
  "phone_on": 0,
  "inactivity_mins": 200,
  "route_deviation_km": 12,
  "crime_index": 0.8,
  "is_night": 1
}

Output - Tourist is UNSAFE
