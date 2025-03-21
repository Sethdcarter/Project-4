# Project-4

### Prezi Presentation Link:
* https://prezi.com/view/SvaRVUz2DZ2iQBWQtYPS/

<br><br>

### Dataset To Be Used:
* Online Sales Dataset - Online Shopping Patterns and Retail Performance Dataset
    * Number of Records: 49,782
    * Dates: 1/1/2020 - 9/5/2025
    * Columns: InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country, Discount, PaymentMethod, ShippingCost, Category, SalesChannel, ReturnStatus, ShipmentProvider, WarehouseLocation, OrderPriority

<br><br>

### Project Description Outline:

The goal of our project is to develop a model that forecasts future consumer online purchases based on online shopping data. We will investigate various key factors that influence purchasing decisions, including the relationships between payment methods, the impact of discounts on sales, and purchase trends across different countries overtime. Additionally, we will explore other relevant patterns within the data to uncover valuable insights that can help businesses optimize their sales strategies and anticipate customer behavior.

<br><br>

### Questions To Answer With The Data:
* Is there a trend in the monthly sales over time?
* Which countries had the highest number of sales?
* Which categories had the highest number of sales?
* Is it possible to predict what someone will buy?
* What items get returned the most?

<br><br>

### Tasks:
# ADD IN TASKS AND HOW WE DID THEM
<br>

1. **Data Ingestion & Preparation**
   * **CSV File Loading:**
      * Imported the original dataset (`shopping_data.csv`) using Python and Pandas.
      * Verified the file’s encoding, delimiter, and header structure to ensure a clean import.
   * **Data Cleaning:**
      * **Handling Missing Values:** Identified missing entries in both numeric and categorical columns.
         * Filled numeric columns with mean values to maintain consistent distributions.
         * Filled categorical columns with the mode (most frequent category) to preserve logical groupings.
      * **Date Parsing:** Converted `InvoiceDate` (and `order_date` if applicable) to datetime format, dropping rows with invalid dates.
      * **Stripping Text Columns:** Removed leading/trailing spaces in columns like `ReturnStatus` to avoid inconsistent matches (e.g., `"Returned "` vs. `"Returned"`).

2. **Data Standardization & Normalization**
   * **Feature Selection:**
      * Determined which numeric columns were appropriate for scaling (e.g., `Quantity`, `UnitPrice`, `Discount`, `ShippingCost`), excluding ID-like columns.
   * **Standardization:**
      * Employed `StandardScaler` to transform features to have mean 0 and standard deviation 1, useful for algorithms sensitive to feature scales.
   * **Normalization:**
      * Used `MinMaxScaler` to rescale the same numeric columns to the [0, 1] range, which can benefit models like KNN or neural networks.

3. **Initial Explorations & Visualizations**
   * **Histograms & Correlation Matrix:**
      * Generated histograms for numeric columns to understand their distributions.
      * Created a correlation matrix heatmap to reveal any strong relationships among features (e.g., whether `Quantity` correlates with `TotalSales`).
   * **Trend Analysis:**
      * Computed total sales by month (`TotalSales = Quantity * UnitPrice * (1 - Discount)`) and plotted a time series to observe how sales changed over the dataset’s timeframe.
      * Noted a modest upward trend in monthly sales (roughly \$600k–\$700k), but with significant month-to-month fluctuations.
   * **Boxplots & Scatter Plots:**
      * Created boxplots to visualize the distribution of discounts across order priorities.
      * Used scatter plots to examine potential relationships (e.g., `Quantity` vs. `ShippingCost`).

4. **Storing Processed Data**
   * **Data Integration:**
      * Converted any date periods to strings (if needed) to ensure compatibility with SQLite.
      * Saved the standardized and normalized DataFrames to a local SQLite database (`sales_data.db`) for further analysis and ML modeling.

5. **Create ML models**

6. **Create ML model visualizations**

<br><br>

### Findings:
# ADD IN OBSERVATIONS AND GRAPHS
Maching Learning Model Classification Report:

![Classification Report](https://github.com/user-attachments/assets/2e7c991c-c2fa-4533-a7d6-61256656a5f6)

