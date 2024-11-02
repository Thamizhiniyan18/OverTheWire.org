# Level 22 - Level 23

```
Username: natas23
Password: qjA8cOoKFTzJhtV0Fzvt92fgvxVnVRBj
URL:      http://natas23.natas.labs.overthewire.org
```

## Overview

This we got an input requesting for a password and a link to the source code.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code. The application is looking out for the URL parameter `passwd`, if it exists it checks whether it contains the substring `iloveyou` and also it checks whether the numerical value of `passwd` is greater than 10. If both of the conditions are statisfied, it shows the credentials for the next level.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

The condition `$_REQUEST["passwd"] > 10` involves comparing a string to an integer. In PHP, when such a comparison occurs using the `greater than (>)` operator, PHP attempts to convert the string to a number. If the string begins with a valid numeric value, it undergoes conversion; otherwise, it is treated as `0`.

For example, if `$_REQUEST["passwd"]` is set to `"iloveyou123"`, the string `"iloveyou123"` will be converted to `0` when compared to `10`. Consequently, the condition evaluates as `false`.

***

## Getting the Password

To satisfy both the condition `$_REQUEST["passwd"] > 10` and the additional condition `strstr($_REQUEST["passwd"], "iloveyou")`, you can create a password that starts with a numeric value greater than `10`. For instance, a password like `"11iloveyou"` meets these conditions. When comparing this password to `10`, PHP converts it to the numeric value `11`. As a result, the condition `$_REQUEST["passwd"] > 10` evaluates to `true`. Additionally, the password contains the substring `"iloveyou,"` fulfilling the requirements for both conditions and granting access to the credentials for the next level.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
