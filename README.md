# Predictive Modeling and Optimization of Delivery Time in Logistics Systems

## 📌 Project Overview

This project focuses on applying **predictive analytics and machine learning** to logistics operations to forecast delivery time and evaluate operational scenarios.

The project develops and compares multiple regression models to predict **delivery time in days** using logistics-related factors such as:

* Distance
* Shipment weight
* Traffic level
* Weather conditions
* Carrier
* Vehicle type
* Warehouse processing time
* Shipment priority

The project also extends the predictive model into a **scenario-analysis and optimization framework**, where different combinations of carrier, vehicle type, and priority are evaluated to identify configurations with lower predicted delivery times.

> **Note:** The dataset used in this project is simulated for educational and internship purposes. Therefore, optimization results represent scenario analysis rather than universal real-world recommendations.

---

## 🎯 Objectives

The main objectives of this project are:

1. Analyze logistics factors affecting delivery time.
2. Perform data quality checks and exploratory data analysis.
3. Prepare numerical and categorical features for machine learning.
4. Develop multiple regression models.
5. Compare model performance using MAE, RMSE, and R².
6. Perform 5-fold cross-validation.
7. Apply hyperparameter tuning using GridSearchCV.
8. Analyze prediction errors.
9. Perform operational scenario analysis.
10. Evaluate multiple logistics configurations for delivery-time optimization.
11. Provide practical optimization considerations for logistics operations.

---

## 🛠️ Technologies Used

| Technology   | Purpose                                   |
| ------------ | ----------------------------------------- |
| Python       | Data analysis and machine learning        |
| Pandas       | Data manipulation                         |
| NumPy        | Numerical computations                    |
| Matplotlib   | Data visualization                        |
| Scikit-learn | Machine learning and model evaluation     |
| Google Colab | Development and experimentation           |
| GitHub       | Project version control and documentation |

---

## 📊 Dataset

A simulated logistics dataset containing **1,500 shipments and 9 columns** was created for this project.

### Dataset Features

| Feature                      | Description                                |
| ---------------------------- | ------------------------------------------ |
| `Distance_km`                | Shipment distance in kilometers            |
| `Weight_kg`                  | Shipment weight in kilograms               |
| `Traffic_Level`              | Low, Medium, or High                       |
| `Weather`                    | Clear, Cloudy, Rainy, or Stormy            |
| `Carrier`                    | Carrier A, B, or C                         |
| `Vehicle_Type`               | Van, Truck, or Heavy Truck                 |
| `Warehouse_Processing_Hours` | Processing time at warehouse               |
| `Priority`                   | Standard, Express, or Urgent               |
| `Delivery_Time_Days`         | Target variable representing delivery time |

### Dataset Quality

* Rows: **1,500**
* Columns: **9**
* Missing values: **0**
* Duplicate records: **0**
* Negative values requiring correction: **0**

---

## 🔍 Exploratory Data Analysis

Several analyses were performed to understand relationships between logistics variables and delivery time.

### Distance vs Delivery Time

Distance showed a strong positive relationship with delivery time.

**Correlation:** `0.744`

This indicates that longer shipment distances were generally associated with higher predicted delivery times.

### Traffic Analysis

Average delivery time by traffic level:

| Traffic Level | Average Delivery Time |
| ------------- | --------------------: |
| Low           |             6.70 days |
| Medium        |             7.52 days |
| High          |             8.47 days |

The difference between Low and High traffic conditions was approximately **1.77 days**, or about **42.5 hours**.

### Weather Analysis

| Weather | Average Delivery Time |
| ------- | --------------------: |
| Clear   |             7.22 days |
| Cloudy  |             7.35 days |
| Rainy   |             7.91 days |
| Stormy  |             8.88 days |

The difference between Clear and Stormy conditions was approximately **1.66 days**, or about **39.8 hours**.

### Carrier Analysis

| Carrier   | Average Delivery Time |
| --------- | --------------------: |
| Carrier A |             7.31 days |
| Carrier C |             7.38 days |
| Carrier B |             7.89 days |

Carrier-level differences were observed in the simulated dataset, although carrier selection should also consider cost, capacity, reliability, and availability in real-world applications.

---

## ⚙️ Data Preprocessing

