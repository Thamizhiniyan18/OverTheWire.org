# Level 13 - Level 14

```
Username: natas14
Password: qPazSJBmrmU7UQJv17MHk1PGC4DxZMEP
URL:      http://natas14.natas.labs.overthewire.org
```

## Overview

This time a login form, with a link to the source code.

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code.

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

By just viewing the source code, we can find that its vulnerable to SQL Injection, since the parameters are directly substituted in the SQL query.&#x20;

We can bypass the login by using a simple payload: `" OR 1 = 1 -- -`, and we get the password for the next level.

<div>

<figure><img src="../.gitbook/assets/image (79).png" alt="" width="477"><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (80).png" alt="" width="470"><figcaption></figcaption></figure>

</div>
