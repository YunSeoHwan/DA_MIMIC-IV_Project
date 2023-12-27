# Project Title
This project was conducted during the Data Analytics class in the second semester of 2023.
<br><br>

# Project Background 
In hospitals, identifying the causes of patient mortality is crucial. 
Therefore, we aim to construct a classification model that predicts the risk of mortality using basic admission information and test results of patients, and to suggest ways to utilize this model. <br>
This project utilized the [**MIMIC-IV**](https://physionet.org/content/mimiciv/2.2/) dataset.
<br><br>

# Project Process  

## Stack
### Language & Library
<div>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pytorch-EE4C2C?style=flat&logo=pytorch&logoColor=white"/>
  <img src="https://img.shields.io/badge/Numpy-013243?style=flat&logo=Numpy&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=Pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Scikit learn-F7931E?style=flat&logo=Scikitlearn&logoColor=white"/>
</div>

### Model
<div>
  <img src="https://img.shields.io/badge/DecisionTree-000000?style=flat&logo=&logoColor=white"/>
  <img src="https://img.shields.io/badge/XGBoost-000000?style=flat&logo=&logoColor=white"/>
  <img src="https://img.shields.io/badge/MLP-000000?style=flat&logo=&logoColor=white"/>
  <img src="https://img.shields.io/badge/TabNet-000000?style=flat&logo=&logoColor=white"/>
</div>
<br><br>

## Pipeline
### Dataset
In this project, a total of seven datasets were used from the [**MIMIC-IV**](https://physionet.org/content/mimiciv/2.2/) data: three patient information datasets, ICU data, and three datasets for test indicators. Subsequently, the data were merged based on the 'hadm_id'. For the 'labevents' data, merging was carried out with the 'd_labitems' dataset based on the 'Item_id'. After grouping by each 'item_id', the average values were used as labels. For a detailed explanation of the dataset construction, please refer to the figure below and the MIMIC-IV documentation.
<br><br>
![image](https://github.com/YunSeoHwan/DA_MIMIC-IV_Project/assets/48356954/c0046d18-eebb-4dbe-8ad8-6927ac88fcea)
![image](https://github.com/YunSeoHwan/DA_MIMIC-IV_Project/assets/48356954/b6c32656-78f0-4a4b-aebd-9a9c650b3c91)

### Preprocessing
- To prevent data leakage, the 'discharge_location' and 'dod' features were dropped.
- All admission and discharge times were converted to a value representing 'discharge time - admission time.' Afterward, the skewness of these values was checked, a square root transformation was applied, and they were discretized using the IQR method.
- One-hot encoding was performed for object type features.
- Missing values were treated as zeros, and features with measurement errors were dropped.

### Modeling
Tree-based models such as Decision Tree (DT) and XGBoost, as well as Deep Learning (DL) models like MLP and TabNet, were employed. Comparative experiments were conducted ranging from the most complex and parameter-heavy TabNet to the relatively simple DT. Considering class imbalance and the seriousness of type II errors, evaluation metrics such as F1 score and recall were used. Along with these metrics, the trade-off between bias and variance was taken into account in the search for the optimal model.

### Training & Optimization
- The train, validation, and test split was conducted at a ratio of 7:1:2.
- Seed, GPU, and CPU specifications were kept consistent across all models.
- After deriving feature importance, features with an importance of zero were dropped.
- For the DL models, scaling and oversampling were performed.
- Grid search was utilized for the tree-based models.
- Optuna was used for the DL models.
## Role
### [**YunSeoHwan**](https://github.com/YunSeoHwan) : EDA, Preprocessing, Modeling, Interpretation<br>
### YunSungho : EDA, Preprocessing
<br><br>

# Result
We selected the simplest Decision Tree (DT) as our baseline model. The results of the comparative experiments with other models are shown in the table below. XGBoost demonstrated the highest performance compared to the two DL models. Despite having only a third of the number of nodes compared to XGBoost, the DT's F1 score and recall did not differ significantly from the highest-performing XGBoost. <br><br>
![image](https://github.com/YunSeoHwan/DA_MIMIC-IV_Project/assets/48356954/555962a5-b7bd-40d3-8620-de34ae4fb74c)
<br><br>
# Contribution
We will utilize the two most superior tree-based models. Firstly, leveraging the advantage of Decision Trees (DT) for rule extraction, we can derive top rules and provide them as an auxiliary tool to medical professionals with domain knowledge. Secondly, using the high predictive performance of XGBoost, we can carry out scenario analyses to understand patient mortality risk based on important variables.
<br>
## Rule Extraction
The figure represents rules extracted in text form that had the greatest impact on survival and mortality using the Decision Tree (DT) method. For instance, the first two conditions of the rule that classified the highest number of deceased are when the drg_severity is greater than 3 and Lactate level is over 3.5. These two conditions at the topmost level of the tree significantly influenced the classification of the most fatalities. Utilizing DT allows for the extraction of such rules, offering much more specific interpretations than simply using variable importance. <br><br>
![image](https://github.com/YunSeoHwan/DA_MIMIC-IV_Project/assets/48356954/4f36c9fb-41e7-446c-a36a-8a525c9c0a67)
<br><br>

## Scenario Analysis
Scenario analysis begins by generating 2,500 synthetic data points, considering all possible combinations of key variables for a single patient. Each row of the synthetic data represents one of the 2,500 combinations for that patient. Using the previously developed XGBoost classifier, we conducted scenario analysis to observe changes in the probabilities of mortality and survival.<br><br>
![image](https://github.com/YunSeoHwan/DA_MIMIC-IV_Project/assets/48356954/e889d66a-d4ff-4e06-9928-42985a74cf71)
<br><br>

The graph represents the best and worst-case scenarios for a patient who was initially predicted to have a mortality probability of 0.49. The table below details the values of key variables for each scenario and their corresponding probabilities of survival or death. Reviewing each case, it's evident that the probabilities of survival or death change significantly with the increase or decrease of these important variables' values. By providing this information to medical professionals with domain knowledge, we can offer insights into survival or mortality that may otherwise be overlooked.<br><br>
![image](https://github.com/YunSeoHwan/DA_MIMIC-IV_Project/assets/48356954/084e6c8f-319e-4435-81ed-555b9dd0ae6a) <br><br>
# Limitation
Due to the large size of the dataset, resource limitations restricted the range of model selection. Additionally, optimizing across various combinations proved to be challenging.
