# Web Cache Deception

Web Cache Deception is a vulnerability that arises from server misconfiguration.
This vulnerability becomes critical when requests that should not be cached are Accidentally cached by the server. This can compromise user credentials or other sensitive data.
In a web cache deception attack, the attacker makes a request to a URL that should not be cached, but due to misconfiguration, the caching mechanism misinterprets the request. 

For example, consider the following scenario:

- Attacker's Request: `http://example.com/myaccount/home.php/something.css`
- Server's Misinterpretation: Processes the request as `http://example.com/myaccount/home.php`
- Server Response: Returns sensitive user information.
- Cache Server's Mistake: Sees the `.css` extension, treats it as a static resource, and caches the response.

This leads to sensitive information being stored in the cache and potentially being accessible to unauthorized users.

# Lab For example

- Creds:`alice:123456`
- Creds:`bob:112233`
  #### Now When alice logs in to her profile, se sees some sensitive information that only see knows.
  #### bob (attacker), create an account, and while testing the web appliation's behavior, notice that the web is vulnerable.
  #### Now bob wants to trick alice into clicking a nonexist path so the web server wil caches alice's sensitive data.

https://github.com/Adkali/Owasp10demo/assets/90532971/8967dcc0-1966-4993-8303-e7a399254173

- Note: The codes used are simple html, php and python. The vulnerablity made on purpsoe when path ends with /.css extenson.
<pre>
  $isCSSRequest = strpos($_SERVER['REQUEST_URI'], '.css') !== false;
  //// .... Rest of the code ////
  if ($isCSSRequest) {
    if (isset($_SESSION['username'])) {
        header('Cache-Control: public, max-age=3600');
        echo "User profile: " . ($_SESSION['username']) . ".<br>";
        echo "Security Code: " . $_SESSION['user_info']['security_code'] . ".<br>";
        echo "ID Number: " . $_SESSION['user_info']['id_number'] . ".<br>";
    } else {
        header("Content-Type: text/css");
        echo "/* CSS content */";
</pre>

The main idea is to understand the logic here.
In web development and server configuration, understanding what should and shouldn't be cached is crucial for both performance and security.
Fore more - > <a href="https://beaglesecurity.com/blog/article/web-cache-deception.html">Click here</a>
