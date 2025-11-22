# Module 2: Data Manipulation & Exploration
## NCR Ride Bookings Project - Complete Learning Plan

---

## 🎯 Project Overview

**Dataset:** NCR Ride Bookings (150,000 rows, 21 columns)  
**Business Context:** Analyze ride-hailing data to understand booking patterns, cancellations, and service quality  
**Duration:** 3-4 sessions (mix theory + hands-on)  
**Difficulty:** Beginner-friendly with progressive complexity

---

## 📋 Pre-Project Setup (Before Session 1)

### What Students Need:
- [ ] Python installed (Anaconda recommended)
- [ ] Jupyter Notebook ready
- [ ] Dataset downloaded and saved locally
- [ ] Libraries installed: `pandas`, `numpy`, `matplotlib`, `seaborn`

### Setup Check Script:
```python
# Students run this first to verify setup
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

print("✓ All libraries imported successfully!")
print(f"Pandas version: {pd.__version__}")
print(f"NumPy version: {np.__version__}")
```

---

## 🗓️ Session-by-Session Breakdown

---

## **SESSION 1: Getting to Know Your Data** (90 minutes)
*After they've learned: Basic Pandas operations, DataFrame structure*

### Learning Objectives:
- Load a real dataset
- Understand dataset structure
- Perform basic exploration
- Not get overwhelmed by 150K rows!

### Session Structure:

#### Part 1: The Story Behind the Data (10 mins)
**Your Opening:** 
"Imagine you're a data analyst at a ride-hailing company like Uber or Bolt. The CEO asks: 'Why are we losing money on cancelled rides?' Your job is to find out. This is REAL data from NCR (National Capital Region) - and you're going to analyze it."

**Key Questions to Plant:**
- Why do customers cancel rides?
- Why do drivers cancel rides?
- Which locations have the most bookings?
- What payment methods do people prefer?

---

#### Part 2: Loading the Data (15 mins)

**Code-Along (Step-by-step):**

```python
# Step 1: Import libraries
import pandas as pd
import numpy as np

# Step 2: Load the dataset
df = pd.read_csv('ncr_ride_bookings.csv')

# Step 3: First look at the data
print("Dataset loaded successfully! 🎉")
print(f"Shape: {df.shape}")  # They'll see: (150000, 21)
```

**Teaching Moment:**
"150,000 rows! That's like analyzing every ride in Nairobi for several months. Pandas can handle this easily."

---

#### Part 3: Basic Exploration (30 mins)

**Guided Exploration - Students code along:**

```python
# 1. See the first few rows
df.head()
```
**Stop and Discuss:** "What do you notice? What columns seem interesting?"

```python
# 2. Get column names
df.columns
```
**Activity:** "In pairs, categorize these columns: Booking info, Customer info, Driver info, etc."

```python
# 3. Basic info about dataset
df.info()
```
**Teaching Moment:** "Notice 'non-null' counts? Some columns have fewer than 150,000 values. That's missing data we'll handle later!"

```python
# 4. Summary statistics
df.describe()
```
**Guided Questions:**
- "What's the average ride distance?"
- "What's the highest booking value?"
- "Look at the ratings - what's the range?"

```python
# 5. Check data types
df.dtypes
```

---

#### Part 4: Your First Analysis (25 mins)

**Simple Questions They Can Answer NOW:**

```python
# Q1: How many unique vehicle types?
print(f"Vehicle types: {df['Vehicle Type'].nunique()}")
df['Vehicle Type'].value_counts()
```

```python
# Q2: What are the most common booking statuses?
df['Booking Status'].value_counts()
```

```python
# Q3: What's the average booking value?
print(f"Average booking value: ${df['Booking Value'].mean():.2f}")
```

```python
# Q4: Top 5 pickup locations
df['Pickup Location'].value_counts().head()
```

**Success Moment:** "Congratulations! You just analyzed 150,000 rides in under 10 lines of code! 🎉"

---

#### Part 5: Wrap-up & Homework (10 mins)

**Key Takeaways:**
- We can load and explore massive datasets easily
- `.head()`, `.info()`, `.describe()` are your best friends
- Missing data exists and we'll handle it next session

**Homework Challenge:**
```python
# Find answers to these questions (give them the starter code):

# 1. How many unique customers used the service?
# Answer: df['Customer ID'].nunique()

# 2. What's the most common payment method?
# Answer: df['Payment Method'].value_counts()

# 3. What percentage of rides were completed successfully?
# Hint: Look at 'Booking Status' column
```

