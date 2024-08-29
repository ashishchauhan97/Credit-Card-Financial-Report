# Credit-Card-Financial-Report
#Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.
#Import data to SQL database
1. Prepare csv file
2. Create tables in SQL
3. import csv file into SQL

#DAX Queries

AgeGroup = SWITCH(
TRUE(),
'ccdb cust_detail'[customer_age] < 30, "20-30",
'ccdb cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
'ccdb cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
'ccdb cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
'ccdb cust_detail'[customer_age] >= 60, "60+",
"unknown"
)


IncomeGroup = SWITCH(
TRUE(),
'ccdb cust_detail'[income] < 35000, "Low",
'ccdb cust_detail'[income] >= 35000 && 'ccdb cust_detail'[income] <70000, "Med",
'ccdb cust_detail'[income] >= 70000, "High",
"unknown"
)


#DAX Queries

week_num2 = WEEKNUM('public cc_detail'[week_start_date])

Revenue = 'ccdb cc_detail'[annual_fees] + 'ccdb cc_detail'[total_trans_amt] + 'ccdb cc_detail'[interest_earned]

Current_week_Reveneue = CALCULATE(
SUM('ccdb cc_detail'[Revenue]),
FILTER(
ALL('ccdb cc_detail'),
'ccdb cc_detail'[week_num2] = MAX('ccdb cc_detail'[week_num2])))

Previous_week_Reveneue = CALCULATE(
SUM('ccdb cc_detail'[Revenue]),
FILTER(
ALL('ccdb cc_detail'),
'ccdb cc_detail'[week_num2] = MAX('ccdb cc_detail'[week_num2])-1))

#Project Insights- Week 53 (31st Dec)
WoW change :

• Revenue increased by 28.8%

• Total Transaction amount increased by 35%

• Customer count increased by 28.31%

Overview YTD :

• Overall revenue is 57M

• Total interest is 8M

• Total transaction amount is 46M

• Male customers are contributing more in revenue 31M, female 26M

• Blue & Silver credit card are contributing to 93% of overall transactions

• TX, NY & CA is contributing to 73%

• Overall Activation rate is 57.5%
