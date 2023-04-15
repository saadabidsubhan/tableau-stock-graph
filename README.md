## tableau-stock-graph
A written tutorial on how to create an advanced tableau graph 
Stock Performance Graph

Number of worksheets: 3

 * Main worksheet
 
 * Candlestick 1 month
 
 * Candlestick 6 month

The calculations for this dashboard include:

*	1 date calculation

*	3 levels of delta calculations, 1 month, 6 month and 1 year deltas 

*	2 calculated fields for table calculations

<img width="105" alt="image" src="https://user-images.githubusercontent.com/116935049/232247134-e3732aa0-086f-4ece-85ec-bf27a1f204f6.png">


______________________________________________________________________________

### Date

Calculated field for date

 

Most recent trading day function created to be referenced in the calculations below.

<img width="240" alt="image" src="https://user-images.githubusercontent.com/116935049/232247174-72847c43-11a6-46db-97f3-b3982e55b171.png">


______________________________________________________________________________

### Subset 1
#### 1 Month Delta

<img width="246" alt="image" src="https://user-images.githubusercontent.com/116935049/232247194-a0bb3bee-3202-425e-9a25-fd23c80ed4cb.png">

<img width="247" alt="image" src="https://user-images.githubusercontent.com/116935049/232247199-74e525b5-d1f5-4b68-adf3-2e721ab578dc.png">

These calculated fields are placeholders used to create an axis. 

<img width="234" alt="image" src="https://user-images.githubusercontent.com/116935049/232247218-3246670e-50eb-4b11-8997-05901e9d77cc.png">

This is a fixed Level of Detail calculation on Company. This calculation is used to generate the up and down arrows in the table. The calculation is fixed on the company, which means that the aggregation in this calculation will be at the company level data. The calculation also used an ELSEIF statement to generate the arrows which are copied and pasted into the function “↑”. 

 <img width="232" alt="image" src="https://user-images.githubusercontent.com/116935049/232247225-8f24c766-bc91-45e3-b7fe-2cd5b9f9dfd3.png">

This is a Boolean statement used to generate the colors in the table, i.e., red, and green in the trend lines. This will be added to the marks card on the trend line axis which we will create. 

<img width="228" alt="image" src="https://user-images.githubusercontent.com/116935049/232247231-0c0836b9-da70-442d-a4dc-4ac615388c5a.png">

This date function will be used to generate the dates for the one-month trend axis. Using an IF statement we extract the minimum date from the most recent trading day using the DATEADD function and extracting the date a month in the past and maximum date from the most recent trading day.

 <img width="245" alt="image" src="https://user-images.githubusercontent.com/116935049/232247235-4af2b563-69f2-4bfc-a3be-547908624b43.png">

This statement checks if the [Date] field in the current row is equal to the minimum value of the [1 Month Trend Axis] field across the entire view (indicated by the curly braces around MIN([1 Month Trend Axis])). If the condition is true, the expression returns the value of the [Close] field in that row; otherwise, it returns null. The AVG() function is redundant in this calculation but valid as this calculation is used in the 1 Month Delta Sign calculation which is a fixed LOD calculation and accepts aggregate functions only. This is why we have to add the AVG() operator.

<img width="228" alt="image" src="https://user-images.githubusercontent.com/116935049/232247239-7e7d4cf1-67f6-48aa-8802-21e5e3a3c0d8.png">

Similarly, we are using the same functions mentioned above to calculate the 1 month delta of each stock. The AVG() operator is added to keep the calculation an aggregate. 

#### These are the functions needed to create the one-month delta. Duplicate these for the 6 month and 1 year delta respectively with the appropriate editions.

______________________________________________________________________________

### Values for table calculations

<img width="232" alt="image" src="https://user-images.githubusercontent.com/116935049/232247243-b467d513-039f-4b05-abde-a0993c6f3922.png">

This function calculates the minimum value of a conditional expression within a window or partition. The condition checks if the minimum value of the [Symbol] field within the window or partition is equal to the minimum value of the [Symbol] field across the entire data set, and returns 1 if true and 0 if false. This just means that wherever the symbol field is added the result will be 1. 

 <img width="242" alt="image" src="https://user-images.githubusercontent.com/116935049/232247259-2c17a326-e325-4188-884e-8be6ca0335e1.png">

This function is used to display the values for the trend axis. The function first checks if the size of the partition defined by the dimensions in the view is not equal to 1 (meaning there is more than one value in the partition), and if the value of the "WinMin Test" field is equal to 1. If both conditions are met, the function calculates a normalized trend line for the average close price of the stocks in the partition. Otherwise, it creates a mark in the middle of the Y Axis which will be where we place our symbols.
______________________________________________________________________________

### Adding rows and columns

 <img width="468" alt="image" src="https://user-images.githubusercontent.com/116935049/232247264-6026f39a-1164-4385-9f2a-2bdfd3316127.png">

For the rows shelf add:
*	Company 
*	Values. Create a custom table calculation to display the values of the trend lines by extracting values from each axis. 

<img width="160" alt="image" src="https://user-images.githubusercontent.com/116935049/232247285-410c0ecf-4dfc-4ec7-8a71-47860e3fb27f.png">

For the columns shelf add:
*	The logo
*	Stock and symbol
*	Latest day close price

*	1 month delta arrow
*	1 month delta axis
*	Both these fields will be combined and synchronized into a dual axis

*	1 month trend axis
*	1 month trend axis again. 
*	Both these fields will be combined and synchronized into a dual axis again. 

#### Repeat 1 month axis again for 6 month and 1 year trends. Hide all headers and grid lines for a clean display. 

 <img width="156" alt="image" src="https://user-images.githubusercontent.com/116935049/232247292-4f17ad70-1ec4-4ee3-bc55-62b0e3f72bd5.png">

#### Download the workbook and look at the values added to the marks card to output the correct display. For the trend axis, the first axis is selected as an area chart and the second is selected as a line chart to create the desired visual appearance. The axes are synchronized and therefore overlap each other.

______________________________________________________________________________

### Candlesticks

For the candlestick graphs I’m linking a YouTube video which will explain how to create them in sufficient detail. 

https://www.youtube.com/watch?v=ZcuXGiQWCTc&t=265s&ab_channel=AndyKriebel

You can link these sheets by adding them to the tooltip on the marks card for each delta axis so that it displays the sheets when you hover over that axis. 

