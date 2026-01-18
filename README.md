# Claims Prediction
This project focuses on building and evaluating machine learning models to predict whether a building will incur an insurance claim during its policy tenure.
The primary objective is to identify high-risk buildings early, enabling proactive risk management and pricing decisions.

Seven (7) classification models were developed, compared, and evaluated with a strong emphasis on recall, due to the imbalanced nature of insurance claim data.

## Dataset Summary

- Records: 7,160
- Features: 14
- Target Variable: Claim
- Duplicates: None

| Feature            | Missing Count |
| ------------------ | ------------- |
| Building Dimension | 106           |
| Garden             | 7             |
| Date of Occupancy  | 508           |
| Geo Code           | 102           |

## Models Trained & Compared

The following seven models were evaluated:
- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier
- Support Vector Classifier (SVC)
- Gradient Boosting Classifier
- XGBoost Classifier
- KNN (SMOTE)

## Key Insights 
#### Exploratory Data Analysis (EDA)
- The target variable exhibits an imbalance ratio of 3.4:1, indicating that buildings without insurance claims significantly outnumber those with claims.
    - This level of imbalance suggests that a naive model could achieve high accuracy by predominantly predicting the majority class (no claim), while failing to correctly identify buildings that do experience claims. As a result, accuracy alone is not a sufficient evaluation metric. Metrics such as recall, precision, F1-score, and AUC-ROC are more appropriate for assessing model performance.
    - Resampling techniques (e.g., SMOTE) or class-weighted models should also be considered to improve minority class detection.
- Approximately 44.8% of all insurance claims were associated with houses that have no windows. This suggests that buildings without windows may be structurally or functionally different from typical residential properties, potentially indicating:
    - Storage facilities, industrial units, or older constructions
    - Reduced ventilation or lighting, which could contribute to higher risk exposure
    - Proxy indicators of building age, usage, or maintenance quality
- Painted buildings exhibited fewer insurance claims compared to unpainted buildings. This finding suggests that building maintenance indicators play an important role in claim risk, and reinforces the importance of incorporating condition-related features into the predictive model. Painted buildings may suggest:
    - Better overall maintenance
    - Regular upkeep and inspections
    - Lower exposure to environmental damage (e.g., moisture, corrosion)

#### Pre-processing
- 'Building dimension' shows the strongest linear relationship with insurance claims among all evaluated features.
- Building type demonstrates a weak but meaningful positive correlation with claim occurrence.
- The insured period shows a slight positive correlation, indicating that some insurance coverage durations have more likelihood to attract claims than others.

#### Modelling
- Out of the 7 models built and compared, the Decision Tree model demonstrates the strongest ability to correctly identify claim cases (Test Recall: 0.59), making it the most effective model for minimizing false negatives. 
    - This is particularly important in an insurance context, where failing to identify a high-risk building can result in unexpected financial exposure.
    - However, a slight drop observed in cross-validated recall (0.54) suggests some degree of overfitting and sensitivity to the specific train–test split.
    - This indicates that while the Decision Tree performs well, it may benefit from pruning or hyperparameter tuning to improve generalization.  

- The SVC model also shows robust and stable recall performance (Test Recall: 0.52), with cross-validation results (0.57) slightly outperforming the single test split. 
    - This consistency suggests better generalisation across different data subsets, and lower variance compared to the Decision Tree
    - Although its test recall is marginally lower than that of the Decision Tree, the SVC’s stronger cross-validated recall highlights it as a reliable alternative, particularly in production environments.

### Repository Structure
```
├── data/
├── notebooks/
│   ├── claims_prediction.ipynb
│   ├── claims_prediction.html
├── README.md
```