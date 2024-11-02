# Level 6 - Level 7

```
Username: natas7
Password: jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr
URL:      http://natas7.natas.labs.overthewire.org
```

This the page had two links, Home and About

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

On checking these links found nothing.

<div>

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption><p>Home Page</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption><p>About Page</p></figcaption></figure>

</div>

But both of the above mentioned pages were fetched using the URL Query Parameter `page`.

And on the index page [http://natas7.natas.labs.overthewire.org/](http://natas7.natas.labs.overthewire.org/), there was a hint in the source code of the page, which stated that the password for webuser `natas8` is in `/etc/natas_webpass/natas8`.

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

The URL parameter and the hint triggered me about the [LFI](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web\_Application\_Security\_Testing/07-Input\_Validation\_Testing/11.1-Testing\_for\_Local\_File\_Inclusion) vulnerability. On testing whether the paramter is vulnerable to LFI by entering the password file location `/etc/natas_webpass/natas8` to the `page` URL parameter \[ [http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas\_webpass/natas8](http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas\_webpass/natas8) ], resulted with the contents of the password file.

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>
