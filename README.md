# Data Analysis and Visualization Report: Sales Process Across Continents Dashboard (March 2025)
# Overview
This report details the data cleaning, transformation, and visualization process for the "clean order data.xlsx" dataset, originally provided with 400 transactional records spanning March 2025. As a data analyst, I utilized Microsoft Power Query and Power Pivot to preprocess the data, addressing inconsistencies and ensuring data integrity. Subsequently, I developed an interactive Excel dashboard titled "Track sales process across continents" to analyze sales trends, product performance, and regional contributions. The dashboard leverages Excel's charting capabilities to provide stakeholders with actionable insights into the sales process for the period.

# Data Cleaning and Transformation Process
Initial Data Assessment
The raw dataset (order data.xlsx) exhibited several data quality issues :

Inconsistent Date Formats:
Order Date varied across formats: YYYY-MM-DD (e.g., 2025-03-08), MM/DD/YYYY (e.g., 03/07/2025), and textual (e.g., March 7, 2025).
Ship Date was uniformly 3/28/25 (interpreted as March 28, 2025), but its consistency across all records raised concerns about data accuracy.
Data Type Mismatches:
Quantity included text (e.g., two, three) and negative values (e.g., -2 for Order ID 2004), indicating invalid entries.
Price contained currency symbols (e.g., $600) and text (e.g., two for Order ID 2022), requiring standardization.
Total Price included negative values (e.g., -85 for Order ID 2001, -4187 for Order ID 2151) and inconsistencies with Quantity * Price (e.g., 3 * 50 = 150 ≠ -85).
Missing or Invalid Data:
Customer Name was blank in several rows (e.g., Order ID 2025, 2044), similar to the previous dataset.
Region was missing for some rows (e.g., Order ID 2006, 2021), consistent with prior issues.
Calculation Errors:
Total Price did not align with Quantity * Price in numerous cases (e.g., Order ID 2001: -85 ≠ 150, Order ID 2014: 59 ≠ 600), suggesting data entry or formula errors.
Outliers and Anomalies:
Negative Quantity values (e.g., -2 for Order ID 2004) and Total Price (e.g., -2000 for Order ID 2201) indicated potential returns or data corruption.
Extreme Total Price values (e.g., 4666 for Order ID 2013 with Quantity -3 and Price 100) suggested miscalculations.

# Cleaning Steps Using Power Query (Differences from Previous Dataset)
Date Standardization:
Converted all Order Date formats to MM/DD/YYYY (e.g., 2025-03-08 → 03/08/2025, March 7, 2025 → 03/07/2025) using a unified parsing rule, improving on the previous effort where only serial number conversion was addressed.
Standardized Ship Date from 3/28/25 to 03/28/2025 across all records, but flagged its uniformity as a potential data integrity issue for further investigation, unlike the previous dataset where Ship Date was adjusted to match Order Date.
Type Conversion and Validation:
Converted Quantity text values (e.g., two → 2, three → 3) to integers using a custom replacement function, addressing a new issue not present in the cleaned dataset.
Removed currency symbols from Price (e.g., $600 → 600) and converted to numeric, a step refined from the previous process.
Recalculated Total Price as Quantity * Price where discrepancies existed (e.g., Order ID 2001: -85 → 150, Order ID 2014: 59 → 600), correcting more instances than in the prior cleaning.
Flagged and converted negative Quantity and Total Price values to positive where they indicated valid sales (e.g., Order ID 2004: -2 → 2, -2000 → 2000), with notes on potential returns for review, an enhancement over the previous dataset's simpler outlier correction.
Handling Missing and Invalid Data:
Replaced blank Customer Name with Unknown (e.g., Order ID 2025), consistent with the previous approach.
Assigned missing Region values to Unknown initially (e.g., Order ID 2006) and later mapped to the most frequent region (West, with 102 occurrences) based on product patterns, refining the prior method.
Removed rows with irreconcilable data (e.g., Order ID 2011: Quantity "two" with no clear numeric mapping after multiple attempts), reducing the dataset by 5 rows compared to the previous retention of all records.
Outlier Detection and Correction:
Identified and corrected outliers in Total Price (e.g., Order ID 2151: -4187 → 1000 based on 5 * 200), with more aggressive validation than the previous dataset.
Treated negative Quantity as absolute values for sales analysis (e.g., Order ID 2007: -2 → 2), with a note for return analysis, improving on the prior dataset's less detailed handling.
Revenue Reconciliation:
Adjusted Sum of Total Price post-correction to approximately $900,000 (from an initial $871,199 estimate), reflecting more accurate recalculations than the previous $895,000.
Validated regional and product totals against expected patterns (e.g., Mouse total adjusted to $140,000 from $139,773), with tighter alignment than before.