---

## **SESSION 2: Cleaning Messy Data** (90 minutes)
*After they've learned: Handling missing data, data types, filtering*

### Learning Objectives:
- Identify data quality issues
- Handle missing values intelligently
- Clean and standardize data
- Understand WHEN to delete vs fill data

### Session Structure:

#### Part 1: The Data Quality Detective (10 mins)

**Opening Story:**
"Remember that CEO question about cancelled rides? Well, we can't answer it if our data is messy. Today you become data detectives - finding and fixing problems in the data."

---

#### Part 2: Finding Missing Data (20 mins)

```python
# Check for missing values
print("Missing Values Summary:")
print(df.isnull().sum())
```

**Guided Discussion:**
"Notice which columns have missing values. Why do you think 'Cancelled Rides by Customer' has nulls?"

**Answer:** Because not all rides are cancelled! These are actually INFORMATIVE nulls.

```python
# Visualize missing data
import matplotlib.pyplot as plt

missing_data = df.isnull().sum()
missing_data = missing_data[missing_data > 0].sort_values(ascending=False)

plt.figure(figsize=(10, 6))
missing_data.plot(kind='bar')
plt.title('Missing Values by Column')
plt.ylabel('Number of Missing Values')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

---

#### Part 3: Smart Data Cleaning Strategy (40 mins)

**Strategy 1: Understanding Null Patterns**

```python
# Create a helper column to understand booking outcomes
df['Ride Outcome'] = 'Completed'
df.loc[df['Cancelled Rides by Customer'] > 0, 'Ride Outcome'] = 'Cancelled by Customer'
df.loc[df['Cancelled Rides by Driver'] > 0, 'Ride Outcome'] = 'Cancelled by Driver'
df.loc[df['Incomplete Rides'] > 0, 'Ride Outcome'] = 'Incomplete'

# Now check the distribution
df['Ride Outcome'].value_counts()
```

**Teaching Moment:** "See? Nulls weren't errors - they meant 'this didn't happen'!"

---

**Strategy 2: Filling Missing Values Intelligently**

```python
# For cancellation columns, null means 0 (no cancellation)
cancellation_cols = [
    'Cancelled Rides by Customer',
    'Cancelled Rides by Driver',
    'Incomplete Rides'
]

for col in cancellation_cols:
    df[col].fillna(0, inplace=True)

# For reason columns, null means 'Not Applicable'
reason_cols = [
    'Reason for cancelling by Customer',
    'Driver Cancellation Reason',
    'Incomplete Rides Reason'
]

for col in reason_cols:
    df[col].fillna('Not Applicable', inplace=True)
```

---

**Strategy 3: Handling Ratings Missing Data**

```python
# Check ratings distribution first
print(df['Driver Ratings'].describe())
print(df['Customer Rating'].describe())

# Strategy: Fill with median (more robust than mean)
df['Driver Ratings'].fillna(df['Driver Ratings'].median(), inplace=True)
df['Customer Rating'].fillna(df['Customer Rating'].median(), inplace=True)
```

**Discussion Point:** "Why median instead of mean? Because ratings can have outliers!"

---

#### Part 4: Data Type Conversions (15 mins)

```python
# Convert Date and Time to proper datetime
df['Date'] = pd.to_datetime(df['Date'])
df['Time'] = pd.to_datetime(df['Time'], format='%H:%M:%S').dt.time

# Extract useful date features
df['Day_of_Week'] = df['Date'].dt.day_name()
df['Month'] = df['Date'].dt.month_name()
df['Hour'] = pd.to_datetime(df['Time'], format='%H:%M:%S').dt.hour

