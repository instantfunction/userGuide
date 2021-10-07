## How to take users request when invoking functions

Simply add
```
##INSTANTFUNCTION##  
```
to your code when you submit your code. When you invoke your function, for any type of request, instant function will replace   ##INSTANTFUNCTION##   with your request body. You can use this to pass variables to your function. Following the example above, you can make the following request (notice ##INSTANTFUNCTION## in your code)

```
curl --location --request POST 'https://instant-function.p.rapidapi.com/code' \
--header 'x-rapidapi-hos: instant-function.p.rapidapi.com' \
--header 'x-rapidapi-key: <your-key-here>' \
--header 'Content-Type: application/json' \
--data-raw 'import json

x = {
  "name": "John",
  "age": 30,
  "married": True,
  "divorced": False,
  "children": ("Ann","Billy"),
  ##INSTANTFUNCTION##  
  "pets": None,
  "cars": [
    {"model": "BMW 230", "mpg": 27.5},
    {"model": "Ford Edge", "mpg": 24.1}
  ]
}


print(json.dumps(x))
'
```

and when you invoke here's a sample request

```
curl --location --request POST 'https://instant-function.p.rapidapi.com/run/079b6e2e-8d12-460d-8a06-680e4cfdca2a' \
--header 'x-rapidapi-hos: instant-function.p.rapidapi.com' \
--header 'x-rapidapi-key: <your-key-here>' \
--data-raw '                "GlossEntry": {
                    "ID": "SGML",
					"SortAs": "SGML",
					"GlossTerm": "Standard Generalized Markup Language",
					"Acronym": "SGML",
					"Abbrev": "ISO 8879:1986",
					"GlossDef": {
                        "para": "A meta-markup language, used to create markup languages such as DocBook.",
						"GlossSeeAlso": ["GML", "XML"]
                    },
					"GlossSee": "markup"
                },'
```

It will take your request and add to the static response. Your response in this case will look like this 


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
    "GlossEntry": {
        "ID": "SGML",
        "SortAs": "SGML",
        "GlossTerm": "Standard Generalized Markup Language",
        "Acronym": "SGML",
        "Abbrev": "ISO 8879:1986",
        "GlossDef": {
            "para": "A meta-markup language, used to create markup languages such as DocBook.",
            "GlossSeeAlso": [
                "GML",
                "XML"
            ]
        },
        "GlossSee": "markup"
    },
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
