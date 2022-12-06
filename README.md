# Dimensionality-Reduction
PCA applied to Parkinson's Disease Classification Dataset

## Parkinson's Disease Detection Dataset – Dimensionality reduction


This is work from the Data Science Techniques and Applications (DSTA) module of the MSc in Data Science at Birkbeck, University of London. Coursework was set in two parts, this shows a representative combination of both. The theme of the work was dimensionality reduction.


### The brief was as follows:

Pick a data set from Kaggle, suitable for applying Principal Component Analysis (PCA).

Select a small number of features that you consider key to understanding how the data is distributed.

Select three dimensions that could be used as predictors of a fourth, predicted, dimension.

Visualise the values of the predictor dimensions with appropriate plots

Discuss the question of whether the three selected dimensions, taken together, could become a good predictor for the predicted dimension

Apply PCA to this data

Describe the results. Does the selection provide a good dimensionality reduction?


### My solution consists of the following:

Dataset is on Parkinson's Disease classification See here:

https://www.kaggle.com/datasets/sohelranaccselab/parkinsons-disease-classification

It is a dataset of 188 patients with diagnosed Parkinson's Disease (PD) plus a control group of 64 without PD, 252 participants in total. The data is from a study recording speech patterns of the subjects saying the vowel sound “a” for a sustained period, repeated 3 times each, resulting in 756 observations. There are 753 features plus the class label.

Sci-kit learn features and methods are used throughout: https://scikit-learn.org

The data set is split into train and test sets at 80/20 split at an early stage in the work.

Features are selected by first reducing the data set using SelectKBest as a filter method.

Three features are then further selected from this reduced set, PCA was applied to this (somewhat manually) reduced set.

As comparison, to answer the set questions, further datasets are created:

A full dataset with no PCA applied, the data is scaled.

PCA applied to the whole dataset, with output of the first 3 principal components. ( n_components = 3) For direct comparison to the 3 selected features.

PCA applied to the whole dataset using a threshold of 90% variance explained by the data (n_components = 0.9). To compare PCA where most of the data variance is explained, for comparison to the full dataset with no PCA

PCA applied to the whole dataset with the first 50 principal components. (n_components = 50). For comparison to the 0.9 threshold set and the total dataset.

The 5 datasets are then compared by applying predictive models from a selection which are spot-checked using K-fold cross validation, using accuracy as the scoring function.

K-Nearest Neighbors (KNN) delivers the best performance using this K-fold cross validation. The models are not tuned in any way.

KNN is fitted to the 5 data training sets, and used to predict the test sets.

Confusion matrices are produced as visualisation of the predictive accuracy of the trained models for each dataset.


### Results:

PCA on the 3 selected features did not produce a clear transformation of the data. The data still being somewhat scattered, as the selection of three features is arbitrary to the task and not based on the ‘best’ number of features for the dataset.

PCA using the whole dataset with output of the first 3 principal components performed better than the 3 selected features. The proportion of variance explained achieving 39%, missing the majority of the information contained in the dataset.

The threshold at 0.9 (or 90%), output 76 principal components in comparison to the set using 50 components which explain 85.5% of the variance. This highlights the small contribution of the components after the first 50


The manually selected 3 features set with PCA performed particularly poorly, only classifying negative values.

The best performing models are those containing the most data, that is the set with all the data (no PCA), the set at 0.9 threshold and with 50 components.

The results are comparable to those in the study for which the dataset was created, where results delivered accuracy of 0.86, an F1 score of 0.84 and MCC of 0.59.

The F1 score takes the mean of the detection rate and the precision. Where detection rate is the proportion of correctly classified positives as a total of all actual positives.

Precision is, of all the predictions classified as positive, how many were correct.

Matthews Correlation Coefficient (MCC) is a more general measure of performance overall. Unlike some of the other measures, it uses each of the values from the confusion matrix, taking into account the proportion of positives and negatives. This is quite low in all the models. Reflected in the low measure for False Alarm Rate (FAR) which in this case would be the number of cases predicted to show Parkinson’s that in fact were not.

No tuning was performed on the models, and other models were not explored which may enhance performance overall.

As this data is for the purpose of a medical diagnosis, it is reasonable to trade better classification of true positive (TP) at expense of false positives and therefore the False Alarm Rate (FAR). Improving the FAR will improve the MCC. Minimising the False Negative Rate (FNR) is desirable as it represents missed diagnoses. This should be taken into consideration when assessing the performance of a model for this type of application.


![image](https://user-images.githubusercontent.com/74421484/205926338-c6efc3af-2781-4e93-9979-bcaff679b113.png)
