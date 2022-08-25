# Diabetes Detection by XGBoost Classifier
In this project, XGBoost model is used to detecting Diabetes for about 70K sample. It is also contains some preprocessing and Hyperparameter tuning steps to enhance the detection performance. 

## Table of Contents
* [Dataset]()
* [Preprocessing]()
* [XGBoost Model]()
* [Hyperparameter Tuninning]()
* [Impact of Each Hyperparameter]()

## Dataset
Dataset of this project is sampled from [Diabetes Health Indicators Datase](https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset) which contains 22 features and 441456 samples. We work on about 70k samples in this project. beleow table demonstrate the features, for more details read this [document](https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset).  

<table>
  <tr>
    <td>HighBP (High Blood Pressure)</td>
    <td>High Cholesterol</td>
    <td>Cholesterol Check</td>
    <td>BMI</td>
    <td>Smoker</td>
    <td>Stroke</td>
    <td>Heart Diseaseor Attack</td>
    <td></td>
  </tr>
  <tr>
    <td>Centro comercial Moctezuma</td>
    <td>Francisco Chang</td>
    <td>Mexico</td>
  </tr>
</table>

HighBP: High Blood Pressure
High Cholesterol
Cholesterol Check: Whether the patient has done a cholesterol check
BMI: Body Mass Index
Smoker
Stroke
HeartDiseaseorAttack
Physical Activity
Fruits
Veggies
Heavy Alcohol Consumption
Any Health Care
No Doctor because of Cost: Whether the patient posponed or canceled a doctor's appointment due to the costs
General Health
Mental Health
Physical Health
Difficulty Walking
Sex: Gender
Age
Education
Income