# Level 24 - Level 25

```
Username: natas25
Password: O9QD9DZBDq1YpswiTM5oqMDaOtuZtAcx
URL:      http://natas25.natas.labs.overthewire.org
```

## Overview

This time we got a page with a quote and also a dropdown menu to change the language of the quote. Also we got a link to the source code.

<figure><img src="../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

Let's take a look at the source code.

<figure><img src="../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

The `setLanguage()` function looks out for a URL parameter `lang`, if it exists, it calls the `safeinclude()` function, with an argument `"language/" . $_REQUEST["lang"]`, else it calls the `safeinclude()` function, with an argument `"language/en"`. So, basically this function sets the language, if provided and valid, else it defaults to `"language/en"`.

<figure><img src="../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

Let's breakdown the `safeinclude()` function.

<figure><img src="../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

* First, the `safeinclude()` function checks for directory traversal by looking out for `"../"` in the given `$filename` using the PHP function `strstr()`,  and if it contains the sub-string `"../"`, it calls the `logRequest()` function to log the directory traversal attempt and it fixes the `$filename` by replacing all the occurrences of the sub-string `"../"` with `""`.
* Next, it checks whether the `$filename` contains the sub-string `"natas_webpass"` using the PHP function `strstr()`, and if it contains the sub-string `"natas_webpass"`, it calls the `logRequest()` function to log the illegal file access attempt and it calls `exit(-1)` to terminate the further execution of the code.
* Finally, if the $filename satisfies the first two conditions, it checks whether the file exists, and if true it returns 1, else it returns 0.

The check for directory traversal in the `safeinclude()` function can be easily bypassed. Since, the function replaces all instances of `"../"`, if we give  `"..././"` as the input, it will result as `"../"`. With this bypass, we can successfully read other files in the file system. For example, the input `"..././..././..././..././..././etc/passwd"`, will result as `"../../../../../etc/passwd"`, which will show the contents of the `/etc/passwd` file.

***

## Testing the Application

Let's try the above mentioned example. First I tried to change the language from the dropdown menu and captured that request using burpsuite. Next I repeated the request from burpsuite, with the value of the parameter `lang` to be `"..././..././..././..././..././etc/passwd"`, which responded with the content's of the `/etc/passwd` file.

<figure><img src="../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>

We can leverage the above bypass and try to read the contents of the file `/etc/natas_webpass/natas26`, which contains the password for the next level. But it won't work since the `safeinclude()` function terminates the code execution if the filename contains the sub-string `"natas_webpass"`.

We have to find some other way to get the password for the next level.

Now, Let's take a look at the `logRequest()` function. It writes to a file with a path `"/var/www/natas/natas25/logs/natas25_" . session_id() .".log"`. The `logRequest()` function, logs the a lot of details, of which most of them are server side that we can't modify, except the logging of user agent from the request, which we can modify.

<figure><img src="../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

***

## Getting the Password

We can set/modify the value of the user agent from burpsuite. If we set the value of the user agent to be the following PHP code, it will fetch the password and stored it the log file.

```php
<?php echo shell_exec("cat /etc/natas_webpass/natas26"); ?>
```

In order to make the above payload work, we have to send a request that triggers the `logRequest()` funciton, with the value of the user agent set to the above payload as shown in the following image:

<figure><img src="../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

Now, its time to check whether the password is fetched and stored in the log file. Since we know whether the log file is stored and the format of the log filename, we can access the log file using the directory traversal technique with the bypass \[`"..././"`] which we discussed earlier.

You can access the log file using the payload, `"lang=..././logs/natas25_<PHPSESSID>.log"`.

If everything works fine, you can get the password for the next level in the response as shown in the following figure.

<figure><img src="../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>
