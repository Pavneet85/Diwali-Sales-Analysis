
# Python Project For Data Analysis

## Project Overview: 

The goal of this project is to Analyze Diwali sales data to improve customer experience and sales using python libraries, dataframes and functions.
 
## Objectives: 

    a) Improve customer experience by analyzing sales data during holidays(Diwali).
    b) OSEMN Operations: Perform functions such as Obtain, Scrub, and Explore data to filter out important results.
    c) Increase revenue by making required changes on the basis of insights generated. 

### Tools Used: 
a) *Python 3.13:* computer programming language often used to build websites and software, automate tasks, and conduct data analysis.

b) *Jupyter Notebook:* allows you to run code, display the results, and add explanations, formulas, and charts all in one place. 

### Part 1: Importing Python Library Packages
A Python library is a collection of functions and methods that allow you to perform lots of actions without writing any code. The libraries usually contain built-in modules providing different functionalities which you can use directly. 
For example: 

    import pandas as pd
    import matplotlib.pyplot as plt
    %matplotlib inline
    import numpy as np
    import seaborn as sns

- Step 1 : Review the dataset which is available as csv files 

- Step 2: Use the read_csv method to import the data: 

      df = pd.read_csv('Diwali_Sales_Data.csv', encoding='unicode_escape'

encoding = 'unicode_escape' is used in encoding error cases when there is an error while loading the data. 

- Step 3: Now, in order to check and to ensure that everything occurred the way you expected, we will use the following codes rather than printing the entire dataset(which will consume a lot of time and resources):  

        df.shape For displaying the total count of rows and columns
        df.head(n) For first n rows
        df.head() For first 5 rows
        df.tail() For last 5 rows

Following is the screenshot of how the code is entered and the result is displayed on the Jupyter notebook - 

![PP1](https://github.com/user-attachments/assets/b6e8e91d-7881-4f43-9af4-d78504d09ebe)

- Step 4: We can preserve the progress of modified dataset at any time using the following export function -

      df.to_csv('DiwaliSalesData.csv', index = False)

### Part 2: Explore the dataset: 

a) Basic Insights -  data type, statistical summary of each column to learn about the distribution of data in each column

    df.dtypes  ## For checking the data types of the columns(for viewing and making modifications, if necessary)
    df.describe() ## For evaluating the statistical summary
    df.info() ## For concise summary of the data

b) Dropping the null/blank columns in the dataset - There are 2 columns in the dataset which are blank, and hence we need to delete/drop them for cleaning the data and analyzing it at a later stage. 

    df.drop(['Status', 'unnamed1'], axis=1, inplace=True)

axis = 1 is used to drop the entire column while inplace = True is applied for implementing the code in the same line only. 

c) Another data cleaning involves the checking of 'null' values in the dataset using: 

      pd.isnull(df).sum()
      or
      df.isnull().sum() 

There are 12 null values in the 'Amount' column, and we need to drop it for cleaning purpose. 

      df.dropna(inplace = True)
For rechecking, whether the null value rows are dropped, we can use the *df.isnull.sum()* function. 

d)  Correcting data types of columns(Change the data type of "Amount" column from float to int) - 

    df['Amount'].astype('int')

Followng is the screenshot of retesting the changed datatype of 'Amount' column using the desired code: 
![PP2](https://github.com/user-attachments/assets/43eafce4-e2f6-4106-b2f4-02506f7fdaac)

e) Evaluating the statistical data like percentile, mean and std of the numerical values of the Series or DataFrame -
    
    df.describe() For statistical data of all the numeric columns
    df[['Age', 'Orders', 'Amount']].describe() For statistical data of some columns


### Part 2: Exploratory Data Analysis:

f) Plotting a bar chart for Gender and it's count: 

    plt.figure(figsize=(10, 6))
    ax = sns.countplot(x = 'Gender', data = df, color='green')
    for bars in ax.containers:
      ax.bar_label(bars)
    plt.title('Gender vs Frequency')
    plt.show()

Following will be the graphical representation of above code - 

