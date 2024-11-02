# Level 23 - Level 24

```
Username: natas24
Password: 0xzF30T9Av8lgXhW7slhFCIsVKAPyl2r
URL:      http://natas24.natas.labs.overthewire.org
```

## Overview

This time we got an input field and also a link to the source code.

<figure><img src="../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Anlysis

The application looks out for a URL parameter `passwd` and if it exists, it compares with the the `<censored>` string using PHP `strcmp` function, and if it satisfies the condition, it will show the credentials for the next level.

<figure><img src="../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

In the above PHP code block, the comparison is done using the `strcmp` function. This function is not array-aware, and it is designed for comparing two strings. When you pass an array to `strcmp`, it will treat the array as a string, resulting in unexpected behavior.

***

## Getting the Password

The problem here is that `strcmp` is expecting a string, but the value of "passwd" is an array (`passwd[]= ''`). When `strcmp` encounters an array, it treats it as a string, and the result might not be as expected. In this case, result will be `0` because the array is cast to a string, resulting in an empty string (`''`), and `strcmp` compares it with the other string (`'<censored>'`), which satisfies the condition and shows the credentials for the next level.

<figure><img src="../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>
