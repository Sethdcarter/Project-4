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

   
   * **Data Preprocessing:**
   
      *The dataset (online_sales_dataset.csv) is loaded into a pandas DataFrame.
      *The InvoiceDate is converted to datetime format.
      *A new column TotalSales is calculated by multiplying Quantity, UnitPrice, and applying the Discount.
   
  * **Customer's Last Purchase Information:**
   
      *The latest purchase date for each customer is calculated using groupby on CustomerID.
      *This date is merged into the dataset to create a new column, LastPurchaseDate.
   
  * **Active Status Calculation:**
   
      *The threshold date is set to 90 days before the most recent purchase date.
      *Customers whose last purchase is older than the threshold are labeled as inactive (0), and those whose last purchase is within the last 90 days are marked as active (1).
   
  * **Feature Engineering:**
   
      *New customer-level features are aggregated, such as:
         *total_spent: Total money spent by the customer.
         *purchase_count: Number of unique purchases made by the customer.
         *avg_discount: Average discount the customer received.
      *These features are merged with the Active status.
   
  * **Model Training:**
   
      *The dataset is split into training and test sets (80%/20%).
      *A Logistic Regression model is trained to predict the Active status of a customer.
      *The model is evaluated using classification report and confusion matrix.
   
  * **Model Evaluation:**
   
      *The model's performance is shown in a classification report, which provides precision, recall, f1-score, and support for each class (active vs inactive).
      *The confusion matrix is also printed to show true positives, false positives, true negatives, and false negatives.
   
   
7. **Create ML model visualizations**

   * **Learning Curve:**
     
      *The learning curve is plotted, showing the accuracy of the model for different training set sizes.

<br><br>

### Findings:
# ADD IN OBSERVATIONS AND GRAPHS

<br>

* **Total Sales Trench Over Time**
   * **Slight Upward Trend:** The red regression line has a gentle positive slope, indicating that overall monthly total sales are increasing over time, although the increase is modest
   * **Significant Fluctuations Month-to-Month:** The blue markers (actual sales) vary notably above and below the regression line. This suggests other factors—seasonality, promotions, economic shifts, etc.—may influence sales in individual months
   * **Overall Range of Sales:** Most data points hover roughly between 600,000 and 700,000 in total sales each month. The data doesn’t show a dramatic or sustained dip/rise outside this band
   * **Volatility vs. Trend:** While the trend line shows a gradual increase, the actual sales often spike or drop in ways that a simple linear model doesn’t fully capture, which indicates that month-to-month variations may be driven by complex factors beyond a basic linear pattern
   ![image](https://github.com/user-attachments/assets/f2234a44-b6f2-48a9-90ba-1a68878865ce)

* **Discount Distribution by Order Priority**
   * All three categories appear to have a relatively similar median discount, but there are numerous high-discount outliers across each priority
   * “Low” priority orders might have a slightly higher median discount than “Medium” or “High,” or vice versa—interpret based on the actual positions of the median lines
   * The wide range of outliers suggests that, while most orders receive modest discounts, a subset of orders in each priority category receive much larger discounts
   ![image](https://github.com/user-attachments/assets/0b103262-1303-4da4-84e7-73e6987d6201)

* **Returned vs. Sold Quantity**
   * **Similar Sold Quantities Across Items:** Most items appear to have a sold quantity in a relatively narrow range (roughly 80k–100k). No single product drastically outperforms or underperforms the others in terms of total sales.
   * **Returned Quantities Are Consistently Close:** Returned quantities also cluster within a narrow band (about 12k–14k). None of the items shows a notably high or low return count compared to the rest.
   * **Uniform Return-to-Sales Ratio:** Because both sold and returned values are close across all items, the return rate (returned ÷ sold) seems fairly consistent. There isn’t a clear outlier with a disproportionately high or low return rate.
   * **Potentially Synthetic or Highly Uniform Data:** The tight grouping for both sold and returned quantities might indicate a synthetic dataset or one where each product line sees similar performance. In real-world scenarios, you often see more variation among products.
   * **No Clear “Problem” Product:** Since returned quantities are all in a similar range, there isn’t a single product that stands out as having an unusually large number of returns. If you were looking for items with high return issues, you might need to investigate further or compare the return rate specifically.
   ![image](https://github.com/user-attachments/assets/f807fbd2-60bd-40d2-ac38-d3c071a7edc4)

* **Items by Return Rate**
   * The bar chart shows Notebook has the highest return rate, while Desk Lamp is on the lower end.
   * Overall, return rates across items range within a few percentage points, suggesting there’s no single extreme outlier.
   * **Takeaway:** Returns are relatively evenly distributed among products, though certain items (e.g., Notebook) see a slightly higher proportion of returns.
   ![image](https://github.com/user-attachments/assets/299f5e5c-fb47-4f37-9153-c46fa4e2d93e)

* **Average Discount by Country**
  * Netherlands and Germany offer the highest average discounts, while Sweden and the United States are at the lower end.
   * The differences among countries could reflect varying promotional strategies, tax rules, or localized pricing policies.
   * **Takeaway:** Geographical pricing differences exist, with some European markets applying more aggressive discounts than others.
   ![image](https://github.com/user-attachments/assets/3f6706c2-b953-45ce-bddb-2fa4afe8d3c8)


* **Average Shipping Cost by Category**
   * Electronics has the highest average shipping cost, closely followed by Stationery and Furniture.
   * Accessories is the least expensive to ship, likely due to smaller or lighter products.
   * **Takeaway:** Heavier or more fragile product categories (like electronics or large furniture items) incur higher shipping costs, while smaller items cost less.
   ![image](https://github.com/user-attachments/assets/a4204703-27ad-4436-b1d5-bf4c5a51cbfd)

* **Average Shipping Cost by Order Priority**
   * High priority orders show a slightly higher shipping cost, consistent with expedited shipping or premium handling fees.
   * Low and Medium priority orders are cheaper, though the difference across priorities is not large.
   * **Takeaway:** While shipping cost does rise for higher-priority orders, the gap is not dramatically large, suggesting only moderate upcharges for faster service.
   ![image](https://github.com/user-attachments/assets/9758a256-8da3-4861-a3db-206a8dc12bec)

* **Overall Conclusions**
   * **Sales & Returns:** Items and countries show modest variations, with some items (like Notebook) having slightly higher return rates, and some countries (like the Netherlands) applying higher discounts.
   * **Correlations:** Only Quantity and TotalSales stand out, confirming that total revenue depends partly on volume. Discount is negatively correlated with total sales, but not strongly.
   * **Shipping Behavior:** Shipping costs are more influenced by product category and order priority than by quantity alone, and certain categories (e.g., Electronics) are notably more expensive to ship.

<br>


Maching Learning Model Classification Report:

![Classification Report](https://github.com/user-attachments/assets/2e7c991c-c2fa-4533-a7d6-61256656a5f6)

