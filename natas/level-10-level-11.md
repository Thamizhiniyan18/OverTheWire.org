# Level 10 - Level 11

```
Username: natas11
Password: 1KFqoJXi6hRaPluAmk8ESDW4fSysRoIg
URL:      http://natas11.natas.labs.overthewire.org
```

## Overview

This time we have got cookies that are encrypted with XOR scheme.

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

***

## Source Code Analysis

The source code had the php logic that performed the XOR encryption.

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Let's first breakdown, how the default cookie data is encrypted:

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

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

***

## Decryption using XOR Cipher

We can get the default data from the source code.

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

The data given in the source code has to be converted to JSON format:

```json
{
    "showpassword": "no",
    "bgcolor": "#ffffff"
}
```

Next, we can get the cookie from the browser dev tools application tab:

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

***

## Getting the Password

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

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>
