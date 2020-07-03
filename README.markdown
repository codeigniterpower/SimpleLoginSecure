Codeigniter - SimpleLogin Secure
=============

Quick and simple login library that will get you up and running with an unobtrusive authorization system very quickly. It does not try to guess how you want to structure your app, it simply tries to give you a little help

SimpleLogin-Secure uses the phpass framework for secure, portable password hashing instead of straight md5 without a salt.  Secondly, SimpleLogin-Secure uses an e-mail address instead of a user name as the login key.  And finally, it adds user_date, user_modified and user_last_login date/time fields to the default install.

For Original more information, visit Simple login library for CI

## FEATURES

* **easy helper/class with autouser management**. to archieve login attemps.
* Ugraded to work with BOTH CodeIgniter 2.0 AND 3.0
* Added a version test and use "sess regenerate" or "sess create" depending on version
* Use the PHPASS library 
* Update function to allow to change the user's email from your classes or whatever.
* An edit_password function to compare and change passwords

## INSTALLING

Comes included with CodeigniterPowered, but for CI 2 or CI3:

**Requirements**

* Codeigniter 2.x or 3.x
* PHP 5.3

**Manual controlled install**

**1)** Located your Codeigniter proyect and then download the repository at the `Applications` root directory

`wget https://github.com/codeigniterpower/codeigniter-SimpleLoginSecure/archive/master.tar.gz -O ci-simpleloginsecure.tar.gz`

**2)** Copy  and the entire phpass-0.3 directory to your application/libraries directory.

```
untar -xz ci-simpleloginsecure.tar.gz
mv codeigniter-SimpleLoginSecure/SimpleLoginSecure.php libraries/
mv codeigniter-SimpleLoginSecure/phpass-0.3 libraries/
rm -rf codeigniter-SimpleLoginSecure
```

**3)** Then, just In controlers or in the views:

``` php
$this->load->library('SimpleLoginSecure'); // load the library
$this->simpleloginsecure->create('user@example.com', 'uS$rpass!'); // create a new user
echo "User? " . $this->simpleloginsecure->login('user@example.com', 'uS$rpass!');
```

## CONFIGURATION

Create your database table using the following SQL sample. SQL files are provided [create_users_table.sql](create_users_table.sql)
You can also edit the hash length and portability constants at the top of SimpleLoginSecure.php.

``` sql
CREATE TABLE `users` (
  `user_id` INTEGER NOT NULL DEFAULT 00000000000000, -- must use gen id in php code
  `user_email` TEXT NOT NULL DEFAULT '', -- compat with all dbs, but cannot be empty
  `user_pass` TEXT NOT NULL DEFAULT '', -- compat with all dbs, but cannot be empty
  `user_date` DATETIME NOT NULL DEFAULT '1000-01-01 00:00:00',  -- compat with all dbs
  `user_modified` DATETIME NOT NULL DEFAULT '1000-01-01 00:00:00',  -- compat with all dbs
  `user_last_login` DATETIME NULL DEFAULT '1000-01-01 00:00:00', -- compat with all dbs
  PRIMARY KEY  (`user_id`)
);
```

## USAGE


```php
    $this->load->library('SimpleLoginSecure'); // load the library
    $this->simpleloginsecure->create('user@example.com', 'uS$rpass!'); // create a new user
    if($this->simpleloginsecure->login('user@example.com', 'uS$rpass!')) {
        // success attempt to login
    }
    if($this->session->userdata('logged_in')) {
        // success check if logged in
    }
    $this->simpleloginsecure->logout();// logout
    $this->simpleloginsecure->delete($user_id);  // delete by user ID
    $this->simpleloginsecure->update($user_id, $user_email, $auto_login); // Update user Email
    $this->simpleloginsecure->edit_password($user_email, $old_pass, $new_pass) // Update Password
```


## Credits

This is specific AD-HOC folk for Codeigniter-powered, see original project for.

- Copyright © original Simplelogin library was written by Anthony Graddy._    
- Copyright © _SimpleLogin-Secure was written by Alex Dunae, 2008._  
- Copyright © _SimpleLogin-Secure new version, 2.0, for Code Igniter II by Stéphane Bourzeix 2011/2013._
- Copyright © _SimpleLogin-Secure new version, 3.0, for Code Igniter II and III by Stéphane Bourzeix 2016._
