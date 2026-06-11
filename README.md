# 📊 Customer Churn & Revenue Risk Analysis Using Python

<p align="center">
  <img src="images/thumbnail.png" alt="Customer Churn Analysis Banner" width="100%">
</p>

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-blue?logo=numpy)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-green)
![EDA](https://img.shields.io/badge/EDA-Exploratory%20Data%20Analysis-yellow)
![Business Analytics](https://img.shields.io/badge/Business-Analytics-red)

</p>

---

# 📌 Project Overview

Customer retention is a major challenge for subscription-based businesses. Every time a customer leaves, the organization loses recurring revenue and may incur additional costs to acquire a replacement customer.

This project applies data analytics techniques to understand customer churn behaviour, identify customer segments with elevated churn risk, estimate potential revenue loss, and provide business recommendations aimed at improving customer retention.

Using Python and Exploratory Data Analysis (EDA), this project transforms raw customer subscription data into actionable business insights that can support strategic decision-making.

---

# 🎯 Business Problem

Organizations often struggle to answer questions such as:

- Why are customers leaving?
- Which customers are most likely to churn?
- Which business factors influence churn?
- How much revenue is being lost due to churn?
- What actions can improve customer retention?

Without answering these questions, businesses risk losing customers, revenue, and market share.

This project seeks to address these challenges through a structured data analytics workflow.

---

# 🎯 Project Objectives

The primary objectives of this project are:

### 1. Analyze Customer Churn

Identify patterns and characteristics associated with customers who leave the company.

### 2. Quantify Revenue Risk

Estimate the potential financial impact associated with customer churn.

### 3. Segment Customers

Group customers according to tenure and value in order to identify high-risk populations.

### 4. Generate Actionable Insights

Provide business recommendations that can reduce churn and improve customer retention.

### 5. Demonstrate Data Analytics Skills

Showcase practical skills in:

- Data Cleaning
- Data Transformation
- Feature Engineering
- Exploratory Data Analysis
- Business Analytics
- Data Visualization
- Insight Generation

---

# ❓ Business Questions

This analysis seeks to answer the following questions:

1. What proportion of customers have churned?

2. Which contract types have the highest churn rates?

3. Which payment methods are associated with higher churn?

4. Are new customers more likely to leave than long-term customers?

5. Which customer segments represent the highest revenue risk?

6. Does monthly pricing influence churn behaviour?

7. Which business interventions could improve retention?

---

# 🛠 Tools & Technologies

| Category | Technology |
|-----------|-----------|
| Programming Language | Python |
| Data Manipulation | Pandas |
| Numerical Analysis | NumPy |
| Visualization | Matplotlib |
| Development Environment | Jupyter Notebook |
| Version Control | Git & GitHub |

---

# 📂 Repository Structure

```text
Customer-Churn-Revenue-Risk-Analysis/
│
├── README.md
├── customer_churn_analysis.py
├── CUSTOMER CHURN AND REVENUE RISK ANALYSIS.ipynb
│
├── images/
│   ├── thumbnail.png
│   ├── churn_distribution.png
│   ├── churn_by_contract.png
│   ├── churn_by_tenure_group.png
│   ├── churn_by_payment_method.png
│   ├── churn_by_customer_value_segment.png
│   ├── monthly_charges_by_churn.png
│   └── revenue_risk_by_contract.png
│
├── outputs/
│   ├── raw_customer_churn_data.csv
│   ├── kpi_summary.csv
│   ├── churn_by_contract.csv
│   ├── churn_by_payment.csv
│   ├── churn_by_tenure.csv
│   ├── churn_by_value_segment.csv
│   └── business_recommendations.txt
│
└── requirements.txt
```

---

# 📑 Table of Contents

- Project Overview
- Business Problem
- Project Objectives
- Business Questions
- Dataset Description
- Methodology
- Data Cleaning
- Feature Engineering
- KPI Analysis
- Visualizations & Insights
- Key Findings
- Business Recommendations
- Installation Guide
- Future Improvements
- Skills Demonstrated
- Author

# 📊 Dataset Description

The dataset contains customer subscription information collected from a telecommunications company.

Each record represents a unique customer and includes demographic information, service subscriptions, contract details, payment methods, and churn status.

## Dataset Features

| Feature | Description |
|----------|------------|
| customerID | Unique customer identifier |
| gender | Customer gender |
| SeniorCitizen | Indicates whether customer is a senior citizen |
| Partner | Customer has a partner |
| Dependents | Customer has dependents |
| tenure | Number of months customer stayed with company |
| PhoneService | Subscription to phone service |
| InternetService | Internet subscription type |
| Contract | Contract type |
| PaymentMethod | Customer payment method |
| MonthlyCharges | Monthly subscription fee |
| TotalCharges | Total accumulated charges |
| Churn | Indicates whether customer left |

---

# 🎯 Analytical Approach

The project follows a structured analytics workflow consisting of:

1. Data Collection
2. Data Cleaning
3. Data Transformation
4. Feature Engineering
5. Exploratory Data Analysis
6. KPI Analysis
7. Data Visualization
8. Business Insight Generation
9. Business Recommendations

The objective is not only to identify churn patterns but also to explain the business implications behind those patterns.

---

# 🔄 Project Workflow

<p align="center">

Raw Data
⬇
Data Cleaning
⬇
Feature Engineering
⬇
EDA
⬇
KPI Analysis
⬇
Visualizations
⬇
Business Insights
⬇
Recommendations

</p>

---

# 🧹 Data Cleaning

Before analysis, the dataset was examined for quality issues.

The following checks were performed:

### Missing Values

Missing values were identified and treated appropriately.

```python
df.isnull().sum()
```

### Duplicate Records

Duplicate entries were checked to ensure data integrity.

```python
df.duplicated().sum()
```

### Data Type Conversion

The `TotalCharges` field contained non-numeric values and was converted to a numerical format.

```python
df["TotalCharges"] = pd.to_numeric(
    df["TotalCharges"],
    errors="coerce"
)
```

### Missing Value Imputation

Missing values were replaced using the median.

```python
df["TotalCharges"] = (
    df["TotalCharges"]
    .fillna(df["TotalCharges"].median())
)
```

### Churn Encoding

The target variable was converted to numerical format.

```python
df["Churn_Flag"] = df["Churn"].map(
    {"Yes": 1, "No": 0}
)
```

This enabled quantitative analysis of customer churn.

---

# ⚙ Feature Engineering

Feature engineering was performed to create business-focused variables that provide additional insight.

---

## Revenue Risk

A new variable was created to estimate revenue exposure associated with churned customers.

```python
df["Revenue_Risk"] = np.where(
    df["Churn"] == "Yes",
    df["MonthlyCharges"],
    0
)
```

### Business Meaning

Revenue Risk represents the monthly recurring revenue that may be lost when a customer leaves.

---

## Tenure Group

Customers were grouped according to the number of months they remained with the company.

```python
df["Tenure_Group"] = pd.cut(
    df["tenure"],
    bins=[-1,12,24,48,72],
    labels=[
        "0-12 Months",
        "13-24 Months",
        "25-48 Months",
        "49-72 Months"
    ]
)
```

### Business Meaning

Grouping customers by tenure helps determine whether new customers or long-term customers are more likely to churn.

---

## Customer Value Segment

Customers were categorized according to monthly spending.

```python
df["Customer_Value_Segment"] = pd.cut(
    df["MonthlyCharges"],
    bins=[0,35,70,120],
    labels=[
        "Low Value",
        "Medium Value",
        "High Value"
    ]
)
```

### Business Meaning

This segmentation helps identify whether high-value customers present greater revenue risk.

---

# 📈 Key Performance Indicators (KPIs)

Several KPIs were calculated to evaluate customer retention performance.

---

## Total Customers

Represents the total number of customers in the dataset.

```python
total_customers = len(df)
```

### Why It Matters

Provides the baseline population for all analysis.

---

## Total Churned Customers

Represents the total number of customers who left the company.

```python
total_churned = df["Churn_Flag"].sum()
```

### Why It Matters

Measures the scale of customer attrition.

---

## Churn Rate

Represents the percentage of customers who left.

```python
churn_rate = (
    df["Churn_Flag"].mean() * 100
)
```

### Formula

\[
Churn\ Rate =
\frac{Customers\ Lost}
{Total\ Customers}
\times 100
\]

### Why It Matters

One of the most important metrics for subscription-based businesses.

---

## Average Monthly Charges

Represents the average monthly subscription fee paid by customers.

```python
avg_monthly_charge = (
    df["MonthlyCharges"].mean()
)
```

### Why It Matters

Helps evaluate pricing behaviour and customer spending patterns.

---

## Revenue at Risk

Represents the total monthly revenue associated with churned customers.

```python
total_revenue_risk = (
    df["Revenue_Risk"].sum()
)
```

### Why It Matters

Quantifies the financial impact of churn.

---

# 📊 Summary of Analytical Focus

The analysis focuses on understanding:

- Customer retention behaviour
- Revenue exposure
- Contract effectiveness
- Customer lifecycle patterns
- Pricing impact on churn
- High-risk customer segments

The next section presents visualizations and interprets the business insights derived from the data.
# 📊 Visualizations & Business Insights

Data visualization plays a critical role in transforming analytical results into actionable business insights.

The following visualizations were developed to understand customer churn behaviour and identify revenue risks.

---

# 1️⃣ Customer Churn Distribution

![Customer Churn Distribution](images/churn_distribution.png)

## Objective

To understand the overall distribution of churned and retained customers.

---

## Interpretation

The chart shows two customer groups:

- Customers who remained with the company
- Customers who left the company

The majority of customers remained with the company; however, a significant proportion churned.

---

## Business Insight

Although customer retention is relatively strong, customer attrition remains substantial enough to impact revenue and profitability.

Customer churn should therefore be treated as a strategic business concern.

---

## Business Recommendation

- Implement proactive customer retention programs.
- Monitor churn trends regularly.
- Establish churn reduction KPIs.

---

# 2️⃣ Churn Rate by Contract Type

![Churn Rate by Contract Type](images/churn_by_contract.png)

## Objective

To determine whether contract duration influences customer retention.

---

## Interpretation

The visualization shows that:

- Month-to-Month customers have the highest churn rate.
- One-Year contract customers have lower churn.
- Two-Year contract customers have the lowest churn.

---

## Business Insight

Customers with short-term commitments are significantly more likely to leave.

Long-term contracts appear to strengthen customer loyalty and reduce switching behaviour.

---

## Business Impact

High churn among month-to-month customers creates instability in recurring revenue.

---

## Business Recommendation

- Offer discounts for annual contracts.
- Create loyalty rewards for contract upgrades.
- Encourage customers to move from month-to-month plans to longer-term subscriptions.

---

# 3️⃣ Churn Rate by Tenure Group

![Churn Rate by Tenure Group](images/churn_by_tenure_group.png)

## Objective

To evaluate the relationship between customer tenure and churn.

---

## Interpretation

The chart demonstrates that:

- Customers within their first year exhibit the highest churn rate.
- Churn decreases as tenure increases.
- Long-term customers are more likely to remain loyal.

---

## Business Insight

Customer retention challenges are concentrated in the early stages of the customer lifecycle.

New customers are particularly vulnerable to leaving before becoming fully engaged with the service.

---

## Business Impact

High churn among new customers increases customer acquisition costs and reduces customer lifetime value.

---

## Business Recommendation

- Improve onboarding programs.
- Increase customer engagement during the first year.
- Provide proactive support to newly acquired customers.

---

# 4️⃣ Churn Rate by Payment Method

![Churn Rate by Payment Method](images/churn_by_payment_method.png)

## Objective

To investigate whether payment behaviour is associated with churn.

---

## Interpretation

The chart reveals that customers using Electronic Check experience the highest churn rates.

Customers using automatic payment methods show comparatively lower churn rates.

---

## Business Insight

Payment experience may influence customer satisfaction and retention.

Customers who use automatic payment options may experience fewer service interruptions and greater convenience.

---

## Business Impact

Payment-related friction may contribute to customer attrition.

---

## Business Recommendation

- Encourage automatic payment enrollment.
- Investigate payment-related customer complaints.
- Offer incentives for automated payment methods.

---

# 5️⃣ Churn Rate by Customer Value Segment

![Churn Rate by Customer Value Segment](images/churn_by_customer_value_segment.png)

## Objective

To determine which customer value groups are most likely to churn.

---

## Interpretation

The chart indicates that:

- High-Value customers exhibit the highest churn rate.
- Medium-Value customers show moderate churn.
- Low-Value customers demonstrate lower churn rates.

---

## Business Insight

The loss of high-value customers creates a disproportionately large financial impact.

Even small increases in churn among high-value customers can significantly affect revenue.

---

## Business Impact

Revenue losses are amplified when high-spending customers leave.

---

## Business Recommendation

- Develop premium customer retention programs.
- Create personalized engagement campaigns.
- Monitor high-value customers more closely.

---

# 6️⃣ Monthly Charges by Churn Status

![Monthly Charges by Churn Status](images/monthly_charges_by_churn.png)

## Objective

To evaluate the relationship between pricing and customer churn.

---

## Interpretation

The boxplot indicates that churned customers generally have higher monthly charges than retained customers.

---

## Business Insight

Customers paying higher subscription fees may be more sensitive to perceived value.

If customers believe they are not receiving sufficient value for the price paid, churn becomes more likely.

---

## Business Impact

Pricing structures can influence customer retention outcomes.

---

## Business Recommendation

- Review pricing strategy.
- Improve value communication.
- Enhance premium service offerings.

---

# 7️⃣ Monthly Revenue at Risk by Contract Type

![Monthly Revenue at Risk by Contract Type](images/revenue_risk_by_contract.png)

## Objective

To quantify the financial impact of churn across customer contract types.

---

## Interpretation

The chart shows that:

- Month-to-Month customers account for the majority of revenue at risk.
- Long-term contract customers contribute substantially less revenue risk.

---

## Business Insight

Month-to-month customers represent both:

- The highest churn risk.
- The highest revenue exposure.

This segment should therefore be prioritized for retention efforts.

---

## Business Impact

Reducing churn among month-to-month customers could significantly improve financial performance.

---

## Business Recommendation

- Prioritize retention campaigns for month-to-month customers.
- Introduce loyalty incentives.
- Improve customer engagement initiatives.

---

# 🔍 Overall Findings

The analysis reveals several important patterns:

### Finding 1

Month-to-month customers have the highest churn rates.

### Finding 2

New customers are more likely to churn than long-term customers.

### Finding 3

Electronic Check users exhibit elevated churn rates.

### Finding 4

High-value customers create the greatest revenue risk.

### Finding 5

Customers paying higher monthly fees tend to churn more frequently.

### Finding 6

Most revenue at risk originates from month-to-month customers.

---

# 💼 Executive Summary

This analysis demonstrates that customer churn is not evenly distributed across the customer base.

Specific customer groups contribute disproportionately to revenue risk:

- New customers
- Month-to-month customers
- High-value customers
- Electronic Check users

Targeted interventions aimed at these segments could substantially reduce churn and improve customer lifetime value.

The findings emphasize the importance of combining customer analytics with business strategy to support data-driven decision-making.

---

# 💡 Strategic Business Recommendations

Based on the findings, the following actions are recommended:

### Customer Retention

- Improve onboarding processes.
- Develop proactive customer support initiatives.
- Increase customer engagement during the first year.

### Contract Strategy

- Promote annual and multi-year contracts.
- Offer incentives for long-term commitments.

### Pricing Strategy

- Evaluate premium pricing structures.
- Improve value communication.

### Revenue Protection

- Monitor high-value customers.
- Launch targeted retention campaigns.

### Payment Experience

- Encourage automatic payment methods.
- Investigate electronic check customer behaviour.

These actions can help reduce churn, protect revenue, and improve overall customer satisfaction.

# 🎯 Project Outcomes

Through this project I was able to:

✅ Analyze customer churn patterns

✅ Quantify potential revenue risk

✅ Segment customers into meaningful business categories

✅ Develop actionable business recommendations

✅ Communicate findings through data visualization

✅ Demonstrate end-to-end data analytics capabilities

---

# 📚 Key Learning Outcomes

The project reinforced several important concepts:

### Customer Churn Analysis

Understanding customer attrition behavior and its impact on business performance.

### Revenue Risk Assessment

Estimating the financial consequences of customer loss.

### Customer Segmentation

Identifying customer groups with different risk profiles.

### Data Storytelling

Transforming technical findings into business recommendations.

### Business Decision Support

Using analytics to support strategic decisions.

---

# 🏆 Why This Project Matters

Customer churn directly impacts:

- Revenue
- Profitability
- Customer Lifetime Value
- Business Growth

Organizations that effectively understand and manage churn often outperform competitors because they can retain more customers and reduce acquisition costs.

This project demonstrates how data analytics can support those goals.
