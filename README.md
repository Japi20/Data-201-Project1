# Data-201-Project1
Classification in Practice : Comparing logistic regression, LDA, QDA, and KNN to classify breast-mass samples as benign or malignant, with particular attention to missed malignancies.

This project investigates whether measurements of cell nuclei can distinguish malignant from benign breast-mass samples. Particular attention is given to malignant samples incorrectly classified as benign.

### Data

The brca.csv contains 569 samples and 30 numerical predictors. Each row summarizes nuclei from one breast-mass sample from fine needle extraction. The predictors describe ten nuclear characteristics using their mean, standard error, and worst summaries. The response is y, encoded as benign = 0 and malignant = 1. The exported row-number column is excluded from modeling.

Dataset background: https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

### Methods

A shuffled, stratified split reserves 143 samples for final testing and leaves 426 for training. Five-fold stratified validation is performed within the training set. Scaling is learned inside each pipeline. Logistic regression, LDA, QDA, and KNN use all 30 predictors. Validation selects K = 11 for KNN and reg_param = 0.1 for QDA.

Thresholds are selected using validation probabilities, aiming for at least 98% sensitivity and then reducing false positives. The selected thresholds are 0.40 for logistic regression, 0.02 for LDA, 0.02 for QDA, and 0.10 for KNN. Logistic regression is selected from validation results before test evaluation.

### Main finding

On the held-out test set, logistic regression reaches 97.90% accuracy, 96.23% sensitivity, 98.89% specificity, and ROC-AUC 0.9969. It misses 2 of 53 malignant samples and produces 1 false positive among 90 benign samples. LDA misses none and produces 8 false positives. QDA misses 1 and produces 4 false positives. KNN misses 3 and produces 9 false positives.

Logistic regression makes the fewest total errors and remains the project recommendation selected through validation. Its test sensitivity falls below the validation target. The small test set and differing error consequences motivate further evaluation on independent data before clinical use.

#### Files and execution

Run the project notebook in Google Colab from top to bottom after mounting Google Drive and setting the path to brca.csv. The work uses pandas, NumPy, matplotlib, seaborn, and scikit-learn. The local verification used scikit-learn 1.8.0.
