# NCR Ride Bookings Analysis

## Project Overview

This project presents a comprehensive analysis of 150,000 ride booking records from the National Capital Region (NCR) ride-hailing service. As a data analyst, I explored patterns in customer behavior, cancellation trends, revenue generation, and service quality to provide actionable insights for business improvement.

## Dataset Information

- **Records:** 150,000 ride bookings
- **Columns:** 29 features (after feature engineering)
- **Period:** March 2024 - November 2024
- **Region:** National Capital Region (NCR)

## Business Questions Answered

1. Why are customers and drivers cancelling rides?
2. Which locations generate the most revenue?
3. When is demand highest?
4. What factors influence customer satisfaction?
5. How do different vehicle types perform?

## Project Structure

```
ncr-ride-bookings-analysis/
│
├── ncr_ride_bookings.csv              # Original dataset
├── ncr_ride_bookings_cleaned.csv      # Cleaned dataset
├── NCR_ride_bookings.ipynb            # Data loading, cleaning, and preprocessing
├── EDA.ipynb                          # Exploratory data analysis and visualizations
├── Numpy.ipynb                        # NumPy practice exercises
├── Pandas.ipynb                       # Pandas practice exercises
├── module2_project_plan.md            # Detailed project planning guide
└── README.md                          # Project documentation
```

## Technical Skills Demonstrated

### 1. Data Cleaning & Preprocessing
- Handled missing values using context-aware strategies
- Converted data types for temporal analysis
- Created derived features for deeper insights
- Detected and flagged outliers (0.96% of data)
- Cleaned text fields and standardized formats

### 2. Feature Engineering
- Extracted temporal features: `Day_of_Week`, `Month`, `Hour`, `Is_Weekend`
- Created categorical features: `Ride_Outcome`, `Is_High_Value`, `Is_Long_Distance`
- Built route combinations for geographical analysis

### 3. Exploratory Data Analysis (EDA)
- Revenue analysis by location, vehicle type, and time
- Cancellation pattern analysis
- Time-based demand patterns
- Customer and driver satisfaction metrics
- Payment method preferences
- Geographic insights and popular routes

### 4. Data Visualization
- Distribution plots (histograms, density plots)
- Bar charts and horizontal bar charts
- Line plots for time series trends
- Pie charts for categorical distributions
- Multi-panel comparative visualizations

### 5. Statistical Analysis
- Descriptive statistics (mean, median, standard deviation)
- Correlation analysis
- Group-by aggregations
- Percentile-based segmentation

## Key Findings & Insights

### Executive Summary

- **Total Rides:** 150,000
- **Total Revenue:** ₹51,846,183
- **Average Booking Value:** ₹508.30
- **Completion Rate:** 69.0%
- **Unique Customers:** 148,788
- **Average Customer Rating:** 4.44/5.0
- **Average Driver Rating:** 4.26/5.0

### Top Insights

1. **Busiest Day:** Monday shows highest ride volume
2. **Peak Hour:** 6:00 PM (18:00) - evening commute
3. **Most Profitable Location:** Barakhamba Road
4. **Most Popular Vehicle:** Auto (most frequently booked)
5. **Preferred Payment Method:** UPI dominates transactions
6. **Top Cancellation Reason:** Wrong Address

### Cancellation Analysis

- **Completed Rides:** 103,500 (69.0%)
- **Cancelled by Driver:** 27,000 (18.0%)
- **Cancelled by Customer:** 10,500 (7.0%)
- **Incomplete Rides:** 9,000 (6.0%)

**Top Customer Cancellation Reasons:**
1. Wrong Address
2. Driver taking too long
3. Found alternative transportation

### Revenue Insights

- **Top 10 locations** contribute disproportionately to total revenue
- **Premier Sedan** has highest average booking value
- **Peak revenue hours:** 7-9 AM and 5-8 PM (commute times)
- **Weekend patterns** show longer distance rides

### Time-Based Patterns

- **Morning Peak:** 7-9 AM (office commute)
- **Evening Peak:** 5-8 PM (return commute)
- **Weekday vs Weekend:** Weekdays show higher volume but lower average distance
- **Monday** consistently shows highest demand

### Geographic Insights

- **Barakhamba Road** is the most profitable pickup location
- Certain locations show higher cancellation rates
- Popular routes identified between business districts
- Average ride distance varies significantly by pickup location

## Recommendations

Based on the data analysis, I recommend the following strategic actions:

1. **Reduce Cancellations:**
   - Implement address verification before driver dispatch
   - Optimize driver assignment algorithms to reduce wait times
   - Provide estimated arrival times more accurately

2. **Optimize Driver Availability:**
   - Increase driver allocation during peak hours (7-9 AM, 5-8 PM)
   - Focus on high-demand locations on Mondays
   - Adjust weekend driver distribution for longer distance rides

3. **Revenue Growth:**
   - Focus marketing efforts on top 10 profitable locations
   - Implement dynamic pricing during peak hours
   - Incentivize Premier Sedan usage in high-value areas

4. **Customer Experience:**
   - Investigate reasons for driver rating gaps (4.26 vs 4.44 customer rating)
   - Address top 3 cancellation reasons through process improvements
   - Improve driver-customer matching to reduce cancellations

5. **Payment Strategy:**
   - Continue promoting digital payment methods (UPI)
   - Ensure seamless payment experience to maintain high adoption

## Technologies & Libraries Used

- **Python 3.x**
- **Pandas:** Data manipulation and analysis
- **NumPy:** Numerical computations
- **Matplotlib:** Data visualization
- **Seaborn:** Statistical visualizations
- **Jupyter Notebook:** Interactive analysis environment

## Installation & Usage

### Prerequisites
```bash
python 3.x
pandas
numpy
matplotlib
seaborn
jupyter
```

### Setup
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/ncr-ride-bookings-analysis.git

# Navigate to project directory
cd ncr-ride-bookings-analysis

# Install required libraries
pip install pandas numpy matplotlib seaborn jupyter

# Launch Jupyter Notebook
jupyter notebook
```

### Running the Analysis
1. Open `NCR_ride_bookings.ipynb` to see data loading and cleaning process
2. Open `EDA.ipynb` to explore the full exploratory data analysis
3. All visualizations and insights are documented within the notebooks

## Project Highlights

This project demonstrates:
- ✅ **Real-world data analysis** on a large dataset (150K records)
- ✅ **End-to-end workflow** from raw data to actionable insights
- ✅ **Business-focused approach** linking analysis to recommendations
- ✅ **Clean code practices** with proper documentation
- ✅ **Professional visualizations** for stakeholder communication
- ✅ **Statistical rigor** in drawing conclusions

## Learning Outcomes

Through this project, I developed proficiency in:
- Working with large datasets efficiently
- Making data-driven business recommendations
- Communicating insights through visualization
- Handling missing data and outliers appropriately
- Feature engineering for enhanced analysis
- Time series pattern recognition
- Geographic data analysis

## Future Enhancements

Potential extensions to this analysis:
- Predictive modeling for cancellation risk
- Customer segmentation analysis
- Route optimization recommendations
- Seasonal trend analysis
- Driver performance benchmarking
- Interactive dashboard development with Plotly/Dash

## Author

**Your Name**
Data Analyst | Python Enthusiast
[LinkedIn](your-linkedin) | [Portfolio](your-portfolio) | [Email](your-email)

## Acknowledgments

- Dataset provided as part of Module 2: Data Manipulation & Exploration project
- Analysis conducted using industry-standard data science practices

---

**Last Updated:** November 2024

*This project is part of my data analytics portfolio showcasing skills in Python, Pandas, data visualization, and business intelligence.*
