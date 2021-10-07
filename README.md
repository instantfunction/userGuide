# Welcome to instant function   

Instant Function helps you to test your ideas and develop your code easily. Enter your code and your api is immediately ready to use from your application, command line, browser or any network protocol tool that can make an API call (curl, POSTMAN etc). You can build apps or websites that use instant functions as back end. Instant Function manages everything so you can focus on your ideas. 

## How it works
Instant function runs on the cloud, we handle servers, scaling, making your api publicly accessible basically anything that lets you quickly develop your code and run it on the cloud. There is no servers, provisioning, dealing with api gateway settings, deploying containers. It also doesn't require (like AWS lambda) to use a specific framework or modify your controllers to handle a type of request. Simply upload your code and you are ready to go. We will keep your code in our database. You can configure to accept any type of request, simple or complex data structures etc. (we don't keep your request in our database) Once you run your code, instant function will simply return what you print back. You can print in JSON format or in any format. 

### Compilers and supported languages
Instant function supports more than 100 programming languages / versions. It also supports high-level programming languages or computing environments that run on linux and that is open sourced, such as R, Julia, Octave. With this version we are only allowing python 3.9 and its base libraries. With each release we will support more compilers. 

## How to use

I will enter more examples and tutorials but here's the gist of it.
You provide your code. We will persist your code in our database and provide you a unqiue id. You invoke instant function with unique id and we will run your code. All the data you print in the code will return from instant function. Note, by default we will persist your code for one year and time it out at the end. But everytime you use your code we will reset the 1 year period so if you are continously using your function it should not easily expire.

### Step 1:
Submit your code. Your code should run in the compiler you pick and it should print the response you'd like to have from your code. However, it can be a simple method or can have multiple classes / methods. As long as it runs in the compiler environment you choose you should be fine. Here's a simple python code that returns a static json response

```
import json

x = {
  "name": "John",
  "age": 30,
  "married": True,
  "divorced": False,
  "children": ("Ann","Billy"),
  "pets": None,
  "cars": [
    {"model": "BMW 230", "mpg": 27.5},
    {"model": "Ford Edge", "mpg": 24.1}
  ]
}


print(json.dumps(x))
```

We need to POST this to codeBlock endpoint which is
```
/codeblock2
```
endpoint.

In essence our request looks like this 
```
curl --location --request POST 'https://instant-function.p.rapidapi.com/code' \
--header 'x-rapidapi-hos: instant-function.p.rapidapi.com' \
--header 'x-rapidapi-key: <your-key>' \
--header 'Content-Type: application/json' \
--data-raw 'import json

x = {
  "name": "John",
  "age": 30,
  "married": True,
  "divorced": False,
  "children": ("Ann","Billy"),
  "pets": None,
  "cars": [
    {"model": "BMW 230", "mpg": 27.5},
    {"model": "Ford Edge", "mpg": 24.1}
  ]
}


print(json.dumps(x))
'
```

If everything goes well, you'll see a response in the following format..
```
{
    "codeId": "7cf82f25-addd-41f8-8462-16e3ca01fa9d"
}
```
Not down your url (codeId). You are done now.

### Step 2:
Use the id from step 1, invoke instant function. At this step you need to call another endpoint with your codeId. You can use POST, PUT, GET, PATCH requests

Simply make a requst to this endpoint
```
run/{use-your-codeId}
```

In essence your request will look like this

```
curl --location --request POST 'https://instant-function.p.rapidapi.com/run/079b6e2e-8d12-460d-8a06-680e4cfdca2a' \
--header 'x-rapidapi-hos: instant-function.p.rapidapi.com' \
--header 'x-rapidapi-key: <your-key>' \
--data-raw ''
```

You can use the sample code id. You should get a response back 

```
{
    "name": "John",
    "age": 30,
    "married": true,
    "divorced": false,
    "children": [
        "Ann",
        "Billy"
    ],
    "pets": null,
    "cars": [
        {
            "model": "BMW 230",
            "mpg": 27.5
        },
        {
            "model": "Ford Edge",
            "mpg": 24.1
        }
    ]
}
```

## More Basic Tutorials
Instant function lets you process clients' data as well (the request payload when they invoke instant functions). 
This tutorial shows how to use clients data

https://github.com/instantfunction/userGuide/blob/main/processingUserRequest.md#how-to-take-users-request-when-invoking-functions



## What can you do with instant function?

### Test Ideas Quickly
* If you are a front end developer, don't wait for backend to be ready, create a simple function that is good enough for development and get going
* If you are a backnd developer, don't wait for downstream services to be ready (or don't be blocked if they are down) use instant function and get going
* Simulate various cases such as adding a variety of response types, http status codes or simulating server errors and latencies.

### Use Instant Function as A Back End
* Use it as your back end. Take advantage of various programming languages and libraries such as scipy or R packages to enhance your user interface.

### Develop Tools and Share with Others
* Share your function with team mates to help others more effectively develop software. 
* Develop tools such as text formatters, automatic code generators, json generators use your own and share with the team

### Take advantage of an environment / stack that you aren't using
* Take advantage of functionalities of various stacks available in instant function (call a machine learning library in python from your front end code or backend java code etc.)
