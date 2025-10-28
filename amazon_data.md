## Credit Card and Amazon Order Data Exploration

**Project description:** I used to keep all my receipts and track my spending in an Excel file manually, but I decided it was time to embrace the digital era and make use of Chase and Amazon storing my data. I downloaded my Amazon Order History (which goes all the way back to when I opened my account in 2013) and I downloaded the last few years of my credit card transaction data.


**Raw Data** Although the data from Amazon was more granular because it has every item listed, the data was not categorized making it difficult to summarize in a meaningful way.  The credit card data was the opposite.  Each observation was at the transaction level, lacking insight into items, but each transaction was labeled using the following categories: *Shopping, Groceries, Food & Drink, Home, Bills & Utilities, Professional Services, Automotive, Personal, Health & Wellness, and Gas*

My goal was to gain a better understanding of my Amazon spending habits in hopes of reducing spending.  I also wanted to categorize the orders using the same labels that my Chase credit card uses so that I can look at my spending as a whole picture.  Chase categorizes all Amazon purchases as "Shopping", but I buy a lot of groceries on Amazon so I want them categorized that way.  I manually labeled the data by looking at the item description, but I used this labeled data to train a Naive Bayes model so that I can run future order data through the model for automated labeling.

<img src="images/CCmonthly_dash.png?raw=true"/>

<img src="images/amazon_shopping2025.png?raw=true"/>



