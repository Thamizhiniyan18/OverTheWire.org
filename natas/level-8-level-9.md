# Level 8 - Level 9

```
Username: natas9
Password: Sda6t0vkOPkM8YeOZkAGVhFoaplvlJFd
URL:      http://natas9.natas.labs.overthewire.org
```

This time also an input field with a link to the source code.

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

On checking the source code, input keyword/string that we give is directly supplied as a parameter to the grep command, which looks out for matching strings in the `dictionary.txt` file and returns the output.

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

This logic is vulnerable to [Command Injection](https://owasp.org/www-community/attacks/Command\_Injection), since the input is directly substituted in the command and no input sanitization is performed.

So, I tried to get the password for the next level by using the following input value:

`; cat /etc/natas_webpass/natas10 ;`

Direct link to the solution:

[http://natas9.natas.labs.overthewire.org/?needle=%3B+cat+%2Fetc%2Fnatas\_webpass%2Fnatas10+%3B\&submit=Search](http://natas9.natas.labs.overthewire.org/?needle=%3B+cat+%2Fetc%2Fnatas\_webpass%2Fnatas10+%3B\&submit=Search)

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
