# Project Overview
This project addresses stroke prediction using clinical data, with a focus on minimizing
false negatives due to their high medical cost.

## Problem Framing
* Since the dataset is medical, false negatives are
  significantly more costly than false positives in stroke prediction.
* Class imbalance exists, making accuracy a misleading metric.
* The task involves mixed feature types with missing and ambiguous values.

## Data Understanding
### Context
According to the World Health Organization (WHO), stroke is the second leading cause of death globally, responsible for approximately 11% of total deaths.
### Dataset Description
This dataset is used to predict whether a patient is likely to experience a stroke based on clinical and demographic attributes such as age, gender, medical history, and lifestyle factors. Each row represents an individual patient.

### Attribute Information
- id: Unique identifier  
- gender: "Male", "Female", or "Other"  
- age: Age of the patient  
- hypertension: 0 = No hypertension, 1 = Hypertension  
- heart_disease: 0 = No heart disease, 1 = Heart disease  
- ever_married: "No" or "Yes"  
- work_type: "children", "Govt_job", "Never_worked", "Private", or "Self-employed"  
- Residence_type: "Rural" or "Urban"  
- avg_glucose_level: Average glucose level in blood  
- bmi: Body mass index  
- smoking_status: "formerly smoked", "never smoked", "smokes", or "Unknown"  
- **stroke (target)**: 1 = Stroke, 0 = No stroke  
*Note: "Unknown" in smoking_status indicates missing information.*

### Data Quality & Constraints
- The dataset contains mixed feature types (numerical, categorical, binary).
- Missing values are present in several attributes.
- Some columns provide little or no predictive signal and may negatively affect model performance.
- Certain features contain irrelevant or noisy information.
- Some attributes include a high proportion of unknown or ambiguous values.

### Data Source
- Dataset sourced from Kaggle, originally compiled using World Health Organization (WHO) data.

## Modeling Strategy
- Logistic Regression was used as a baseline model due to its simplicity, interpretability, and suitability for binary classification. It provides probabilistic outputs, which are useful for analyzing confidence and adjusting decision thresholds in the presence of class imbalance.
- Support Vector Machines were explored as a margin-based alternative that can perform well on smaller datasets with clear class separation, providing a contrast to the probabilistic behavior of Logistic Regression.
## Evaluation Strategy
- The accuracy can be misleading in the medical datasets because we need to minimize the most critical negative effect. which is the false negative; therefore, the metric used is the recall by minimizing the threshold.
## Results & Observations
### Observations
- I noticed that The dataset contains mixed feature types (numerical and categorical).
- I noticed that Several features exhibit outliers that likely represent valid clinical values rather than noise.
- The 'bmi' feature contains missing values, which prevent direct model training if not handled.
- The 'id' feature and the 'Other' category in gender showed no meaningful predictive signal and introduced noise.
- I noticed that The target variable is highly imbalanced toward the “no stroke” class, which biases learning and inflates accuracy-based evaluation.
### Strengths
- The baseline Logistic Regression model demonstrated stable performance across validation splits.
- Probabilistic outputs enabled analysis beyond hard class predictions.
- Preprocessing decisions reduced training instability caused by missing values and noisy features.
- The model remained interpretable, allowing inspection of feature influence.
### Weaknesses
- Model performance is sensitive to data quality and feature encoding choices.
- Results may not generalize well due to dataset size and population bias.
### Results

- Applying SMOTE significantly improved the model’s ability to learn minority (stroke) patterns by balancing the class distribution during training.
- Combined with threshold reduction, recall for the positive (stroke) class increased substantially, effectively minimizing false negatives.
- This improvement was accompanied by a decline in precision and overall accuracy, which is acceptable given the medical risk associated with missed stroke cases.
- Confusion matrix analysis confirmed a clear reduction in false negatives after resampling and threshold adjustment.
  
### Conclusion

This project demonstrates that accuracy-driven evaluation is inappropriate for highly imbalanced medical datasets. By incorporating SMOTE to address class imbalance and adjusting the decision threshold to prioritize recall, the model better reflects real clinical priorities. Logistic Regression remained an effective and interpretable baseline, allowing insight into feature influence while maintaining strong recall performance.
Future Work Compare SMOTE with alternative resampling techniques such as ADASYN or Tomek Links.
Explore ensemble models that naturally handle imbalance, such as Gradient Boosting or Balanced Random Forests.
Perform cost-sensitive learning by explicitly weighting false negatives higher than false positives.
Validate the model on external or real-world clinical datasets to assess generalizability.

## Future Work

- Compare SMOTE with alternative resampling techniques such as ADASYN or Tomek Links.
- Explore ensemble models that naturally handle imbalance, such as Gradient Boosting or Balanced Random Forests.
- Compare explicit cost-sensitive learning (class weights or custom loss functions) against post-training threshold tuning to evaluate which approach yields more stable recall across validation splits.
- Validate the model on external or real-world clinical datasets to assess generalizability.
