## [Interacting with APIs to import data from the web](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2)

In this chapter, you will gain a deeper understanding of how to import data from the web. You will learn the basics of extracting data from APIs, gain insight on the importance of APIs, and practice extracting data by diving into the OMDB and Library of Congress APIs.

<br>

### [Pop quiz: What exactly is a JSON?](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=2)

```
Q:Which of the following is NOT true of the JSON file format?
A:The function json.load() will load the JSON into Python as a list.
```

### [Loading and exploring a JSON](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=3)

```
# Load JSON: json_data
with open("a_movie.json") as json_file:
    json_data = json.load(json_file)

# Print each key-value pair in json_data
for k in json_data.keys():
    print(k + ': ', json_data[k])
```

### [Pop quiz: Exploring your JSON](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=4)

```
Q: Which of the following statements is true of the movie in question?
A: The title is 'The Social Network' and the year is 2010.
```

### [Pop quiz: What's an API?](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=6)

```
Q: Which of the following statements about APIs is NOT true?
A: All APIs transmit data only in the JSON file format.
```

### [API requests](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=7)

```
# Import requests package
import requests

# Assign URL to variable: url
url = 'http://www.omdbapi.com/?apikey=72bc447a&t=the+social+network'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Print the text of the response
print(r.text)
```

### [JSON–from the web to Python](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=8)

```
# Import package
import requests

# Assign URL to variable: url
url = 'http://www.omdbapi.com/?apikey=72bc447a&t=social+network'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Decode the JSON data into a dictionary: json_data
json_data = r.json()

# Print each key-value pair in json_data
for k in json_data.keys():
    print(k + ': ', json_data[k])

```

### [Checking out the Wikipedia API](https://campus.datacamp.com/courses/intermediate-importing-data-in-python/interacting-with-apis-to-import-data-from-the-web-2?ex=9)

```
# Import package
import requests

# Assign URL to variable: url
url = 'https://en.wikipedia.org/w/api.php?action=query&prop=extracts&format=json&exintro=&titles=pizza'

# Package the request, send the request and catch the response: r
r = requests.get(url)

# Decode the JSON data into a dictionary: json_data
json_data = r.json()

# Print the Wikipedia page extract
pizza_extract = json_data['query']['pages']['24768']['extract']
print(pizza_extract)
```