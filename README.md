# **Battery Capacity Prediction Using EIS Data**

### **1. Introduction**
- **Objective**: The goal of this analysis is to predict the battery capacity based on Electrochemical Impedance Spectroscopy (EIS) data (Re, Rct) using machine learning techniques.
- **Dataset**: The dataset consists of EIS measurements and battery metadata, including temperature, test IDs, and filenames.

### **2. Data Preprocessing**
- **Missing Data Handling**: 
  - Columns related to EIS (Re, Rct) and capacity had missing values, which were handled by:
    - Dropping rows with missing EIS data to create the EIS dataset (`df_eis`).
    - Estimating missing capacity values by using the closest matching test IDs from the **df_ml** dataset.
  - After cleaning, 1947 rows of valid EIS data and 2769 rows with estimated capacity values were available.

### **3. Feature Selection and Model Training**
- **Initial Feature Set**: We started with two features, **Re** and **Rct**, to train the model.
- **Model**: A **Random Forest Regressor** was chosen to predict battery capacity, and the dataset was split into training (80%) and testing (20%) sets.
  - **Initial Model Performance**:
    - **R² score**: 0.5889
    - **Mean Absolute Error (MAE)**: 0.1517

### **4. Model Optimization**
- **Hyperparameter Tuning**: We performed a **Grid Search** to find the optimal parameters for the Random Forest model. The best parameters were:
  - **n_estimators**: 100
  - **max_depth**: 10
  - **min_samples_split**: 5
  - **min_samples_leaf**: 2
- **Optimized Model Performance**:
  - **R² score**: 0.6259
  - **Mean Absolute Error (MAE)**: 0.1507

### **5. Feature Importance**
- From the feature importance analysis, we observed that **Rct** had a higher importance than **Re** in predicting battery capacity.
  - **Feature Importance**:
    - **Rct**: 67.29%
    - **Re**: 32.71%

### **6. Feature Reduction**
- Based on feature importance, we reduced the feature set to **Rct** only, retrained the model, and evaluated the performance:
  - **R² score** and **MAE** were compared to the full feature model.
  - Final performance showed that the reduced model (using only **Rct**) still performed well, with a similar **R² score** and a slight improvement in the MAE.

### **7. Residual Analysis**
- **Residuals vs. Fitted Values**: No significant patterns were found in the residuals, indicating a well-fitted model.
- **Residuals Histogram**: The residuals showed an approximately normal distribution, supporting the model's reliability.

### **8. Conclusion**
- **Final Model**: The final Random Forest model, using only **Rct**, demonstrated strong predictive performance with an **R² score** of 0.6259 and an **MAE** of 0.1507.
- **Key Insights**:
  - Feature selection and optimization improved the model’s performance, and reducing features to **Rct** did not result in significant performance loss.
  - Residual analysis confirmed that the model is reliable and free from major biases.
