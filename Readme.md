# Introduction
This repository aims to show the result and the methodology used to achieve the objectives of the technical test. The task is based on binary clasification problem, using Python programming language for their development.

# Getting Started

1. Installation process:
    * Install conda
    * conda create -n testcw python=3.6
    * conda activate testcw
    * pip install -r requirements.txt
    
1. Software dependencies
    * All python packages needed are included in `requirements.txt`

1. Run notebook
    * The notebook `Analysis.ipynb` contains all the process to achive the goal.
    * Notebook's structure:
        * Imports
        * Loading data
        * EDA
        * Preprocess data
        * Train and evaluate the a model
        * Making predictions

# Methodology
The repository is structured in the following folders:
* code: You will find the forlder scripts that contains the python scripts and a folder called "notebooks" that contains the notebook of all analysis. 

* dataset: You will find the following datasets.
    * train_file = 'accounts_train.csv'
    * quotes_train_file = 'quotes_train.csv'
    * test_file = 'accounts_test.csv'
    * quotes_test_file = 'quotes_test.csv'

* models: You will find the models already trained.
    * lstm_model.h5
    * lstm_model_.h5
    * model_gbc.pickle

* results: You will find the `predict_account_value.csv` that contains the **account_uuid** with their respective **account_value**

## Generate Dataset

1. A dataset was created with a merge between **train_file** and  **quotes_train_file**  the same process is repeated for the test set.
    * To view the Dataset go to **Analysis.ipynb** 

## OBJECTIVE 1: Create a model to predict if a client buy or not a product.

## Pre-process

To perform pre-processing, a class called "Preprocces" was developed. This class has different methods:

* clean_dataframe: It was used to clean / pre-process the data.
* fill_numerical_na: Null values are replace with the method `IterativeImputer`
* fill_categorical_na: Two methods were implemented.
    * Impute NaN for **not indicated**
    * Impute NaN using `KNNImputer`
* encode_and_bind : Apply OneHotEncoder to transform categorical variables into numeric.


## Model 

### Classifier:

For this task, two data sets were generated by the method **fill_categorical_na** to train a model and compare which method gives better results.

* Different classifiers were trained, among them the following stand out:
    * MultinomialNB()
    * GaussianNB()
    * AdaBoostClassifier()
    * MLPClassifier()
    * DecisionTreeClassifier()
    * RandomForestClassifier()
    * XGBClassifier()
    * LogisticRegression()
    * GradientBoostingClassifier()

* Moreover a RNN was trained:
    * LSTM

In the notebook **Analysis.ipynb** the performance of all models is appreciated, the comparison is made using the f1_score and roc_auc_score metric.

In this case, by comparing all models, the **GradientBoostingClassifier** achieved better results for each classes using the metric mentioned before, for this reason it was chosen to make the final model and be used to make predictions for the test dataset.

# CONCLUSION

In accordance with the objectives set out in the test, different classifiers and recurrent neural networks were used to classify if a client buy or not a product. The results showed that the optimal way to classify using sparse data is to use **GradientBoostingClassifier** and impute NaN as new class, in our case was called **not indicated**, because is very well suited for sparse data problems with large dimension generated by many categorical variables.

It was decided to use f1_score and roc_auc_score metrics to measure the performance of the model optimally in each class. 
