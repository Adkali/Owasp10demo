# CORS
Cross-Origin Resource Sharing (CORS) is a security feature implemented in web browsers to control how resources on a web server can be requested from another domain.
In the web's early days, the Same-Origin Policy (SOP) was the primary security measure for browser-based applications. SOP restricts web pages from making requests to a different domain than the one that served the web page.
However, this policy is too restrictive in the modern web, where applications often need to access resources across different domains.
CORS provides a way to allow such cross-origin requests securely.

When a web page makes a cross-origin HTTP request (like AJAX calls), the browser adds an Origin header to the request, indicating the domain from which the request originated. The server can then decide whether to allow or deny this request based on its CORS policy.
If the server allows the request, it responds with specific CORS headers (Access-Control-Allow-Origin, for instance) indicating which origins are permitted. The browser then permits or blocks the response to the JavaScript code based on these headers.

* Allowing All Origins: Setting Access-Control-Allow-Origin to * (wildcard) allows any website to make requests to your server, which can be dangerous.
* Reflecting the Origin: Dynamically setting the Access-Control-Allow-Origin header to match the Origin header in the request can be exploited if not implemented correctly.

# Demo

```10.0.2.14 - > login page```<br>
```/userinfo.php - > API of the user after logged in```<br>
```/details - > request made holding sensitive info with JSON format.```<br>

![1](https://github.com/Adkali/Owasp10demo/assets/90532971/6096ef3e-b176-46d8-9828-40f9cecc270e)

Now, checking the target contents for CORS, reveals that /details ( a request made ) is vulnerable to CORS.<br>

![2](https://github.com/Adkali/Owasp10demo/assets/90532971/e79a5d9e-3edb-4fb0-aad8-aa0672e4bcaf)

When adding "Origin", the response reflect back, showing the "Access-Control-Allow-Origin" with our malicious web.
in this case, the web is vulnerable to CORS. also, the header "Access-Control-Allow-Credentials" with the value "true" means that the server
is allowing the inclusion of credentials (such as cookies, HTTP authentication, or client-side certificates) in cross-origin requests.

![3](https://github.com/Adkali/Owasp10demo/assets/90532971/ff27a1fc-84de-47b3-9cdd-4ebeee5d4ff0)

With this, attacker can craft a malicious .js script file or some other exploit, tricking the victim into clicking it and forward the  sensitive data to the attacker's web server. for more info and knowledge, visit [portswigger](https://portswigger.net/web-security/cors#what-is-cors-cross-origin-resource-sharing).