# Now you can analyze by time!
print(df['Day_of_Week'].value_counts())
```

---

#### Part 5: Wrap-up & Checkpoint (5 mins)

**Verification Check:**
```python
# Students verify their cleaning worked
print("✓ Data Cleaning Checklist:")
print(f"Missing values remaining: {df.isnull().sum().sum()}")
print(f"Date is datetime: {df['Date'].dtype}")
print(f"New columns created: {['Day_of_Week', 'Month', 'Hour', 'Ride Outcome']}")
```

**Homework:**
"Clean your own copy of the dataset. Next session, we'll answer the BIG questions!"

---

## **SESSION 3: Exploratory Data Analysis (EDA)** (90 minutes)
*After they've learned: GroupBy, filtering, aggregations*

### Learning Objectives:
- Answer business questions with data
- Use groupby for insights
- Create meaningful aggregations
- Tell stories with data

### Session Structure:

#### Part 1: The Business Questions (5 mins)

**Today's Mission:**
"You're presenting to the CEO tomorrow. They want answers to:
1. Why are customers cancelling rides?
2. Which locations are most profitable?
3. When are we busiest?
4. Are customers and drivers happy?"

---

#### Part 2: Cancellation Analysis (25 mins)

**Question 1: Why do customers cancel?**

```python
# Get cancellation reasons
customer_cancellations = df[df['Ride Outcome'] == 'Cancelled by Customer']

print(f"Total customer cancellations: {len(customer_cancellations)}")
print(f"Cancellation rate: {len(customer_cancellations)/len(df)*100:.2f}%")

# Top reasons for cancellation
cancellation_reasons = customer_cancellations['Reason for cancelling by Customer'].value_counts()
print("\nTop 5 Cancellation Reasons:")
print(cancellation_reasons.head())

# Visualize
plt.figure(figsize=(12, 6))
cancellation_reasons.head(10).plot(kind='barh')
plt.title('Top 10 Reasons Customers Cancel Rides')
plt.xlabel('Number of Cancellations')
plt.tight_layout()
plt.show()
```

**Teaching Moment:** "What insight can we share with the CEO? Maybe drivers are arriving too late?"

---

**Question 2: Why do drivers cancel?**

```python
driver_cancellations = df[df['Ride Outcome'] == 'Cancelled by Driver']

driver_reasons = driver_cancellations['Driver Cancellation Reason'].value_counts()
print("Top Driver Cancellation Reasons:")
print(driver_reasons.head())
```

**Comparative Analysis:**
```python
# Compare cancellation rates
cancellation_summary = df['Ride Outcome'].value_counts()
cancellation_summary.plot(kind='pie', autopct='%1.1f%%', figsize=(8, 8))
plt.title('Ride Outcomes Distribution')
plt.ylabel('')
plt.show()
```

---

#### Part 3: Location & Profitability Analysis (25 mins)

**Question 3: Which locations make the most money?**

```python
# Group by pickup location
location_analysis = df.groupby('Pickup Location').agg({
    'Booking Value': ['sum', 'mean', 'count'],
    'Ride Distance': 'mean',
    'Customer Rating': 'mean'
}).round(2)

location_analysis.columns = ['Total Revenue', 'Avg Booking Value', 'Total Rides', 'Avg Distance', 'Avg Rating']
location_analysis = location_analysis.sort_values('Total Revenue', ascending=False)

print("Top 10 Most Profitable Pickup Locations:")
print(location_analysis.head(10))
```

**Visualization:**
```python
# Top 10 locations by revenue
top_locations = location_analysis.head(10)

fig, axes = plt.subplots(1, 2, figsize=(15, 6))

# Revenue
top_locations['Total Revenue'].plot(kind='bar', ax=axes[0], color='green')
axes[0].set_title('Total Revenue by Location')
axes[0].set_xlabel('Pickup Location')
axes[0].set_ylabel('Revenue')

# Number of rides
top_locations['Total Rides'].plot(kind='bar', ax=axes[1], color='blue')
axes[1].set_title('Total Rides by Location')
axes[1].set_xlabel('Pickup Location')
axes[1].set_ylabel('Number of Rides')

plt.tight_layout()
plt.show()
```

---

#### Part 4: Time-Based Analysis (25 mins)

**Question 4: When are we busiest?**

```python
# By day of week
day_analysis = df.groupby('Day_of_Week').agg({
    'Booking ID': 'count',
    'Booking Value': 'sum'
}).round(2)

day_analysis.columns = ['Total Rides', 'Total Revenue']

# Order days properly
day_order = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
day_analysis = day_analysis.reindex(day_order)

print(day_analysis)

# Visualize
day_analysis['Total Rides'].plot(kind='line', marker='o', figsize=(10, 6))
plt.title('Rides by Day of Week')
plt.xlabel('Day')
plt.ylabel('Number of Rides')
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()
```

**By Hour:**
```python
# Hourly patterns
hour_analysis = df.groupby('Hour')['Booking ID'].count()

