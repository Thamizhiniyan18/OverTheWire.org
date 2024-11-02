# Level 9 - Level 10

```
Username: natas10
Password: D44EcsFkLxPIkAAKLosx8z3hxX1Z4MCE
URL:      http://natas10.natas.labs.overthewire.org
```

## Overview

Again an input field with a link to the source code.

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

This time,  the source code logic contains input validation using Regular Expression.

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

Breaking down the RegExp pattern:

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

This time also, the input field is vulnerable to command injection, since the input is directly substituted in the command. But this time we have to bypass the input validation.

Grep will return the entire content if we give an empty string ( "" ) as a filter. We can leverage this feature to bypass the validation by using the payload: `"" /etc/natas_webpass/natas11 #`.

If we give the above payload as the input the resultant command on the server would be:

`grep -i "" /etc/natas_webpass/natas11 #`` `~~`dictionary.txt`~~

where:

* `/etc/natas_webpass/natas11` - location of the password file.
* `#` is used to comment out the remaining command ( [PHP Comments](https://www.w3schools.com/php/php\_comments.asp) )

Direct link to solution: [http://natas10.natas.labs.overthewire.org/?needle=+%22%22+%2Fetc%2Fnatas\_webpass%2Fnatas11+%23\&submit=Search](http://natas10.natas.labs.overthewire.org/?needle=+%22%22+%2Fetc%2Fnatas\_webpass%2Fnatas11+%23\&submit=Search)

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>
