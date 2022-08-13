# Classification by Neural Network
This project is mainly based on working with Tensorflow to create several neural networks and evaluate the effects of different parts of a neural network. here we have two main steps: 
- [Evaluating Neural Network's Elements](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Classification%20by%20Neural%20Network/README.md#evaluating-neural-networks-elements)
- [Fashion MNIST Classification](https://github.com/MohammadJavadArdestani/Data-Mining-projects/edit/main/Classification%20by%20Neural%20Network/README.md#fashion-mnist-classification)

## Evaluating Neural Network's Elements

In this part, ```sklearn.datasets.make_circles``` is used to create our dataset by the flowing line of code. You can make this task more complicated by increasing the value of this method's ```noise``` parameter.
```bash
X, y = sklearn.datasets.make_circles(n_samples=2000, shuffle=True, noise=0.2, random_state=10, factor=0.8)
```
Several neural networks were created, and different parts of a neural network were evaluated, such as: 


* No Activation Function 
* Linear vs. Nonlinear Activation Function 
* Loss Function 
* Number of Hidden Layers
* Starting Learning_Rate


After evaluating the role of all the elements mentioned, we define the best Neural Network to classify the dataset, which needs a small amount of time to train and reached 83.55% accuracy.<br>
You can find results and analysis of all the following parts in the [Notebook](https://github.com/MohammadJavadArdestani/Data-Mining-projects/blob/main/Classification%20by%20Neural%20Network/Classification%20by%20Neural%20Network.ipynb).

## Fashion MNIST Classification