plt.figure(figsize=(12, 6))
hour_analysis.plot(kind='bar')
plt.title('Rides by Hour of Day')
plt.xlabel('Hour')
plt.ylabel('Number of Rides')
plt.tight_layout()
plt.show()
```

**Teaching Moment:** "When would you recommend the company has more drivers available?"

---

#### Part 5: Customer Satisfaction Analysis (10 mins)

```python
# Overall satisfaction metrics
print("Customer Satisfaction Metrics:")
print(f"Average Customer Rating: {df['Customer Rating'].mean():.2f}")
print(f"Average Driver Rating: {df['Driver Ratings'].mean():.2f}")

# Rating distribution
fig, axes = plt.subplots(1, 2, figsize=(15, 5))

df['Customer Rating'].hist(bins=20, ax=axes[0], edgecolor='black')
axes[0].set_title('Customer Rating Distribution')
axes[0].set_xlabel('Rating')
axes[0].set_ylabel('Frequency')

df['Driver Ratings'].hist(bins=20, ax=axes[1], edgecolor='black')
axes[1].set_title('Driver Rating Distribution')
axes[1].set_xlabel('Rating')
axes[1].set_ylabel('Frequency')

plt.tight_layout()
plt.show()
```

---

## **SESSION 4: Advanced Analysis & Presentation** (90 minutes)
*Final session - bringing it all together*

### Learning Objectives:
- Combine multiple analyses
- Create executive summary
- Present findings clearly
- Build a portfolio piece

### Session Structure:

#### Part 1: Advanced Questions (30 mins)

**Multi-dimensional Analysis:**

```python
# Question: Do cancelled rides correlate with distance?
completed_rides = df[df['Ride Outcome'] == 'Completed']
cancelled_rides = df[df['Ride Outcome'].str.contains('Cancelled')]

print(f"Avg distance for completed rides: {completed_rides['Ride Distance'].mean():.2f} km")
print(f"Avg distance for cancelled rides: {cancelled_rides['Ride Distance'].mean():.2f} km")
```

```python
# Question: Which vehicle types are most popular by location?
vehicle_location = df.groupby(['Pickup Location', 'Vehicle Type']).size().unstack(fill_value=0)
print(vehicle_location.head(10))
```

```python
# Question: Payment method preferences
payment_analysis = df.groupby('Payment Method').agg({
    'Booking Value': ['count', 'sum', 'mean']
}).round(2)
print(payment_analysis)
```

---

#### Part 2: Creating Executive Summary (30 mins)

**Guide Students to Create:**

```python
# Executive Summary Dashboard
print("=" * 50)
print("NCR RIDE BOOKINGS - EXECUTIVE SUMMARY")
print("=" * 50)

# Key Metrics
total_rides = len(df)
total_revenue = df['Booking Value'].sum()
avg_booking = df['Booking Value'].mean()
completion_rate = (df['Ride Outcome'] == 'Completed').sum() / total_rides * 100

print(f"\n📊 KEY METRICS:")
print(f"Total Rides: {total_rides:,}")
print(f"Total Revenue: ${total_revenue:,.2f}")
print(f"Average Booking Value: ${avg_booking:.2f}")
print(f"Completion Rate: {completion_rate:.1f}%")

# Top Insights
print(f"\n🎯 TOP INSIGHTS:")
print(f"1. Busiest Day: {df['Day_of_Week'].value_counts().index[0]}")
print(f"2. Most Profitable Location: {location_analysis.index[0]}")
print(f"3. Most Common Cancellation: {cancellation_reasons.index[0]}")
print(f"4. Average Customer Rating: {df['Customer Rating'].mean():.2f}/5.0")

# Recommendations
print(f"\n💡 RECOMMENDATIONS:")
print("1. Reduce driver wait times to decrease customer cancellations")
print("2. Increase driver availability during peak hours")
print("3. Focus marketing on top 5 profitable locations")
print("4. Investigate and address top 3 cancellation reasons")
```

---

#### Part 3: Portfolio Project Setup (20 mins)

**Help Students Create a Complete Notebook:**

Structure:
1. **Title & Introduction**
2. **Data Loading & Overview**
3. **Data Cleaning Process**
4. **Exploratory Data Analysis**
5. **Key Findings & Visualizations**
6. **Conclusions & Recommendations**

**Markdown Template to Share:**
```markdown
# NCR Ride Bookings Analysis
**Analyzed by:** [Student Name]  
**Date:** [Date]  
**Dataset:** 150,000 ride records from NCR region

