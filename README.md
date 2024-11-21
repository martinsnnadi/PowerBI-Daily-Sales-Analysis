# PowerBI-Daily-Sales-Analysis
Daily Sales Analysis with Conditional Formatting and Monthly Slicer in PowerBI

Create a daily sales column chart with a monthly slicer, calculate average sales for selected months and color bars above average as green and below average as red, utilize a date table/calendar table for solution

Solution

•	I downloaded the Financial Sample Excel workbook data from Microsoft Learn. Although the data wasn’t exactly what I initially wanted, my goal was to use the first dataset I downloaded and make it work.
•	I imported this data into Power BI Desktop. The first thing I did was create a date table.

        Date Table = CALENDAR(MIN(financials[New Date]),MAX(financials[New Date]))

•	In my new date table, I created a Day column and a Month Name column in the “mmm” format.

        Month Number = MONTH('Date Table'[Date])
        New Day = DAY('Date Table'[Date])
        New Month = FORMAT('Date Table'[Date], "mmmm")
        New Year = YEAR('Date Table'[Date])

•	I noticed that the date data from the financial table only had “1” as the day for all date entries. For the visualization I wanted to create, I needed different days in the month.
•	To address this, I created a formula in Power Query to populate a New Day column with random numbers from 1 to 30.

        New Day = Number.RoundDown(Number.RandomBetween(1, 30))

•	I then created a New Date column in the financial sample workbook using the existing Year, Month, and New Day I created in the previous step.
•	Returning to step 3, I created the date table and established a relationship using the New Date column in the financial sample workbook and the Date column in the date table.
•	Next, I added a column chart to my Visualization pane and dragged New Day into the X-axis and Total Sales into the Y-axis.
•	I added a slicer and included the Month Name from the date table, formatting it as a dropdown so we can filter by month according to instructions.
•	I added a further analysis visual called Constant Line to show the average sales on the column chart.
•	Finally, I needed to color the bars above average as green and below average as red. To do this, I created a new measure called 

        Color bars = IF([Total Sales] >= [Avg Sales], "Above Average", "Below Average"), 

then applied conditional formatting to change the colors accordingly.

