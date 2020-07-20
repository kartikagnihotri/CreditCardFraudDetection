# CreditCardFraudDetection
This project uses dataset which contains transactions made by credit cards. This dataset presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions to recognize whether a transaction is fraudulent or not so that customers are not charged for items they did not purchase. The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions.The dataset is obtained from Kaggle

It contains only numerical input variables which are the result of a PCA transformation. Due to confidentiality issues, we cannot provide the original features and more background information about the data.Features V1, V2, ... V28 are the principal components obtained with PCA, the only features which have not been transformed with PCA are 'Time' and 'Amount'. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount.Feature 'Class' is the target variable and it takes value 1 in case of fraud and 0 otherwise.

We import all the necessary libraries and then read the dataset using pandas.read_csv() library and get a look of the data using data.head().

In preprocessing part we check whether there are any missing values or categorical values that we need to convert to numerical data.
Using data.isnull().values.any() we see that there are no missing values also the data consists of only numerical values so we don't have to make any changes to the data.

Next, we check the count of normal and fraudulent transactions and plot a graph for it.
From the graph we can see that normal transactions are more than 250000 and fraudulent transactions are very less compared to that, thus we see that the data is very unbalanced.

Next, we Get the Fraud and the normal dataset by applying condition: 
fraud = data[data['Class']==1]
normal = data[data['Class']==0]

We analyze more amount of information from the transaction data such as how different are the amount of money used in different transaction classes?

We plot a graph for showing Amount of money used in different transaction classes i.e Normal vs Fraudulent transactions.From the graph we can see, the transaction amount is large for normal and small for fraud transactions.
 
Intead of taking the whole data we take just a sample of the data as the original data is very huge so it will take a lot of time.
data1= data.sample(frac = 0.1,random_state=1)
We can determine the fraction of data we want to use.

Next, we create independent and Dependent Features, X contains all the columns except "class" which is our target variable and Y contains the "class" variable.

We use Isolation Forest algorith and Local Outlier Factor(LOF) Algorithm for our data.
How Isolation Forests Work The Isolation Forest algorithm isolates observations by randomly selecting a feature and then randomly selecting a split value between the maximum and minimum values of the selected feature. The logic argument goes: isolating anomaly observations is easier because only a few conditions are needed to separate those cases from the normal observations. On the other hand, isolating normal observations require more conditions. Therefore, an anomaly score can be calculated as the number of conditions required to separate a given observation.
The way that the algorithm constructs the separation is by first creating isolation trees, or random decision trees. Then, the score is calculated as the path length to isolate the observation.

The LOF algorithm is an unsupervised outlier detection method which computes the local density deviation of a given data point with respect to its neighbors. It considers as outlier samples that have a substantially lower density than their neighbors.

The number of neighbors considered, (parameter n_neighbors) is typically chosen 1) greater than the minimum number of objects a cluster has to contain, so that other objects can be local outliers relative to this cluster, and 2) smaller than the maximum number of close by objects that can potentially be local outliers. In practice, such informations are generally not available, and taking n_neighbors=20 appears to work well in general.

Observations :
->Isolation Forest detected 73 errors versus Local Outlier Factor detecting 97 errors vs. SVM detecting 8516 errors
->Isolation Forest has a 99.74% more accurate than LOF of 99.65% and SVM of 70.09
->When comparing error precision & recall for 3 models , the Isolation Forest performed much better than the LOF as we can see that the detection of fraud cases is around 27 % versus LOF detection rate of just 2 % and SVM of 0%.
->So overall Isolation Forest Method performed much better in determining the fraud cases which is around 30%.
->We can also improve on this accuracy by increasing the sample size or use deep learning algorithms however at the cost of computational expense.We can also use complex anomaly detection models to get better accuracy in determining more fraudulent cases.

