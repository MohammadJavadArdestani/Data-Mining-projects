# Iris Dataset analysis
This project contains five main parts, which are implemented by two major preprocessing libraries ```Pandas``` and ```Scikit-learn```: 
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
