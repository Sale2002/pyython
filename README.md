# **[Python] RFM Analysis**
# **I. Introduction**
## 1.1. Project Overview: 
This project aims to assist SuperStore, a global **retail company**, in launching **effective marketing campaigns** for the Christmas and New Year's seasons. The primary goal is to **express appreciation to existing customers and identify potential loyal customers** for personalized engagement. By applying **RFM** (Recency, Frequency, Monetary) analysis, the project seeks to **segment the large customer base**, enabling the development of **targeted marketing strategies** and **customized customer care programs**. This approach helps SuperStore **increase ROI,** **reduce customer churn, optimize marketing expenses, and improve customer relationships**.

In this project, the following libraries were utilized for data analysis:
* pandas
* numpy
* datetime
* matplotlib
* seaborn
* squarify

## 1.2. Business Problem: 
SuperStore needs to identify **key customer segments** to focus their marketing resources on the right groups, ensuring more effective outreach and personalized customer engagement during the holiday seasons. This involves determining which customers are most loyal, most active, and most profitable, allowing the business to allocate resources efficiently and improve customer satisfaction.

## 1.3 Solution Approach: 
The **RFM analysis model** is employed, which segments customers based on three factors:

* **Recency:** How recently a customer made a purchase.
* **Frequency:** How often the customer has made purchases.
* **Monetary:** How much the customer has spent overall.

By scoring customers on these dimensions, the company can create **meaningful customer segments**, such as high-value, inactive, or recent customers, and tailor marketing strategies for each segment.

