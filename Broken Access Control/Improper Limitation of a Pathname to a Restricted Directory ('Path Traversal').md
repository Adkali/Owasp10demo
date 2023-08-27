## OWASP Top 10 - Broken Access Control
source - > https://cwe.mitre.org/data/definitions/22.html
### Vulnerability: Unrestricted File Path Access

**Description**:
this vulnerability arises when an application does not properly validate or restrict the paths that a user can specify, allowing attackers to access, read, modify, or execute files that they shouldn't have access to.

**Common Scenarios:**
1. Directory Traversal -  This occurs when an attacker uses special characters like ../ to traverse out of the restricted directory. For example, if a web application allows users to download files by specifying a filename, an attacker might specify ../../etc/passwd to access the system's password file.

#### Vulnerable Code (Perl):
In our given Perl script, user profile information is fetched based on the `user` parameter provided in the URL. The script constructs the path to the user's profile by appending this parameter directly to the file path without any validation.

```perl
my $dataPath = "/var/www/html/Owasp10/profiles";
my $username = $cgi->param("user");
my $profilePath = $dataPath . "/" . $username;
```

Issue:
The problem arises when an attacker manipulates the user parameter to traverse directories (e.g., ../../etc/passwd) or access files they shouldn't be able to. Without proper validation and controls, this can lead to unauthorized file access.

Solutions:
1. Always validate input: Ensure the input meets specific criteria before use.
2. Limit access: Ensure users can only access the files they are authorized to.
3. Avoid direct file paths: Don't use direct file paths in user-facing functions. Use identifiers and map those to actual file paths server-side.