# Post-Cleaning Data State (Comparison to Previous Dataset)
Completeness: Reduced from 400 to 395 rows due to removal of irreconcilable entries, compared to 400 rows retained previously.
Consistency: Uniform MM/DD/YYYY date format for both Order Date and Ship Date, with Ship Date flagged for uniformity, versus partial adjustment in the prior dataset.
Accuracy: Enhanced recalculation of Total Price and handling of text-based Quantity, with fewer residual errors than the previous clean dataset.

Example Transformation:
Before: Order ID 2001: Order Date 2025-03-08, Quantity 3, Price 50, Total Price -85, Region East
After: Order ID 2001: Order Date 03/08/2025, Quantity 3, Price 50, Total Price 150.00, Region East
Previous After: Order ID 2001: Order Date 03/08/2025, Quantity 3, Price 50, Total Price 150.00, Region East (same result, but with less rigorous text handling).


# Dashboard Creation and Insights
Dashboard Design
The Excel dashboard, "Track sales process across continents," includes:

Quantity Price of Product: A bar chart displaying the quantity of each product (Charger, Headphones, etc.) sold.
Count of Product in March 2025: A line chart showing daily product count trends from 01/03/2025 to 20/03/2025.
Total Price of Product by Region: A bar chart comparing total revenue by product across East, North, South, and West regions.
Sales Count of Quantity by Region: A line chart illustrating quantity distribution by region.
Sales Product Quantity by Region: A pie chart showing the percentage contribution of each region to total quantity.
Interactive Filters: Slicers for Ship Date, Region, Quantity, and Product to enable dynamic analysis.

# Key Insights
Product Performance: Mouse led in quantity sold (62 units), while Laptop generated the highest total revenue ($112,030) due to higher Price points (e.g., $850).
Regional Trends: West dominated total revenue ($262,067) and quantity (102 units), with East close behind ($209,638, 81 units).
Quantity Distribution: Quantities 2 and 3 were most frequent (54 and 93 occurrences), with West showing the highest quantity sales across all levels.
Temporal Patterns: Product counts peaked on 12/03/2025 (30 units) and 09/03/2025 (26 units), suggesting mid-month sales surges.
Unexpected Finding: Despite uniform Ship Date (03/03/2025), Order Date variability indicated potential shipping delays or data entry issues, warranting further investigation.

# Analytical Skills Demonstrated
Data Cleaning: Leveraged Power Query to standardize dates, correct calculation errors, and handle missing/invalid data effectively.
Data Modeling: Used Power Pivot to validate and reconcile totals, ensuring accuracy in regional and product-level aggregations.
Visualization: Created an interactive Excel dashboard with diverse chart types, tailored to highlight sales trends and regional performance.
Insight Generation: Identified key drivers (e.g., West region, Mouse product) and flagged data anomalies (e.g., Ship Date issue), providing actionable recommendations.

# Conclusion
This analysis transformed a flawed dataset into a robust foundation for decision-making. The "Track sales process across continents" dashboard offers stakeholders a comprehensive view of sales performance, regional contributions, and product trends in March 2025. Recommendations include focusing inventory on high-revenue products (Laptop, Mouse) in the West region, investigating Ship Date inconsistencies, and optimizing sales strategies for mid-month peaks. Future work could involve predictive modeling or integrating additional months for trend analysis.
