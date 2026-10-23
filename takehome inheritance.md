# APPLICATION OF INHERITANCE, POLYMORPHISM AND ENCAPSULATION IN OUR LOGISTIC REGRESSION PROJECT

## 1. Introduction

Our Machine Learning 4 project involves implementing Logistic Regression from scratch in C++. The system uses the Wisconsin Diagnostic Breast Cancer dataset to classify tumours as malignant or benign based on numerical features extracted from cell nuclei.

The project is organized into classes and modules responsible for loading data, preprocessing, training the logistic regression model, making predictions, evaluating performance and conducting statistical analysis.

Object-oriented programming principles help organize these components, promote modularity and make the system easier to maintain and extend.

This report examines three important object-oriented programming principles: inheritance, polymorphism and encapsulation, in relation to our project implementation.

## 2. Encapsulation

### 2.1 Definition

Encapsulation is an object-oriented programming principle that combines data and the functions that operate on that data within a class. It also controls access to the internal members of an object through access specifiers.

C++ provides three main access specifiers:

* `public`: Members can be accessed through the class's public interface.
* `private`: Members can be accessed directly within the class and by its permitted friends.
* `protected`: Members can be accessed within the class, by its permitted friends and by derived classes.

### 2.2 Encapsulation in our project

The `LogisticModel` class demonstrates encapsulation by keeping the model's internal parameters and implementation details separate from the functions used by other components.

Its internal members include the model weights, bias and last recorded loss. Public functions allow other components to train the model, make predictions and retrieve model parameters.

For example, `getBias()` allows the program to retrieve the bias through a public member function instead of accessing the private bias member directly.

Similarly, `predict()` provides a public interface for obtaining predictions without requiring the calling component to implement the model's internal calculations.

The `StatisticsAnalyzer` class also demonstrates encapsulation. Its public `analyze()` function provides access to the statistical analysis, while internal calculation functions are declared private.

### 2.3 Benefits of encapsulation

Encapsulation provides several benefits in our project:

1. **Data protection:** Private members cannot ordinarily be accessed directly by unrelated code.
2. **Modularity:** Each class manages its own responsibilities.
3. **Maintainability:** Internal implementation details can be changed without necessarily changing the public interface.
4. **Reduced coupling:** Other components can use a class without needing to understand every detail of its internal implementation.
5. **Controlled access:** Public member functions provide defined ways to interact with the model and analysis components.

Therefore, encapsulation helps keep our logistic regression implementation organized and manageable.

## 3. Inheritance

### 3.1 Definition

Inheritance is an object-oriented programming principle in which a new class, called a derived class, acquires accessible members and behaviours from an existing class, called a base class.

Inheritance supports code reuse and allows related classes to share common functionality.

In C++, inheritance can be declared using syntax such as:

`class Derived : public Base`

Here, `Derived` is the derived class, while `Base` is the base class.

### 3.2 Inheritance in our project

In the class declarations examined so far, we have not identified an inheritance relationship among the main project classes.

The `DataLoader`, `Preprocessor`, `LogisticModel`, `Trainer`, `Evaluator` and `StatisticsAnalyzer` classes have different responsibilities and are used as separate components.

For example, the `Evaluator` uses the trained model to evaluate predictions, while the `StatisticsAnalyzer` calculates statistical measures. This interaction does not, by itself, constitute inheritance.

Consequently, inheritance should not be claimed as an implemented feature unless further inspection of the project source code identifies a base class and a derived class.

### 3.3 Possible use of inheritance

Inheritance could be introduced in a future version of the project by defining an abstract base class for classification models.

For example, a base class named `ClassificationModel` could declare a virtual prediction function. A `LogisticModel` class could then derive from it and provide its own implementation.

This would allow the system to support additional classification algorithms through a common interface.

However, this is a possible future extension rather than a feature established in the current implementation.

### 3.4 Benefits of inheritance

If introduced appropriately, inheritance could:

1. Reduce duplication of common functionality.
2. Establish a common interface for different classification models.
3. Make the project easier to extend with additional algorithms.
4. Support runtime polymorphism through virtual functions.

## 4. Polymorphism

### 4.1 Definition

Polymorphism means that the same interface or operation can be used in different forms.

C++ supports several forms of polymorphism, including:

* Compile-time polymorphism through function overloading and templates.
* Runtime polymorphism through virtual functions and overriding.

### 4.2 Function overloading in our project

Our `LogisticModel` class declares two `predict()` functions:

* One accepts a single feature vector.
* The other accepts a collection of feature vectors.

The function signatures are:

`int predict(const std::vector<double>& features) const;`

`std::vector<int> predict(const std::vector<std::vector<double>>& X) const;`

Although both functions have the same name, they accept different parameter types.

The first function predicts the class of an individual sample, while the second predicts classes for multiple samples.

The compiler distinguishes between these functions based on their parameter lists. This is an example of function overloading, which is a form of compile-time polymorphism.

### 4.3 Benefits of polymorphism

Function overloading provides several benefits in our project:

1. It allows a consistent function name to be used for related operations.
2. It supports prediction for individual samples and batches of samples.
3. It improves readability by grouping related operations under one name.
4. It provides a convenient interface for other components of the system.

Runtime polymorphism through virtual functions and overriding has not been established in the class declarations examined so far. Therefore, we should not claim that it is implemented without finding supporting code.

## 5. Class Organization in the Project

Our project uses several classes, each responsible for a particular part of the machine learning workflow.

### 5.1 DataLoader

The `DataLoader` class is responsible for loading the dataset from a file.

It provides the data required by the subsequent preprocessing and training stages.

### 5.2 Preprocessor

The `Preprocessor` class prepares the dataset for model training. Its responsibilities include transforming the dataset, splitting it into training and testing sets, and normalizing features.

### 5.3 LogisticModel

The `LogisticModel` class represents the logistic regression model. It stores model parameters, calculates predictions and provides functions for training and accessing model parameters.

### 5.4 Trainer

The `Trainer` class is responsible for the training process. It coordinates the model's learning procedure and provides information about the training loss.

### 5.5 Evaluator

The `Evaluator` class assesses the trained model's classification performance. The evaluation includes accuracy, precision, recall, specificity, F1-score and the confusion matrix.

### 5.6 StatisticsAnalyzer

The `StatisticsAnalyzer` class performs statistical analysis, including the calculation of log-likelihood, null log-likelihood and McFadden's pseudo-R². It also supports coefficient inference where the necessary calculations are available.

These classes separate the major responsibilities of the application, making the implementation easier to understand, test and maintain.

## 6. Conclusion

Object-oriented programming principles help organize our Logistic Regression project into manageable components.

Encapsulation is demonstrated through classes such as `LogisticModel` and `StatisticsAnalyzer`, which separate public interfaces from private implementation details.

Function overloading in `LogisticModel`, particularly the two `predict()` functions, demonstrates compile-time polymorphism by supporting predictions for individual samples and batches of samples through the same function name.

Inheritance has not yet been established as an implemented feature in the class declarations examined. It could be introduced in a future version to support a common interface for multiple classification algorithms.

Overall, these principles contribute to modularity, readability, maintainability and the extensibility of our machine learning implementation.
