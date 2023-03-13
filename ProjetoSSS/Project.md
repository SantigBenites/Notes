# Part1

## VulnApp

4 - The vulnerability in the code derives from then following snippet of code:
![[4.1.png]]
In these lines we use the function readlink to copy MAXPATHLEN bytes from `resolved` to `p` and we get the number of bytes copied in n.
After that, we then use `n` on line 299 to put the end of line operand in `resolved`, the problem with this line is that we use `resolved[n] = '\0'` which leads to instead of putting the character `'\0'` at the end of the `resolved` buffer it puts the operand one byte in front of the end considering it doesn't take into account the index of the memory not going from 1 .. n but from 0 .. n-1.

5- This vulnerability can be solved if we take into account the indexes of the resolved buffer and instead of `resolved[n] = '\0'` we use `resolved[n-1] = '\0'`.

6- This program is meant to scan data and sanitise it, it works by looping thorough the given input and making sure some characteristics are met, this being that all symbol are valid( not something we will exploit), and making sure some types of char have pairs to themselves, these being `()` and `<>` , the function makes sure that the string as these types of pairs by adding them if they are missing (we will exploit this).
This being said, the exploit is simple we will pass to the function a string missing one of these pairs and making sure that when the function adds this char to the string it leads to a buffer overflow. Considering it doesn't take into consideration it own added chars when calculating the length of the string.

7- A string like `<<<<<<<<<<<<<<<<<<<` could be used for this purpose (not sure)

## SSS-DB

8-Vulnerability can be exploited by introducing “| ifconfig” in the input field
![[8.1.png|1200x500]]

9-
![[9.1.png]]
We can see from the previous excerpt of code that the variable $targethost receives unsanitized input.
![[9.2.png]]
Then the variable will be used in echo shell_exec(“nslookup” . $targethost) without any previous validation.
To protect from this attack is necessary that the input is validated, in this case it means verify that the input follows the patterns used by IPV4, IPV6 and the domain names.

10- Vulnerability can be exploited by introducing <script> alert("hello") </script> in the input field of the page DNS Lookup option of the Operations menu (or may page of the sss-db that writes to log, uses the method POST, and as insufficient security regarding XSS attacks).
![[10.1.png|1400x600]]
After analysing dns-lookup.php is possible to see that the variable $lTargetHostText receives the input from $targethost that receives unsanitized input. Being that $lTargetHostText will be used in WriteLog without any validation.So when introducing “<script> alert("hello") </script>” in the input field, this will be written to the logs.
Being that show-log.php will execute a SELECT from the logs, <td>Executed operating system command: nslookup <script> alert("hello") </script></td> will be part of the HTML.

|Code1: | Code2:|
|------------ | ------------|
|![[10.2.png]]|![[10.3.png]]|


11-Vulnerability can be exploited by using ZAP to alter the request, adding <script> alert("hello") </script> to the input field.
|Request: | Response:|
|------------ | ------------|
|![[11.1.png]]|![[11.2.png]]|
12-
text-file-viewer.php:
![[11.3.png]]
Variable $pTextFile receives unsanatized input,
Following the request presented previous we will have $pTextFile =.%2FFILES%2Fauditool.txt <script> alert("hello") </script>, and the response will contain <p class="label"> File: ./FILES/auditool.txt <script> alert("hello") </script></p>.
To protect from this attack is necessary verify if the input received is valid, in this case it means verify if the input received correspond to any of the options presented.

13- Vulnerability can be exploited by using ZAP to alter the request, by altering the variable of the input to `file:///etc/passwd`


|Request: | Response:|
|------------ | ------------|
|![[13.1.png]] | ![[13.2.png]]

text-file-viewer.php:
![[13.3.png]]



This attacks can be executed because, has seen previous variable $pTextFile receives unverified input, so when fopen is executed it will use the unverified input, the same thing happens with the stream_get_contents.

14-Vulnerability can be exploited by inserting “1' or '1'='1' #” in the name input field.

Result:
![[14.1.png]]
user-info.php:
![[14.2.png]]

$lUsername = 1' or '1'='1' #
$lQuery = SELECT * FROM accounts WHERE username = ‘ 1' or '1'='1' # ‘AND password = ‘’, being that # is comment
$lQuery = SELECT * FROM accounts WHERE username = ‘ 1' or '1'='1'
$lQuery = SELECT * FROM accounts WHERE username = true

![[14.3.png]]
When executing query all rows will be selected


## Flawfinder



## WAP

## index.php

Using WAP over the index.php file it finds only one vulnerability:

![[16.1.png]]

This vulnerability refers to an unsanitized SQL query that could lead to SQL injection attack, and therefore we can say that WAP found a real vulnerability.
The way to exploit this vulnerability is to have a cookie of name `uid` and with value being the ending part of the SQL query, making sure that whatever it returns is one of the accounts in the website.
![[16.2.png]]
When the SQL query is not sanitised, and this cookie exists, any client side change runs the following code
![[16.3.png]]
And instantly signing in the user with the result of the SQL query, in our case considering the only user in the database was the admin, we logged in as admin.
![[16.4.png]]
When analysing the corrected code given by WAP, we can see that the main security flaw was successfully corrected considering the SQL query has been sanitised and therefore SQL injections wont be possible anymore.

## user-poll.php
Using WAP over user-poll.php file it finds 2 vulnerabilities
![[16.5.png]]
In this case we have an input from the URL, which means we can by changing the URL influence the page as seen below:
![[16.6.png]]
This input comes from line 40, in which we set the value of `$lUserChoiceMessage` as the value of choice from the URL. Which leads to this value being manipulated by the atacker.
![[16.7.png]]
Regardless, in this case WAP wasnt able to solve the vulnerability, and moreover with the changes proposed the code wouldnt have valid sintax.


## AFL

After using AFL for 2 hours we got 41 'unique' crashes 
![[17.1.png]]
Regardless of what was reported by AFL, all of these crashes referred to the same vulnerability, that being said we took 3 of these files and run then in gdb doing a backtrace everytime, we therefore concluded that the tiffcp.c had a vulnerability in line 315
![[17.2.png]]
Which resulted from the call of the function opensrcImage that called the function TIFFOpen() in line 180 which is the source of the vulnerability.
![[17.3.png]]
As we can see in the Code above the call of the function TIFFOpen in line 180, opens a file and returns a handler for said file in the variable tif. 
This being said, unlike the other call of the function TIFFOpen in line 169, in line 180 we don't have the assurance that the file didnt fail in opening, this would be done by the lines 172 to 177 for the first call.
Considering that the argument passed to openSrcImage is &imageCursor, and as we can see in line 314 of the second image &imageCursor is dependant of the args, we can say that this lack of check is a vulnerability we can exploit.
