
#Testplan

## TC01
Description: User creates a bar graph that shows the monthly product count from the laptop datamodels between 12/06/2020 – 12/06/2023.
Input)
GraphType        Bar 
DataOption        Product
DataCategory        Datamodel
DataId            Laptop
DataGrouper        created_at
DataFilter        count
DateStart        12/06/2020
DateEnd        12/06/2023.
DateGrouper        Month

Output
A list is returned with the requested values and put in a bar-chart. The bars are grouped by month. 

## TC02
Description: The user wants to create a chart that shows the monthly products count from the L’Oréal brand between 24/04/2020 – 24/04/2023. 
Input
GraphType        Bar 
DataOption        Product
DataCategory        Brand
DataId            L’Oréal
DataGrouper        created_at
DataFilter        count
DateStart        12/06/2023
DateEnd        12/06/2020.
DateGrouper        Month

Output
A list is returned with no values and no graph is made as the dates were incorrect.
