# POWER-BI-Power-BI-Assignment-1-
## Data Transformation and Data Modeling 
### E-Commerce Sales Analysis 
              This assignment will help you explore e-commerce sales data analysis using Power BI. Below are the files you will be working with (click on each to download): 
★ List of Orders.csv 
★ Order Details.csv 
★ Sales target.csv
In this exercise, you will leverage Power BI's capabilities to import, transform, model, and analyze the provided data.
 Instructions:- 
Import Data: 
● Import “List of Orders.csv” into Power BI. 
               ● Open Power BI and using get data option from Home tab import the file “List of Orders.csv”
               ● Open “List of Orders” in Power Query Editor by clicking on ‘Transform’.
               ● Import “Order Details.csv” and “Sales target.csv” into Power Query Editor by using “New source “option from File Tab
# Data Transformation:
## ● Restrict the "List of Orders" table to only the first 500 rows.
                                  Home Tab | Keep rows| Keep top rows|500
## ● Ensure the “Order Date” column in the “List of Orders” table is set to data type 'Date'.
            Select the “Order Date” column in the “List of Orders” table and is set to data type 'Date' Format.
## ●Change the data type of “Amount” and “Target” columns to ‘Fixed Decimal Number’.
                        Change the data type of “Amount” in Order details table is set to data type decimal format and “Target” columns in sales target table is set to data type ‘Fixed Decimal Number’.
## ●Format the "Customer Name" column into proper case, ensuring consistent capitalization for each word.
                                   Add column| Custom column | formula: Text.proper([CustomerNames])
                                   Using Text.proper function modified Customer Name" column into proper case, ensuring consistent capitalization for each word and rename as “Customer_Name_Mod”
## ● Merge the "State" and "City" columns to create a new column named "Location" in the format ‘City, State’.
                         1)Select two column: Using “CTRL” | Transform tab| Merge Column | separator: comma| Merged.
                         2)Rename column as “Location”
## *●Create a new custom column named "Profit Margin" as the percentage of "Profit" divided by "Amount".*
1.	Go to Add Column → Custom Column.
2.	Enter Profit Margin as the new column name.
3.	Use this formula:
                     if [Amount] = 0 then null else [Profit] / [Amount]
4.	Convert the created Profit Margin Column set to “round “and data type as percentage.
## 	●Add a new conditional column named "Profit Status" based on the values in the "Profit" column. The conditions are as follows: if the profit is less than 0, the label should be "Loss"; if the profit equals 0, the label should be "Break-Even"; and if the profit is greater than 0, the label should be "Profit".
                                     Add Column| Custom Column| Rename Column as Profit Status
                Here I use conditional formula:
                                              If [Profit]<0 then "Loss" else if [Profit]=0 then "Break-Even" else "Profit") 
# Merging Data (Joins):
 ## ● Merge the "List of Orders" and "Order Details" tables into a new single table named "Orders Data" based on the "Order ID" relationship
1.	Click Home → Transform data to open Power Query Editor.
2.	Select List of Orders from the left-side Queries pane.
3.	Go to Home → Merge Queries → Merge Queries as New.
4.	In the merge window:
o	First table: List of Orders
o	Second table: Order Details
5.	Click Order ID in List of Orders.
6.	Click Order ID in Order Details.
7.	For Join kind, select Left Outer (all from first, matching from second).
8.	Click OK.
9.	A new query will appear. Rename it Orders Data.
10.	You'll see a new column containing Table values. Click the expand (↔) button in that column.
11.	Select the columns from Order Details that you want to add.
12.	Click OK.
13.	Finally, click Home → Close & Apply.
# Handling Missing Data & Duplicate Data:
  ## ● Identify missing values in the data and determine a strategy to address them. 
                                    1)Using filter method, or creating calculated column like by using measures and Coalesce function, we can fill value in numerical data
                                    2)Check nulls/blanks → Fix missing values → Remove true duplicates → Check errors
                                    3)By using replace as a value method we can rectify.
### Check for Errors
In Power Query, check columns for errors:
Home → Keep Rows → Keep Errors
This lets you inspect problematic rows before deciding whether to fix or remove them.

## ● Check for duplicate rows and define a strategy to handle duplicates.
 Remove duplicate records:
1.	Select the column(s) that should uniquely identify the record.
2.	For example, select Order ID.
3.	Go to Home → Remove Rows → Remove Duplicates.
### Important: *If Order ID appears multiple times because one order contains multiple products, do not remove duplicates using Order ID alone. In that case, select a combination such as Order ID + Product.*
# Sorting and Filtering Data: 
  ## ● In the ‘Orders Data’ table, utilize sorting and filtering techniques on columns like Order Date, State or Category to analyze data based on specific criteria: 
               ◆ Sort the orders by Order Date in descending order to analyze recent trends.  
	                     #Select your Orders Data table.
	                     #Find the Order Date column.
	                     #Click the drop-down arrow on Order Date.
	                     #Select Sort Descending.

               ◆ Filter the orders to focus only on a specific state (e.g., Tamil Nadu) for regional analysis.
                       Here I already done the "State" and "City" columns to merge and create a new column named "Location" in the format ‘City, State’.
So In this case I create an duplicate column of Location and using split to column option to separate State and city, Then filtered the text “Tamil Nadu.”
  # Grouping and Aggregating Data:     
## ● Duplicate the “Order Details” table and calculate the count of each Order ID, average profit by Category or total amount by Sub-Category. 
                                   Duplicate “Order Detail” and Renamed as “Order Detail Summary”
 ### Count each Order ID
    In the duplicated table:
                              Select Order ID.
                              Go to Home → Group By.
                              In the Group By window:
                                              o	by: Group Order ID
                                              o	New column name: Order Count
                                              o	Operation: Count Rows

### Average Profit by Category
                Make another Duplicate Orders Data and Named “Order Summary 2”
1.	Select “Order Summary 2 “ table
2.	Select Home → Group By.
3.	Choose Advanced.
4.	Set:
                      o	Group by: Category
                      o	New column name: Average Profit
                      o	Operation: Average
                      o	Column: Profit
5.	Click OK.
                                              
## ● Duplicate the “Sales Target” table and aggregate the total target amount by Month of Order Date.
                       Make a duplicate of ‘Sales Target” table and renamed as Monthly sales target
1.	Select Home → Group By.
2.	Select Advanced.
3.	Set:
               o	Group by: Month of Order Date
               o	New column name: Total _target_ Amount
               o	Operation: Sum
               o	Column: Target Amount
4. Click 
# Data Modeling: 
## ● Establish a relationship between the “List of Orders” and “Order Details” tables using the ‘Order ID’ column. 
1.	Go to Model view 
2.	Click Manage relationships from the top ribbon.
3.	Click New.
4.	Set the relationship as:

  ### Create the relationship using:
•	Table: List of Orders
•	Column: Order ID
•	Related table: Order Details
•	Column: Order ID

                                                                                      
## ● Build a relationship between the “Order Details” and “Sales Target” tables based on the ‘Category’ column. Click "Manage relationships" and ensure this relationship is active.
	Go to Model view 
	Click Manage relationships from the top ribbon.
	Click New.
	Set the relationship as:
### First table
       o	Table: Order Details
       o	Column: Category
 ### Second table
       o	Table: Sales Target
       o	Column: Category
	For Cardinality, select Many to many (:) 
	For Cross-filter direction:-“Both” is commonly used for a many-to-many relationship




