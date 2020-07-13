# Test Data Science Metranet
#### Name : Agung Nugraha
#### Email : nugraha.agung@alumni.ui.ac.id
#### Phone : +6282388884985

# Table of Content
### A. Task
### B. Step of work
### C. Question Answer


# A. Task :

- File training_set.csv berisi data training yang terdiri dari 7500 observasi dan 21 kolom, 20 kolom pertama adalah variabel input (x_0, x_1, ..., x_19), sedangkan kolom terakhir adalah target (y).
- Ada 3 kemungkinan nilai target: 0, 1, dan 2
- Missing value direpresentasikan oleh string "nan"
- File test_set.csv adalah data test yang terdiri dari 2500 baris, namun hanya ada 20 kolom variabel input
- Tugas anda adalah membuat model berdasarkan data training lalu memprediksi target pada data test
- Algoritma dan bahasa pemrograman yang digunakan bebas
- File yang harus anda sediakan:
  - output.csv: file yang tiap barisnya merupakan prediksi dari masing-masing baris pada data test. Jadi, file akan terdiri dari 2500 baris berisi angka 0, 1 atau 2
  - README.md: dokumentasi dalam format Markdown, berisi langkah-langkah pemecahan masalah, penjelasan source code dan jawaban pertanyaan
  - File-file source code
- Jawablah pertanyaan berikut dan sertakan jawaban dalam file README.md:
  1. Algoritma machine learning apa yang anda gunakan?
  2. Apa alasan anda menggunakan algoritma tersebut?
  3. Variabel-variabel mana saja yang paling penting diantara (x_0, x_1, ..., x_19)?
  4. Apakah anda menemukan variabel yang collinear/redundant? Variabel mana sajakah itu?
  5. Metric apa sajakah yang anda gunakan untuk mengevaluasi performansi model? Berapa nilai dari tiap metric tersebut?



# B. Step of work

### 1. Import Train and Test Data from CSV

### 2. Check Train Data Information
After checking data training, we could get these informations :
- The columns is covered up, so we could not know what each column meaning for the others
- There is some nan value. We need to do data preprocessing, but since our columns is covered up, it is very hard to fill the nan value based on other features, then the numbers of nan values are not to much, so we will delete the rows that have nan value.
- From the df describe we could see which it looks like our data may have good distribution, we need to check it before make decission that we will not normalize this data.

### 3. Data Preprocessing

### 4. Exploratory Data Analysis (EDA)
#### 4.1 Pairplot
#### 4.2 Check Distribution
#### 4.3 Correlation & Heatmap
#### 4.4 Target value counts
After doing several exploratory data analysis, we could get some insight from our data which are :
- Our data is not linearly separable if we see in the form of 2D pairplot, but it may separable in more dimensions.
- The distribution for each feature is really good (normally distributed), I think we did not need to normalize or scale the data anymore.
- From the heatmap we could see that some features are well correlated with target, but there is feature that has high correlation each other which is like x_4 and x_2, it may answer the question about the redundant feature/variable.
- From the the countplot we could see that our target is balance, so we do not need doing over sampling method. And we could use accuracy metric for it.

### 5. Machine Learning
Since one of our task is to look the most important variable / feature for our machine learning classification, so I will not try to do PCA (Principal Component Analysis) or other feature engineering that will reduce the number of the features.
#### 5.1 Setting Features and Target
#### 5.2 Find The Best Algorithm
I use several algorithms for this classification, which are :
  - Logistic Regression
  - Decision Tree Classifier
  - Random Forest Classifier
  - LGBM Classifier
  - KNN
  - XGBoost
  
Objective : Find the best accuracy with cross_val_method. **using accuracy metric because of our data in balanced condition.**

Result : From the cross_validation result **the best algorithm for this classification is Light GBM.** So I will use this algorithm and try to tuning the hyperparameter.

#### 5.3 LightGBM Classifier without Tuning Hyperparameter
#### 5.4 Tuning Hyperparameter
From tuning result, it looks like the model has good better performance in precission and recall for all class than the model without tuning. And the accuracy is pretty good enough for dummy data. This accuracy value might be increased again if we know the meaning of each feature and do feature engineering. Or by adding more data before training model.
#### 5.5 Final LightGBM Model Evaluation
The information from evaluation :
  - Good classification report
  - From feature importances the top 5 important features are X_7 (17.7%), X_17 (14.6%), x_3 (9.7%), x_2 (8.8%), and x_4 (8.4%). The other features have score arround 2-3,5% for each of them.
  - It shows good roc curve with good roc score, that means the model is good.
 #### 5.6 Validate LightGBM Model
 It shows that the model has good stability when it validated with 5 Kfold. So, I decide to use this model for predicting test_data.csv
 
 ### 6. Prediction Test Data
 
 # C. Question Answer
 
 #### 1. Algorithm that I used ?
 I have tried 6 algorithm for classification, which are listed on step of work 5.2. Then for <b>the final model I use LightGBM Classifier</b>
 #### 2. The reason why using that algorithm ?
 Because after trying 6 Algorithms using cross_val method, <b>I have found that LightGBM is the best with accuracy score 81%.</b> The following below is the table of result cross_validation from several algorithms :
 
|Algorithm               | ACC  |
|------------------------|------|
|LogisticRegression      | 0.69 |
|DecisionTreeClassifier  | 0.73 |
|RandomForestClassifier  | 0.80 |
|LGBMClassifier          | 0.81	|
|KNeighborsClassifier    | 0.69 |
|XGBoost                 | 0.80 |

#### 3. Most important variable / features ?
The most important variable could we see in the step of work 5.5 (Model Evaluation). The top 5 important features that affect the prediction are :
  1. x_7 (17.7%)
  2. x_17 (14.6%)
  3. x_3 (9.7%)
  4. x_2 (8.8%)
  5. x_4 (8.4%)
  
The complete feature importances could we see in the following plot :
<center><img src="https://i.ibb.co/XyY6C65/Screen-Shot-2020-07-13-at-11-20-30.png"></center>

#### 4. Redundant Variable?
After checking the correlation at exploratory data analysis 4.3, I got insight about redundant variable. The result shows that there is feature that has high correlation each other which are **x_4 and x_2**

#### 5. What metric that I have used to evaluate / validate model? Score for every metric?
Because our data has balance target for each class, so I decide to use accuracy metric for find the best algorithm. Then to evaluate model I have used some metrics, which are :
1. Using classification report to look precission, recall, f1_score for each class. The result could we see in the following below :
```
=============== CLASSIFICATION REPORT ===============
              precision    recall  f1-score   support

         0.0       0.83      0.89      0.86       727
         1.0       0.89      0.75      0.82       751
         2.0       0.74      0.80      0.77       730

    accuracy                           0.81      2208
   macro avg       0.82      0.82      0.81      2208
weighted avg       0.82      0.81      0.81      2208
```
2. I'm also looking for ROC to look the quality of our model, and the result shows that the model is good. The following plot is the result from ROC :
<center><img src="https://i.ibb.co/bvhC9JT/Screen-Shot-2020-07-13-at-11-40-28.png"></center>

3. I'm also validate the model to check the model stability when using 5 KFold. In this validation I used accuracy and f1_score metrics. The following below is the result from accuracy and f1_score for each fold :
```
F1 Scores :  [0.81, 0.8, 0.82, 0.8, 0.81]

Accuracy Scores :  [0.81, 0.8, 0.82, 0.8, 0.81]
```


NB : The complete explanation and source code is available at the notebook.
