---
title: Troubleshoot common database errors 
excerpt: `Diagnose the most common cases of database errors`
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
- one of our database offers [Web Cloud](https://www.ovh.com/fr/hebergement-web/options-sql.xml) or [Private SQL](../getting started-with-private-sql/).

Instructions

### `Error connecting to database`

### Check ongoing incidents

First, check [http://travaux.ovh.com/](http://travaux.ovh.com/) that your datacentre, hosting cluster, Private SQL server or Cloud Databases server is not affected by an incident on OVHcloud infrastructure.

[!primary]
>
> To find this information, log in to your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), in the `Web Cloud`{.action} section:
>
> - To find your web hosting plan's datacentre and filer (file server), choose `Hosting`{.action}` from the left-hand menu, then the hosting plan concerned. You can find this information in the `General information`{.action} tab.
> - To find the **cluster** of servers on which your hosting is located, click on the `FTP-SSH`{.action} tab. This information will appear in the name of your FTP server.
> - To retrieve the name of your **Private SQL** or **Cloud Databases** server, click on `Databases`{.action} in the left-hand menu, then on the relevant solution. You can find this information under the heading 'Host' in the tab 'General information`{.action}.
>

#### Verify login credentials for your database <a name=`config_file`></a>

Log in to the file storage space on your web hosting plan by [FTP](../login-storage-ftp-web-hosting-ftp/) and find your website’s configuration file (for example, for a WordPress website, this is the **wp-config.php** file located in the folder containing your website).

Warning
>
> The choice and configuration of the file containing the database connection information is the responsibility of the content editor (CMS) concerned and not OVHcloud.
>
> We recommend that you contact the publisher of the [CMS](../modules-en-1-clic/) used to create your website, or contact a [specialised service provider](https://partner.ovhcloud.com/fr/) if you need one. We will not be able to assist you with this.
>

Then check the **exact** match between the login details for [PhpMyAdmin](../create-database/#access-a-interface-phpmyadmin) and the login details for your website’s configuration file.

If necessary, change your [database password](../change-database password/).

#### Example for WordPress

If your website displays an **“Error connecting to the database”** message and it is not affected by an [incident](http://travaux.ovh.com/), log in [FTP](../login-storage-ftp-web-hosting/) to your hosting plan, then open the directory containing your website (by default, this is the `www' folder).

If this is a WordPress site, open the file `wp-config.php'.

```php
define('DB_NAME', 'my_database');
 
/** MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
,

In your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), in the Hosting section, click on the `Databases`{.action} tab, then check the correspondence between the elements displayed and those in the file `wp-config.php`:

- **my_database** must match what is noted in `Database name`;
- **my_user** must match what is noted in `User name`;
- **my_password** corresponds to [your database password](../change-database-password/)
- **my_server.mysql.db** must match what is noted in 'Server address'.

[!primary]
>
> If you are unable to restore access to your website as a result of these changes, [back up your database](../export-databases/) then [restore it to an earlier date](../restore-import-database/#1-restore-an-existing-backup) from your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB).
>
> Then contact a [specialist provider](https://partner.ovhcloud.com/fr/) if necessary. We will not be able to assist you with this.
>

### Exceeding the authorised quota of the database

You have received an email from our services stating that the amount of data on your database exceeds the authorised limit. Your database has therefore been switched to read-only mode. This will prevent your website from being modified.

![mail_overquota](images/mail_overquota.png){.thumbnail}

There are three ways you can unblock your database:

### Method 1: upgrade your subscription

If you have a **Personal2014** or **Pro2014** plan, we recommend that you switch to the [higher web hosting plan](https://www.ovh.com/fr/hebergement-web/). This subscription change will increase the size of your database, which will automatically reopen it. This method is the simplest and does not require any particular technical expertise.

Warning
>
> The increase in the size of your database may be linked to a malfunction in your website's internal code.
>
> An anomaly may result in a permanent increase in the size of your database, in which case the change of hosting offer would be ineffective.
>
> If you notice a sudden increase in the size of your database, or if you have a `blog` type site that normally does not use much data, we advise you to contact immediately a [specialist provider](https://partner.ovhcloud.com/fr/). We will not be able to provide you with support on this matter.
>

To make this change, log in to your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB) then click on `Hosting`{.action}, then the relevant hosting plan. Click the `... button`{.action} in the `Offer' section on the right of your screen, then `Change Offer`{.action}.

If you are using a **Performance** offer, refer to [method 2](#method2).

### Method 2: migrate your data to a larger database <a name=`method2`></a>

You can also migrate your data to a new database:

- Order a larger [database](https://www.ovh.com/fr/hebergement-web/options-sql.xml) if necessary, then launch its [creation](../create-database/)
- Perform a [export your data](../export-databases/), then [import them](../share-guide-import-of-a-mysql-database/) in the new database;
- Integrate the credentials of the new database into the [configuration file](#config_file) of your site.

[!primary]
>
> If you have a **Performance** hosting plan, you can also [activate a free Private SQL server](../get-started-with-private-sql/#activate-your-private-sql-server-included-with-your-web-hosting-offer).
>

### Method 3: delete unnecessary data

Once you have made a [database backup](../export-databases/), log in to your [PhpMyAdmin] interface(../create-database/#access-a-phpmyadmin) to delete any unnecessary data using the Drop, Delete and Truncate commands.

Then recalculate the quota used from the `Databases`{.action} tab of the relevant hosting plan: click the `...`{.action} concerned, then `Recalculate quota`{.action}.

Warning
>
> This operation requires a high level of technical skill. We recommend contacting a [specialist provider](https://partner.ovhcloud.com/fr/) if you need to do so. We will not be able to assist you with this.
>

### Method 4: optimise your database

To optimise your database, follow the instructions in our guide `[Configure your database server](.../configure-optimise-your-database-server/#optimise-your-databases_1)`. Then recalculate the quota used from the `Databases`{.action} tab of your hosting, by clicking on the `...`{.action} of the database concerned.

Warning
>
> If the advice provided on optimising your database was not enough to unblock access to your website, we recommend that you contact our [user community](https://community.ovh.com) or [OVHcloud partners](https://partner.ovhcloud.com/fr/). We will not be able to assist you in this regard.
>

RAM overflows

The following message in the `Databases`{.action} section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB) indicates that your [Private SQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) or [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) server has consumed too many resources on OVHcloud infrastructure:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

In this situation, you can increase the [amount of RAM](.../configure-optimise-your-database-server/#monitor-usage) available from the `Databases`{.action} section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB). In the `General information`{.action} tab, click the `...`{.action} in the `RAM' section.

You can also optimise your database by following the instructions in our guide “[Configure your database server](../configure-optimise-your-database-server/#optimise-your-databases_1)”.

[!primary]
>
> If you experience any difficulties in decreasing the use of resources on your database server, and you do not wish to increase them, please contact our [community of users](https://community.ovh.com) or [OVHcloud partners](https://partner.ovhcloud.com/fr/). We will not be able to assist you with this.
>

### Database import errors

### “Access denied for user to database”

>
> **“#1044 - Access denied for user to database”**
>

First make sure that your database is empty from the `Databases`{.action} tab of the relevant hosting plan (click on the `...`{.action} concerned, then `Recalculate quota`{.action}) in order to [save the data present](../export-databases/).

You can also tick the `Empty the current database`{.action} box just before [launching the import](.../mysql-database-import-guide/#import-your-own-backup-from-the-control-panel):

![database-import-empty](images/database-import-empty.png){.thumbnail}

This error message means that the database you are trying to import contains elements that are not authorised on the OVHcloud shared infrastructure. If necessary, contact our [user community](https://community.ovh.com) or a [specialised provider](https://partner.ovhcloud.com/fr/) for more information. We will not be able to assist you in correcting this issue.

> [!success]
>
> You cannot have a **“trigger”** in your database’s import script on OVHcloud shared hosting servers. In this situation, import your database to a [Private SQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) or [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) server.
>
> The following query is not allowed:
>
>```bash
>CREATE DATABASE IF NOT EXISTS `Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
,
>
> Replace it with:
>
>```bash
>USE `Database-Name`;
,
>
>(`Database-Name`: Enter the name of the database in your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB)
>

### “MySQL server has gone away”

>
404 ERROR MySQL server has gone away”**
>

This error message appears when [importing a database](../restore-import-database/#2-import-a-local-backup) on a server [Private SQL](../getting-started-with-private-sql/). Most of the time it is related to too much data to import or a lack of SQL query optimisation in the import script.

To resolve this issue, you can:

- Increase the [amount of RAM](../configure-optimise-your-database-server/#monitor-usage). To do this, go to the [Private SQL server](../getting started-with-private-sql/) concerned in the ‘Databases’ section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB). Then click the `... button.`{.action} in the `RAM' section, then `Change RAM`{.action}.

- Split your database, in order to import it into several operations instead of one (for any questions on the manipulations to be carried out, contact our [community of users](https://community.ovh.com) or the [OVHcloud partners](https://partner.ovhcloud.com/fr/). We will not be able to assist you with this.)

- [Optimise your database](../configure-optimise-your-database-server/#optimise-your-databases_1) then repeat the export/import operations.

### Unable to access PhpMyAdmin

### `Access denied for user`

>
> **“mysqli::real_connect(): (HY000/1045): Access denied for user”*
>

This error message may appear when connecting to your database by [PhpMyAdmin](../create-database/#access-a-phpmyadmin-interface). It indicates that the credentials entered are incorrect.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

In this situation, [check the credentials entered](../database-login-database-server-db/#in-practice) and change [your database password](../change-database-password/) if necessary.

### `Too many connections`

>
> **“mysqli_real_connect(): (HY000/1040): Too many connections”**
>

The maximum number of active connections for databases delivered with shared hosting ([StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml)) is **30**.

This number is **200** for the [Private SQL](../getting-started-with-private-sql/) and [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) server databases. (This setting can be modified in the `Configuration`{.action} section of your database server.)

This message appears when [connecting to PhpMyAdmin](../create-database/#access-a-interface-phpmyadmin) when this maximum number of connections is exceeded.

In this situation, you will need to [optimise your databases](../configure-optimise-your-database-server/#optimise-your-databases_1) in order to reduce the number of active connections.

Warning
>
> If you have any questions about the changes you need to make in order to reduce the number of active connections to your database, please contact our [user community](https://community.ovh.com) or [OVHcloud partners](https://partner.ovhcloud.com/fr/). We will not be able to assist you in this regard.
>

### `Name or service not known`

>
> **“mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known**
>

This error message appears when [connecting to PhpMyAdmin](../database-database-server-connection/#in-practice) when the server name entered is incorrect.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Check the name of the server to be registered in your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB).

> [!success]
>
> If the database you would like to connect to appears in the `Databases`{.action} tab in the `Hosting`{.action} section of your [OVHcloud Control Panel](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.co.uk/&ovhSubsidiary=GB), the name to enter is entered in the `Server address' column.
>
> If you want to connect to a database on a server [Private SQL](../getting started-with-private-sql/) or [Cloud Databases](https://www.ovh.com/fr/cloud-databases/), the server name to enter is entered in the tab `General information`{.action}, part `Connection information`{.action}, `SQL`{.action} and in the topic `Host name`{.action}.
>

### Unable to connect to a Cloud Databases database

Having a [Cloud Databases] server (https://docs.ovh.com/fr/clouddb/) allows you to [connect to your databases](../database-connection-database-database-server/) from your computer or a server outside the OVHcloud infrastructure.

If this connection is not possible, first verify that you have [authorised your public IP address](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/#autoriser-une-adresse-ip) to connect to the database server.

If this operation has been carried out successfully, contact your Internet Service Provider or [OVHcloud partners](https://partner.ovhcloud.com/fr/). We will not be able to assist you in this situation.

## Go further <a name=`go further`></a>

[Getting started with Private SQL](../getting started-with-private-sql/)

[Getting started with the CloudDB service](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/)

For specialised services (SEO, development, etc.), contact [OVHcloud partners](https://partner.ovhcloud.com/fr/).

Join our community of users on https://https://community.ovh.com/en/{.external}
