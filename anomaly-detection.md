Tourist Anomaly Detection – AI/ML Model Report
Model Training Summary

Model: Random Forest Classifier

Dataset Features:

phone_on (1 = ON, 0 = OFF)

inactivity_mins (minutes of no movement)

route_deviation_km (distance from planned route)

crime_index (normalized 0–1 from NCRB data)

is_night (1 = night, 0 = day)

📊 Model Performance

✅ Model trained successfully

🎯 Accuracy: 92.50%

✔️ Safe tourists correctly detected: 145 / 150

🚨 Unsafe tourists correctly detected: 120 / 130

1. Normal Case (Safe)
Input:
{
  "phone_on": 1,
  "inactivity_mins": 20,
  "route_deviation_km": 1.5,
  "crime_index": 0.2,
  "is_night": 0
}

Output:
SAFE – Tourist is normal.

2. High-Risk Case (Unsafe)
Input:
{
  "phone_on": 0,
  "inactivity_mins": 200,
  "route_deviation_km": 12,
  "crime_index": 0.8,
  "is_night": 1
}

Output:
ALERT – Tourist is unsafe!

3. Risk Combination Case (Unsafe)
Input:
{
  "phone_on": 1,
  "inactivity_mins": 150,
  "route_deviation_km": 0.5,
  "crime_index": 0.9,
  "is_night": 1
}

Output:
ALERT – Tourist is unsafe!
