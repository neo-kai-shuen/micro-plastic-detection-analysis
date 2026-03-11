# Micro/Nano Plastic Detection via Paper Microfluidic Chips

## University of Arizona - SIE533 Fundamentals of Data Science for Engineers


#### Problem
Micro- and nano-plastics (MNPs) are pervasive in the environment, varying in type (e.g., PMMA, PS, PET), origin (primary or secondary), and size (1 mm to <1 µm). The goal of this project is to detect and classify MNPs in water samples using binary classification (“Plastic” vs “No Plastic”), addressing the challenges posed by unbalanced classes and minimal missing data.


#### Data source
The dataset consists of 304 samples with 340 features, collected using two reagents (Reagent A and Reagent B). After averaging a few missing replicates, the dataset is clean and ready for analysis, though the classes remain unbalanced with 240 “Plastic” and 64 “No Plastic” samples.


#### Approach
Binary classification algorithms will be applied to predict the presence of plastic, evaluated primarily using the F1 score and stratified K-fold cross-validation to account for class imbalance. Feature importance will be analyzed to test the hypothesis that Bovine Serum Albumin (BSA) and Aspartic Acid are the most influential reagents in distinguishing plastic from non-plastic samples.


#### Exploratory Data Analysis
Initial exploratory analysis using pairwise plots indicated that most features are generally uncorrelated, with some expected correlation along the diagonal based on domain knowledge. This insight guided the choice of algorithms, including linear methods (Logistic Regression with no regularization, LASSO, Ridge; Linear SVM) and tree-based methods (Random Forest, Gradient Boosting, LightGBM, XGBoost) for binary classification of plastic vs. non-plastic samples.


#### Key results

**Linear Models (L1/L2 Regularization & SVM):**
* **Logistic regression** achieved an accuracy of 95.1%, F1-score of 0.919 and ROC-AUC of 0.990.
* **LASSO (L1)** achieved an accuracy of 80.3%, F1-score of 0.882, and ROC-AUC of 0.883.
* **Ridge (L2)** improved slightly with 85.3% accuracy, F1-score of 0.909, and ROC-AUC of 0.870.
* **SVM (linear kernel)** outperformed both, achieving 93.4% accuracy, F1-score of 0.960, and perfect ROC-AUC of 1.0.
* Feature selection revealed **15 key features** for L1 and L2, with **150_KH** consistently among the most important features across all models.

**Decision Tree-Based Models:**
* **LightGBM** achieved the highest performance, with 98.36% accuracy, F1-score of 0.9895, and ROC-AUC of 1.0.
* **Random Forest** and **XGBoost** also performed strongly, achieving F1-scores above 0.94.
* Feature importance analysis consistently highlighted **150_KH** as the top predictor, emphasizing its critical role.
* Even reduced feature sets (40–100 features) maintained high F1-scores, showing robust dimensionality reduction.

**Summary Table of Model Performance:**
| Model | Accuracy | Precision | Recall | F1    | F2    | ROC-AUC |
| ----- | -------- | --------- | ------ | ----- | ----- | ------- |
| L1    | 0.803    | 0.938     | 0.833  | 0.882 | 0.915 | 0.883   |
| L2    | 0.853    | 0.938     | 0.882  | 0.909 | 0.926 | 0.870   |
| SVM   | 0.934    | 0.923     | 1.000  | 0.960 | 0.984 | 1.000   |
| RF    | 0.918    | 0.978     | 0.917  | 0.946 | 0.928 | 0.960   |
| GB    | 0.885    | 0.977     | 0.875  | 0.923 | 0.893 | 0.960   |
| LGB   | 0.984    | 1.000     | 0.979  | 0.989 | 0.983 | 1.000   |
| XGB   | 0.950    | 0.979     | 0.958  | 0.968 | 0.961 | 0.980   |
| LR    | 0.951    | 0.970     | 0.885  | 0.919 | 0.988 | 0.990   |

**Insights:**
* Tree-based ensemble methods, particularly **LightGBM**, deliver the most accurate and robust predictions for plastic detection.
* Feature **150_KH** is consistently the most influential, underscoring its significance across all models.
* High n_estimators and proper feature selection improve model stability and reduce variance.


#### Conclusion
The analysis highlighted the importance of chemical variety in classifying the dataset, with top features including lysine, glycine, glutamine, cysteine, and BSA, each exhibiting distinct polarity, charge, and water interaction properties. Hypothesis 1 was supported: the data were effectively classifiable using binary algorithms, achieving F1 scores between 0.882 and 0.989 (median 0.935). Hypothesis 2 was not supported, as BSA and aspartic acid were not consistently the most important reagents for classification.


#### Technical stack
The analysis was implemented in Python, utilizing key libraries for data manipulation, visualization, and modeling, including NumPy, Pandas, Seaborn, Matplotlib, and SciPy. Machine learning and statistical modeling were performed using scikit-learn, with specific tools for logistic regression, model evaluation metrics, and train-test splitting.








