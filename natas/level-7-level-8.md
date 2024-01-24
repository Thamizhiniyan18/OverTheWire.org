# Level 7 - Level 8

```
Username: natas8
Password: a6bZCNYwdKqN5cGP11ZdtPg0iImQQhAB
URL:      http://natas8.natas.labs.overthewire.org
```

This time also the website welcomed me with a input requesting for secret key and also there was a link to the source code of the logic behind the secret key validation.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

This time the secret key was encoded and the function/algorithm that is used to encode the secret key was given.&#x20;

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Let's breakdown the above function into steps:

1. First, the given secret string is encoded with base\_64 encoding scheme.
2. Secondly, the resultant string from the previous step is reversed.
3. Finally, the reversed string is converted to hexadecimal.

So decode the given encoded secret key we have to perform the above mentioned steps in reverse order, i.e.,

1. First, convert the encoded secret to binary.
2. Secondly, the resultant string from the previous step is reversed.
3. Finally, the reversed string is decoded with base\_64 decoding scheme.

The above decoding steps can be performed with CyberChef.

CyberChef has a handy URL scheme that preserves data and operations, so I can link directly to the solution: [https://gchq.github.io/CyberChef/#recipe=From\_Hex('None')Reverse('Character')From\_Base64('A-Za-z0-9%2B/%3D',true,false)\&input=M2QzZDUxNjM0Mzc0NmQ0ZDZkNmMzMTU2Njk1NjMzNjI](https://gchq.github.io/CyberChef/#recipe=From\_Hex\('None'\)Reverse\('Character'\)From\_Base64\('A-Za-z0-9%2B/%3D',true,false\)\&input=M2QzZDUxNjM0Mzc0NmQ0ZDZkNmMzMTU2Njk1NjMzNjI)

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

On giving the decoded string as the input, got the password for the next level.

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>
