# Project Title
This project was conducted during the Data Analytics class in the second semester of 2023.
<br><br>

# Project Background 
In hospitals, patient mortality and its causes are of utmost importance. 
Therefore, this project aims to construct a classification model that predicts the risk of mortality using basic admission information and test results of patients, and to suggest ways to utilize this model. <br>
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
# Contribution
# Limitation
