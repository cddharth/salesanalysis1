
# Awesome Chocolate Sales Analysis




## Table of Contents




    1. Problem Statement
    2. Cleaning and Pre processing Data
    3. Generating Visuals, Report and Insights provided
    4. Analysis on insights provided
    5. Appendix





## Problem Statement

This dashboard is the sales analysis of awesome choclate. It is a fictional company with sample sales data provided for their employees sales over a period of 1 year.

We have 2 csv files for our analysis actuals and target. Actuals contain data of the sales person sales from Aug-21 to Aug-22, no. of boxes sold, expenses occured on each sale and the category of product being sold. Furthermore we also have details of team each sales person belong to.

Target contains the detail of target for each employee for every month over a period of one year from Aug-21 to Aug-22.

This dashboard provide insights on some key factors such as sales by team, profit generated, sales over the year and forecasting future sales based on trend, variance from target and many more. This provide some amazing insights to high selling products, most profitable products and many more. Based on these data decison makers can take data driven decisions which further helps in company growth.


### Cleaning and pre processing data 

- step 1: Import data from the CSV files into Power BI from the get data button

- step 2: We need to transform data as we see a many to many relation in targets and actuals with respect to date and sales person
    
    Snap of dataset :-

    Actuals-
    ![image](https://github.com/user-attachments/assets/7f66c5de-772a-46fd-907e-18a394c69354)

    Target-
    ![image](https://github.com/user-attachments/assets/05160bfa-7967-4793-83a5-f7a75450c958)


- step 3: Open power query editor to transform data, first we clean  the data by removing any null values(if any), then we change the data types of the respective field

- step 4: I added and extra coloumn Month and created it by selecting the date coloumn then using the start of month button from the add coloumn option so that we get start of each month as an extra coloumn.

    Snap-
    ![image](https://github.com/user-attachments/assets/99b7db92-373f-4ba3-aecf-5095b6852e5d)



- step 5: Now we load the target CSV file into power query. We clean the data first.

- step 6: After cleaning I change data type for the currency, then we unpivot other coloumn based on sales person, so now we have 2 fields one date and the 2nd one as value.

    snap-

    before unpivoting-
    ![image](https://github.com/user-attachments/assets/e9b878b3-0e17-46a0-9cf3-0a642d1cce5f)

    after unpivoting-
    ![image](https://github.com/user-attachments/assets/28f779a9-081b-4756-8d3b-00bc9ac3930d)



- step 7: Added prefix "1-" to each value of the date coloumn so that it can be converted into date data type. Renamed the coloumn heading as Month and Target. Now we reference this table twice to create 2 dublicates so that we can introduce 2 dimension tables. Month and sales person each will contain unique values. So that we can introduce a 1 to many relation in the schema for convinient mapping
    
    snap -
    
    prefix add-
    ![image](https://github.com/user-attachments/assets/b61df4c3-cf75-498b-af52-093b1f1b178e)

    final table-
    ![image](https://github.com/user-attachments/assets/707d2e60-61c8-43f5-b7be-78086f1afecf)




- step 8: Go to the first reference table, select sales person coloumn and remove other coloumns. Now remove duplicates from the sales person coloumn. We name this dimension table as dSalesPerson.

    snap of dsalesperson-
    ![image](https://github.com/user-attachments/assets/e057ff99-bd7a-4cd6-82a3-56a574131573)



- step 9: Go to the second reference table, select Month coloumn and remove other coloumns. Now remove duplicates from the Month coloumn. We name this dimension table as dMonth.

    snap of dmonth-
    ![image](https://github.com/user-attachments/assets/6bc35645-4c25-432b-8ef8-732104817467)


- step 10: Now load the data as the required transformtion has been completed.

- step 11: Now we map the coloumn months in dmonths to the coloumn months in the table actuals and target to form one to many relationship.


- step 12: We introduce some new measures which will help in detailed analysis. The new measure which were introduced are listed below with their DAX expression.

    - Total Sales = SUM(actuals[Sales])

    - Total Expenses = sum(actuals[Expenses])

    - Total Boxes = SUM((actuals[Boxes]))

    - Total Target = SUM(targets[Target])

    -  Profit = [Total Sales] - [Total Expenses]

    - Profit per Box = DIVIDE([Profit], [Total Boxes], "No boxes Shipped")

    - Variance = [Total Sales] - [Total Target]

    - Variance % = DIVIDE([Variance], [Total Target])

    - No. of Products = DISTINCTCOUNT(actuals[Product])

    - Most Sold Product = 
        MAXX(
	        KEEPFILTERS(VALUES('actuals'[Sales])),
	        CALCULATE(MAX('actuals'[Product]))
        )

    
    snap of schema after introduction of new measures-
    ![image](https://github.com/user-attachments/assets/82310a95-52aa-4600-bd63-50d87aa446af)



### Generating Visuals, Report and Insights provided

Now since we have cleaned and processed our data we are now ready to generate some insights and answer to some of question based on our datasets. The report created is of 7 pages. I'll try to guide through each component used and the insights it is providing.

Page 1 is a brief overview with some charts, slicer and cards which will be explained in details later on.

From page 2 onwards I've tried to answer the following questions which were formed by me while analysing this dataset.

    1. Actual performance by product, person and team
    2. Variance analysis by person
    3. Who has most variance in each month
    4. which product has highest profit
    5. Forecast for next 3 months.....

- page 1: I've added 3 cards, a slicer, 4 charts and a gauge meter for the 1st page of the report.

    cards- Will provide information on total sales, total boxes shipped, No. of products and the average of sales

    slicer- added category of product as a filter so that we can sort data based on category

    charts- first chart is a coloumn chart which provide profits by product details, second chart is a clustered coloumn chart which provide information on the best performing team, 3rd chart is a line chart which provides profit by month forecasting 3 months into future. furth chart is a coloumn chart which provides insight on variance by team.

    Gauge- I also added profit as a gauge metric to analyze profit. As the entire dashboard is interactive we can filter the profit according to product, category and team.



    snap of Dashboard-
    ![image](https://github.com/user-attachments/assets/4da1ec69-a813-49ac-9451-fcb1f58fc52c)



- page 2: Gives insights on performance of product, we have two cards on top which gives specific details of the product which you can choose from the slicer.
Further breakdown of product performance we have a bar chart which provide details for sales person for the product. We have a coloumn chart which give perfomance of team for the product and we have a line chart for the sale of product  over the year forecasting 2 months of future sale


    snap of dashboard-
    ![image](https://github.com/user-attachments/assets/ec0caf36-41c8-4c0f-ba32-e597a0576b8d)



- page 3: Gives more insights on product performance, we have a table which lists all the products and how they have performed. I've also added two card with more product specific details. Also added a chart which tells how team has performed across the product

    snap of dashboard-
    ![image](https://github.com/user-attachments/assets/157080c7-5517-485e-8756-53bdb8300741)



- Page 4: Gives insight on Sales person performance. We have a table which lists all the sales person and their performance. We also have 2 bar charts showing sales and profit by sales person. We also have a coloumn chart showing their variance from target

    snap of dashboard-
    ![image](https://github.com/user-attachments/assets/187d60fa-c644-4984-b487-9473744d8d01)



- Page 5: Gives insights on variance of sales person. We have a table showing variance from target by every sales person. We can select the range of date for which we want our data from the slicer. Also we have two charts which gives sales and variance for the particular date range

    snap of dashboard-
    ![image](https://github.com/user-attachments/assets/7c275067-2450-4418-ae7c-e6a1435a3984)





### Analysis on insights provided

An overall sales of 22M was achieved while shipping a total of 1M boxes, we did a profit of 15M.

85% dark choco bars was the most profittable product, Orange Choco was the least

Yummies was the most profitable team, Karlen Mccafrey did the most sales while Roddy Speechley was the most profitable. Gunner CockShoot was the sales person with the highest variance

85% dark bars was the most profitsable item ($968,053), but milk bars had the most profit per box ($23.08), White Choc was the most sold product

Over the one year period we saw rise and fall in our sales, but we witnessed a steep rise in sales in the month of jul with sale peaking on aug 1. The trend line and forecast however suggest that this will not continue to increase and we may see decline in the coming 3 months.





## Appendix

The dataset is purely fictious and is used for analysis purpose, awesome chocolate is a made up company. Lot of hardwork and understanding was required to create this report. Hope you read through all of it and like it.

For any suggession and addition of any section feel free to reach out to -

sarkarsiddhartha14@gmail.com

Finally, thanks for taking the time to read through the report, hope you enjoy it.

Thanks,
Siddhartha









 