The dataset was divided into:

* **Features (`X`)** – 8 input variables
* **Target (`y`)** – `Delivery_Time_Days`

### Numerical Features

* `Distance_km`
* `Weight_kg`
* `Warehouse_Processing_Hours`

### Categorical Features

* `Traffic_Level`
* `Weather`
* `Carrier`
* `Vehicle_Type`
* `Priority`

Categorical variables were converted using **OneHotEncoder**, while numerical variables were passed through the preprocessing pipeline.

An **80:20 train-test split** was used:

* Training samples: **1,200**
* Testing samples: **300**

---

## 🤖 Machine Learning Models

Three regression models were developed and evaluated:

1. Linear Regression
2. Decision Tree Regressor
3. Random Forest Regressor

### Model Performance

| Model             |       MAE |      RMSE |        R² |
| ----------------- | --------: | --------: | --------: |
| Linear Regression | **0.541** | **0.675** | **0.885** |
| Random Forest     |     0.715 |     0.896 |     0.797 |
| Decision Tree     |     0.941 |     1.185 |     0.645 |

For this simulated dataset, Linear Regression produced the lowest test-set MAE and RMSE and the highest R² among the evaluated models.

---

## 📈 Model Evaluation

The models were evaluated using three standard regression metrics.

### Mean Absolute Error (MAE)

MAE represents the average absolute difference between actual and predicted delivery time.

**Linear Regression MAE:** `0.541 days`

This corresponds to approximately **13 hours** of average absolute prediction error.

### Root Mean Squared Error (RMSE)

RMSE gives greater weight to larger prediction errors.

**Linear Regression RMSE:** `0.675 days`

### R² Score

R² represents the proportion of variation in the target explained by the model.

**Linear Regression R²:** `0.885`

---

## 🔄 Cross-Validation

Five-fold cross-validation was performed using Mean Absolute Error.

| Model             | Mean CV MAE | Std CV MAE |
| ----------------- | ----------: | ---------: |
| Linear Regression |   **0.553** |      0.025 |
| Random Forest     |       0.715 |      0.027 |
| Decision Tree     |       0.999 |      0.018 |

The cross-validation results were consistent with the test-set evaluation, with Linear Regression producing the lowest average CV MAE.

---

## 🎛️ Hyperparameter Tuning

Random Forest hyperparameters were optimized using `GridSearchCV`.

### Parameters Tested

* `n_estimators`: 100, 200
* `max_depth`: 8, 12, None
* `min_samples_split`: 2, 5

### Best Parameters

```text
n_estimators = 200
max_depth = 12
min_samples_split = 2
```

### Best Grid Search CV MAE

```text
0.738 days
```

The tuned Random Forest achieved:

```text
MAE  = 0.715
RMSE = 0.896
R²   = 0.797
```

Hyperparameter tuning did not improve the Random Forest's test-set performance compared with the initial Random Forest configuration.

---

## 📉 Prediction Error Analysis

The selected Linear Regression model produced the following error statistics:

* MAE: **0.541 days**
* Maximum absolute error: **1.987 days**
* Predictions within 1 day: **87%**
* Predictions within 0.5 day: **55%**

These results indicate that most predictions were reasonably close to the actual delivery times, although larger errors occurred for some shipments.

---

## 🔎 Feature Interpretation

The Linear Regression model was also examined to understand the influence of encoded categorical variables.

Some of the larger learned coefficients included:

| Feature             | Coefficient |
| ------------------- | ----------: |
| Weather – Stormy    |      +0.934 |
| Traffic – High      |      +0.924 |
| Traffic – Low       |      -0.836 |
| Priority – Standard |      +0.686 |
| Weather – Clear     |      -0.634 |
| Priority – Urgent   |      -0.564 |
| Weather – Cloudy    |      -0.426 |
| Carrier B           |      +0.341 |
| Carrier A           |      -0.306 |

These coefficients describe relationships learned from the simulated dataset. They should **not be interpreted as causal effects**, and because all categorical levels were one-hot encoded, individual coefficients should not be treated as simple standalone comparisons without considering the encoding structure.

---

# 🚚 Optimization and Scenario Analysis

The predictive model was extended to evaluate operational scenarios.

A fixed shipment scenario was created:

