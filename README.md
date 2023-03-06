# Online Payment Fraud Detection

## Project Background

Applying machine learning models on a the e-commerce transactions dataset, which contains a wide range of features from device type to product features, to detect fraudulent transactions and improve the efficacy of alerts to reduce fraud loss as well as save the hassle of false positives.

![transaction](asset/payment.jpeg)
*Photo by <a href="https://unsplash.com/pt/@servuspaul?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Paul Felberbauer</a> on <a href="https://unsplash.com/photos/idNOBU5k_80?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>*

## Data Source & Description

The data comes from real-world e-commerce transactions, source: [IEEE-CIS Fraud Detection](https://www.kaggle.com/competitions/ieee-fraud-detection/data)
- Train Set: **590,540** transactions with **433** features
- Test Set: **506,691** transactions with **433** features
- Data Description:
  - TransactionDT: timedelta from a given reference datetime (not an actual timestamp)
  - TransactionAMT: transaction payment amount in USD
  - ProductCD: product code, the product for each transaction
  - card1 - card6: payment card information, such as card type, card category, issue bank, country, etc.
  - addr: address
  - dist: distance
  - P_ and (R__) emaildomain: purchaser and recipient email domain
  - C1-C14: counting, such as how many addresses are found to be associated with the payment card, etc. The actual meaning is masked.
  - D1-D15: timedelta, such as days between previous transaction, etc.
  - M1-M9: match, such as names on card and address, etc.
  - identity information – network connection information (IP, ISP, Proxy, etc) and digital signature (UA/browser/os/version, etc) associated with transactions.

## PART 1 - Data Wrangling & EDA

### Overall Target Variable(IsFraud) & Transaction Amount Distribution

- In the training dataset, there is ~3.5% fraud cases, which is a highly imbalanced datase
- Majority of the payment amount is less than 200, while even higher proportion of fruad transactions are within and around 100

Percentage of Fraudulent Transactions   |  Transaction Amount Distribution across Two Classes
:-------------------------:|:-------------------------:
![1](asset/target_distribution.png)  |  ![2](asset/transactionamt.png)


### Card Types 

- Majority payments are through **Visa** and **MasterCard**, accounts for **65%** and **32%** respectively, with roughly ~**3.5%** of fraudulent transactions, while **discover** has the highest percentage of fraud cases, which is close to 8%
- Over 74.5% of transactions are paid via **debit card**, while 25.2% are done with **credit card** which contains highest percentage(close to 7%) of fraudulent transactions

Transaction Distribution across Card Types
:-------------------------:
![3](asset/cardtype.png)  


### Email Domains

- Top purchaser email domains including gmail (46%), yahoo(20%), hotmail(9%) of the known transactions
- Among the top email domains, 'mail.com' with highest percentage of fraud cases ~20%, while 'outlook.com' contains ~10%

Transaction Distribution across Email Domains
:-------------------------:
![4](asset/email.png)  


### Counting Information
(such as how many addresses are found to be associated with the payment card)

Since the data for couting information is heavily right skewed, thus looking further into the higher quantile values, and it's interesting to find that for most of the columns, fraud class has much higher values and only columns `C4` & `C9` are opposite.

Quantiles for Counting Variables
:-------------------------:
![5](asset/countingcolumns.png)  


### Web - Browser Types
- Opera's percentage of fraudulent transactions is the highest among various categories with over 30%, while Chrome is the most popular web browser.

Transaction Distribution across Browser Types
:-------------------------:
![5](asset/browser.png)  


## PART 2 - Analysis & Modeling - TBC

- Applicated XGBoost and LGBM models to detect fraudulent transactions, after initial hyperparameter tuning, LGBM(AUC score: 0.94) performed better than XGBoost model(AUC score: 0.91).
- To further investigate hyperparameter influence and feature importance.

AUC Curve for Tree Based Models
:-------------------------:
![6](asset/roc_curve.png)  
