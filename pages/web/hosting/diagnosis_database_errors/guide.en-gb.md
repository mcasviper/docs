---
title: Troubleshoot common database errors 
excerpt: Diagnose the most common cases of database errors
slug: database-frequent-errors
Section: Diagnosis
Order: 4
---

**Last updated 8th October 2021**

## Objective

Your database usage may result in a number of anomalies on your website or [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), as well as on the interface [PhpMyAdmin](../creating-database/#accessing-the-phpmyadmin-interface).

**Find out how to troubleshoot database errors with OVHcloud web hosting plans.**

> [!warning]
>
> OVHcloud provides services that you are responsible for with regard to their configuration and management. It is therefore your responsibility to ensure that they function properly.
>
> We have published this guide to assist you as much as we can with common tasks. We recommend contacting a specialist provider and/or getting in touch with the publisher of the interface or software if you encounter any difficulties. OVH cannot assist you in this regard. You can find more information in the [Go further](#gofurther) section of this guide.
>

## Requirements

- an [OVHcloud Web Hosting plan](https://www.ovh.co.uk/web-hosting)
- access to the [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB)
- one of our database offers [Web Cloud](https://www.ovh.co.uk/web-hosting/sql-options.xml) or [Private SQL](../getting-started-with-private-sql/).

## Instructions

### "Error establishing a database connection"

#### Check ongoing incidents

First, check [http://travaux.ovh.com/](http://travaux.ovh.com/) that your datacentre, hosting cluster or Private SQL server is not affected by an incident on OVHcloud infrastructure.

> [!primary]
>
> To find this information, log in to your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), in the `Web Cloud`{.action} section:
>
> - To find your web hosting plan's datacentre and filer (file server), choose `Hosting plans`{.action} from the left-hand menu then the hosting plan concerned. You can find this information in the `General information`{.action} tab.
> - To find the **cluster** of servers on which your hosting is located, click on the `FTP-SSH`{.action} tab. This information will appear in the name of your `FTP server`.
> - To retrieve the name of your **Private SQL** server, click on `Databases`{.action} in the left-hand menu, then on the relevant offer. You can find this information under the heading `Host name` in the `SQL` part of `General information`{.action} tab.
>

#### Verify login credentials for your database <a name="config_file"></a>

Log in to the file storage space on your web hosting plan by [FTP](../log-in-to-storage-ftp-web-hosting/) and find your website’s configuration file (for example, for a WordPress website, this is the **wp-config.php** file located in the folder containing your website).

> [!warning]
>
> The choice and configuration of the file containing the database connection information is the responsibility of the content editor (CMS) concerned and not OVHcloud.
>
> We recommend that you contact the publisher of the [CMS](../web_hosting_web_hosting_modules/) used to create your website or a [specialised service provider](https://partner.ovhcloud.com/en-gb/) if you need one. We will not be able to assist you with this.
>

Then check the **exact** match between the login details for [PhpMyAdmin](../creating-database/#accessing-the-phpmyadmin-interface) and the login details for your website’s configuration file.

If necessary, change your [database password](../change-password-database/).

#### Example for WordPress

If your website displays an **"Error establishing a database connection"** message and none of your servers is affected by an [incident](http://travaux.ovh.com/), log in [FTP](../login-storage-ftp-web-hosting/) to your hosting plan then open the directory containing your website (by default, this is the `www' folder).

If this is a WordPress site, open the file "wp-config.php".

```php
define('DB_NAME', 'my_database');
 
/** MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

In your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), in the `Hosting plans`{.action} section, click on the `Databases`{.action} tab then check the correspondence between the elements displayed and those in the file `wp-config.php`:

- **my_database** must match what is noted as `Database name`;
- **my_user** must match what is noted as `User name`;
- **my_password** corresponds to your [database password](../change-password-database/);
- **my_server.mysql.db** must match what is noted as `Server address`.

> [!primary]
>
> If you are unable to restore access to your website as a result of these changes, [back up your database](../web_hosting_database_export_guide/) then [restore it to an earlier date](../restore-import-database/#restoring-a-specific-backup) from your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB).
>
> Then contact a [specialist provider](https://partner.ovhcloud.com/en-gb/) if necessary. We will not be able to assist you with this.
>

### You have exceeded the authorised quota

You have received an e-mail from our services stating that the amount of data on your database exceeds the authorised limit. Your database has therefore been switched to read-only mode. This will prevent your website from being modified.

![mail_overquota](images/mail_overquota.png){.thumbnail}

There are three ways you can unblock your database in this situation:

#### Method 1: upgrade your subscription

If you have a **Personal** or **Professional** web hosting plan, we recommend that you switch to the [higher web hosting plan](https://www.ovh.co.uk/web-hosting/). This subscription change will increase the size of your database which will automatically reopen it. This method is the simplest and does not require any particular technical expertise.

> [!warning]
>
> The increase of the size of your database may be linked to a malfunction in your website's internal code.
>
> In this case, changing your hosting plan would be ineffective, as your database will continue to fill up.
>
> If you notice a sudden increase in the size of your database, or if you have a "blog" type site that normally does not use much data, we advise you to contact immediately a [specialist provider](https://partner.ovhcloud.com/en-gb/). We will not be able to provide you with support on this matter.
>

To make this change, log in to your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB) then click on `Hosting plans`{.action} and on the relevant platform. Click on the `...`{.action} button in the `Solution` section on the right of your screen, then `Upgrade`{.action}.

If you are using a **Performance** offer, refer to [method 2](#method2).

#### Method 2: migrate your data to a larger database <a name=""method2"></a>

You can also migrate your data to a new database:

- order a larger [database](https://www.ovh.co.uk/web-hosting/sql-options.xml) if necessary then launch its [creation](../creating-database/);
- perform an [export of your data](../web_hosting_database_export_guide/), then [import them](../web_hosting_guide_to_importing_a_mysql_database/) in the new database;
- integrate the credentials of the new database into the [configuration file](#config_file) of your site.

> [!primary]
>
> If you have a **Performance** hosting plan, you can also [activate a free Private SQL server](../getting-started-with-private-sql/#private-sql-server-activation-included-with-your-web-hosting-plan).
>

#### Method 3: delete unnecessary data

Once you have made a [database backup](../web_hosting_database_export_guide/), log in to your [PhpMyAdmin interface](../creating-database/#accessing-the-phpmyadmin-interface) to delete any unnecessary data using the Drop, Delete and Truncate commands.

Then recalculate the size of your data from the `Databases`{.action} tab of the relevant hosting plan: click on the `...`{.action} button concerned, then on `Recalculate quota`{.action}.

> [!warning]
>
> This operation requires a high level of technical skill. We recommend contacting a [specialist provider](https://partner.ovhcloud.com/en-gb/) if you need to use this method. We will not be able to assist you with this.
>

#### Method 4: optimise your database

To optimise your database, follow the instructions in our guide [Configure your database server](../configure-optimise-database-server/#managing-your-databases_1). Then recalculate the quota used from the `Databases`{.action} tab of your hosting by clicking on the `...`{.action} button of the database concerned.

> [!warning]
>
> If the advices provided on how to optimise your database are not sufficient to unblock the access to your website, we recommend you to contact our [community](https://community.ovh.com/en/) or [OVHcloud partners](https://partner.ovhcloud.com/en-gb/). We will not be able to assist you in this regard.
>

### RAM overflows

The following message in the `Databases`{.action} section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB) indicates that your [Private SQL](https://www.ovh.co.uk/web-hosting/sql-options.xml) server has consumed too much resources on OVHcloud infrastructure:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

In this situation, you can increase the [amount of RAM](../configure-optimise-database-server/#modifying-the-database-server-solution_1) available from the `Databases`{.action} section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB). In the `General information`{.action} tab, click on the `...`{.action} in the `RAM` section.

You can also optimise your database by following the instructions of our guide "[Configure your database server](../configure-optimise-database-server/#managing-your-databases_1)".

[!primary]
>
> If you experience any difficulties in decreasing the use of resources on your database server, and you do not wish to increase them, please contact our [community of users](https://community.ovh.com/en/) or [OVHcloud partners](https://partner.ovhcloud.com/en-gb/). We will not be able to assist you with this.
>

### Database import errors

#### User access denied to database

>
> **"#1044 - Access denied for user to database"**
>

This error message means that the database you are trying to import contains elements that are not authorised on the OVHcloud shared infrastructure.

First make sure that your database is empty from the `Databases`{.action} tab of the relevant hosting plan (click on the `...`{.action} concerned then `Recalculate quota`{.action}) in order to [save your data ](../web_hosting_database_export_guide/) at first, delete the remaining ones then relaunch the import operation).

You can also tick the `Empty the current database`{.action} box just before [launching the import](../web_hosting_guide_to_importing_a_mysql_database/#import-your-own-backup-via-your-control-panel):

![database-import-empty](images/database-import-empty.png){.thumbnail}

If necessary, contact our [user community](https://community.ovh.com/en/) or a [specialised provider](https://partner.ovhcloud.com/en-gb/) for more information. We will not be able to assist you in correcting this issue.

> [!success]
>
> You cannot have a **"trigger"** in your database’s import script on OVHcloud shared hosting servers. In this situation, import your database to a [Private SQL server](https://www.ovh.co.uk/web-hosting/sql-options.xml).
>
> The following query is also not allowed:
>
>```bash
>CREATE DATABASE IF NOT EXISTS `Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
>```
>
> Remplacez-la par :
>
>```bash
>USE `Database-Name`;
>```
>
> (`Database-Name`: Enter the name of the database in your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB)
>

#### "MySQL server has gone away"

>
> **"404 ERROR MySQL server has gone away"**
>

This error message appears when [importing a database](../restore-import-database/#importing-a-local-backup) on a [Private SQL server](../getting-started-with-private-sql/). Most of the time it is related to a too important amount of data to import or a lack of SQL query optimisation in the  import script.

To resolve this issue, you can:

- Increase the [amount of RAM](../configure-optimise-database-server/#modifying-the-database-server-solution_1): go to the concerned [Private SQL server](../getting started-with-private-sql/) in the `Databases` section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB). Then click on the `...`{.action} button in the `RAM` section then on `Change the amount of RAM`{.action}.

- Split your database, in order to import it through several operations instead of one (for any questions on the manipulations to be carried out, contact our [community](https://community.ovh.com/en/) or the [OVHcloud partners](https://partner.ovhcloud.com/en-gb/). We will not be able to assist you with this.)

- [Optimise your database](../configure-optimise-database-server/#managing-your-databases_1) then repeat the export/import operations.

### Unable to access PhpMyAdmin

#### "Access denied for user"

>
> **"mysqli::real_connect(): (HY000/1045): Access denied for user"**
>

This error message may appear when connecting to your database by [PhpMyAdmin](../creating-database/#accessing-the-phpmyadmin-interface). It indicates that the credentials entered are incorrect.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

In this situation, [check the credentials entered](../connecting-to-database-on-database-server/#instructions) and change your [database password](../change-password-database/) if necessary.

#### "Too many connections"

>
> **"mysqli_real_connect(): (HY000/1040): Too many connections"**
>

The maximum number of active connections for databases delivered with shared hosting ([StartSQL](https://www.ovh.co.uk/web-hosting/sql-options.xml)) is **30**.

This number is **200** for the [Private SQL server](../getting-started-with-private-sql/). (This setting can be modified in the `Configuration`{.action} section of your database server.)

This message appears when [connecting to PhpMyAdmin](../creating-database/#accessing-the-phpmyadmin-interface) when this maximum number of connections is exceeded.

In this situation, you will need to [optimise your databases](../configure-optimise-database-server/#managing-your-databases_1) in order to reduce the number of active connections.

> [!warning]
>
> If you have any questions about the changes you need to make in order to reduce the number of active connections to your database, please contact our [community](https://community.ovh.com/en/) or [OVHcloud partners](https://partner.ovhcloud.com/en-gb/). We will not be able to assist you in this regard.
>

### "Name or service not known"

>
> **"mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known"**
>

This error message appears when [connecting to PhpMyAdmin](../connecting-to-database-on-database-server/#with-ovhcloud-phpmyadmin-for-private-sql-only) if the server name entered is incorrect.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Check the name of the server to be registered in your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB).

> [!success]
>
> If the database you would like to connect to appears in the `Databases`{.action} tab in the `Hosting plans`{.action} section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), the name to enter is in the `Server address` column.
>
> If you want to connect to a database on a [Private SQL server](../getting started-with-private-sql/), the server name to enter is in the tab `General information`{.action}, part `Login information`{.action}, `SQL`{.action} and labelled as `Host name`{.action}.
>

## Go further <a name="go further"></a>

[Getting started with Private SQL](../getting started-with-private-sql/)

[Resolving the most common 1-click module errors](../error-frequently-1-click-modules/)

For specialised services (SEO, development, etc.), contact [OVHcloud partners](https://partner.ovhcloud.com/en-gb/).

Join our community of users on https://https://community.ovh.com/en/
