# Level 5 - Level 6

```
Username: natas6
Password: fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR
URL:      http://natas6.natas.labs.overthewire.org
```

This time the page welcomed me with an input box requesting for a secret. Also there was a link "View sourcecode".

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

The link lead to `index-source.html` page, which had the logic that is behind the verification of the secret key that we enter as input. The variable `$secret`, which is used in the code is imported from the file/path `includes/secret.inc`.

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

The path `includes/secret.inc` \[ [http://natas6.natas.labs.overthewire.org/includes/secret.inc](http://natas6.natas.labs.overthewire.org/includes/secret.inc) ]  had the value for the variable `$secret`.

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

On entering the found secret value in the input, got the password for the next level.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>
