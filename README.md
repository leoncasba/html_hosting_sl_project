# Supervised Learning Case: Predicting potential customers for a personal loan in a financial institution

Project made with R libraries. You can fin all the code here: https://leoncasba.github.io/predicting_potential_loan_customers/Predicting_potential_loan_cxs.html

# Business Understanding

## Case Statement

Loans represents the main income from banks, which comes from the loan’s interests. By this premise, banks definitely will be looking for prospective customers in order to encourage and persuade them to take a personal loan and consequently increase their income by the profitable interests.

Marketing efforts should be directed to those prospective customers likely to take the loan and that is the reason the analytics team from a financial institution would like to model and predict which new/passive customers are prospectives to become personal loan customers.

There is data from around 5000 customers from a past marketing campaign which had recent success. It was targeted to convert trusted passive customers to personal loan customers. This valuable asset (raw data) can be converted into a powerful tool to increase conversion rate success on the company.

Let’s find out how Data Science extracts the gold from the raw data.

## Objective

The objective of this analysis is to model the characteristics of the clients of the previous campaign in order to analyze what combination of factors make a client more likely to accept a personal loan. By modeling this factors we will construct a model able to predict if new customers are prospective/have higher probability to get a personal loan.

## Business Benefit

To help Business Development and Marketing Teams to create product & marketing strategies targeted to those prospective customers more likely to become personal loan customers and ensure its efforts and resources are going to be spent on the right people. Consequently, we expect more revenue coming from loan’s interests making more profitable the business.

## Scope

This analysis parts from the hypothesis that all the customers being analyzed are trusted customers, for hence, eligible customers to get a loan. I am not analyzing whether the customers are good or bad payers.

Also I want to clarify all the insights come strictly from the data and not from subjective opinion. However, we should have opinion from a Subject Matter Expert (SME) to get better understanding of some policies or rules on loan and fin-tech business.

## Key Business Questions

  * How are characterized the personal loan customers?
  * What is the most important variable/s which defines if a customer will get a loan customer?
  * What is the expected accuracy of the model to be developed? Will it predict correctly?
 
## Expected Outcomes

  * To obtain an accurate model which can predict prospective customers likely to get a personal loan.
  * To know which variables or characteristics are the most important to know in order to convert a new customer into a personal loan customer.

# Methodology & Analytics Techniques Used

  * Data understanding
  * Data cleaning and preparation.
  * Exploratory data analysis.
  * Data splitting (training/test).
  * Machine Learning Classification Models:
    * Logistic Regression.
    * Classification Trees.
    * Random Forest.
    * K-Nearest Neighbors.

##  Data Understanding

  * Data consists in customers’ personal information from a financial institution.
  * Data was directly downloaded from a GitHub repository. You can find it here.
  * The dat aset has 14 columns and 5000 rows.
  * Data dictionary:
    * ID: customer id.
    * Age: customer’s age in completed years.
    * Experience: number of years of professional experience.
    * Income: annual customer earnings ($ thousands).
    * ZIP.Code: customer’s address zip code.
    * Family: family size.
    * CCAvg: average credit card spend per month ($ thousands).
    * Education: Level of studies, 1= Undergraduate, 2= Graduate, 3= Advanced/Professional.
    * Mortgage: mortgage value of the house.
    * Personal.Loan: coded with 1 if the client has accepted the personal loan from the bank in the previous campaign. This variable is going to be the predictor/dependent variable.
    * Securities.Account: coded with 1 if the client has a security account with the bank.
    * CD.Account: coded with 1 if the client has a certificate of deposit (CD) with the bank.
    * Online: coded 1 if the client has online services with the bank.
    * CreditCard: coded 1 if the customer uses has at least one credit card with the bank.
 
## Data Cleaning and Preparation.

Findings and actions:

  * There are not missing values on the database.
  * I found an error on variable Experience, which corresponds to value -3. This value is incorrect as the minimum value for the variable Experience has to be 0 as there are not negative years of experience. Probably is a data entry error, so I proceeded replacing for a 0.
  * There are two variables not suitable for the analysis: ID and ZIP.Code. I proceed eliminating them.
  * Categorical variables have been read as numerical, so I proceed converting them to factor, as we need it for the further steps.

