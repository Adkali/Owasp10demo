# Exposure of Sensitive Information: Login Feedback Vulnerability
source - > https://cwe.mitre.org/data/definitions/200.html
## Introduction
While this can result from broken access controls, it's broader and can also result from other vulnerabilities or misconfigurations.
In the web security, one crucial aspect often overlooked is the information revealed during the login process. While user-friendly error messages assist
legitimate users, they might provide a good information to potential attackers. This write-scenario shows a simple impactful, illustrating the potential security concerns surrounding login feedback.

## Vulnerable Code Explanation:

### HTML Form (Frontend)

Simple HTML form to capture the username and password provided by the front-user [front-end]

```html
<form action="login.php" method="post">
    Username: <input type="text" name="username"><br><br>
    Password: <input type="password" name="password"><br><br>
    <input type="submit" value="Login">
</form>
```

### PHP Logic (Backend)
The backend, written in PHP, maintains an in-memory "database" of users and their corresponding passwords. Make sure to understand that this approach is  for demonstrative purposes and should never be employed.
```
$users = array(
    'alice' => 'password123',
    'bob' => 'bobsecure',
    'charlie' => 'charliepass'
);
```
### The code proceeds to authenticate users based on the supplied credentials:
```
if (isValidUsername($username, $users)) {
    if (isValidPassword($username, $password, $users)) {
        echo "Login Successful";
    } else {
        echo "Login Failed - incorrect password";
    }
} else {
    echo "Login Failed - unknown username";
}
```

Vulnerability: The vulnerability lies in the granularity of the error messages provided during login attempts. In cases where the username does not exist, the message "Login Failed - unknown username" indicates to attackers that the username in question is invalid. Similarly, if an incorrect password is entered, the message "Login Failed - incorrect password" discloses the validity of the username. These specific error messages aid attackers in identifying valid usernames for potential brute-force attacks or targeted exploitation. To address this vulnerability, ensure that error messages are generic and do not disclose specific details about the authentication process. Maintain consistency in error messages regardless of the nature of the error. This approach prevents attackers from gaining insights into the authentication mechanism.

### Demo
Soon!
