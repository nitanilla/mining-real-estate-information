# First Floor
This is the real estate web application project using Laravel framework.


# Installation Procedure
 I hope you already installed composer in your system(your local computer or server)

Now clone this app by running this command =><b> git clone https://github.com/parthp1808/firstfloor.git</b>
Or you can simply download zip file and unzip it.

Now go inside the folder and using console, run composer by executing => <b>composer install</b>
Now run using cmd => <b>cp .env.example .env</b>
Now edit .env file :
<h3>Change below config as per your database</h3>
<i><br/>
DB_CONNECTION=mysql<br/>
 DB_HOST=127.0.0.1<br/>
 DB_PORT=3306<br/>
 DB_DATABASE=homestead<br/>
 DB_USERNAME=homestead<br/>
 DB_PASSWORD=secret</i>


Now , run => <b>php artisan migrate</b>

Now set file permissions:
<b>sudo chgrp -R www-data storage bootstrap/cache<br/>
sudo chmod -R ug+rwx storage bootstrap/cache<br/>
chmod 777 -R public</b>

Now run this command to generate new key

<b>php artisan key:generate</b>

and the clear config cache using

<b>php artisan config:clear</b>

