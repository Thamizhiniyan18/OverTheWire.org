# Level 3 - Level 4

```
Username: natas4
Password: tKOcJIbzM4lTs8hbCmzn5Zr4434fGZQm
URL:      http://natas4.natas.labs.overthewire.org
```

This time the target website stated that we have to come from [http://natas5.natas.labs.overthewire.org](http://natas5.natas.labs.overthewire.org/) to access the content of the page.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

So I intercepted the request using burpsuite and modified the [Referer URL](https://support.google.com/google-ads/answer/2382957?hl=en) from [http://natas4.natas.labs.overthewire.org](http://natas4.natas.labs.overthewire.org/) to [http://natas5.natas.labs.overthewire.org](http://natas5.natas.labs.overthewire.org/) and then sent the request and got the password for the next level in the response.

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>
