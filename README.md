# FlaskApp Web Application
This document provides an overview of the Flask web application "flaskApp", including setup instructions, Apache configuration details, and how to access the application.

Project Overview

MyApp is a Flask-based web application designed to demonstrate user registration, detail submission, and profile viewing functionalities. It is developed in Python and uses Flask as the web framework, with data stored in an SQLite database.

Prerequisites

Before you begin, ensure you have the following installed on your Ubuntu server:

-->Python 3.8 or higher

-->pip for Python 3

-->virtualenv or venv module for creating virtual environments.

Installation & Setup

Step 1: Update and Upgrade Ubuntu Packages
sudo apt update && sudo apt upgrade -y

Step 2: Install Apache and mod_wsgi
sudo apt install apache2 libapache2-mod-wsgi-py3 -y

Step 3: Install Python and Flask

Install Python and necessary packages:
sudo apt install python3-pip python3-venv -y

Create a Python virtual environment and activate it:
python3 -m venv venv
source venv/bin/activate

Install Flask:
pip install Flask

Step 4: Clone/Transfer Your Flask Application
Place your Flask application in the /var/www/MyApp directory (adjust as needed).

Step 5: Configure Flask Application
Create your Flask application entry point and configure it to run with Apache. See the included myapp.wsgi file for an example.

Step 6: Apache Virtual Host Configuration
Configure Apache to serve your Flask application by creating a new site configuration in /etc/apache2/sites-available/MyApp.conf. Refer to the configuration section below for details.

Step 7: Enable the Site and Restart Apache
sudo a2ensite MyApp.conf
sudo systemctl restart apache2

#Configuration

Apache Virtual Host

Below is a sample Virtual Host configuration for Apache. Adjust paths and domain names as necessary.




    <VirtualHost *:80>

    ServerName example.com
    
    WSGIDaemonProcess MyApp python-path=/var/www/MyApp python-home=/var/www/MyApp/venv
    
    WSGIScriptAlias / /var/www/MyApp/myapp.wsgi
    
    <Directory /var/www/MyApp>
    
        Require all granted
        
    </Directory>
    

    ErrorLog ${APACHE_LOG_DIR}/MyApp_error.log
    
    CustomLog ${APACHE_LOG_DIR}/MyApp_access.log combined
    
    </VirtualHost>

Usage

Access your application via your server's IP address or domain name configured in the Apache Virtual Host.

My FlaskApp: ec2-44-202-228-49.compute-1.amazonaws.com

Troubleshooting

For issues related to Apache configurations or Flask application errors, check the Apache error logs at /var/log/apache2/error.log.


