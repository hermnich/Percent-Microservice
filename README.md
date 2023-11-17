# Percent-Microservice
This microservice will calculate the percent of a whole for the input paramters provided.
It takes in an object with an arbitrary amount of numerical input parameters, along with a numerical total that is the whole that it will calculate the percentages of.
It returns an object containing the same input parameters with their calculated percentage values.

### Requesting Data
Requesting data is done by sending a POST request to the localhost port that the service is running on at the address /percent. A query parameter is added to the end of the request that specifies the total to be used. The body of the request should be a single JSON object that contains only name/value pairs of the data that you want calculated. The names of these parameters can be anything, as long as it is valid JSON. The values must be non negative numeric values.
For example, here is a valid request from the test-requests file. 
```
POST http://localhost:4000/percent?total=50 HTTP/1.1
content-type: application/json

{
    "param1": 4.4,
    "param2": 3,
    "param3": 1
}
```
More examples of requests can be found in test-requests.http. If you are using VS code, these requests can be run directly by using the REST Client extension.
In javascript, the same request would look something like:
```
const total = 50;
parameters = {
    "param1": 4.4,
    "param2": 3,
    "param3": 1
}
const response = await fetch(`/percent?total=${total}`, {
    method: 'POST',
    body: JSON.stringify(parameters),
    headers: {
        'Content-Type': 'application/json',
    },
});
```

### Receiving Data
Results will be returned in the same format that they were sent, as a JSON object connected to the HTTP response. For the example above, this object should look like:
```
{
  "param1": 8.8,
  "param2": 6,
  "param3": 2
}
```
A successful request will return with a response status of '200'. If the request fails in any way, the status will be '400'. 
To get the results data object in javascript something like the following can be used after a response has been received.
```
let percentages;
if (response.status === 200) {
    percentages = await response.json();
}
```