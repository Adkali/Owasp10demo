# CSRF
```
source - > https://cwe.mitre.org/data/definitions/352.html
```
Cross-Site Request Forgery (CSRF) is a type of attack that making the victim into executing unwanted actions on a web application in which they are already authenticated.
With a little help of social engineering, CSRF attacks can be crucials. While this kind of attack is not aimed for data theft, it can lead to risks such as account-take-over and more.
The attack relies on the web application's trust in the user's browser, and exploits this behaviour which is WRONG in real life scenarios.
In our DEMO web application, the page where this flaw occurs is on the 'profile.php'. The core of the vulnerability revolves around session management and trusting all requests that come with a valid session cookie, regardless of their origin.

#### Vulnerable Code:
```
session_start();
if (!isset($_SESSION['username'])) {
    die("You must be logged in to view this page.");
}
```
Now, The above code starts or resumes an existing session. It checks if there's a 'username' stored in the session, and if not, it prevents access. However, this authentication method only checks for the presence of a session and doesn't validate the request source.

#### Aattacker HTML-Form-Attack
```
<!DOCTYPE html>
<html>
<body>
    <form action="http://10.0.2.14/Owasp10/BAC/profile.php" id="CSRF" method="post">
        <input type="hidden" name="email" value="Maaaalicious-threat@evil.com">
        <input type="submit" value="Click Me!">
    </form>
</body>
</html>
```

Now when user enter this URL and click on the 'Click Me!' button, he is actually sending a POST request to profile.php ( which he currently logged in).
This Innocent form is designed in a way that changes the user's profile ( notice the hidden field ), and eventually trust the user's own authenticated session to do so.
No other machanism are in place, which is a BAD thing.

### Purpose
The attack is aimed at demonstrating how an attacker can exploit a user's authenticated session to perform actions on their behalf, without their knowledge. By tricking the user into loading the attack.html, an attacker can change the user's email address.
in real-world applications, a scenarios like changing passwords, emails, names and more are a real-mess when a web application does not protect agains CSRF attacks. For more, enter the <b>source</b> above.

![csrf-gif](https://github.com/Adkali/Owasp10demo/assets/90532971/2b9a2df1-a0c2-4ff9-a198-89c098276343)

