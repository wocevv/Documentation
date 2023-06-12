# Code Explanation
In this document i will describe the highlights of our code and try to make clear what they do. We have two parts to the project. A front-end and a back-end. 
They will be separated at first but further down in the document I will describe how they work together.

##### Table of Contents  
- [Front-End](#front-end)  
    - [Graph component](#graph-component)
    - [How to use Graph components](#how-to-use-graph-components)
    - [Call the API](#call-the-api)
- [Back-End](#back-end) 
    - [API Endpoint](#api-endpoint)
    - [Queries](#queries)

## Front-End
In our front-end we use Vue.js and mostly use it to create graphs and communicate to the back-end. 

### Graph component
We started with importing the necessary dependencies:
```vue
    import { Bar } from 'vue-chartjs'
    import { Chart as ChartJS, Colors, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
```
We use the Chart.js charting library to create our Graphs. Find more information [here](https://www.chartjs.org/docs/latest/).

After importing the dependencies, we need to register the components and plugins:
```vue
    ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
    ChartJS.register(Colors)
```
Here we tell the code what parts of ChartJS we want to use.

Next come the component properties. 
There are many different properties for the Vue component. The ones we use are:<br/>
<br/>**Name:**
```vue
        name: 'BarChart',
```
With name you describe the name of the component. This is used internally by Vue for debugging and defining components.

<br/>**Components:**
```vue
        components: { Bar },
```
The components property defines the props that the current component uses. In this case it uses the Bar component inported from from Chart.js. It is responsible for rendering the bar chart.

<br/>**Props:**
```vue
        props: {
            widgetdata: {
                type: Array,
            },
            testValue: {
                type: Number,
            }
        },
```
The props property defines the props that the current component accepts. Props allow parent components to pass data to child components. 
In this instance we have the prop widgetdata which represents the data that will be displayed in the chart. We also have the prop testValue and it is used to determine the orientation of the chart(X-axis or Y-axis)

<br/>**Data:**
```vue
        data() {
            return {
                chartData: {
                    labels: labelArray,
                    datasets: [
                        {
                            data: dataArray,
                            label: 'ProductCount'
                        }
                    ]
                },
                chartOptions: {
                    responsive: true,
                    indexAxis: 'y',
                    scales: {
                        x: {
                            beginAtZero: true
                        },
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            }
        },
```
The property data is not defined as an object but as a function. By doing this it allows each instance of the current component to have its own independent copu of the data properties, preventing any unintended sharing or interference between instances.
This property returns an object that contains the components data properties.
In this case it returns an object with the properties chartData and chartOptions. chartData for the data within the chart and chartOptions for the orientation of the chart(X-axis or Y-axis).

<br/>**Watch:**
```vue
        watch: {
            widgetdata: {
                handler(newVal) {
                    this.updateChartData(newVal)
                },
                immediate: true
            },
            testValue: {
                handler(newVal) {
                    this.updateChartOptions(newVal)
                },
                immediate: true
            }
        },
```
The watch property defines watchers for the props. Watchers allow the components to reactively respond to changes in the props values. 
For both widgetdata and testValue that means that they update the chart's options based on the new prop value.

<br/>**Methods:**
```vue
        methods: {
            updateChartOptions(testValue) {
                if (testValue === 1) {
                    this.chartOptions.indexAxis = 'x'
                } else if (testValue === 2) {
                    this.chartOptions.indexAxis = 'y'
                    // Swap the x and y scales
                    this.chartOptions.scales.x = { beginAtZero: true }
                    this.chartOptions.scales.y = { beginAtZero: true }
                }
            },
            updateChartData(data) {
                labelArray.length = 0
                dataArray.length = 0

                for (const item of data) {
                    labelArray.push(item.group)
                    dataArray.push(item.value)
                }

                this.chartData.labels = labelArray
                this.chartData.datasets[0].data = dataArray
            }
        }
```
The methods property contains the methods used within the current component. Methods are functions that can be called within the component's context. 
The updateChartOptions method updates the chartOptions property based on the provided testValue. It determines the orientation of the chart and uptdates the corresponding options.
The updateChartData method updates the chartData property based on the provided widgetdata. It extracts the labels and data values from the prop and updates the corresponding properties of the chartData object.

### How to use Graph components
First import the component you want to use. We want to use the bargraph so we inport it like:
```vue
    import bargraphtest from '../../src/components/Bargraph.vue'
```

Then when we want to use this component, in the ```html <template> ``` part of the page we use a HTML object with the import like this:
```html
        <bargraphtest :widgetdata="widgetdata" :testValue="TestValue"></bargraphtest>
```
Widgetdata is a ```vue const widgetdata = ref([]) ``` initiated at the top of the file. Its value is filled with the response value of an API.

### Call the API
To get the data for a graph you need to call an API that will get you the right data. For the dropdowns where you can select what data the graph will show are also API calls.
The ones for the dropdowns are all getters while the ones for getting the right data are all posts.
Lets say we want to get all the properties to go into the dropdown to select all the brand groupby values, you can call the following API like this:
```vue
                    const res = await fetch("https://localhost:5001/api/Widget/Brands/Properties");
                    const finalRes = await res.json();
                    this.Listgroupby = finalRes
                    listgroupby.value = finalRes;
```
This way all the brand properties go into the right array.

The API call for getting the data to show in a graph looks a bit different. Like this:
```vue
        const queryParams = new URLSearchParams(requestData);
                axios
                    .post(`https://localhost:5001/api/widget/ApiModelTest2?${queryParams.toString()}`)
                    .then((response) => {
                        widgetdata.value = response.data;
                        console.log(widgetdata);
                        TestValue = 1
                    })
                    .catch((error) => {
                        console.error(error);
                    });
```
https://localhost:5001/api/widget/ApiModelTest2 is the endpoint to the API where you get the data from that fills the graph.
With ```vue const queryParams = new URLSearchParams(requestData); ``` you create the searchparam with the data revieved from the dropdowns.
The response of the API is where the returned data is recieved. You can see we fill the value of widgetdata with the data in the response.

## Back-End 

### API Endpoint
To see more in depth documentation about our API End-points, see [this](https://github.com/wocevv/Documentation/blob/main/api-documentation.md) page.

### Queries
For the connection to the database we have decided to use raw SQL queries. We use a postgresql database so some functions may be only for postgresql.
These are all the Database methods we have:

- Get*PerGrouper    X2
    - GetDatamodelsPerGrouper
    - GetBrandsPerGrouper
    - GetProductsPerGrouper
- ReadAllPropertyNames
- ReadAll*Names
    - ReadAllDatamodelNames
    - ReadAllBrandNames
- ReadAllProducts

For the Get*perGrouper method we needed two variants, one for grouping by date and the other for the other possibilities. We did this because the date query lhas a different way of grouping and delivers datetime variables as a result.
These are the different queries for these methods:
```c#
string.Format("SELECT DATE_TRUNC(@dateGrouper,{0}) AS created_to_specificDate, {1}(id) AS count FROM products WHERE {0} IS NOT NULL AND {2}_id = @datacategoryid AND created_at BETWEEN @startdate AND @enddate GROUP BY DATE_TRUNC(@dateGrouper,{0})", Grouper, action, lowerDataCategory);
```
In this one we have the date has the ``` DATE_TRUNC()``` funtion. This function is used to select sertain parts of a date. It uses 2 parametes, in the first you define what kind of timestamp(millisencond, month, year, etc) and second you select what date you to use it on, the way we did it it is selected on the column you have selcted(created_at, deleted_at, etc). We group by this item so you can get the first to latest in order.

```c#
string.Format("SELECT {0}, {1}(id) FROM products WHERE {0} IS NOT NULL AND {2}_id = @datacategoryid AND created_at BETWEEN @startdate AND @enddate GROUP BY {0}", groupColumnName, action, lowerDataCategory);
```
You can also group by something that is not a date. To be able to do this we have this second query. it selects one of the other columns to group by.

In both queries we use the string.format(). This we do so that we can call direct columns in the queries. When you add to a query with a parameter like below it is added as a variable. This way a column cant be adressed. 
```c#
    cmd.Parameters.AddWithValue("datacategoryid", DataCategoryID); 
``` 
The string.format() takes multiple parameters, the first being the query and the ones after being the values you want in the query. To add these values to the query you define them with {} and a number to the corresponding parameter. This starts at 0 and continues opwards. 




