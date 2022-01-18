# Titanic-Dataset
My submission for the Kaggle Titanic competition

Accuracy 78.47% - Top 17%

- Performed preprocessing on the dataset by parsing columns or creating new features
- Performed Exploratory Data Analysis
- Created Dummy variables for categorical features and tested several models
- Further tuned the models and created ensembles
- Submitted the results
- As this is one of my first Data Science projects, it is loosely based on this [video walkthrough](https://www.youtube.com/watch?v=I3FBJdiExcg&list=RDQMw8PLZ_0hYSc&index=8)


## Data preprocessing

- Created new columns:
  - Last Names of the passenger, to see if they can produce any insights
  - The title of each passenger (Mr., Miss., etc)
  - Total family members on board
  - Family (Boolean) to see if the person was part of a family or not
- Imputed missing values from Age column with the median
- Dropped rows which had missing values on the Embarked column


## Exploratory Data Analysis

- From a very basic analysis we can see that according to our subset:
  - 38.38% or just over one third of our passengers survived
  - The average age of the passengers was almost 30 years old and the median was 28 years old
  - The mean fare was 32.2$ but with a large deviation due to differences in class

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Correlation_matrix.png "Correlation Matrix")

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Numerical%20Pivot.png "Numerical Pivot")

- A Survivor was on average:
  - 28 years old
  - had less siblings/spouses on board than those who did not survived
  - had more parents/children on board than those who did not survived
  - paid a fare more than twice greater than those who did not make it

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Survived_Pclass.png "Survived_Pclass")

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Survived_Sex.png "Survived_Sex")

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Survived_Family.png "Survived_Family")

- We get that most Survivors were: 1st class passengers and females and were part of a family

## Model Building

- I tried 2 methods for getting dummy variables (OneHotEncoding and get_dummies method) and the get_dummies method performed significantly better

- The models I ran for this experiment and their performances were:
  - Naive Bayes (73.3%)
  - Logistic Regression (82.1%)
  - Decision Tree (78.3%)
  - K Nearest Neighbor (80.5%)
  - Random Forest (79.2%)
  - Support Vector Classifier (65.1%)
  - Xtreme Gradient Boosting (82.3%)
  - **Soft Voting Classifier - All Models (82.7%)**

- Also, I tried running the models with scaled and unscaled data

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Scaled.png "Scaled")

## Tuning the Models
- I tuned the models using GridsearchCV or RandomizedSearchCV and their performances improved across the board

![alt text](https://github.com/MarlinMyrte/Titanic-Dataset/blob/main/Tuned.png "Tuned")

- Created ensembles of the tuned models using VotingClassifier
  - Experimented with a hard voting classifier of the three best estimators (RF, SVC, XGB) (83.0%)
  - Experimented with a soft voting classifier of the three best estimators (RF, SVC, XGB) (82.2%)
  - Experimented with soft voting on all estimators (KNN, SVM, RF, LR, XGB) (83.1%)
  - Experimented with hard voting on all estimators (KNN, SVM, RF, LR, XGB) (83.2%)

- Soft voting on all tuned models had the best performance on the competition
