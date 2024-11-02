# Level 20 - Level 21

```
Username: natas21
Password: 89OWrTkGmiLZLv12JY4tLj2c4FW0xn56
URL:      http://natas21.natas.labs.overthewire.org
```

## Overview

In this level, we have got a page with a link to another website and also a link to the source code.

<figure><img src="../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

On visiting the website mentioned in the above page, its a css style experimenter application, which also a had link referring to the above page and a link to the source code of the css style app.

<figure><img src="../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code of the first page. The page is looking out for the admin key with a value of 1 in the session file. If the key is present in the session, it shows the credentials for the next level.

<figure><img src="../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

Now let's take a look at the source code of the experimenter website. The page looks out for a URL parameter `debug` and if its present, it displays the session contents. Also, there is an array named `validkeys`, which has the default key and values.

<figure><img src="../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>

The for each loop in the above source code checks whether if the key already exists in the session, and if it exists it updates the key value with the given value, else it creates a key with the given value.

<figure><img src="../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure>

From my understanding till now, both of the above mentioned websites shares / uses the same session files, which means both websites uses same session values.

***

## Testing the Application

I tried a GET request with the debug parameter, it showed an empty array.

<figure><img src="../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

Next, I tried submitting the form and captured the request using burpsuite, and requested with the `debug=true` parameter, which had the session values in its response. In the response, you can see that the value for debug is set as true.

<figure><img src="../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

***

## Getting the Password

Since we know that the for each loop will create session values, if its not present in the session already, I tried adding `admin=1` value to the request body and sent the request, You can see that the response for the request contains the `admin=1` in the session contents which is displayed by the debug feature.

<figure><img src="../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

Since, we have added the `admin=1` value to the session, if we try to login to the first website with this session, we can get the credentials for the next level. To do that, copy the value of the `PHPSESSID` from the above request and replace the `PHPSESSID` value present in the first website as shown below and refresh the webpage to get the credentials for the next level.

<figure><img src="../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>
