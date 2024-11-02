# Level 4 - Level 5

```
Username: natas5
Password: Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD
URL:      http://natas5.natas.labs.overthewire.org
```

This time, the responded that "You are not logged in".

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

So I checked the HTTP history of burpsuite and found a cookie named `loggedin` in the response header, with a value of 0.

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

I tried modifying the value to 1 using the Dev-Tools.

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

And refreshed the site and got the password for the next level.

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>