```text
Distance: 1200 km
Weight: 500 kg
Warehouse Processing: 12 hours
Traffic: Medium
Weather: Clear
```

Different carrier, vehicle, and priority combinations were then tested.

---

## 🚛 Carrier Scenario

| Carrier   | Predicted Delivery Time |
| --------- | ----------------------: |
| Carrier A |               6.94 days |
| Carrier C |               7.21 days |
| Carrier B |               7.59 days |

Relative to Carrier A in this scenario:

* Carrier C: approximately **+0.27 days**
* Carrier B: approximately **+0.65 days**

---

## 🚦 Traffic Scenario

| Traffic | Predicted Delivery Time |
| ------- | ----------------------: |
| Low     |               6.19 days |
| Medium  |               6.94 days |
| High    |               7.95 days |

The difference between Low and High traffic scenarios was approximately **1.76 days**, or **42.2 hours**.

---

## 🌦️ Weather Scenario

| Weather | Predicted Delivery Time |
| ------- | ----------------------: |
| Clear   |               6.94 days |
| Cloudy  |               7.15 days |
| Rainy   |               7.70 days |
| Stormy  |               8.51 days |

The difference between Clear and Stormy conditions was approximately **1.57 days**, or **37.7 hours** for the fixed shipment scenario.

---

## 🔧 Operational Configuration Analysis

A total of **27 combinations** were evaluated using:

* 3 carriers
* 3 vehicle types
* 3 priority levels

This resulted in:

```text
3 × 3 × 3 = 27 configurations
```

### Lowest Predicted Configuration

The lowest predicted delivery time among the tested configurations was:

```text
Carrier: Carrier A
Vehicle: Heavy Truck
Priority: Urgent

Predicted Delivery Time: 5.59 days
```

The baseline configuration was:

```text
Carrier: Carrier A
Vehicle: Truck
Priority: Standard

Predicted Delivery Time: 6.94 days
```

Difference:

```text
6.94 - 5.59 = 1.35 days
```

Approximately:

```text
1.35 × 24 = 32.4 hours
```

Therefore, the lowest-predicted configuration showed a **1.35-day reduction** compared with the defined baseline scenario.

This result is a model-based scenario comparison and should not automatically be considered the final operational decision.

---

## 💡 Optimization Considerations

The predictive model can support logistics planning by helping planners compare possible operational scenarios.

Potential areas for optimization include:

### 1. Traffic-Aware Planning

Use predicted delivery times to identify routes or dispatch periods associated with lower traffic conditions.

### 2. Weather-Aware Scheduling

Weather conditions can be incorporated into delivery-time forecasts to support contingency planning.

### 3. Carrier Comparison

Predicted delivery performance can be compared across carriers while also considering:

* Cost
* Capacity
* Reliability
* Availability
* Service-level agreements

### 4. Vehicle Selection

Different vehicle configurations can be evaluated according to shipment requirements, capacity, cost, and predicted delivery time.

### 5. Priority Management

Priority levels can be incorporated into predictive planning when urgent shipments require faster handling.

### 6. Scenario-Based Decision Support

Instead of relying only on historical averages, logistics teams can simulate different operational configurations before making decisions.

---

## 📊 Optimization Visualization

The project includes a bar chart showing the **Top 10 Operational Configurations by Predicted Delivery Time**.

The visualization makes it easier to compare the tested configurations and identify combinations with lower predicted delivery times.

The chart is available in the project notebook/report.

---

## 🧪 Methodology

The complete workflow followed in this project is:

```text
Dataset Creation
       ↓
Data Quality Check
       ↓
Exploratory Data Analysis
       ↓
Feature Selection
       ↓
Data Preprocessing
       ↓
Train-Test Split
       ↓
Model Development
       ↓
Model Comparison
       ↓
Cross-Validation
       ↓
Hyperparameter Tuning
       ↓
Prediction Error Analysis
       ↓
Scenario Analysis
       ↓
Operational Configuration Testing
       ↓
Optimization Interpretation
```

---

## 💻 Example Python Code

### Model Pipeline

