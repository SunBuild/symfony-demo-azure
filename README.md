#Symfony Demo Application

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)

This application is a fork of [Symfony-demo application](https://github.com/symfony/symfony-demo). It  is a blog application that uses SQLite by default. 

To update the application to use MySQL in-app , you need to update 2 files : config.yml and parameters.yml under app/config directory. If you are update this same application , then you need to convert the SQLite data into a MySQL database and [import your database content](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/exporting-your-database-to-local-mysql/) prior to updating the files below. 

In parameters.yml , update the connection information for the MySQL database information
```
# This file is auto-generated during the composer install
parameters:
    database_host: 127.0.0.1
    database_name: localdb
    database_user: azure
    database_password: '6#vWHD_$'
    mailer_transport: smtp
    mailer_host: 127.0.0.1
    mailer_user: null
    mailer_password: null
    secret: ThisTokenIsNotSoSecretChangeIt
    locale: en
    env(SYMFONY_SECRET): secret_value_for_symfony_demo_application
    env(SYMFONY_LOG): '%kernel.logs_dir%/%kernel.environment%.log'

```
In config.yml , replace the connection string for SQLite DB file with the MySQL connection information as shown below. Note to always use ENV variables for the MYSQL port to prevent any downtime issues in case port changes during a scaling operation or service update. 
```
driver:   pdo_mysql
        host:     "%database_host%"
        port:     "%env(WEBSITE_MYSQL_PORT)%"
        dbname:   "%database_name%"
        user:     "%database_user%"
        password: "%database_password%"
```