**Reference:** [RFM analysis](https://www.putler.com/rfm-analysis)
# II. Data Exploration & Data Processing
## 2.1. Data Information
This is a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.
* InvoiceNo: Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'C', it indicates a cancellation.
* StockCode: Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.
* Description: Product (item) name. Nominal.
* Quantity: The quantities of each product (item) per transaction. Numeric.
* InvoiceDate: Invoice Date and time. Numeric, the day and time when each transaction was generated.
* UnitPrice: Unit price. Numeric, Product price per unit in sterling.
* CustomerID: Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer.
* Country: Country name. Nominal, the name of the country where each customer resides.
## 2.2. Data Exploration & Data Processing
**Each Step of Data Exploration and Processing:**
* **Step 1:** Data Preparation: The dataset was loaded and underwent a cleaning process to eliminate missing values and duplicates. Additionally, necessary columns were converted to the appropriate data types (e.g., conversion of InvoiceDate to datetime format).

* **Step 2:** Transaction Segmentation: The data was filtered to distinguish between cancelled transactions (negative quantities) and successful ones. The total revenue was calculated for both categories.

* **Step 3:** Data Aggregation: Transactions were grouped by CustomerID to compute key metrics, including total revenue (Monetary), the number of purchases (Frequency), and the date of the most recent purchase (Recency).

* **Step 4:** RFM Metric Calculation: The RFM metrics were calculated for each customer:

  * _Recency:_ The number of days since the last purchase.
  * _Frequency:_ The total number of transactions.
  * _Monetary:_ The total amount spent.

* **Step 5:** RFM Scoring: Customers were assigned RFM scores based on the distribution of their RFM values using quantiles (e.g., a 1–5 scale).

* **Step 6:** Customer Segmentation: The RFM scores were combined to classify customers into distinct segments (e.g., top customers, at-risk customers, and new customers).

 To view the steps for executing the aforementioned process, please refer to the: [Appendix 1](#appendix_1)
# III. Data Visualization
![image](https://github.com/user-attachments/assets/f9cf82bf-7fa1-46bc-8707-1041dde8d129)

**Function Used:**

* _plt.subplots():_ Creates a subplot for each RFM variable.
* _sns.distplot():_ Plots the distribution of each RFM variable.

**Purpose:** To visualize the distribution of Recency, Frequency, and Monetary values across customers.

**Result:**
![image](https://github.com/user-attachments/assets/75d53551-ea52-4779-a54c-708a797ced9a)

=> **Insight:** The customer purchase distribution is right-skewed, indicating many recent purchases and fewer customers who have not bought anything for a long time. The peak occurs in the 0-50 day range, suggesting that many customers make repeat purchases within this timeframe. The longer tail on the right indicates some customers have not purchased in a while, signaling they may be less engaged or at risk of being lost.

![image](https://github.com/user-attachments/assets/69029c34-39ae-4a02-b928-f3a16ee7369f)

=> **Insight:** The customer transaction distribution is right-skewed, indicating that many customers have made only a few transactions, while a few have made significantly more. The peak is in the 0-10 range, showing that a substantial portion of customers has completed only a few transactions. The longer right tail indicates the presence of high-value or repeat customers. 

![image](https://github.com/user-attachments/assets/b298101c-7e4c-4eaa-866a-9458fb73ce3c)

=> **Insight:** The distribution of customer spending is right-skewed, similar to the recency and frequency distributions, indicating that many customers have made relatively small expenditures, while a few have spent significantly larger amounts. The peak occurs in the 0-50,000 range, suggesting that a substantial portion of customers has relatively low total spending. The longer right tail highlights the presence of high-value or VIP customers who have made large expenditures. 

**Preprocess the data before performing visualization:** [Appendix 2](#appendix_2)

![image](https://github.com/user-attachments/assets/257da369-8947-4eb4-a2ea-b5d64735f434)

![image](https://github.com/user-attachments/assets/1e68ba97-1fa9-4001-b81d-e16882e946d5)

# IV. Recommendation

| Segment                | Characteristics                                                                              | Recommendation                                                                                                   |
|------------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Champions**          | Bought recently, buy often and spend the most!                                            | Reward them. Can be early adopters for new products. Will promote your brand.                                  |
| **Loyal**              | Spend good money with us often. Responsive to promotions.                                  | Upsell higher value products. Ask for reviews. Engage them.                                                   |
| **Potential Loyalist** | Recent customers, but spent a good amount and bought more than once.                      | Offer membership/loyalty program, recommend other products.                                                    |
| **New customers**      | Bought most recently, but not often.                                                      | Provide on-boarding support, give them early success, start building a relationship.                          |
| **Promising**          | Recent shoppers, but haven’t spent much.                                                  | Create brand awareness, offer free trials.                                                                       |
| **Need attention**     | Above average recency, frequency and monetary values. May not have bought very recently.   | Make limited-time offers, recommend based on past purchases. Reactivate them.                                   |
| **About to sleep**     | Below average recency, frequency and monetary values. Will lose them if not reactivated.   | Share valuable resources, recommend popular products/renewals at discount, reconnect with them.                |
| **At risk**            | Spent big money and purchased often, but a long time ago. Need to bring them back!        | Send personalized emails to reconnect, offer renewals, provide helpful resources.                               |
| **Cannot lose them**   | Made biggest purchases, and often, but haven’t returned for a long time.                   | Win them back via renewals or newer products, don’t lose them to competition, talk to them.                    |
| **Hibernating customers** | Last purchase was long back, low spenders and low number of orders.                    | Offer other relevant products and special discounts. Recreate brand value.                                     |
| **Lost customers**     | Lowest recency, frequency and monetary scores.                                            | Revive interest with a reach-out campaign, ignore otherwise.                                                  |

# Appendix_1
## 1. Data Exploration 
### 1.1. Loading and Initial Data Inspection:
![image](https://github.com/user-attachments/assets/138031db-776e-483b-ac83-a41c23e59d67)
![image](https://github.com/user-attachments/assets/8576331f-f384-4657-b65f-abbfef9417aa)
![image](https://github.com/user-attachments/assets/aa68be79-a282-4b7d-8f9b-3604e533bb05)
![image](https://github.com/user-attachments/assets/bda0fdb9-c545-42bf-8117-0f721a85674d)


**Function Used:**
* _pd.read_excel():_ Loads the data from an Excel file.
* _data.head():_ Displays the first five rows of the dataframe.
* _data.info():_ Provides information about the dataframe (data types, non-null counts).
* _data.shape:_ Returns the dimensions of the dataframe (rows, columns).

**Purpose:** To load and inspect the dataset structure before manipulation.
### 1.2. Data Cleaning:
After reviewing the data, we observed that a significant portion of the data **contained null values**. Therefore, we have decided on the following approach: given the available data and context, it is not feasible to impute values for approximately 140,000 rows where the CustomerID is null. As a result, we will **delete these rows** from the dataframe. Additionally, **duplicate rows will be removed** in this step as well.

![image](https://github.com/user-attachments/assets/ea5a87ad-cb2f-47cc-90b2-a2e672aee960)

**Function Used:**

* _dropna():_ Removes rows with missing values in the CustomerID column.
* _drop_duplicates():_ Removes duplicate rows.

**Purpose:** To clean the dataset by removing invalid or redundant rows.
### 1.3. Converting Data Types:
Convert some columns to the potentially correct data type

![image](https://github.com/user-attachments/assets/6571b9ad-f4ba-4a9f-948c-5aebf1fa5acc)

**Function Used:**

* _pd.to_datetime():_ Converts the InvoiceDate column to datetime format.
* _astype():_ Changes the data type of CustomerID to object.

**Purpose:** Ensures the correct data types for analysis.
## 2. Data Processing
### 2.1. Handling Cancellations:

![image](https://github.com/user-attachments/assets/2a255b8b-de92-4650-acf6-e2cc67ae59b8)
![image](https://github.com/user-attachments/assets/4e66e3ef-d02f-402a-9d28-08defa8a8624)

**Function Used:**

* _Filtering:_ data[data['Quantity'] < 0] filters out transactions where Quantity is negative (indicating cancellations).
* _Multiplication:_ Calculates the loss for canceled transactions (Quantity × UnitPrice).

**Purpose:** To isolate and calculate the loss from canceled transactions.
### 2.2. Aggregating Canceled Transactions:

![image](https://github.com/user-attachments/assets/18486b97-6f68-40b5-b8f9-29378e55a007)
![image](https://github.com/user-attachments/assets/5f0e80e7-cadc-4bc4-b68f-604bc7390db8)


**Function Used:**

* _groupby():_ Groups the data by InvoiceNo, Country, and CustomerID.
* _agg():_ Aggregates the grouped data by taking the maximum InvoiceDate and summing the Loss.
* _reset_index():_ Resets the index after the aggregation.

**Purpose:** To summarize canceled transactions by invoice and customer.
### 2.3. Handling Delivered Transactions:

![image](https://github.com/user-attachments/assets/66cf604e-7060-43a0-96af-7c86a2709264)

![image](https://github.com/user-attachments/assets/605f5def-4f18-43bb-942c-0a6884d2f112)

**Function Used:**

* _Filtering:_ data[data['Quantity'] >= 0] filters out transactions where Quantity is non-negative.
* _Multiplication:_ Calculates the revenue for delivered transactions (Quantity × UnitPrice).

**Purpose:** To isolate and calculate the revenue from delivered transactions.

### 2.4. Aggregating Delivered Transactions:

![image](https://github.com/user-attachments/assets/4531e4c5-ac14-4acf-a40a-d33c9408f1cd)
![image](https://github.com/user-attachments/assets/5522d653-6b4a-4e4a-a8c4-40a6d601aacc)

**Function Used:**

* _groupby():_ Groups the data by InvoiceNo, Country, and CustomerID.
* _agg():_ Aggregates the grouped data by taking the maximum InvoiceDate and summing the Revenue.
* _reset_index():_ Resets the index after the aggregation.

**Purpose:** To summarize delivered transactions by invoice and customer.
### 2.5. Percentage of Cancelled Transactions:
![image](https://github.com/user-attachments/assets/53604f98-bf72-4978-a8a6-82a098a5fa0a)

* _agg_cancelled.shape[0]:_ Counts the number of cancelled transactions (rows where Quantity < 0).
* _agg_delivered.shape[0]:_ Counts the number of delivered transactions (rows where Quantity >= 0).
* _The formula_ (agg_cancelled.shape[0] * 100 / (agg_cancelled.shape[0] + agg_delivered.shape[0])) calculates the percentage of cancelled transactions by dividing the number of cancelled transactions by the total number of transactions (cancelled + delivered) and multiplying by 100.

**=>** _A high cancellation rate may point to problems in operations, product quality, or customer satisfaction, signaling areas that need immediate attention to prevent revenue loss and improve customer retention._

### 2.6. Calculating RFM Metrics (Recency, Frequency, Monetary):
![image](https://github.com/user-attachments/assets/2ccf5c21-d4c8-4b10-a080-f5e740392a06)

**Function Used:**
* _Recency:_ The number of days since the customer's last purchase.
* _Frequency:_ The total number of purchases by the customer.
* _Monetary:_ The total revenue generated by the customer.
* _The Recency value is calculated by subtracting the last purchase date from a fixed "current date" (today)_.

**Purpose:**  Group transactions by CustomerID to compute the three key metrics—Recency, Frequency, and Monetary (RFM).

### 2.7. RFM Score Calculation:
![image](https://github.com/user-attachments/assets/6b8321d5-384c-4bff-8285-6d86fed08fb4)
![image](https://github.com/user-attachments/assets/d174e1fa-761a-4373-8aeb-62a97270ab6c)

**Function Used:**
* _pd.qcut():_ Divides the Recency, Frequency, and Monetary values into quantiles (with 5 groups here).
* _rank():_ Ranks the Frequency before quantile assignment.

**Purpose:** To assign scores (1-5) to each customer for Recency, Frequency, and Monetary, based on their relative values.
### 2.8. Creating RFM Combined Score:
![image](https://github.com/user-attachments/assets/d15cd6b1-a6a7-433f-9193-1ff83799c391)
![image](https://github.com/user-attachments/assets/de78dab2-4b7e-4574-99e8-ef5e70a091cf)

**Function Used:**

* _astype():_ Converts the scores to string, concatenates them, and converts the result back to integer.

**Purpose:** To create a combined RFM score for each customer by joining their individual Recency, Frequency, and Monetary scores.
### 2.9. Merging with Segmentation Data:
![image](https://github.com/user-attachments/assets/714b5c6e-6ec6-4c1c-9e56-e2e8d5bc1e7b)
![image](https://github.com/user-attachments/assets/6f3aabd0-b310-4cbf-a554-7df48f34ea65)
![image](https://github.com/user-attachments/assets/00868004-8343-435c-939b-bff5d8ff4f69)
![image](https://github.com/user-attachments/assets/d059c3f0-4f56-417b-92a6-6829b3d14b08)

**Function Used:**

* _pd.read_excel():_ Reads the segmentation data from another sheet in the Excel file.
* _str.split():_ Splits the comma-separated RFM scores into a list.
* _explode():_ Expands list-like elements into separate rows.
* _astype():_ Converts RFM scores to integer.

**Purpose:** To process the segmentation data and prepare it for merging with the RFM analysis results.
 ### 2.10. Final Merge of RFM and Segmentation:
![image](https://github.com/user-attachments/assets/2821b00d-e3a8-477c-bc74-14bb5900e26d)

**Function Used:**

* _merge():_ Joins the RFM analysis data with the segmentation data on the RFM_Score column.

**Purpose:** To associate each customer with their respective segment based on the combined RFM score.

# Appendix_2
![image](https://github.com/user-attachments/assets/9e62f71a-2666-4591-88f4-1bca8f7db739)
![image](https://github.com/user-attachments/assets/6265a74e-03e4-4215-9cc5-6d47748235d8)

**Purpose:** This aggregation step provides a clear overview of customer segments by summarizing essential metrics. It allows businesses to evaluate customer engagement, profitability, and retention strategies effectively.

![image](https://github.com/user-attachments/assets/aa78224c-f913-4961-9ded-5a6c1802748e)

**Purpose:** Calculating these shares enables businesses to identify and prioritize customer segments based on their size and revenue contribution. 

**Visualization:**
_Code:_
![image](https://github.com/user-attachments/assets/3e5a4ebf-1526-4dd2-913a-6f5912e6d09b)

_Result:_
![image](https://github.com/user-attachments/assets/cf1c7ae3-75be-40da-ad90-5c8cfab509d0)

_Code:_
![image](https://github.com/user-attachments/assets/fac8803f-03c0-4faa-b08c-db0c2bb5e3c1)

_Result:_
![image](https://github.com/user-attachments/assets/d5efcfbc-2e7b-4296-bccc-dbdf9bfd95e9)