![PP3](https://github.com/user-attachments/assets/14697baa-0a31-41cc-96bb-94339fe16249)

g) Plotting a bar chart for gender vs total amount spent:

    sales_gen = df.groupby(['Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending= False)
    ax = sns.barplot(x='Gender', y='Amount', data=sales_gen, color='blue')
    for bars in ax.containers:
        ax.bar_label(bars)
    ax.set_title('Gender vs Amount')

![PP4](https://github.com/user-attachments/assets/198b7e68-3953-4906-8a1f-85d9fab01809)

h) Plotting a bar chart for Age Group and it's count: 

    ax=sns.countplot(x='Age Group', data=df, hue='Gender', order=["0-17", "18-25", "26-35", "36-45", "46-50", "51-55", "55+"])
    for bars in ax.containers:
        ax.bar_label(bars)
    ax.set_title('Age Group vs Count')


![PP5](https://github.com/user-attachments/assets/d2593d7d-a41f-47fe-9549-20eb5e205a4f)

i) Plotting a bar chart for Age Group vs total amount spent:

    sales_age = df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending= False)
    ax = sns.barplot(x='Age Group', y='Amount', data=sales_age, hue ='Age Group')
    ax.set_title('Age Group vs Amount')


![PP6](https://github.com/user-attachments/assets/a0bdaae0-107b-4bac-b140-34cc2b1f2b12)

j) Top 10 states with most amount spent using a bar chart: 

    plt.figure(figsize=(15, 5))
    sales_state = df.groupby(['State'], as_index = False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10)
    sns.barplot(data = sales_state, x = 'State',y= 'Amount', hue='State')
    ax.set_title('Top 10 States vs Total Amount')


![PP7](https://github.com/user-attachments/assets/91e7158d-0f58-492e-9861-bd20787eeb19)

k)  Top 10 states with most orders placed using a bar chart:

    plt.figure(figsize=(18,5))
    orders_state = df.groupby(['State'],as_index=False)['Orders'].sum().sort_values(by='Orders',ascending=False).head(10)
    ax = sns.barplot(data=orders_state, x='State', y='Orders', hue='State')
    ax.set_title('Top 10 States vs Orders') 


![PP8](https://github.com/user-attachments/assets/cd15568d-a4b0-4cb6-b427-ed3b9aa9f8ca)

l) Analysis w.r.t. Marital Status: 
    
    ax = sns.countplot(data=df, x='Marital_Status', hue ='Marital_Status')
    for bars in ax.containers:
        ax.bar_label(bars)


m) Marital Analysis of Genders w.r.t. Amount Spent: 

    sales_gen_ms = df.groupby(['Marital_Status', 'Gender'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False)
    ax = sns.barplot(data=sales_gen_ms, x='Marital_Status', y='Amount', hue='Gender')
    ax.set_title('Marital_Status of Genders vs Amount Spent')

![PP9](https://github.com/user-attachments/assets/6a34329f-5520-4249-b4ab-f44de393a571)

n) Analysis w.r.t. Occupation:

    plt.figure(figsize=(20,5))
    ax = sns.countplot(data = df, x = 'Occupation', hue='Occupation')
    for bars in ax.containers:
        ax.bar_label(bars)
    

o) Occupation Analysis w.r.t. Total Amount Spent:
  

    plt.figure(figsize=(20,5))
    sales_occ = df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False)
    ax = sns.barplot(data = sales_occ, x = 'Occupation',y= 'Amount', hue='Occupation')
    ax.set_title('Occupation vs Total Amount Spent')

![PP10](https://github.com/user-attachments/assets/29bea94f-bf50-4e71-940d-a75dd9b7f167)  

p) Analysis w.r.t. Product Category: 

    plt.figure(figsize=(25,5))
    ax = sns.countplot(data = df, x = 'Product_Category', hue='Product_Category')

    for bars in ax.containers:
        ax.bar_label(bars)

q) Top 10 Product Categories w.r.t. Total Amount Spent:

    plt.figure(figsize=(25,10))
    sales_pc = df.groupby(['Product_Category'],as_index=False)['Amount'].sum().sort_values(by='Amount',ascending=False).head(10)
    ax= sns.barplot(data=sales_pc, x='Product_Category', y='Amount', hue='Product_Category')
    ax.set_title('Top 10 Product Categories w.r.t. Amount Spent')

![PP11](https://github.com/user-attachments/assets/0df97c11-38b0-4402-8dd9-89d97f087648)

r) Analysis w.r.t. Product_ID:

    plt.figure(figsize=(20,5))
    sales_pro_ID = df.groupby(['Product_ID'],as_index=False)['Orders'].sum().sort_values(by='Orders',ascending=False).head(10)
    ax = sns.barplot(data = sales_pro_ID, x='Product_ID', y='Orders', hue='Product_ID')
    ax.set_title('Top 10 sold Products')

![pp12](https://github.com/user-attachments/assets/d1272ec7-6388-475f-be70-eec73cbc3969)


## Insights: 

1) Most of the buyers were females and even the purchasing power of females are greater than men which is quite evident from the Total Amount spent and the number of orders delivered w.r.t. Gender bar plot.

2) Females from the age group of 26-35 years placed the most number of orders(3269), thus making them the target customer for the sellers. 

3) Most of the orders & total sales amount were from Uttar Pradesh, Maharashtra and Karnataka respectively.

4) Buyers were majorly married (women) and they have high purchasing power as it is depicted in the bar plots.

5) Majority of the buyers were working in IT, Healthcare and Aviation sector respectively. 

6) Food, Clothing and Electronics category was the most popular among buyers. 

## Conclusion:
Married women age group 26-35 yrs from UP, Maharastra and Karnataka working in IT, Healthcare and Aviation are more likely to buy products from Food, Clothing and Electronics category. 
