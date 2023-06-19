# Usability test
Creating widgets is the main purpose of our project. The purpose of the tests we let people make was to see them go through the flow of creating a widget. 
We gave the testers an assignment and recorded the screen to follow the movement. During the test we took some notes on their process and some issues we saw ourselves. 

## Assignment 1 
Create a graph that counts products from the laptop datamodel grouped by their owner_id between two dates. 

### Tester 1 - Kubi
#### Notes
For this test I made a small error at the start. I showed the page that does not show the “Add Widget” button from the get-go. This caused confusion as the tester could not find the correct button. 
After clicking around he eventually found it. Unfortunately, Kubi was not able to complete the assignment as intended. The idea was to select Products and afterwards select the laptop datamodel as your category. 
Kubi instead chose datamodels as your data option resulting in not being able to select laptops. He did still pick owner_id and count. 

#### Errors
1. Line graph is still an option in the ‘select graph type’ dropdown. 
2. After selecting ‘Datamodels’ as your Data Option, Category is greyed out and shows ‘Please choose Dataoption first’. 


### Tester 2 - Bryan
#### Notes
For this test I did put the website on the correct site. Because of this, it did not require the tester as much time as the previous tester. He did mention afterwards it was unclear the ‘Add Widget’ button was an actual button. 
Some functionality that changes the colour of the button when you hover it would clear this up. Bryan picked line diagram from the chart type. At the time of the test, this was not a working chart type. 
We shouldn’t have made that an option if it doesn’t work. He also chose the same option as Kubi, picking Datamodel as your data option. The other options he did fill in correctly. 
Because he picked line diagram though, a chart was not able to be created. 

#### Errors
1. Same as previous test.
2. No colour on the ‘add widget’ button.
 

### Tester 3 - Evalynn
#### Notes
Evalynn was the only tester to complete the assingment as we had hoped. She started out picking line graph which does not work but also was not mentioned in the assignment. Besides that, she picked the option products selecting laptops datamodel later on. The only issue we had here was selecting a date range that had no data. She made the distance between start and end-date around 2 weeks. 

#### Errors
1. Picked line graph again; removed it after the test.
2. Date's were not far enough apart to get data. 

### Tester 4 - Daan
#### Notes
Like the first two testers, Daan had picked datamodel instead of products. We are unsure if this mistake is due to bad UX design or the assignment being unclear. Furthermore, Daan also forgot to select one of the input fields. Since we have no error validation, leaving one of the boxes open and clicking create widget still makes the post request. This resulted in a 500 error and obviously no widget. 

#### Errors
1. Forgot to fill in one of the boxes resulting in an 500 error. 