## Exploratory Data Analysis

  * Do the customers who accepted the personal loan have more services in the same bank as Security Account, Certificate of Deposit, Online Services, Credit Card?
 
More than 50% of loan customers have Online Services, which is a good place where to target and promote personal loans. Around 25% have certificate of Deposit and Credit Cards. Around 12% have a Security Account.

![image](https://user-images.githubusercontent.com/73316046/159059098-d6718308-deff-4d04-8dc2-4b143dfacc1a.png)

* How are the salaries distributed? Is there any difference regarding the education? Are differences on the customers who accepted/rejected the loan?

It seems customers with higher salaries tend to get the loan, independently of the education level. Figure also shows there’s a gap of salary on undergraduate customers, where there is people which earns more than /$200k per year and in the other hand, people who earn around $10k per year. This quick insight let us have the hypothesis that income will be one of the most important variables to define the model.

![image](https://user-images.githubusercontent.com/73316046/159059202-e84dbb9f-0e04-4cb6-a9fe-0dcacf087aac.png)

  * What is the size of families? How are the frequencies per family group size?

It seems like there is a slight difference between the family size groups on those customers who accepted the loan. It may not be an important variable to consider on the models, however, is just a hypothesis we will definitely confirm on further steps.

![image](https://user-images.githubusercontent.com/73316046/159059292-165cb738-73fd-416e-86ce-a590ce7b6065.png)

  * What is the average credit card spent per month on personal loan customers?
 
 As we can see on the density plot, most of the loan customers spent around $ 2500 and $ 5000 dollars in credit card. This can be a really useful information at the time of setting the loan amounts to offer to the clients.
  
  ![image](https://user-images.githubusercontent.com/73316046/159059421-6b61b311-c904-458c-84b9-37ada23ae100.png)

## Data splitting (Train and Test)

In order to evaluate the accuracy of the classification models, the data must be partitioned into training and test data sets. The training partition is used to build the model, and the test partition is used to see how well the model performs when applied to new data and measure its error. For the partition, we will take 70% of the data for training and 30% for testing.

## Classification Models

## Linear Regression

  * Logistic regression works very similar to linear regression, but with a binomial response variable. Instead of fitting a straight line or hyperplane, the logistic regression model uses the logistic function to squeeze the output of a linear equation between 0 and 1.
  * When first model trained, I had to eliminate variables that were not significant (p-value > 0.05): age, experience, mortgage and securities account. Also I tried interactions between income and family, and income and ccavg.
  * Finak variables in LR model were: Income, Family, CCAvg, Education, CD.Account, Online, CreditCard, Income * Family and Income * CCAvg.
  * Below the resulting confusion matrix obtained:

![image](https://user-images.githubusercontent.com/73316046/159061869-b0a13f42-ae8b-4002-96dd-f7df81e3cc34.png)

## Decision Tree

  * Decision tree is one of the simplest and more understandable predictive modelling approaches used for classification. It builds classification or regression models in the form of a tree structure by breaking down a data set into smaller and smaller subsets while at the same time an associated decision tree is incrementally developed. 
  * The final result is a tree with decision nodes and leaf nodes. A decision node has two or more branches and the leaf node represents a classification or decision. The topmost decision node in a tree which corresponds to the best predictor called root node.
 * As one common problem with Decision trees, is that they tend to over fit. Sometimes it looks like the tree memorized the training data set, it this affects the accuracy when predicting samples that are not part of the training set. In order to avoid overfitting we prune the tree, pruning is the process of reducing the size of the tree by turning some branch nodes into leaf nodes, and removing the leaf nodes under the original branch.
 * Here is the pruned decision tree structure:

![image](https://user-images.githubusercontent.com/73316046/159062296-5402bba5-0050-4416-8ba6-37e2b80f9968.png)

  * The resulting confusion matrix below.
 
 ![image](https://user-images.githubusercontent.com/73316046/159062405-82afc61b-2c2e-4e19-9545-fa2cfb09501f.png)

## Random Forest

  * The power of this algorithm comes from a collection of smaller and simple trees that together reflect the data’s complexity. Each of the forest’s trees is diverse and may reflect subtle patterns in the outcome to be modeled. Generating this diversity is the key to building powerful decision tree forests.
  * The algorithm allocate to each tree a random subset of the data, one may receive a vastly different training set than another, that is known as the bagging ensemble method.
  * Now we can see how important is each variable in classifying the data modeling the Random Forest algorithm by the Mean Decrease Accuracy and Mean Decrease in Gini Coefficient Metrics

![image](https://user-images.githubusercontent.com/73316046/159062895-737ff1ee-56f3-46d4-93d1-e5d1b6169be5.png)

  * The resulting confusion matrix below.

![image](https://user-images.githubusercontent.com/73316046/159062990-8895d578-62bc-4a3d-997f-77d7d0ce00fa.png)

## K-Nearest Neighbor

  * K-NN algorithm predicts the correct class for the test data by calculating the distance between the test data and all the training points, then selects the K number of points which is closest to the test data.
  * The K-NN algorithm calculates the probability of the test data belonging to the classes of ‘K’ training data and class holds the highest probability will be selected. In the case of regression, the value is the mean of the ‘K’ selected training points.
  * The k variable specifies the number of neighbors to consider when making the classification, for hence, choosing the k value is very critical. A really small value of k means that noise will have a higher influence on the result and large value make it computationally expensive and kinda defeats the basic philosophy behind KNN (that points that are near might have similar densities or classes).
  * There is not an universal rule to select k, however, a simple approach to select k is set k = n^(1/2), being n the number of variables we are classifying.
  * Below you can fin the confusion matrix.

![image](https://user-images.githubusercontent.com/73316046/159063631-6b8c4b49-98ad-4ef0-aa70-6c1c94fdcf5c.png)

# Evaluation and Selection of Best Model

![image](![image](https://user-images.githubusercontent.com/73316046/160277944-95997054-eb17-4919-810d-9c98f85cde18.png)

![image](https://user-images.githubusercontent.com/73316046/159060356-8c66c959-7987-46be-bd67-b780f8aa5a35.png)
![image](https://user-images.githubusercontent.com/73316046/159060409-f0295e74-bc40-4d5c-a485-bb0cca4ed035.png)

First we notice the performance of K-NN does not seems really appropriate, despite has good specificity and accuracy metrics (but lower than the other models), sensibility has a poor value for our expectations. We notice Random Forest and Decision Tree’s accuracy are the best compared with the other models. Checking the ROC curve it seems like the Logistic Regression has the best performance fit by evaluating the AUC (0.9). However, as we follow the rule to look for a model with a good sensibility metric keeping in mind the reasoning mentioned previously above, the sensibility performance in Logistic Regression is not good for our business purposes.

Finally the election would be between Random Forest and Decision Tree models..

In this case I select Decision Tree as the best model to deploy. The reasoning behind is not only it has a better sensibility score, this model is also very intuitive and easy to explain to technical teams as well as stakeholders. Moreover, this model is really useful for business strategy, especially where transparency is needed, and as we are developing a solution for a financial institution it seems like a great choice because it allows to visualize through its structure how the decisions are being made.

# Conclusions and Recomendations

  * Model choose to deploy is Decision Tree. It has an accuracy of 97.8% and AUC=0.93, that means it predicts in valid and trustful way for our purposes.
  
  * The most important variables which defines if a customer is more likely to get a personal loan are: Income, Education, Family size and Average Credit Card Monthly Spent.
  
  * Our **ideal candidate** and for hence the one Business Development and Marketing Teams should focus are customers who has a salary around 80-200k$ per year, is graduate or advanced/professional, has a family size equal or +3 people, and spend around 2.5-5k$ monthly on credit cards.
