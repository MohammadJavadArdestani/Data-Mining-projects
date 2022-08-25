﻿# Data Mining projects
This repository contains five different projects. In each of these projects, essential subjects of Data Mining are covered.

# Projects

* [Diabetes Detection by ‍‍‍XGBoost Classifier](https://github.com/MohammadJavadArdestani/Data-Mining-projects/tree/main/Diabetes_detection_by_XGBoost_Classifier)<br>
-- In this project, the ```XGBoost``` model is used to detect Diabetes for about 70K samples. It also contains some ```preprocessing``` and ``Hyperparameter tuning`` steps to enhance the detection performance.


### Table of Contents
* [Dataset](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Diabetes_detection_by_XGBoost_Classifier/README.md#dataset)
* [Preprocessing](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Diabetes_detection_by_XGBoost_Classifier/README.md#preprocessing)
* [XGBoost Model](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Diabetes_detection_by_XGBoost_Classifier/README.md#xgboost-model)
* [Hyperparameter Tuninning](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Diabetes_detection_by_XGBoost_Classifier/README.md#hyperparameter-tuning)
* [Impact of Each Hyperparameter](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Diabetes_detection_by_XGBoost_Classifier/README.md#impact-of-each-hyperparameter)

## Dataset
Dataset of this project is sampled from [Diabetes Health Indicators Datase](https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset), which contains 22 features and 441456 samples. We work on about 70k samples in this project. The below table demonstrates 20 main features. For more details read this [document](https://www.kaggle.com/datasets/alexteboul/diabetes-health-indicators-dataset).  

<table>
  <tr>
    <td>HighBP (High Blood Pressure)</td>
    <td>High Cholesterol</td>
    <td>Cholesterol Check</td>
    <td>Any Health Care</td>
  </tr>
  <tr>
    <td>BMI</td>
    <td>Smoker</td>
    <td>Stroke</td>
    <td>Heart Diseaseor Attack</td>
  </tr>

   <tr>
    <td>Physical Activity</td>
    <td>Fruits</td>
    <td>Veggies</td>
    <td>Heavy Alcohol Consumption</td>
  </tr>

   <tr>
    <td>No Doctor because of Cost</td>
    <td>canceled a doctor's appointment due to the costs</td>
    <td>General Health</td>
    <td>Mental Health</td>
  </tr>

   <tr>
    <td>Physical Health</td>
    <td>Difficulty Walking</td>
    <td>Age</td>
    <td>Education</td>
  </tr>
</table>

## Preprocessing
This part includes five steps:
1. **Remove Nan values**: The number of rows containing nan values are minimal compared to the total data points. In this situation, for cases such as ```MBI``` and ```AGE```, which are numerical and continuous values, we can use the method of substituting the median or average. But, removing these data points is preferred because they have a tiny share in the dataset. 
2. **Remove white space:** Renaming columns or words from the data set with spaces. These whitespaces may cause some model errors. Therefore, removing these whitespaces or placing them with a hyphen "_" is recommended.
3. **Normalize data**: 
    1. Body shapes can be divided based on BMI, so I divided all the values into four categories
    2. ```Mental_Health```, ```Age```, ```Physical_Health``` values should be scaled. At first, I used the StandardScaler, but I didn't get good results, so I chose the min-max scaling method.
4. **One-Hot Ecnoding**:
In general, data is divided into two groups, numerical and categorical. In building a decision tree, the preference is not to use categorical type, so I converted them to numerical attributes by the ```one-hot-encoding``` method.
5. **Train and Test split**: 
I use train_test_split from sklearn in this part and stratify arg to split the data into balanced groups.
```bash
 train_test_split(data_dims, labels, test_size=0.2, random_state=42, stratify=labels)
```

## XGBoost Model
In this part of the project, an XGBClassifier is defined with the following parameters:

```bash
tree_method='gpu_hist'
Learning_rate=0.1
Max_depth=4
N_estimator=200
Subsample=0.5
Colsample_bytree=1
Random_seed=123
Eval_metric='auc'
Verbosity=1
```
```gpu_hist``` ss used to train the model and run ```GridSearchCV``` on GPU, which increases our speed consid


## Hyperparameter Tuning 
List of candidates for each hyperparameter:
```
hyper_param_dict = {
    "learning_rate_list" : [0.02, 0.05, 0.1, 0.3],
    "max_depth_list" : [2, 3, 4] ,
    "n_estimators_list" : [100, 200, 300],
    "colsample_bytree" : [0.8, 1]
}
```
```GridSearchCV``` is used to constructing ``` 4 * 3 * 3 *2 = 72 ```  different models from all possible combinations of the candidate parameters.```StratifiedKFold``` is also used to imply  cross-validation by 3 split-points. I defined the below function for this part.
```bash
def tunner(hyper_params, X_train, actual_labels, my_roc_auc_score ):
  untuned_model = XGBClassifier(eval_metric='auc', Subsample=0.5) 
  kfold = StratifiedKFold(n_splits=3, shuffle=True, random_state=42)
  grid_search = GridSearchCV(model,hyper_params,scoring= my_roc_auc_score, n_jobs=-1, cv=kfold)
  grid_result = grid_search.fit(X_train, actual_labels)
  return grid_result
  ```
and I got the results as ```best_param```: 
```
'colsample_bytree': 0.8
 'learning_rate_list': 0.02
 'max_depth_list': 2
 'n_estimators_list': 100
 ```

## Impact of Each Hyperparameter
In the last part of This project, we used best_param values for each subplot and placed only one variable on the horizontal axis to see the effects of that variable on the best_param model. Based on the results, it was found that the colsample_bytree parameter has a more significant impact on the quality and performance of the model than other parameters. <br><br><br>
![Impact of Each Hyperparameter](https://github.com/MohammadJavadArdestani/Data-Mining-projects/blob/main/Diabetes_detection_by_XGBoost_Classifier/Hyperparameter_imapct.PNG)




* [Iris Dataset analysis](https://github.com/MohammadJavadArdestani/Data-Mining-projects/tree/main/Iris%20Dataset%20analysis)<br>
-- This project contains five main parts, which are implemented by two major preprocessing libraries ```Pandas``` and ```Scikit-learn```.

## Table of Contents
* [Handling Missing Values](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Iris%20Dataset%20analysis/README.md#handling-missing-values)
* [Target Labeling](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Iris%20Dataset%20analysis/README.md#target-labeling)
* [Standardizing](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Iris%20Dataset%20analysis/README.md#standardizing)
* [PCA Analysis](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Iris%20Dataset%20analysis/README.md#pca_analysis)
* [Plotting Dataset](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Iris%20Dataset%20analysis/README.md#plotting-dataset)

## Handling Missing values
 In this part, we looked for nan and missed values in the dataset. Several methods handle missing values, like replacing them with mean, median, or a fixed value. There is a small number of missing values in the dataset. Therefore we can remove missing values. 

## Target Labeling
```Scikit-learn``` proposes two different ways of labeling: One Hot Encoding and Label Encoding. 
We chose the label Encoding to deal with a problem. 
```
Iris-setosa --> 0
Iris-versicolor --> 1
Iris-virginica --> 2
```
The problem here is since there are different numbers in the same column, models will misunderstand the data to be in some order, 0 < 1 <2.

## Standardizing
Standardizing the features around the center and 0 with a standard deviation of 1 is essential when comparing measurements with  Variables measured at different scales.```sklearn.preprocessing.StandardScaler``` is used for standardizing. The mean and var are reported before and after the normalization

## PCA 
Plotting datasets with more than 2 or 3 features is challenging for us. in the Iris dataset, we have four characteristics: 
```
sepal length 
sepal width 
petal length 
petal width
```
We used PCA for Dimensionality Reduction and decreased the number of features to two. 

## Plotting Dataset
In the last part of the project, we plotted the PCA result. Also, some Boxplots of the dataset before and after normalization are used to analyze the distribution. plots can be found in [notebook file](https://github.com/MohammadJavadArdestani/Data-Mining-projects/blob/main/Iris%20Dataset%20analysis/Iris_analysis.ipynb)





* [Classification by Neural Network](https://github.com/MohammadJavadArdestani/Data-Mining-projects/tree/main/Classification%20by%20Neural%20Network)<br>
-- This project is mainly based on working with ```Tensorflow``` to create several neural networks and evaluate their different elements.


* [Association Rules](https://github.com/MohammadJavadArdestani/Data-Mining-projects/tree/main/Association%20Rules)<br>
-- The goal of this project is extracting ```Association Rules```  from ```Hypermarket_dataset``` using ```TransactionEncoder``` and```Apriori algorithm```.

* [Clustering](https://github.com/MohammadJavadArdestani/Data-Mining-projects/tree/main/Clustering) <br>
I used the ```K-means``` algorithm and ```elbow``` technique to find the best value of ```K``` for a dataset created by ```make_blobs```. Also, the ```DBSCAN``` algorithm and some parameter tuning for the ```epsilon``` and ```MinPts``` are implemented.
