# Code Explanation
In this document i will describe the highlights of our code and try to make clear what they do. We have two parts to the project. A front-end and a back-end. 
They will be separated at first but further down in the document I will describe how they work together.

##### Table of Contents  
- [Front-End](#front-end)  
    - [Graph components](#graph-components)
    - [How to use Graph components](#how-to-use-graph-components)
    - [Call the API](#call-the-api)
- [Back-End](#back-end) 
    - [API Endpoint](#api-endpoint)
    - [Queries](#queries)

## Front-End
In our front-end we use Vue.js and mostly use it to create graphs and communicate to the back-end. 

### Graph components
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

### Call the API

## Back-End 

### API Endpoint
To see more in depth documentation about our API End-points, see [this](https://github.com/wocevv/Documentation/blob/main/api-documentation.md) page.

### Queries
