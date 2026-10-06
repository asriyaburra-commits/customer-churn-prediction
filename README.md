# Customer Churn Prediction

## About the Project

This project is about predicting whether a customer is likely to leave a service or continue using it.

I used the Telco Customer Churn dataset for this project. The dataset contains information about customers such as their tenure, contract type, monthly charges, payment method, services, and other account details.

The main goal was to understand the data, prepare it for machine learning, train different classification models, compare their performance, and check how well the selected model works on unseen data.

This project was completed as part of the **Arrowstack Machine Learning Internship**.

---

## Objective

The main objectives of this project are:

* Understand the customer churn dataset.
* Clean and prepare the data for machine learning.
* Perform exploratory data analysis.
* Create useful features from the existing data.
* Split the data into training, validation, and test sets.
* Build a baseline model.
* Train and compare different classification models.
* Evaluate the final model using suitable metrics.
* Check the incorrect predictions made by the model.
* Save the trained model and final results.

---

## Dataset

I used the **Telco Customer Churn** dataset.

The dataset contains information about customers and the services they use.

Some of the important columns are:

* `gender`
* `SeniorCitizen`
* `Partner`
* `Dependents`
* `tenure`
* `PhoneService`
* `InternetService`
* `Contract`
* `PaymentMethod`
* `MonthlyCharges`
* `TotalCharges`
* `Churn`

The column `Churn` is the target variable.

```text
No  → 0
Yes → 1
```

The `customerID` column was removed because it is only used to identify a customer and is not useful for making predictions.

---

## Project Structure

```text
Project_1_Customer_Churn/
│
├── data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
│
├── notebooks/
│   └── customer_churn_prediction.ipynb
│
├── models/
│   └── customer_churn_model.pkl
│
├── results/
│   └── final_test_results.csv
│
├── src/
│
├── README.md
├── model_card.md
└── requirements.txt
```

### Folder Details

* **data/** – contains the dataset.
* **notebooks/** – contains the Jupyter Notebook used for analysis and model building.
* **models/** – contains the saved trained model.
* **results/** – contains the final model evaluation results.
* **src/** – used for reusable source code.
* **README.md** – project information and instructions.
* **model_card.md** – information about the final model, its use and limitations.
* **requirements.txt** – Python packages required to run the project.

---

## Data Cleaning

Before training the models, I checked the dataset for missing values and incorrect data types.

The `TotalCharges` column contained values that needed to be converted into numeric format. I used `pd.to_numeric()` with `errors="coerce"` so that invalid values would be treated as missing values.

The `customerID` column was removed because it is an identifier.

---

## Exploratory Data Analysis

I performed some basic EDA to understand the relationship between the customer details and churn.

The analysis included:

* Checking the distribution of churn.
* Comparing tenure between churned and non-churned customers.
* Comparing monthly charges with churn.
* Checking how contract type is related to churn.

I used **Matplotlib** and **Seaborn** for the visualizations.

---

## Feature Engineering

I created a new feature called `TenureGroup` using the customer's tenure.

The customers were grouped into:

```text
0-1 Year
1-2 Years
2-4 Years
4+ Years
```

This was done to get a grouped view of customer tenure.

---

## Data Splitting

I divided the dataset into training, validation, and test data.

```text
Training Data   → 70%
Validation Data → 15%
Test Data       → 15%
```

The training data was used to train the models.

The validation data was used to compare the models and decide which model to use as the final model.

The test data was kept separate until the final evaluation.

I also used stratified splitting so that the churn class distribution remains similar across the different datasets.

---

## Data Preprocessing

The dataset contains both numerical and categorical columns, so I handled them separately.

### Numerical Columns

For numerical columns:

* Missing values were filled using the median.
* `StandardScaler` was used for scaling.

### Categorical Columns

For categorical columns:

* Missing values were filled using the most frequent value.
* `OneHotEncoder` was used to convert categorical values into numerical features.

The preprocessing steps were combined with the models using a Scikit-learn pipeline.

---

## Models Used

I trained and compared three classification models.

### 1. Logistic Regression

I used Logistic Regression as the baseline model.

It gives a simple starting point for comparing the performance of the other models.

### 2. Decision Tree Classifier

Decision Tree was used to see whether a tree-based model could improve the predictions.

### 3. Random Forest Classifier

Random Forest was also tested because it combines multiple decision trees and can handle more complex relationships in the data.

---

## Model Evaluation

I compared the models using the validation data.

The following metrics were used:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

After comparing the validation results, the better-performing model was selected for final testing.

The final model was then evaluated using the test dataset, which was not used during model selection.

---

## Error Analysis

After getting the final predictions, I checked the cases where the model made incorrect predictions.

There are two main types of errors:

### False Positive

The model predicted that a customer would churn, but the customer actually did not churn.

### False Negative

The customer actually churned, but the model predicted that the customer would not churn.

I used the confusion matrix and prediction results to understand these errors.

---

## Final Results

The final test results are saved in:

```text
results/final_test_results.csv
```

The file contains the final values for:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

The notebook contains the detailed model comparison and evaluation.

---

## Saved Model

The selected model is saved using Joblib:

```text
models/customer_churn_model.pkl
```

This saved model can be loaded later without training the model again.

---

## Model Card

A separate `model_card.md` file is included in the project.

It contains information about:

* What the model is used for
* Dataset used
* Model used
* Evaluation results
* Limitations
* Possible improvements

---

## Limitations

There are some limitations to this project.

* The dataset represents a particular telecom customer environment.
* The model may not perform in the same way on data from another company.
* Customer behavior can change over time.
* The model predictions should be treated as supporting information rather than the only factor used for business decisions.
* More data and regular model evaluation would be needed for a real production system.

---

## Future Improvements

Some improvements that can be considered in the future are:

* Hyperparameter tuning.
* Cross-validation.
* Trying additional classification algorithms.
* Feature importance analysis.
* Explainability techniques.
* Finding a suitable prediction threshold.
* Deploying the model through an API.
* Creating a simple web application for predictions.
* Monitoring the model after deployment.

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

### 2. Open the project folder

```bash
cd Project_1_Customer_Churn
```

### 3. Create a virtual environment

```bash
python -m venv venv
```

### 4. Activate the environment

For Windows:

```bash
venv\Scripts\activate
```

### 5. Install the required packages

```bash
pip install -r requirements.txt
```

### 6. Open the notebook

Open:

```text
notebooks/customer_churn_prediction.ipynb
```

Run the cells from top to bottom to reproduce the analysis and model training.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Joblib
* Jupyter Notebook

---

## Project Status

**Completed**

**Project:** Customer Churn Prediction

**Internship:** Arrowstack Machine Learning Internship

**Type:** Foundation / Core Industry Task
