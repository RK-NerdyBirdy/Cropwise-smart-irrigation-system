# Cropwise-smart-irrigation-system


## Overview

This project implements a **Smart Irrigation System** using an **XGBoost** model to predict whether irrigation is required based on crop type, soil conditions, and real-time weather data. The system integrates **IP-based geolocation**, **weather forecasting**, and **hydrological calculations** (runoff, slope) to make intelligent irrigation decisions.

## Features

- Uses **XGBoost** for decision-making.
- Integrates **real-time weather data** using the Open-Meteo API.
- Determines **soil moisture and water requirements** based on crop conditions.
- Uses **Haversine distance** to compute slope and **SCS Curve Number Method** to estimate runoff.
- Supports multiple **crop types and soil conditions**.

## Dependencies

Ensure you have the following installed:

```bash
pip install pandas numpy requests scikit-learn xgboost joblib
```

## Project Structure

```
smart_irrigation/
│── model/
│   ├── xgboost_smart_irrigation_model.pkl  # Trained XGBoost model
│   ├── label_encoders.pkl                   # Encoders for categorical features
│   ├── scaler.pkl                           # Scaler for feature normalization
│── src/
│   ├── irrigation.py                        # Main prediction script
│   ├── utils.py                             # Helper functions
│── README.md
```

## Model Inputs

The model takes the following inputs:

- **Crop Name**: The name of the crop (e.g., Rice, Banana, Wheat, etc.).
- **Soil Type**: The type of soil (e.g., Alluvial, Loam, Clay).
- **Soil Moisture**: Current soil moisture level in percentage.

## Weather Data

Weather data is fetched using **Open-Meteo API** based on the user's IP address to determine:

- **Temperature**
- **Humidity**
- **Rainfall** (current and forecasted)
- **Weather Condition** (Sunny, Cloudy, Rainy, Heavy Rain)

## Prediction Process

1. **Fetch Location & Weather Data**

   - Uses IP-based geolocation to get latitude and longitude.
   - Retrieves **current and future weather** from Open-Meteo API.

2. **Estimate Soil & Hydrological Factors**

   - Calculates **slope** using the Haversine formula.
   - Computes **runoff depth** using the SCS Curve Number Method.

3. **Preprocess Input Data**

   - Encodes categorical variables (crop name, soil type, weather conditions).
   - Normalizes numerical features (soil moisture, humidity, temperature, runoff depth, etc.).

4. **Predict Irrigation Requirement**

   - Uses the trained **XGBoost model** to predict whether irrigation is needed.
   - Outputs **Yes** (run pump) or **No** (do not run pump).

## Usage

### Example Code

```python
from irrigation import predict_irrigation

input_data = {
    "crop_name": "Rice",
    "soil_type": "Alluvial",
    "soil_moisture": 60.0,
}

decision = predict_irrigation(input_data)
print(f"Should the pump run? {decision}")
```

### Expected Output

```bash
Should the pump run? Yes
```

## Supported Crops

&#x20; "Arecanut", "Banana", "Black Pepper", "Cashewnut", "Coconut", "Dry Chillies", "Ginger", "Rice",

&#x20;   "Sugarcane", "Sweet Potato", "Arhar/Tur", "Bajra", "Castor Seed", "Cotton (Lint)", "Gram",

&#x20;   "Groundnut", "Horse-gram", "Jowar", "Maize", "Moong (Green Gram)", "Onion", "Potato", "Ragi",

&#x20;   "Rapeseed & Mustard", "Safflower", "Sesamum", "Soyabean", "Sunflower", "Tobacco", "Turmeric",

&#x20;   "Urad", "Wheat", "Jute", "Masoor", "Barley", "Garlic", "Cardamom", "Coriander", "Cowpea (Lobia)",

&#x20;   "Tapioca", "Tea", "Coffee", "Rubber", "Mango", "Citrus Fruits", "Pulses".





Improvements

- **Integrate IoT Sensors** for real-time soil monitoring.
- **Improve AI Model** using deep learning approaches.
- **Enhance Weather Data** with more detailed meteorological analysis.

## License

This project is open-source under the **MIT License**.

