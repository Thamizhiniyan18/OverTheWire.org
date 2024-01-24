# Level 21 - Level 22

```
Username: natas22
Password: 91awVM9oDiUGm33JdzM7RVLBS8bz9n0s
URL:      http://natas22.natas.labs.overthewire.org
```

## Overview

This time we got an empty page with a link to the source code.

<figure><img src="../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code. The first code block of the application looks out for the URL parameter `revelio` from a GET request and if it exists it checks whether the session contains the key-value pair `admin=1` and if so it sets the header `Location: /`.

<figure><img src="../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

The second code block of the application looks out for the URL parameter `revelio` from a GET request and if exists it shows the credentials for the next level.

***

## Getting the Password

I tried a GET request in the browser with the URL parameter `revelio`, which responded with a empty page.

<figure><img src="../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

I checked the burp HTTP history to get insights on what happend. You can see that the request got redirected and we got an empty page as a result. But the response for the GET request with the URL parameter `revelio` is recorded in the burp HTTP history, which contains the credentials for the next level.

<figure><img src="../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>
