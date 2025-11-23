💳 Credit Card Transaction and Customer Analysis🚀 Project OverviewThis repository contains data and analysis related to credit card transactions and customer demographics. The primary goal is to provide insights into card usage, customer behavior, and financial metrics such as utilization ratio, total transaction amount, and interest earned.The project is structured around two main datasets, which can be linked using the common identifier, Client_Num.📂 Data FilesThe analysis is built upon four primary CSV files, which were designed to be imported into a PostgreSQL database.Transaction Data (Credit Card Details)File NameDescriptionKey Columnscredit_card.csvMain credit card transaction and account details.Client_Num, Card_Category, Credit_Limit, Total_Trans_Amt, Interest_Earnedcc_add.csvAdditional/supplementary credit card data.Client_Num, Exp Type, Annual_Fees, Avg_Utilization_RatioCustomer Data (Demographics)File NameDescriptionKey Columnscustomer.csvMain customer demographic and financial details.Client_Num, Customer_Age, Income, Education_Level, Marital_Statuscust_add.csvAdditional/supplementary customer data.Client_Num, Car_Owner, House_Owner, Personal_loan, Cust_Satisfaction_Score🛠️ Database Schema (PostgreSQL)The uploaded file (credit card record.....txt) indicates the data was prepared for a PostgreSQL environment, defining two tables: cc_detail and cust_detail.cc_detail (Credit Card Details)This table focuses on the transactional and account-specific details.Column NameData TypeDescriptionClient_NumINTPrimary Join Key (Unique Customer Identifier)Card_CategoryVARCHAR(20)Type of credit card (e.g., Blue, Silver)Annual_FeesINTAnnual fee amountCredit_LimitDECIMAL(10,2)Maximum credit allowedTotal_Trans_AmtINTTotal value of transactionsExp_TypeVARCHAR(50)Category of expense (e.g., Travel, Food, Bills)Interest_EarnedDECIMAL(10,3)Total interest earned on the accountDelinquent_AccVARCHAR(5)Indicates if the account is delinquentcust_detail (Customer Details)This table contains customer demographic information.Column NameData TypeDescriptionClient_NumINTPrimary Join Key (Unique Customer Identifier)Customer_AgeINTAge of the customerGenderVARCHAR(5)Customer's genderEducation_LevelVARCHAR(50)Customer's education statusMarital_StatusVARCHAR(20)Customer's marital statusIncomeINTCustomer's annual incomeCust_Satisfaction_ScoreINTCustomer satisfaction rating💻 UsageData Loading (PostgreSQL Example)The following schema creation and data loading commands were suggested in the uploaded text file.Create Tables:SQLCREATE TABLE cc_detail (
    Client_Num INT,
    -- ... other columns
);

CREATE TABLE cust_detail (
    Client_Num INT,
    -- ... other columns
);
Load Data: (Adjust the file path as necessary for your local environment)SQLCOPY cc_detail
FROM 'D:\credit_card1.csv' -- Replace with credit_card.csv or cc_add.csv path
DELIMITER ','
CSV HEADER;

COPY cust_detail
FROM 'D:\customer.csv' -- Replace with customer.csv or cust_add.csv path
DELIMITER ','
CSV HEADER;
Performing AnalysisOnce the data is loaded into the tables (cc_detail and cust_detail), you can perform various SQL queries to gain insights:Joining Data: Join the two tables using Client_Num to analyze transaction habits by demographic.SQLSELECT 
    t1."Card_Category", 
    t2."Gender", 
    AVG(t1."Total_Trans_Amt") AS avg_transaction
FROM 
    cc_detail t1
JOIN 
    cust_detail t2 
ON 
    t1."Client_Num" = t2."Client_Num"
GROUP BY 
    1, 2;
Top Expenses: Find which expense types (Exp_Type) generate the most total transactions.Risk Analysis: Analyze the profile of customers with a high Avg_Utilization_Ratio or those who are Delinquent_Acc.🖼️ Reports and VisualizationsThe images included in this repository (e.g., Credit_Card_Customer_Report_Picture.jpg, Credit_Card_Transaction_Report_picture.jpg) are visual summaries of the key findings derived from this data.
