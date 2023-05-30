For our back-end we have made the decision to use a .NET Core REST API. This document will provide an overview of the endpoints used by our API aswell as briefly explain what a REST APi entails. 

## What is a REST API?
A REST API (Representational State Transfer Application Programming Interface) is a web service that enables interaction between different software systems over the internet. It follows the principles of REST, which is an architectural style for designing networked applications.
The concept behind a REST API is the representation of resources. Resources can be any kind of data or information that the API provides access to, such as user profiles, product listings, or blog posts.  REST APIs use the standard HTTP methods to communicate: 
1.	GET:
Retrieves a representation of a resource or a collection of resources. It is used for reading or fetching data from the API.

2.	POST:
Creates a new resource. It is used for submitting data to the API to be processed and stored.

3.	PUT: 
Updates an existing resource. It is used for modifying or replacing the entire resource with the new representation provided.

4.	PATCH:
Partially updates an existing resource. It is used for making specific modifications to the resource without replacing it entirely.

5.	DELETE: 
Removes a resource. It is used for deleting the specified resource. 

In addition to these HTTP methods, REST APIs also utilize the HTTP status codes to indicate the success or failure of a request. As an example, a successful request would return a status code of 200 (OK). A common one is the 404 (Not found) status code, indicating the resource you requested was not available. 

## API Endpoints
### GET Endpoints
#### /api/Widget/Datamodel
This endpoint is used to retrieve all the stored Datamodels as an ‘id-name’ couple. It returns a JSON list containing two values:
![Example](https://i.imgur.com/o3yrxJV.png)



#### /api/Widget/Brand
Similar to the Datamodel endpoint, this endpoint returns a JSON list as an ‘id-name’ couple. The difference between the two is data it returns. This endpoint retrieves the id and name from all available brands in the database.  

#### api/Widget/…/Properties
We have three endpoints that are categorized under …/Properties:
1.	/api/Widget/Datamodel/Properties
2.	/api/Widget/Brand/Properties
3.	/api/Widget/Product/Properties

All of these return a list of strings in a JSON format when called. They return the database column names from the table corresponding to the endpoint name. As an example, the /api/Widget/Datamodel/Properties returns the following:

![Example2](https://i.imgur.com/dnmR1me.png)
 

### POST Endpoint
#### /api/Widget
W.I.P. 
