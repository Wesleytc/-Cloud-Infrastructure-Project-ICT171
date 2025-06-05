# Installing EC2 Ubuntu / WordPress / DNS / Cert-Bot / SSL

## Prior Configuration Steps taken before installing WordPress:

Launching Ec2 Instance and Configuration

<img width="452" alt="image" src="https://github.com/user-attachments/assets/311632de-3054-40c1-8629-5db70286c8db" />

Follow this image to configure 

<img width="452" alt="image" src="https://github.com/user-attachments/assets/e47b93d2-7dfc-45af-81a9-89b8cd94d36b" />

Associate Elastic IP to your server IP

<img width="452" alt="image" src="https://github.com/user-attachments/assets/0b35f256-6d95-4582-8721-7257ec6fa7fd" />

Click on actions then Press Associate to the IP you want and should look like this 

<img width="452" alt="image" src="https://github.com/user-attachments/assets/15ee015a-ed3e-43b0-b1cd-e5d1b72c6d44" />

After this you can now connect to your Instance with your ssh key 

<img width="452" alt="image" src="https://github.com/user-attachments/assets/9e06e351-66ee-4e09-8758-cbc8f63d6bc3" />

Once copied remembering your key.pem being in downloads, copy the ssh above and input it in a command terminal or power shell like the following:

<img width="452" alt="image" src="https://github.com/user-attachments/assets/bb067294-9c3b-4892-a30a-c5ce766911d9" />

## Now you can begin to install WordPress with the following steps:

### 1.	Install Apache server on Ubuntu

         sudo apt update 
         sudo apt upgrade
         sudo apt install apache2
         
<img width="452" alt="image" src="https://github.com/user-attachments/assets/58bae3d6-e0cd-4faf-b124-690fdd04ed74" />

This command installs Apache on your Ubuntu server so it can serve web pages (like WordPress) to users over HTTP. 

After installation, Apache runs automatically, and you can verify it's working by accessing your server’s IP address in a browser it should show the default Apache welcome page.

<img width="452" alt="image" src="https://github.com/user-attachments/assets/7c8cff9b-9cfb-4565-bbda-dd5ed2527c5a" />

### 2.	Install PHP and MySQL PHP connector

        sudo apt install php libapache2-mod-php php-mysql

<img width="452" alt="image" src="https://github.com/user-attachments/assets/a849d01d-0465-4640-91d5-cab612c3ce64" />

PHP is the scripting language WordPress is written in. The libapache2-mod-php module allows Apache to process. phpfiles. The php-mysql package enables PHP to interact with MySQL databases — essential for WordPress to function. This step ensures your server can run WordPress scripts and connect them to the database.

### 3.	Install MySQL server

        sudo apt install mysql-server

<img width="452" alt="image" src="https://github.com/user-attachments/assets/78181fca-9258-4bc1-aa57-ef40d54a9e11" />

MySQL is the database management system used by WordPress to store content, users, settings, and more. This command installs the full MySQL server package, giving you the ability to create and manage databases locally on your Ubuntu machine.

### 4.	Login to MySQL server

        sudo mysql -u root

<img width="452" alt="image" src="https://github.com/user-attachments/assets/b44b9821-8a41-4c87-9450-d9d6074f0070" />

This opens the MySQL command-line interface (CLI) as the root (admin) user. Using sudo ensures you have administrative privileges. Once inside, you can create users, set passwords, and manage databases.

Change root user's authentication plugin

      ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password';

Newer versions of MySQL use the auth_socket plugin by default, which doesn’t work with PHP in many cases. This command switches the root user's login method to mysql_native_password, which is more compatible with web apps. Be sure to replace the password with a strong one to secure your root account.


Create a new MySQL user for WordPress

      CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Password';

This creates a new MySQL user account named wp_user that will be used by WordPress to connect to the database. Giving WordPress its own user (instead of using root) improves security by limiting database access.

Create the WordPress database

      CREATE DATABASE wp;

This sets up a new MySQL database named wp (short for WordPress) where WordPress will store all its data — posts, pages, themes, settings, users, etc.

Grant database permissions to the WordPress user
        
      GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;

Grants the wp_user full access (read, write, modify) to all tables in the wp database. Without this, WordPress wouldn’t be able to manage its data.

### 5. Download the latest WordPress package

        cd /tmp
        wget https://wordpress.org/latest.tar.gz

<img width="452" alt="image" src="https://github.com/user-attachments/assets/545bc7ad-4429-4e02-86cf-f4164a5d4845" />

This downloads the compressed latest version of WordPress from the official site into the temporary directory. Using /tmp keeps the system organized, and the file is removed on reboot unless you move it elsewhere.

### 6. Extract the WordPress archive
      
       tar -xvf latest.tar.gz

<img width="452" alt="image" src="https://github.com/user-attachments/assets/03187dae-55d8-430c-a65a-a92682fb7f16" />

Extracts the latest.tar.gz archive, unzipping all WordPress files into a new directory named wordpress. These are the core application files needed to run the website.


