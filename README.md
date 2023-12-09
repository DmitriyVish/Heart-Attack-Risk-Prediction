# `<center>`**Heart Attack Risk Prediction**

![](https://image.shutterstock.com/image-vector/heart-attack-risk-factors-vector-260nw-550350928.jpg)

The project is based on a dataset [Heart Attack Risk Prediction](https://www.kaggle.com/datasets/iamsouravbanerjee/heart-attack-prediction-dataset/data) from the Kaggle platform.

[My kaggle profile](https://www.kaggle.com/dmitriyvishnyakov)

## **Context**

The Heart Attack Risk Prediction Dataset serves as a valuable resource for delving into the intricate dynamics of heart health and its predictors. Heart attacks, or myocardial infarctions, continue to be a significant global health issue, necessitating a deeper comprehension of their precursors and potential mitigating factors. This dataset encapsulates a diverse range of attributes including age, cholesterol levels, blood pressure, smoking habits, exercise patterns, dietary preferences, and more, aiming to elucidate the complex interplay of these variables in determining the likelihood of a heart attack. By employing predictive analytics and machine learning on this dataset, researchers and healthcare professionals can work towards proactive strategies for heart disease prevention and management. The dataset stands as a testament to collective efforts to enhance our understanding of cardiovascular health and pave the way for a healthier future.

## **Content**

This dataset provides a comprehensive array of features relevant to heart health and lifestyle choices, encompassing patient-specific details such as age, gender, cholesterol levels, blood pressure, heart rate, and indicators like diabetes, family history, smoking habits, obesity, and alcohol consumption. Additionally, lifestyle factors like exercise hours, dietary habits, stress levels, and sedentary hours are included. Medical aspects comprising previous heart problems, medication usage, and triglyceride levels are considered. Socioeconomic aspects such as income and geographical attributes like country, continent, and hemisphere are incorporated. The dataset, consisting of 8763 records from patients around the globe, culminates in a crucial binary classification feature denoting the presence or absence of a heart attack risk, providing a comprehensive resource for predictive analysis and research in cardiovascular health.

+ Dataset Glossary (Column-wise)
+ Patient ID - Unique identifier for each patient
+ Age - Age of the patient
+ Sex - Gender of the patient (Male/Female)
+ Cholesterol - Cholesterol levels of the patient
+ Blood Pressure - Blood pressure of the patient (systolic/diastolic)
+ Heart Rate - Heart rate of the patient
+ Diabetes - Whether the patient has diabetes (Yes/No)
+ Family History - Family history of heart-related problems (1: Yes, 0: No)
+ Smoking - Smoking status of the patient (1: Smoker, 0: Non-smoker)
+ Obesity - Obesity status of the patient (1: Obese, 0: Not obese)
+ Alcohol Consumption - Level of alcohol consumption by the patient (None/Light/Moderate/Heavy)
+ Exercise Hours Per Week - Number of exercise hours per week
+ Diet - Dietary habits of the patient (Healthy/Average/Unhealthy)
+ Previous Heart Problems - Previous heart problems of the patient (1: Yes, 0: No)
+ Medication Use - Medication usage by the patient (1: Yes, 0: No)
+ Stress Level - Stress level reported by the patient (1-10)
+ Sedentary Hours Per Day - Hours of sedentary activity per day
+ Income - Income level of the patient
+ BMI - Body Mass Index (BMI) of the patient
+ Triglycerides - Triglyceride levels of the patient
+ Physical Activity Days Per Week - Days of physical activity per week
+ Sleep Hours Per Day - Hours of sleep per day
+ Country - Country of the patient
+ Continent - Continent where the patient resides
+ Hemisphere - Hemisphere where the patient resides
+ Heart Attack Risk - Presence of heart attack risk (1: Yes, 0: No)

## Classification metrics

1. Accuracy

One of the simplest, and therefore most common, metrics is accuracy. It shows the number of correctly assigned class labels (true positive and true negative) from the total amount of data and is calculated as follows.

$accuracy = \frac{TP + TN}{TP + TP + FN + FP}$

However, this simplicity is also the reason why it is often criticized and why it may be completely unsuitable for the task at hand. It does not take into account the false positive rate of the model, which can be critical, especially in the medical field, when the task is to recognize all true cases of diagnosis.

Let's return to the example of suspected disease. If our accuracy is 80%, then we can say that on average, out of 100 people, it will correctly determine the presence or absence of a diagnosis in only 80 people, while another 20 will be either false negatives or false positives.

It is worth paying attention to the fact that in some tasks it is necessary to identify all patients with a diagnosis and you can even neglect false positive outcomes, since they can be eliminated at the next stages of the study (for example, after control testing), then you need to add one more metric to this metric , which could estimate the required priority.

2. Precision

Despite the different English names and different calculation formulas, the Russian translation of this metric is also fixed as “accuracy,” which can cause confusion and confusion, so you should clarify what exactly you are talking about. This accuracy shows the number of true positive outcomes from the entire set of positive labels and is calculated using the following formula:

$precision = \frac{TP}{TP + FP}$

The importance of this metric is determined by how high the “cost” of a false positive result is for the task in question. If, for example, the cost of further testing for the presence of a disease in a patient is high and we simply cannot check all false positive results, then it is worth maximizing this metric, because with Precision = 50% of 100 positively identified patients, only 50 of them will be diagnosed.

3. Recall (true positive rate)

In Russian, the word used for this term is “fullness” or “sensitivity”. This metric determines the number of true positives among all class labels that were defined as "positive" and is calculated using the following formula.

 $recall = \frac{TP}{TP + FN}$

It is necessary to pay special attention to this assessment when the error of non-recognition of the positive class in the task at hand is high, for example, when diagnosing a fatal disease.

 4. F1-Score

In the event that Precision and Recall are equally significant, you can use their harmonic mean to estimate the results:

$$
F1 = \frac{2 precision * recall}{precision + racsll}
$$

In addition to point estimates, there are a number of graphical methods that can evaluate the quality of classification.

5. ROC
   ROC (receiver operating characteristic) is a graph showing the dependence of correctly classified objects of a positive class from falsely positively classified objects of a negative class. In other words, the ratio of True Positive Rate (Recall) and False Positive Rate

Using the ROC curve, you can compare models, as well as their parameters, to find the most optimal (in terms of tpr and fpr) combination. In this case, a compromise is sought between the number of patients whose label was correctly identified as positive and the number of patients whose label was incorrectly identified as positive.

6. AUC (Area Under Curve)

As a numerical estimate of the ROC curve, it is customary to take the area under this curve, which is a good “total” for the curve. If between the X and Y curves there is dominance of the first over the second, then AUC (X) > AUC (Y), the opposite is not always true. But AUC also has a statistical meaning: it shows the probability that a randomly selected instance of a negative class will be less likely to be recognized as a positive class than a randomly selected positive class.

## Modeling

1. At the first stage, the models were trained on unbalanced classes.
   It uses a naive Bayes classifier, a decision tree, a random forest, and gradient boosting over decision trees. All models showed a high degree of overfitting.
2. Oversampling with SMOTE. In SMOTE (Synthesized Minority Oversampling Technique) we create elements in close proximity to existing ones in a smaller set.

Using SMOTE, synthetic samples are generated as follows: take the difference between the feature vector in question and its nearest neighbor. We multiply this difference by a random number from 0 to 1 and add it to the feature vector under consideration.

This causes the selection of a random point on a line segment between two specific objects. This approach effectively forces the minority class to make more general decisions.

In a balanced sample, the models did not show overfitting. However, the metrics for medical data are quite low. Precision on the test sample is 0.75

3. Generating artificial data with ctgan

   As an experiment, a random sample of 150 observations was taken from the original dataset. Using CTGAN, artificial data of 10,000 observations were generated.

   The models again showed no overfitting. The best presizhen metric on the test sample was shown by the sulcha forest model - 0.60. But in this case, the recall metric has increased significantly. The best result was shown by gradient boosting - 0.63 on the test sample.
