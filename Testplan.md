
# Testplan

## TC01
Description: User creates a bar graph that shows the monthly product count from the laptop datamodels between 12/06/2020 – 12/06/2023.<br>
Input:<br>
GraphType:        Bar,<br>
DataOption:       Product,<br>
DataCategory:        Datamodel,<br>
DataId:            Laptop,<br>
DataGrouper:        created_at,<br>
DataFilter:        count,<br>
DateStart:        12/06/2020,<br>
DateEnd:        12/06/2023,<br>
DateGrouper:        Month<br>

Output:<br>
A list is returned with the requested values and put in a bar-chart. The bars are grouped by month. 

## TC02
Description: The user wants to create a chart that shows the monthly products count from the L’Oréal brand between 24/04/2020 – 24/04/2023. <br>
Input:<br>
GraphType:       Bar ,<br>
DataOption:      Product,<br>
DataCategory:       Brand,<br>
DataId:      L’Oréal,<br>
DataGrouper:       created_at,<br>
DataFilter:      count,<br>
DateStart:     12/06/2023,<br>
DateEnd:   12/06/2020,<br>
DateGrouper:   Month<br>

Output:<br>
A list is returned with no values and no graph is made as the dates were incorrect.