### 7. Move WordPress to Apache's web root

        sudo mv wordpress/ /var/www/html

<img width="452" alt="image" src="https://github.com/user-attachments/assets/a5eb9f36-864d-4fd5-9b2a-7ada8584b6e2" />

Moves the entire WordPress directory into Apache’s default document root (/var/www/html). This is where Apache serves files from by default. You can now access WordPress by visiting your server’s IP or domain.

<img width="452" alt="image" src="https://github.com/user-attachments/assets/fe6acec0-a216-4782-a9a5-f68966cf38a2" />

Next loading screen should come up like this:

<img width="452" alt="image" src="https://github.com/user-attachments/assets/34e26955-801e-47f6-904c-c03952556d2e" />


After that should take you here:


<img width="452" alt="image" src="https://github.com/user-attachments/assets/7fdd68e3-d355-4ae1-a556-25dd431fa8da" />





When successfully logged in this is the page you’ll come to:

<img width="452" alt="image" src="https://github.com/user-attachments/assets/fe356e49-ff45-49f0-b254-4b681e4cb9f7" />

And by Inserting the HTML code I wrote in WordPress it’ll look like this:


<img width="452" alt="image" src="https://github.com/user-attachments/assets/d8e89cb0-157c-430f-b1c6-7c683c4452f5" />



Connecting Website to DNS Using Hostinger
Manage DNS Records in Hostinger
If your domain is already using Hostinger’s nameservers, you can manage individual records (A, CNAME, MX, TXT, etc.):
To manage DNS records:
1.	Log in to your Hostinger account.
2.	Go to hPanel > Domains > [your domain].
3.	Click on DNS 
4.	Here, you can:
	Add an A record (e.g., point @ or www to your server's IP)
	Add a CNAME (e.g., www to yourdomain.com)
	Set MX records (for email)
	Add TXT records (for verification or SPF, DKIM, etc.)
5.	Click Save after making changes.

<img width="399" alt="image" src="https://github.com/user-attachments/assets/60c619d3-5726-42a9-a51d-84ed1fa5d4bb" />

Example: Point example.com to a VPS
•	A record:
Name: @
Type: A
Value: 13.236.240.94 (your VPS IP)

<img width="399" alt="image" src="https://github.com/user-attachments/assets/74541060-9b67-4fe3-81be-dcd2b646920e" />

Now you can go in your WordPress settings click general, and you should be able to change Address URL & Site URL to your custom DNS:

<img width="451" alt="image" src="https://github.com/user-attachments/assets/e253ae5b-8356-404e-983f-71ff8d4bf431" />


### 8. Restart or reload Apache

       sudo systemctl restart apache2
       # OR
       sudo systemctl reload apache2

Reloads Apache’s configuration and applies any changes you've made (like adding PHP or moving WordPress files). restart will stop and start Apache, while reload only refreshes its configuration without downtime.

### 9. Install Certbot and the Apache plugin

       sudo apt-get update
       sudo apt install certbot python3-certbot-apache

<img width="452" alt="image" src="https://github.com/user-attachments/assets/11184b74-4b3f-4b55-ae5c-f335666ec8d7" />

Certbot is a free tool from Let’s Encrypt that automates the process of securing your website with an SSL certificate. This command installs both the tool, and the Apache plugin needed for automatic configuration.

### 10. Generate and install a free SSL certificate
    
- Detects your Apache virtual host configurations

- Requests an SSL certificate for your domain (you’ll need to enter it)

- Automatically applies HTTPS settings to your Apache configuration

- And sets up automatic certificate renewal.

-	To Install certbot :
  
Make sure your domain name is correctly pointed to your server’s public IP and port 80 is open for this to work.

     sudo apt-get update
       
     sudo apt install certbot python3-certbot-apache  
        
     Request and install ssl on your site with certbot sudo certbot –apache

When prompts Inputted correctly Output should display something like this:

<img width="452" alt="image" src="https://github.com/user-attachments/assets/b7013cbc-6c52-481f-83af-ee9078de972f" />

<img width="452" alt="image" src="https://github.com/user-attachments/assets/34e8fe30-a322-4577-a7de-9eb7f2ccad91" />

<img width="452" alt="image" src="https://github.com/user-attachments/assets/be0b1287-8ee0-4f98-a8b9-701d42f03616" />


Restart or reload Apache

       sudo systemctl restart apache2
       
       OR

       sudo systemctl reload apache2
Go to web with URL and should display this:

<img width="452" alt="image" src="https://github.com/user-attachments/assets/292af308-96f2-4f6b-8d28-a269d0148464" />


Repeat same Process for Apache Blog 

<img width="452" alt="image" src="https://github.com/user-attachments/assets/491dee09-49c2-42bb-8bcc-52915be21973" />

Reference:
Was Aided by this video but was missing a lot of important steps I had to increment myself.

https://www.youtube.com/watch?v=8Uofkq718n8
