# Digital Ocean WordPress Setup

Version 0.9.1

This bash script makes it easy to spin up a new WordPress install using Digital Ocean VPS with Ubuntu and Nginx.


## Installation

Download the script and run `./dowp` from the directory the script is placed in(best in your www folder make sure to first make that file executable by doing chmod +x dowp).

To run the script from anywhere, you can place `dowp` in a folder included in your PATH environment variable.

If you don't want to define the path each time you run the script, open the file and uncomment the line at the top defining `path`. Set that to the root folder of VVV on your machine. **Note:** You do not need to do this if VVV is installed in the default location (`~/vagrant-local/`).


## Usage

Type `./dowp` or `dowp` if in your PATH environment variable and just follow the and answer the proposed options


## WordPress website creation

Creating a new WordPress website ask you and does the following:

* New WordPress install folder name
* WordPress website domain (instructions given at the end of the install if you haven't bought your domain yet)

* Database name, usename and password (yes, this will also create your db but you will need your mysql root password during the process)
* Database prefix(default to wp_)

* WordPress version(default to stable)
* Language(default to en_US)
* WP_DEBUG and WP_DEBUG_LOG(default to enabled)

* WP admin username(default to admin), password(default to password) and email address(default to youremail@email.com)

* WP directory structure, as a security matter, this will be set by default to `wordpress` for the core folder and `wp_content` for your plugin, uploads and themes folder, but this will ask you for new folders name if you decide to(default then to `admin` and `content`)

* During the install it will ask you for a password, this is your mysql root password for creation of both the database and user

* Make sure to update `fastcgi_pass` value in nginx-wp-common.conf file on line 85 according to your nginx.conf file

* TODO add a deploy folder for easy deploying from github or bitbucket

Once you have answered all this questions, this script will do:

* Create a new Database with database user and password
* Create your new WordPress website folder and a `htdocs` folder inside it where your wordpress install will be
* Create a composer.json file inside that `htdocs` folder
* Installing WordPress in the htdocs folder following the folder structure
* Creating both wp-config.php with your db, username, language etc.. and an index.php file inside your `htdocs` folder
* Creating a `youdomain.com` file at the root(here your new website folder) and a symbolic link to both `sites-enabled` and `sites-available` for Nginx config

* Greet you with your successful new install and give you info about it as:
  * Install directory
  * Install domain
  * Your username
  * Your password
  * Your Database creds
  * And what to add to your computer `hosts` file in order to work on your website if you haven't yet your domain name

* Once install is done, make sure to reload/restart nginx `sudo service nginx reload`


## WordPress Webite Deletion

Deleting a site does the following:

* Deletes the site's web root
* Deletes the `yourdomain.com` file in your website directory and the symbolic links in the `sites-enabled` `sites-available` folders

Note that it does not delete the site's database.


## Questions?

Twitter me at [@lostwebdesign](http://twitter.com/lostwebdesign).


## TODO

Add possibility to Deploy from GitHub and Bitbucket on push


## Credits | Thank you

[Alison Barrett](http://twitter.com/alisothegeek) for her brilliant [vvv wizard setup](https://github.com/aliso/vvv-site-wizard)
[Tomaž Zaman](https://twitter.com/tomazzaman) for his very clear and easy [Tutorial on setting up a Digital Ocean VPS](https://codeable.io/community/how-to-set-up-wordpress-vps/)

## Changelog

### 0.9.2
* Added nginx-wp-common.conf file and www redirection to non www

### 0.9

* Initial release
