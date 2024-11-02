# Level 14 - Level 15

```
Username: natas15
Password: TTkaI7AWG4iDERztBcEyKV7kRXH1EZRB
URL:      http://natas15.natas.labs.overthewire.org
```

## Overview

This time we got an input field, which checks whether the given username exists and also we got the link to the source code.

<figure><img src="../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code.

<figure><img src="../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

The input field is vulnerable to SQL Injection and also from the source code, we can identify the current database name and table name as `natas15` and `users` respectively.

***

## Testing SQL Injection

I first checked whether the SQL injection works by using the same payload that we used in the last level.

<div>

<figure><img src="../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

</div>

Next I just gave `"` as the payload, looking out for clues in error thrown in the response, but no details were disclosed in the error.

<div>

<figure><img src="../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

</div>

***

## Getting the Password

Since, no details were disclosed, we have to check for blind and time based SQL injection. So, I captured the request using burpsuite and saved the request to a file to test the input field with sqlmap.

<div>

<figure><img src="../.gitbook/assets/image (113).png" alt="" width="563"><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (114).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

From the results of sqlmap, we can see that the input field is vulnerable to boolean-based blind SQL injection. Since we know the current database name and the table name, I directly dumped the table, in which the password for the next level is present.

<div>

<figure><img src="../.gitbook/assets/image (116).png" alt="" width="563"><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (117).png" alt="" width="359"><figcaption></figcaption></figure>

</div>