```python
linear_model = Pipeline(
    steps=[
        ("preprocessor", preprocessor),
        ("model", LinearRegression())
    ]
)

linear_model.fit(X_train, y_train)

y_pred = linear_model.predict(X_test)

mae = mean_absolute_error(y_test, y_pred)
rmse = np.sqrt(mean_squared_error(y_test, y_pred))
r2 = r2_score(y_test, y_pred)

print("MAE:", mae)
print("RMSE:", rmse)
print("R2:", r2)
```

### Optimization Scenario

```python
scenario = pd.DataFrame({
    "Distance_km": [1200],
    "Weight_kg": [500],
    "Traffic_Level": ["Medium"],
    "Weather": ["Clear"],
    "Carrier": ["Carrier A"],
    "Vehicle_Type": ["Heavy Truck"],
    "Warehouse_Processing_Hours": [12],
    "Priority": ["Urgent"]
})

predicted_time = linear_model.predict(scenario)[0]

print("Predicted Delivery Time:",
      round(predicted_time, 2), "days")
```

---

## 📁 Project Structure

```text
YuvaIntern_Week4_Predictive_Logistics_Optimization/
│
├── YuvaIntern_Week4_Predictive_Logistics_Optimization.ipynb
│
├── README.md
│
├── report/
│   └── Week4_Predictive_Logistics_Optimization_Report.docx
│
└── visualizations/
    ├── distance_vs_delivery_time.png
    ├── model_comparison.png
    └── top_10_optimization_configurations.png
```

---

## ⚠️ Limitations

This project has several limitations:

1. The dataset is simulated rather than collected from a real logistics operation.
2. Transportation cost was not included.
3. Vehicle capacity constraints were not modeled.
4. Route feasibility was not included.
5. Real-time traffic data was not used.
6. Real-time weather information was not incorporated.
7. Fuel consumption and operational costs were not part of the optimization model.
8. Carrier availability and service-level agreements were not modeled.
9. The optimization evaluates predicted delivery time only.
10. Model results should therefore be validated against real operational data before deployment.

---

## 📌 Key Findings

* Distance had a correlation of **0.744** with delivery time.
* High traffic was associated with higher average delivery times.
* Stormy weather produced higher average delivery times than clear weather in the simulated dataset.
* Linear Regression achieved the strongest test-set performance among the evaluated models.
* Linear Regression achieved an MAE of **0.541 days** and R² of **0.885**.
* **87%** of Linear Regression predictions were within one day of the actual delivery time.
* Cross-validation supported the strong performance of Linear Regression on this dataset.
* The optimization analysis evaluated **27 operational configurations**.
* The lowest predicted configuration had a delivery time of **5.59 days** compared with the **6.94-day** baseline scenario.
* Operational decisions should consider additional constraints such as cost, capacity, availability, and service requirements.

---

## 📚 Learning Outcomes

Through this project, the following skills were practiced:

* Data preprocessing
* Exploratory data analysis
* Feature engineering
* Categorical encoding
* Regression modeling
* Model comparison
* Cross-validation
* Hyperparameter tuning
* Error analysis
* Data visualization
* Scenario analysis
* Optimization-oriented predictive analytics
* Business interpretation of machine learning results
* GitHub project documentation

---

## 🚀 Future Improvements

The project can be extended by:

* Using real-world logistics datasets.
* Adding fuel and transportation costs.
* Incorporating GPS and real-time traffic data.
* Adding route-level features.
* Including delivery success and customer satisfaction metrics.
* Applying advanced ensemble models.
* Performing multi-objective optimization for cost and delivery time.
* Adding vehicle capacity and availability constraints.
* Deploying the prediction model as a web application or API.
* Monitoring model performance using real-time logistics data.

---

## 📂 Repository

**GitHub Repository:**
`<PASTE YOUR GITHUB REPOSITORY URL HERE>`

The repository contains the Google Colab notebook, project documentation, visualizations, and supporting files.

---

## 👩‍💻 Author

**Shamini S.**

B.Tech Artificial Intelligence & Data Science
Kumaraguru College of Technology

### Project

**YuvaIntern – Week 4**

**Predictive Modeling and Optimization of Delivery Time in Logistics Systems**

---

## 📜 Disclaimer

This project was developed for educational and internship purposes. The dataset and operational scenarios are simulated. The predictions and optimization results should not be treated as production-level logistics decisions without validation using real-world data and operational constraints.
