# A Complete Guide to the Python Requests Library

[![Bright Data Promo](https://github.com/luminati-io/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.com/)

This tutorial demonstrates ways to work with the Requests library in Python for web scraping:

- [Introduction to the Requests Library](#introduction-to-the-requests-library)
- [HTTP Methods](#http-methods)
- [Breaking Down a Response Object From Requests](#breaking-down-a-response-object-from-requests)
- [Request Customization With the Python Requests Library](#request-customization-with-the-python-requests-library)
- [Other Configurations](#other-configurations)

## Introduction to the Requests Library

[`Requests`](https://github.com/psf/requests) is a straightforward and user-friendly HTTP toolkit for Python. In detail, it provides an intuitive API for making HTTP requests and handling responses in an easy and easy to understand way. With over [50k stars on GitHub](https://github.com/psf/requests) and millions of daily downloads, Requests represents the most popular HTTP client in Python.

Some of the key features offered by this library include a comprehensive API covering all HTTP methods, dealing with server replies, request customization, login mechanisms, handling secure certificates, and more. On top of that, the Python Requests module supports [HTTP/1.1](https://datatracker.ietf.org/doc/html/rfc2616) out of the box.

### Setting up

The easiest and recommended way to install Requests is through `pip`. In particular, the `pip` package associated with the Requests library is `requests`. So, you can install the HTTP client with the following command:

```sh
pip install requests
```

To use `requests` in your Python script, import it with the line below:

```python
import requests
```

Awesome! The Requests package is now installed and ready to be used.

### Use Cases

The main use cases of the Python `requests` library include:

- **Making HTTP requests to web servers**: Retrieve data from web servers by sending GET requests.
- **Consuming APIs**: Send requests to API endpoints and handle their responses, interacting with various web services and accessing their data.
- **Web scraping**: Fetch HTML documents associated with web pages, which can then be [parsed using libraries like `BeautifulSoup`](https://brightdata.com/blog/how-tos/beautiful-soup-web-scraping) for extracting specific information.
- **Testing web applications**: Simulate HTTP requests and verify the responses, automating the testing process and ensuring the proper functioning of web services.
- **Downloading files**: Retrieve files from web servers, such as images, documents, or other media files, by sending HTTP `GET` requests to the respective URLs.

**Methods**

Take a look at the public methods exposed by the `requests` library in the following table:

|     |     |
| --- | --- |
| **Method** | **Description** |
| [`requests.request()`](https://requests.readthedocs.io/en/latest/api/#requests.request) | Sends a custom HTTP request with the specified method to the given URL |
| [`requests.get()`](https://requests.readthedocs.io/en/latest/api/#requests.get) | Sends a `GET` request to the specified URL |
| [`requests.post()`](https://requests.readthedocs.io/en/latest/api/#requests.post) | Sends a `POST` request to the specified URL |
| [`requests.put()`](https://requests.readthedocs.io/en/latest/api/#requests.put) | Sends a `PUT` request to the specified URL |
| [`requests.patch()`](https://requests.readthedocs.io/en/latest/api/#requests.patch) | Sends a `PATCH` request to the specified URL |
| [`requests.delete()`](https://requests.readthedocs.io/en/latest/api/#requests.delete) | Sends a `DELETE` request to the specified URL |
| [`requests.head()`](https://requests.readthedocs.io/en/latest/api/#requests.head) | Sends a `HEAD` request to the specified URL |

These cover the most useful HTTP request methods. Find out more about how to use them in the [official API documentation](https://requests.readthedocs.io/en/latest/api/).

## HTTP Methods

See the `requests` Python library in action when dealing with the `GET`, `POST`, `PUT`, `DELETE`, and `HEAD` methods in HTTP.

### GET

In HTTP, the [`GET`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) method is used to request a specific resource from a server. This is how you can make an HTTP `GET` request with `requests.get()`:

```python
import requests

# send a GET request to the specified URL

response = requests.get('https://api.example.com/data')
```

You can achieve the same result with `requests.request()` as below:

```python
import requests

response = requests.request('GET', 'https://api.example.com/data')
```

In this case, you manually have to specify the HTTP method to use with an additional string variable.

### POST

The HTTP `POST` method is used to submit data to a server for further processing. Here is how to make a `POST` request with `requests.post()`:

```python
import requests

# data to be sent in the POST request

product = {

'name': 'Limitor 500',

'description': 'The Limitor 500 is a high-performance electronic device designed to regulate power consumption in industrial settings. It offers advanced features such as real-time monitoring, adjustable settings, and remote access for efficient energy management.',

'price': 199.99,

'manufacturer': 'TechCorp Inc.',

'category': 'Electronics',

'availability': 'In Stock'

}

# send a POST request to the specified URL

response = requests.post('https://api.example.com/product', data=product)
```

Compared to a `GET` request, this time you also have to specify the data to send to the server through the `data` option. `requests` will add this data to the body of the HTTP request.

For JSON bodies, pass your data object to the `json` option instead of `data`:

```python
response = requests.post('https://api.example.com/product', json=product)
```

Equivalently, you can perform the same request with `request.request()` as follows:

```python
import requests

product = {

'name': 'Limitor 500',

'description': 'The Limitor 500 is a high-performance electronic device designed to regulate power consumption in industrial settings. It offers advanced features such as real-time monitoring, adjustable settings, and remote access for efficient energy management.',

'price': 199.99,

'manufacturer': 'TechCorp Inc.',

'category': 'Electronics',

'availability': 'In Stock'

}

response = requests.request('POST', 'https://api.example.com/product', data=product)
```

### PUT

The [`PUT`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) method is used to update or replace a resource on the server. Sending a `PUT` request with the Python `requests` module is easy and follows a similar pattern as in POST requests. What changes is that the method to use is `requests.put()`. Also, the HTTP method string in `requests.request()` will be `'PUT'`.

### PATCH

The [`PATCH`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) method is used to apply partial modifications to an online resource. Just like for `PUT` requests, sending `PATCH` requests in the Python `requests` library is similar to POST requests. What changes is that the method to employ is `requests.patch()` and the HTTP method string in `requests.request()` is `'PATCH'`.

### DELETE

The [`DELETE`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) method is used to delete a resource identified by a given URI. This is how to make an HTTP `DELETE` request in `requests` using the `delete()` method:

```python
import requests

# send a DELETE request for the product with id = 75

response = requests.delete('https://api.example.com/products/75')
```

Equivalently, you can perform a DELETE request with `requests.request()`:

```python
import requests

response = requests.request('DELETE', 'https://api.example.com/products/75')
```

### HEAD

The [`HEAD`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/HEAD) method is similar to `GET`, but it only requests the headers of the response, without the actual body content. So, the response returned by the server for a `HEAD` request will be equivalent to that of a `GET` request, but with no body data.

Use `requests.head()` to make an HTTP `HEAD` request in Python:

```python
import requests

# send a HEAD request to the specified URL

response = requests.head('https://api.example.com/resource')
```

In the same way, you can perform a `HEAD` request with `requests.request()`:

```python
import requests

response = requests.request('HEAD', 'https://api.example.com/resource')
```

## Breaking Down a Response Object From Requests

Let's see how to deal with response objects.

### Response Object

After making an HTTP request, `requests` will receive the response from the server and map it into a special [Response](https://requests.readthedocs.io/en/latest/api/#requests.Response) object.

Take a look at the Python `requests` example below:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

print(response)
```

This will return:

```python
<Response [200]>
```

`response` is a `Response` object that exposes some useful methods and properties. Explore the most important ones in the next sections!

> **Warning**:
> `requests` do not always return a response. In case of errors (e.g., an invalid URL), it raises a `RequestException`. Protect against this exception with the logic below:

```python
try:

response = requests.get('http://lumtest.com/myip.json')

# handle the response

except requests.exceptions.RequestException as e:

print('An error occurred during the request:', e)
```

### Status Codes

[Response status codes](https://brightdata.com/blog/proxy-101/proxy-error-codes) are standardized values returned by the server to indicate the success, failure, or any other condition of the request.

They are particularly helpful in error handling, allowing the client to identify and handle different types of errors appropriately. For example, a `4xx` status code indicates a client-side error (e.g., an invalid request), while a `5xx` status code indicates a server-side error.

Controlling the status code is generally the first step in handling a response in Python using the `requests` library. After making a request, you should always check the status code of the response to determine if the request was successful or not. Access the status code via the `status_code` attribute of the response object:

```python
response.status_code # 200
```

Depending on the status code received, you should use conditional instructions to handle different scenarios appropriately:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

# check if the request was successful (status code 200)

if response.status_code == 200:

print('Successful request!')

# handle the response...

elif response.status_code == 404:

print('Resource not found!')

else:

print(f'Request failed with status code: {response.status_code}')
```

In most scenarios, you only need to distinguish between a successful request and an error response. `requests` simplifies that process thanks to a custom [`__bool()__`](https://www.pythontutorial.net/python-oop/python-__bool__/) overload. Specifically, you can use a `Response` object directly in a conditional expression. That will evaluate `True` if the status code is between `200` and `399`, `False` otherwise.

In other words, it is possible to check the successful outcome of a request with this logic:

```
if response:

print('Successful request!')

# handle the response...

else:

print(f'Request failed with status code: {response.status_code}')
```

### Response Headers

Access the headers of a server response through the `headers` attribute:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

response_headers = response.headers

print(response_headers)
```

This will print:

```
{'Server': 'nginx', 'Date': 'Thu, 09 May 2024 12:51:08 GMT', 'Content-Type': 'application/json; charset=utf-8', 'Content-Length': '279', 'Connection': 'keep-alive', 'Cache-Control': 'no-store', 'Access-Control-Allow-Origin': '*'}
```

As you can see, `response.headers` returns a dictionary-like object. That means you can access header values by key. For example, assume you want to access the `Content-Type` header of the response. Below is how you can do it:

```python
response_headers['Content-Type'] # 'application/json; charset=utf-8'
```

Since the HTTP specification defines headers as case-insensitive, `requests` enables you to access them without worrying about their capitalization:

```python
response_headers['content-type'] # 'application/json; charset=utf-8'
```

### Response Content

`requests` provides different attributes and methods to access the payload of a response:

- [`response.content`](https://requests.readthedocs.io/en/latest/api/#requests.Response.content): Returns the content of the response in bytes.
- [`response.text`](https://requests.readthedocs.io/en/latest/api/#requests.Response.text): Returns the content of the response as a string in Unicode.
- [`response.json()`](https://requests.readthedocs.io/en/latest/api/#requests.Response.json): Returns the JSON-encoded content of the response in a dictionary.

See them in action in the following example:

```python
import requests

response = requests.get('http://lumtest.com/myip.json')

# access the response as bytes

response_bytes = response.content

print(type(response_bytes))

print(response_bytes)

print()

# retrieve the response as text

response_text = response.text

print(type(response_text))

print(response_text)

print()

# retrieve the response as a JSON-encoded dictionary

response_json = response.json()

print(type(response_json))

print(response_json)

print()
```

`http://lumtest.com/myip.json` is a special endpoint that returns information about the IP of the caller. The result of the above snippet will be something like:

```json
<class 'bytes'>

b'{"ip":"45.85.135.110","country":"US","asn":{"asnum":62240,"org_name":"Clouvider Limited"},"geo":{"city":"Ashburn","region":"VA","region_name":"Virginia","postal_code":"20149","latitude":39.0469,"longitude":-77.4903,"tz":"America/New_York","lum_city":"ashburn","lum_region":"va"}}'

<class 'str'>

{"ip":"45.85.135.110","country":"US","asn":{"asnum":62240,"org_name":"Clouvider Limited"},"geo":{"city":"Ashburn","region":"VA","region_name":"Virginia","postal_code":"20149","latitude":39.0469,"longitude":-77.4903,"tz":"America/New_York","lum_city":"ashburn","lum_region":"va"}}

<class 'dict'>

{'ip': '45.85.135.110', 'country': 'US', 'asn': {'asnum': 62240, 'org_name': 'Clouvider Limited'}, 'geo': {'city': 'Ashburn', 'region': 'VA', 'region_name': 'Virginia', 'postal_code': '20149', 'latitude': 39.0469, 'longitude': -77.4903, 'tz': 'America/New_York', 'lum_city': 'ashburn', 'lum_region': 'va'}}
```

Note the three different response formats. As a dictionary, `response.json()` is particularly useful because it simplifies data access:

```python
response_json['country'] # 'US'
```

For more information, check out our guide on [how to parse JSON in Python](/blog/how-tos/parse-json-data-with-python).

### Response Cookies

While [HTTP cookies](/blog/web-data/http-cookies) are defined via headers, the `Response` object provides a special `cookies` attribute to deal with them. This returns an [http.cookiejar](https://docs.python.org/3/library/http.cookiejar.html) object with the cookies the server sent back.

Take a look at the example below demonstrating how to access cookies from a response object in the Python `requests` library:

```python
import requests

# define the login credentials

credentials = {

'username': 'example_user',

'password': 'example_password'

}

# send a POST request to the login endpoint

response = requests.post('https://www.example.com/login', data=credentials)

# access the cookies set by the server

cookies = response.cookies

# print the cookies received from the server

for cookie in cookies:

print(cookie.name, ':', cookie.value)
```

The sample snippet above may produce something like this:

```
session_id : be400765483cf840dfbbd39

user_id : 7164

expires : Sat, 01 Jan 2025 14:30:00 GMT
```

## Request Customization With the Python Requests Library

HTTP requests often involve special filtering parameters and custom headers. Let’s see how to specify them in `requests`.

### Query String Parameters

[Query parameters](https://www.semrush.com/blog/url-parameters/), also known as URL parameters, are additional parameters appended to the end of a URL in an HTTP request. They provide extra information to the server about the request, usually on how to filter data and customize the response.

Consider this URL:

`https://api.example.com/data?key1=value1&key2=value2`

In this example, `?key1=value1&key2=value2` is the query string while `key1` and `key2` are query parameters.

A query string starts with `?` and consists of a key-value pair separated by an equal sign (`=`) and concatenated by `&`. Programmatically specifying this query string in Python code is not always easy, especially when dealing with optional parameters. That is why `requests` offers the `params` option:

```python
import requests

# define query parameters as a dictionary

params = {

'page': 1,

'limit': 10,

'category': 'electronics'

}

# send a GET request to the following URL:

# 'https://api.example.com/products?page=1&limit=10&category=electronics'

response = requests.get('https://api.example.com/products', params=params)
```

Equivalently, you can pass the parameters to `requests` as a list of tuples:

```python
import requests

# define query parameters as a list of tuples

params = [

('page', '1'),

('limit', '10'),

('category', 'electronics')

]

response = requests.get('https://api.example.com/products', params=params)
```

Or as a `bytes` string:

```python
import requests

# define query parameters as a bytes string

params = b'page=1&limit=10&category=electronics'

response = requests.get('https://api.example.com/products', params=params)
```

### Request Headers

To customize the headers in an HTTP request in `requests`, pass them as a dictionary to the `headers` option. For example, you can set a custom `User-Agent` string in `requests` with:

```python
import requests

# define custom headers

custom_headers = {

'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36',

# other headers...

}

# send a GET request with custom headers

response = requests.get('https://api.example.com/data', headers=custom_headers)
```

### Request Cookies

While HTTP cookies are sent to the server via headers, `requests` provides a dedicated `cookies` option to customize them. Use it as in the following example:

```python
# define custom cookies

custom_cookies = {

'session_id': 'be400765483cf840dfbbd39',

'user_id': '7164'

}

# send a GET request with custom cookies

response = requests.get('https://www.example.com', cookies=custom_cookies)
```

Note that `cookies` accepts a dictionary or an `http.cookiejar` object.

## Other Configurations

`request` offers a rich API and there are many advanced techniques available. Explore some of the most relevant ones!

### Proxy Setup

Proxy integration in `requests` enables you to route your HTTP requests through a proxy server. This is a powerful mechanism to hide your IP address, bypass rate limiters, or access geo-restricted content.

You can integrate a proxy server with the Python `requests` library by using the `proxies` option:

```python
import requests

# define the proxy settings

proxy = {

'http': 'http://username:[email protected]:8080',

'https': 'https://username:[email protected]:8080'

}

# Make a request using the proxy

response = requests.get('https://www.example.com', proxies=proxy)
```

For a complete tutorial, follow our guide to [using a proxy with Python Requests](/blog/proxy-101/proxy-with-python-requests).

### Basic Authentication

[HTTP login mechanisms](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication), better known as “basic login mechanisms,” is a simple login mechanisms scheme built into the HTTP protocol. It involves sending a username and password encoded in [Base64](https://developer.mozilla.org/en-US/docs/Glossary/Base64) format in the `Authorization` header.

Although you could implement it by manually setting the `Authorization` header, `requests` exposes a dedicated `auth` option for it. This accepts a tuple with the username and password. Use it to deal with basic login mechanisms in the `requests` Python library:

```python
import requests

# define the username and password for basic login mechanisms

username = 'sample_username'

password = 'sample_password'

# send a GET request with basic login mechanisms

response = requests.get('https://api.example.com/private/users', auth=(username, password))
```

### SSL Certificate Verification

SSL certificate verification is crucial for ensuring secure communication between clients and servers over the Internet. At the same time, there are situations when you trust the destination server and do not need to enforce verification.

In particular, when routing HTTP traffic through proxy servers, you may encounter errors related to SSL certificates. In this case, you might need to disable SSL certificate verification. In `requests`, that is possible via the [`verify`](https://requests.readthedocs.io/en/latest/user/advanced/#ssl-cert-verification) option:

```python
import requests

# send a GET request to a website with SSL certificate verification disabled

response = requests.get('https://api.example.com/data', verify=False)
```

### Timeouts

By default, requests automatically waits indefinitely for the server to respond. If the server is experiencing an overload or there is a network slowdown, that behavior can become a problem.

To avoid slowing down your application while waiting for a response that may never arrive, `requests` has a [`timeout`](https://requests.readthedocs.io/en/latest/user/advanced/#timeouts) option. This accepts an integer or floating number representing the number of seconds to wait for a response:

```python
import requests

# timeout after 2 second

response1 = requests.get("https://api.example.com/data", timeout=2)
```

Alternatively, `timeout` accepts a tuple with two elements: connect timeout and read timeout. Specify them as in the example below:

```python
import requests

# timeout after 2.5 seconds for connections and 4 seconds for reading response

response = requests.get("https://api.example.com/data", timeout=(2.5, 4))
```

If the request establishes a connection within the specified connect timeout and receives data within the read timeout, the response will be returned as usual. Otherwise, if the request times out, a `Timeout` exception will be raised:

```python
import requests

from requests.exceptions import Timeout

try:

response = requests.get("https://api.example.com/data", timeout=(2.5, 4))

except Timeout:

print("The request timed out")
```

## Conclusion

The Python `requests` module is a useful and popular HTTP library that covers several use cases. However, any HTTP request exposes your public IP. This provides information about who you are and where you live, which is not good for your privacy.

There are several ways to hide your IP address, and the most effective way to achieve greater security and privacy is to use a proxy server. Bright Data controls the best [proxy servers](https://brightdata.com/proxy-types) in the world, serving Fortune 500 companies and more than 20,000 customers.

Register and start a free trial today!