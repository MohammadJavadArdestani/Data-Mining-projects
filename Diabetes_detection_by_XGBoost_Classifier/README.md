# Diabetes Detection by XGBoost Classifier
In this project, XGBoost model is used to detecting Diabetes for about 70K sample. It is also contains some preprocessing and Hyperparameter tuning steps to enhance the detection performance. 

## Table of Contents
* [Dataset]()
* [Preprocessing]()
* [XGBoost Model]()
* [Hyperparameter Tuninning]()
* [Impact of Each Hyperparameter]()

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
1. **Remove Nan values**: The number of rows containing nan value is minimal compared to the total data points. In this situation, for cases such as ```MBI``` and ```AGE```, which are numerical and continuous values, we can use the method of substituting the median or average. But, removing these data points is preferred because they have a tiny share in the dataset. 
2. **Remove white space:** Renaming columns or words from the data set that have spaces. These whitespaces may cause some model errors. Therefore, removing these whitespaces or placing them with a hyphen "_" is recommended.
3. **Normalize data**: 
    1. Body shapes can be divided based on BMI, so I divided all the values into four categories
    2. ```Mental_Health```, ```Age```, ```Physical_Health``` values shoud be scaled. At first, I used the StandardScaler, but I didn't get good results, so I chose the min-max scaling method.
4. **One-Hot Ecnoding**:
In general, data is divided into two groups, numerical and categorical. In building a decision tree, the preference is not to use categorical type, so I converted them to numerical attributes by the ```one-hot-encoding``` method.
5. **Train and Test split**: 
I use train_test_split from sklearn in this part and use stratify arg to split the data into balanced groups.
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
```gpu_hist``` is used to train the model and run gridsearch on GPU, which increases our speed considerably. 


# Hyperparameter Tuning 
a list of candidates for each hyperparameter is defined like this:
```
hyper_param_dict = {
    "learning_rate_list" : [0.02, 0.05, 0.1, 0.3],
    "max_depth_list" : [2, 3, 4] ,
    "n_estimators_list" : [100, 200, 300],
    "colsample_bytree" : [0.8, 1]
}
```
I define the below function for this part:
```bash
def tunner(hyper_params, X_train, actual_labels, my_roc_auc_score ):
  untuned_model = XGBClassifier(eval_metric='auc', Subsample=0.5) 
  kfold = StratifiedKFold(n_splits=3, shuffle=True, random_state=42)
  grid_search = GridSearchCV(model,hyper_params,scoring= my_roc_auc_score, n_jobs=-1, cv=kfold)
  grid_result = grid_search.fit(X_train, actual_labels)
  return grid_result
  ```