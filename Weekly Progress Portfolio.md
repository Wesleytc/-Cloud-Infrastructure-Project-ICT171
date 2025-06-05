# Week 1 to 4 Progress Portfolio
## Week 1: Setting Up My EC2 Server and Installing Apache

In the first week, I focused on setting up the foundation of my WordPress hosting environment using AWS. I began by launching an Ubuntu EC2 instance and allocating an Elastic IP address so that my server would have a fixed public IP. I made sure the correct inbound rules were set in the security group  allowing traffic through ports 22 (SSH), 80 (HTTP), and 443 (HTTPS). 

Once everything was configured, I used my .pem SSH key to securely connect to the instance from my terminal. After establishing the connection, I updated and upgraded the system using sudo apt update && sudo apt upgrade, which ensures all packages are current. I then installed Apache with sudo apt install apache2. When I visited the public IP in my browser and saw the Apache welcome page, I knew the server was running correctly. This week laid the essential groundwork for hosting WordPress securely and efficiently.

## Week 2: Installing MySQL, PHP, and Deploying WordPress

During the second week, I focused on configuring the backend environment needed for WordPress. I installed PHP and all required modules using sudo apt install php libapache2-mod-php php-mysql, then proceeded to install MySQL with sudo apt install mysql-server. I logged into the MySQL shell with sudo mysql -u root and changed the default authentication plugin to mysql_native_password, which works better with WordPress. 

I created a dedicated database (wp) and a new user (wp_user) with full privileges to manage it. This improves both functionality and security. Next, I downloaded the latest version of WordPress into the /tmp directory, extracted it using tar, and moved it into Apache’s root directory at /var/www/html. After restarting Apache, I accessed the server in my browser and completed the WordPress setup through the web interface, linking it to the database I had just created. By the end of the week, I had a fully functioning WordPress website up and running on my AWS instance.

## Week 3: Connecting My Domain Using Hostinger DNS

In the third week, I worked on pointing my custom domain to the AWS-hosted WordPress site using Hostinger’s DNS manager. After logging in to my Hostinger account, I navigated to hPanel, selected my domain, and accessed the DNS records section. I added A records for both @ and www, pointing them to the Elastic IP of my EC2 instance. I also reviewed and configured other DNS entries as needed (such as CNAME, MX, and TXT records for email and verification purposes).

I allowed some time for DNS propagation, and once complete, I went into the WordPress admin dashboard and updated the WordPress Address (URL) and Site Address (URL) to reflect my domain name. This ensured that users would see my domain rather than the raw server IP. Completing this step brought a professional look and feel to my project and prepared it for secure HTTPS access in the next stage.

## Week 4: Installing SSL and Finalising My Website

Week 4: Installing SSL and Finalising My Website
In the final week, I focused on securing my site with SSL encryption and applying the finishing touches. First, I ensured that ports 80 and 443 were open and that the domain was resolving correctly. I then installed Certbot and the Apache plugin with sudo apt install certbot python3-certbot-apache. Using sudo certbot --apache, I automatically requested and installed a Let’s Encrypt SSL certificate. Certbot detected my Apache configuration, verified the domain, applied HTTPS settings, and enabled automatic certificate renewals  a big plus for long term maintenance. 

After restarting Apache, I visited my site and saw the padlock icon in the address bar, confirming that the SSL certificate was working. I repeated this process for my secondary blog site as well. By the end of the week, my website was fully operational, secure, and professionally presented under my custom domain. I documented all configurations and stored backup copies to make future updates or migrations easier.