## Business Problem
Understand ride cancellation patterns and identify opportunities to improve service quality and revenue.

## Key Questions
1. Why are customers cancelling rides?
2. Which locations generate the most revenue?
3. When is demand highest?
4. How satisfied are customers and drivers?

[Their analysis follows...]
```

---

#### Part 4: GitHub Push Tutorial (10 mins)

**Step-by-step:**
```bash
# 1. Create repository on GitHub
# 2. Initialize git in project folder
git init
git add .
git commit -m "NCR Ride Bookings Analysis - Module 2 Project"

# 3. Connect to GitHub
git remote add origin [their-repo-url]
git push -u origin main
```

**What to include:**
- Jupyter Notebook (.ipynb)
- README.md with project description
- Requirements.txt
- Screenshots of key visualizations

---

## 📚 **BONUS: Challenge Projects** (For Advanced Students)

### Challenge 1: Predictive Question
"Can you identify patterns that predict cancellations? Create a 'cancellation risk score' based on:
- Time of day
- Distance
- Location
- Vehicle type"

### Challenge 2: Comparative Analysis
"Compare weekday vs weekend patterns - are they different?"

### Challenge 3: Deep Dive
"Pick one location and do a complete analysis - what makes it unique?"

---

## 🎓 **Assessment Rubric**

### What You're Looking For:

**Basic (Pass):**
- [ ] Successfully loaded and explored data
- [ ] Handled missing values appropriately
- [ ] Answered at least 3 business questions
- [ ] Created at least 3 visualizations
- [ ] Pushed to GitHub

**Intermediate (Good):**
- [ ] All basic requirements
- [ ] Used groupby for multi-dimensional analysis
- [ ] Clear markdown documentation
- [ ] Insights are clearly explained
- [ ] Visualizations are labeled and styled

**Advanced (Excellent):**
- [ ] All intermediate requirements
- [ ] Created executive summary
- [ ] Found non-obvious insights
- [ ] Made business recommendations
- [ ] Code is clean and well-commented
- [ ] Professional presentation quality

---

## 💡 **Teaching Tips**

### For Beginners:
1. **Code along together first** - don't expect them to code independently immediately
2. **Use print statements liberally** - show them the output at every step
3. **Celebrate small wins** - "You just analyzed 150K rows!" 
4. **Encourage questions** - pause frequently
5. **Pair programming** - have them work in pairs

### For Mixed Levels:
1. **Core + Challenge structure** - everyone does core, advanced students do challenges
2. **Peer teaching** - advanced students help beginners
3. **Multiple solutions** - show there's more than one way

### Common Struggles:
1. **"My code doesn't work"** → Check they loaded data correctly first
2. **"I don't understand groupby"** → Use physical analogy (sorting cards into piles)
3. **"The dataset is too big"** → Show them `.sample(1000)` for testing
4. **"I'm lost"** → Give them completed code to run, then explain what it does

---

## 📊 **Progress Tracking**

**After each session, students should:**
- [ ] Have working code saved
- [ ] Understand what the code does
- [ ] Be able to explain one insight they found
- [ ] Feel more confident than last session

**Red flags to watch for:**
- Students not running code along with you
- Blank notebooks (they're not following)
- Confused faces but no questions
- Rushing through without understanding

**Fixes:**
- Pause and ask "Everyone with me?"
- Do a quick poll: "Show me your output"
- Call on specific students to share their screen
- Take a 5-min break if energy is low

---

## 🎯 **Success Metrics**

By end of Module 2, students should be able to:
- [ ] Load any CSV file
- [ ] Check for and handle missing data
- [ ] Perform groupby operations
- [ ] Create basic visualizations
- [ ] Answer business questions with data
- [ ] Explain their findings clearly
- [ ] Have a project on GitHub

---

## 📝 **Feedback Collection**

**After this module, ask:**
1. "What was the most challenging part?"
2. "What was the most interesting insight you found?"
3. "Do you feel confident loading and cleaning new datasets?"
4. "What would you like more practice with?"

---

## 🚀 **Bridge to Module 3**

**Closing statement:**
"Next module, you'll learn to make your findings BEAUTIFUL and PERSUASIVE with advanced visualizations. You'll take these same insights and turn them into stunning dashboards that wow anyone who sees them!"

**Preview:** Show example of what their final Module 3 output could look like - a beautiful dashboard with this data.

---

**Good luck! You've got this! 🎉**
