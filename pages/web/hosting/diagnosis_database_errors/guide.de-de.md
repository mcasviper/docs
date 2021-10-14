---
title: Die häufigsten Datenbankfehler beheben 
excerpt "Diagnose der häufigsten Fehler in Zusammenhang mit Datenbanken"
slug: datenbanken-fehler
section: Diagnose
Bestellung 4
---

„Stand 08.10.2021“

Ziel**

Die Nutzung Ihrer Datenbanken kann zu einer Reihe von Anomalien auf Ihrer Website oder in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) sowie im [PhpMyAdmin](.../Datenbank-erstellen/#acceder-a-linterface-phpmyadmin) führen.

** Erfahren Sie, wie Sie Fehler in Zusammenhang mit Datenbanken auf OVHcloud Webhostings beheben.**

Warnung
>
> OVHcloud stellt Ihnen Dienste zur Verfügung, deren Konfiguration, Verwaltung und Verantwortung Ihnen obliegen. Es liegt daher an Ihnen, dafür zu sorgen, dass sie ordnungsgemäß funktionieren.
>
Wir stellen Ihnen diesen Leitfaden zur Verfügung, um Ihnen bei der Bewältigung alltäglicher Server-Verwaltungsaufgaben zu helfen. Wir empfehlen Ihnen, falls Sie Hilfe brauchen, einen spezialisierten Dienstleister zu kontaktieren und/oder sich auf der Website des Herausgebers zu informieren. Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten. Genauere Informationen finden Sie im Teil "Weiterführende Informationen" dieses Leitfadens.
>

Voraussetzungen

- Sie verfügen über ein [Webhosting](https://www.ovh.com/fr/hebergement-web/) von OVHcloud.
https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/de/&ovhSubsidiary=de
- Eines unserer Datenbankangebote verwenden (Web Cloud)(https://www.ovh.com/fr/hebergement-web/options-sql.xml), [SQL Private](.../erste-Schritte-mit-sql-private/) oder [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).

Beschreibung

## "Fehler bei der Verbindung zur Datenbank"

##### Aktuelle Störungen überprüfen

Überprüfen Sie zunächst auf [http://travaux.ovh.com/](http://travaux.ovh.com/), dass Ihr Rechenzentrum, Ihr Hosting-Cluster, Ihr SQL Private Server oder Cloud Databases nicht von einer Störung auf der OVHcloud Infrastruktur betroffen sind.

[!primary]
>
> Um zu diesen Informationen zu gelangen, loggen Sie sich in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) im Bereich Web Cloud {.action} ein:
>
> - Um zum Rechenzentrum Ihres Webhostings zu gelangen, gehen Sie auf die Liste der Hostings im linken Menü und klicken Sie auf die entsprechenden Hosting-Pakete. Diese Informationen finden Sie im Tab Allgemeine Informationen {.action}.
> - Um zu dem **Cluster** der Server zu gelangen, auf denen sich Ihr Hosting befindet, klicken Sie auf den Tab FTP-SSH {.action}. Diese Information erscheint im Namen Ihres FTP Servers.
> - Um den Namen Ihres Servers wiederzufinden **Private SQL** oder **Cloud Databases**, klicken Sie im linken Menü auf die Datenbanken {.action} und anschließend auf das entsprechende Angebot. Diese Information finden Sie unter dem Eintrag "Host`" im Tab "Allgemeine Informationen" {.action}.
>

##### Überprüfen Sie die Verbindungsdaten zu Ihrer Datenbank <a name="config_file"></a>

Verbinden Sie sich über [FTP](.../Verbindung-Speicherplatz-ftp-webhosting/) mit dem Speicherplatz der Dateien auf Ihrem Hosting und finden Sie die Konfigurationsdatei Ihrer Website (zum Beispiel für eine WordPress-Seite die Datei **wp-config.php** in dem Ordner Ihrer Website).

Warnung
>
> Die Wahl und Konfiguration der Datei mit den Verbindungsinformationen zur Datenbank ist für den jeweiligen Content Editor (CMS) und nicht für OVHcloud relevant.
>
> Wir empfehlen Ihnen daher, sich an den Herausgeber des [CMS](.../Module-en-1-klic/) zu wenden, mit dem Sie Ihre Website erstellen können, oder bei Bedarf einen [spezialisierter Dienstleister](https://partner.ovhcloud.com/fr/) zu kontaktieren. Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

Überprüfen Sie anschließend die Übereinstimmung **exakt** zwischen den Zugangsdaten zu [PhpMyAdmin](.../datenbank/#acceder-a-linterface-phpmyadmin) und denen der Konfigurationsdatei Ihrer Website.

Ändern Sie bei Bedarf das [Passwort Ihrer Datenbank](.../Passwort-Datenbank/).

##### Beispiel für Wordpress

Wenn Ihre Website eine Nachricht **"Fehler beim Login in die Datenbank"*** veröffentlicht und von einer [Störung](http://travaux.ovh.com/) nicht betroffen ist, loggen Sie sich in [FTP](.../ftp-speicherplatz-webhosting/) ein und öffnen Sie dann das Verzeichnis mit Ihrer Website (standardmäßig der Ordner www) .

Wenn es sich um eine WordPress Website handelt, öffnen Sie die Datei wp-config.php`.

PHP
define('DB_NAME', 'my_database');
 
/** MySQL username Database */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

In Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) klicken Sie im Bereich Hosting-Pakete {.action} auf den Tab \Datenbanken {.action} und überprüfen Sie anschließend die Übereinstimmung der angezeigten Elemente mit den in der Datei "wp-config.php"enthaltenen Elementen:

- **my_database** muss dem im Namen der Datenbank hinterlegten Wert entsprechen;
- **my_user** muss dem entsprechen, was in Benutzername` notiert wird;
- **my_password** entspricht dem [Passwort Ihrer Datenbank](.../datenbank-passwort/);
- **my_server.mysql.db* muss dem entsprechen, was in der @ Adresse des Servers angegeben ist.

[!primary]
>
> Wenn Sie mit diesen Änderungen den Zugriff auf Ihre Website nicht wiederherstellen können, [Datenbank-Backup](.../Export-Datenbanken/) und [Wiederherstellen zu einem früheren Zeitpunkt](.../Wiederherstellen-Datenbank-Import/#1-Wiederherstellung-eines-existierenden Backups) von Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) aus.
>
> Kontaktieren Sie gegebenenfalls einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/fr/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

### Überschreitung des erlaubten Quotas der Datenbank

Sie haben eine E-Mail von unseren Diensten erhalten, in der angegeben wird, dass die Datenmenge auf Ihrer Datenbank die erlaubte Grenze überschreitet. Ihre Datenbank wurde also nur gelesen. Dies verhindert jede Änderung Ihrer Website.

![mail_overquota](images/mail_overquota.png){.thumbnail}

Mit drei Methoden können Sie Ihre Datenbank entsperren:

#### Methode 1: Ihr Abo auf ein höheres Angebot umstellen

Wenn Sie über eine Formel **Basic2014** oder **Pro2014** verfügen, empfehlen wir Ihnen in dieser Situation, auf das [höhere Hosting-Angebot](https://www.ovh.com/fr/hebergement-web/) umzustellen. Diese Änderung des Abonnements erhöht die Größe Ihrer Datenbank, was sie automatisch wieder öffnet. Diese Methode ist die einfachste und erfordert keine besondere technische Kompetenz.

Warnung
>
> Die Vergrößerung Ihrer Datenbank kann auf eine Fehlfunktion im internen Code Ihrer Website zurückzuführen sein.
>
> Eine Anomalie kann zu einer dauerhaften Vergrößerung Ihrer Datenbank führen, da ein Wechsel des Webhosting Angebots nicht funktioniert.
>
> Daher empfehlen wir Ihnen, wenn Sie eine plötzliche Vergrößerung Ihrer Datenbank feststellen oder wenn Sie über eine Seite vom Typ "Blog"verfügen, die normalerweise keine Daten verbraucht, sofort einen [spezialisierten Dienstleister] zu kontaktieren(https://partner.ovhcloud.com/fr/). Wir werden Sie in dieser Angelegenheit nicht unterstützen können.
>

Loggen Sie sich hierfür zunächst in Ihr [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) ein, klicken Sie dann auf Hosting-Pakete {.action} und anschließend auf das betreffende Hosting. Klicken Sie auf den Button ...{.action} in der Rubrik Angebot` rechts auf Ihrem Bildschirm, dann auf@ Angebotswechsel {.action}.

Wenn Sie ein Angebot **Performance** verwenden, lesen Sie [Methode 2](#methode2).

#### Methode 2: Ihre Daten auf eine größere Datenbank <a name="methode2"></a> übertragen

Sie können Ihre Daten auch auf eine neue Datenbank migrieren:

- Wenn nötig, bestellen Sie eine [Datenbank](https://www.ovh.com/fr/hebergement-web/options-sql.xml) höherer Größe und starten Sie die [Erstellung](.../erstellen-datenbank/).
- Führen Sie einen [Export Ihrer Daten](.../Export-Datenbanken/) durch und [importieren Sie diese](.../Importieren-Anleitung-einer-mysql-Datenbank/) in die neue Datenbank.
- Integrieren Sie die Login-Daten der neuen Datenbank in die [Konfigurationsdatei] (#config_file) Ihrer Website.

[!primary]
>
> Wenn Sie über ein Hosting-Paket verfügen **Performance**, können Sie auch [kostenlos einen SQL Private Server aktivieren](.../erste-schritte-mit-sql-private/#aktivierung-ihres-sql-private-servers-inklusive-mit-ihrem-webhosting-angebot).
>

#### Methode 3: Unnötige Daten löschen

Loggen Sie sich nach einer [Sicherung Ihrer Datenbank](.../export-datenbanken/) mit Ihrem [PhpMyAdmin](.../erstellen-datenbank/#acceder-a-linterface-phpmyadmin) ein, um unnötige Daten mithilfe der Befehle Drop, Delete und Truncate zu löschen.

Starten Sie anschließend die Berechnung des verwendeten Quotas über den Tab @ Datenbanken {.action} des betreffenden Hostings neu: klicken Sie auf die Schaltfläche Kfz...{.action} betroffen und dann auf Quota {.action} neu berechnen.

Warnung
>
> Dieser Vorgang erfordert umfangreiche technische Kenntnisse. Wir empfehlen Ihnen, falls nötig einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/fr/) zu kontaktieren. Wir werden Ihnen in dieser Angelegenheit nicht helfen können.
>

#### Methode 4: Ihre Datenbank optimieren

Um Ihre Datenbank zu optimieren, folgen Sie den Anweisungen in unserer Anleitung "[Ihren Datenbank-Server konfigurieren](.../konfigurieren-optimieren-ihres-datenbanken/#optimieren-ihrer-datenbanken_1)". Beginnen Sie anschließend mit der Berechnung des verwendeten Quotas im Tab Datenbanken {.action} Ihres Hostings, indem Sie auf den Button klicken...{.action} aus der betreffenden Datenbank.

Warnung
>
> Wenn die Tipps zur Optimierung Ihrer Datenbank nicht ausreichen, um den Zugriff auf Ihre Website zu entsperren, empfehlen wir Ihnen, unsere [User Community](https://community.ovh.com) oder die [OVHcloud Partner](https://partner.ovhcloud.com/fr/) zu kontaktieren. Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

Überschreitungen der RAM-Kapazität

In der folgenden Nachricht im Bereich "Datenbanken {.action}"in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) wird darauf hingewiesen, dass Ihr Server [SQL Private](https://www.ovh.com/fr/hebergement-web/options-sql.xml) oder [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) zu viele Ressourcen auf der OVHcloud Infrastruktur verbraucht hat:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

In diesem Fall können Sie die [RAM-Menge](.../konfigurieren-Sie-Ihren-Datenbank-Server/#Monitoring-Nutzung), die im Bereich {.action} Datenbanken Ihres [OVHcloud Kundencenters](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) verfügbar ist, erhöhen. Klicken Sie im Tab Allgemeine Informationen {.action} auf die Schaltfläche Kfz...{.action} im Bereich RAM`.

Sie können Ihre Datenbank auch weiter optimieren, indem Sie die Anweisungen in unserer Anleitung "[Ihren Datenbankserver konfigurieren](.../konfigurieren-optimieren-ihres-datenbanken/#optimieren-ihrer-datenbanken_1)" befolgen.

[!primary]
>
> Wenn Sie Schwierigkeiten haben, die Nutzung von Ressourcen auf Ihrem Datenbankserver zu reduzieren, und diese nicht erhöhen möchten, kontaktieren Sie unsere [User Community](https://community.ovh.com) oder die [OVHcloud Partner](https://partner.ovhcloud.com/fr/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

## Fehler beim Import von Datenbanken

#### "Access denied for user to database"

>
> **"#1044 - Access denied for user to database**
>

Vergewissern Sie sich zunächst, dass Ihre Datenbank im Tab "Datenbanken des betreffenden Webhostings {.action}" leer ist (klicken Sie auf die Schaltfläche Kfz...{.action} betroffen und dann auf Quota {.action} neu berechnen, um [vorhandene Daten zu sichern](.../export-datenbanken/).

Sie können auch das Kästchen _leerung die aktuelle Datenbank {.action} kurz vor der [Import starten](.../Importhilfe-Hilfe-für-eine-mysql-Datenbank/#Eigene-Sicherung-aus-dem-Kunden importieren) ankreuzen:

![database-import-empty](images/database-import-empty.png){.thumbnail}

Diese Fehlermeldung bedeutet, dass die Datenbank, die Sie importieren möchten, unberechtigte Elemente auf der Shared Hosting Infrastruktur von OVHcloud enthält. Kontaktieren Sie gegebenenfalls unsere [User Community](https://community.ovh.com) oder einen spezialisierten Dienstleister(https://partner.ovhcloud.com/fr/). Wir werden Ihnen keine Hilfe bei der Behebung dieser Anomalie bieten können.

on-success:
>
> Es ist nicht erlaubt, einen **"Trigger"** im Importskript Ihrer Datenbank zu haben. Importieren Sie in diesem Fall Ihre Datenbank auf einen Server [SQL Private](https://www.ovh.com/fr/hebergement-web/options-sql.xml) oder [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).
>
> Außerdem ist folgender Antrag nicht zulässig:
>
>"bash
>CREATE DATABASE IF NOT EXISTS# Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
>```
>
> Ersetzen Sie sie durch:
>
>"bash
PaaS DataBase {{name}}
>```
>
>( Database-Name`: Geben Sie den Namen der Datenbank in Ihrem [OVHcloud Kundencenter] an(https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr)
>

#### "MySQL server has gone away"

>
ERROR MySQL server has gone away"**
>

Diese Fehlermeldung wird bei der [Import einer Datenbank](.../Wiederherstellung-Import-Datenbank/#2-Import-einer-lokalen Sicherung) auf einem Server [SQL Private](.../erste-Schritte-mit-sql-private/) angezeigt. Die Migration hängt meist mit der zu großen Datenmenge zusammen, die importiert werden soll, oder mit einer fehlenden Optimierung der SQL-Anfragen im Importskript.

Um diese Anomalie zu beheben können Sie:

- Erhöhung der [Arbeitsspeicherkapazität (RAM)](.../konfigurieren-Sie-Ihren-Datenbank-Server/#Den-RAM-Verbrauch überwachen). Gehen Sie hierzu auf den [SQL Private Server](.../erste Schritte mit-sql-private/), der im Bereich Datenbanken Ihres [OVHcloud Kundencenters](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) betroffen ist. Klicken Sie dann auf die Schaltfläche Kfz...{.action} im Bereich "RAM", dann wird der Arbeitsspeicher {.action} bearbeitet.

- Teilen Sie Ihre Datenbank auf, um sie in mehrere Operationen zu importieren und nicht in einen (für alle Fragen zu den durchzuführenden Operationen kontaktieren Sie bitte unsere [User Community](https://community.ovh.com) oder die [OVHcloud Partner](https://partner.ovhcloud.com/fr/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.

- [Optimieren Sie Ihre Datenbank](.../konfigurieren-optimieren-ihres-datenbank-servers/#optimieren-ihrer-datenbanken_1) und wiederholen Sie die Export- / Import-Operationen.

## Kein Zugriff auf PhpMyAdmin

### "Access denied for user"

>
> **« mysqli::real_connect(): (HY000/1045): Access denied for user"**
>

Diese Fehlermeldung kann bei der Verbindung zu Ihrer Datenbank durch [PhpMyAdmin](.../datenbank/#acceder-a-linterface-phpmyadmin) angezeigt werden. Sie gibt an, dass die eingegebenen Login-Daten falsch sind.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

Überprüfen Sie in diesem Fall [die eingegebenen Kennungen überprüfen](../datenbank-verbindung-server-bdd/#in der Praxis) und ändern Sie bei Bedarf das [Passwort Ihrer Datenbank](.../datenbank-passwort-ändern/).

### "Too many connections"

>
> **« mysqli_real_connect(): (HY000/1040): Too many connections"**
>

Die maximale Anzahl an aktiven Verbindungen für die mit den Shared Hosting Angeboten gelieferten Datenbanken ([StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml)) beträgt **30**.

Diese Zahl beträgt **200** für die Datenbanken der Server [SQL Private](.../erste Schritte-mit-sql-private/) und [Cloud Databases](https://www.ovh.com/fr/cloud-databases/). (Diese Einstellung kann im Bereich Konfiguration {.action} Ihres Datenbankservers geändert werden).

Diese Nachricht erscheint bei der [Verbindung zu PhpMyAdmin](../Datenbank-erstellen/#acceder-a-linterface-phpmyadmin), wenn diese maximale Anzahl an Verbindungen überschritten wird.

In dieser Situation müssen Sie [Ihre Datenbanken optimieren](.../konfigurieren-optimieren-ihres-datenbank-servers/#optimieren-ihrer-datenbanken_1), um die Anzahl der aktiven Verbindungen zu reduzieren.

Warnung
>
> Wenn Sie Fragen zu den notwendigen Schritten zur Reduzierung der Anzahl aktiver Verbindungen auf Ihrer Datenbank haben, kontaktieren Sie unsere [User Community](https://community.ovh.com) oder die [OVHcloud Partner](https://partner.ovhcloud.com/fr/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

### "Name or service not known"

>
> **« mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known"**
>

Diese Fehlermeldung wird bei der [Verbindung zu PhpMyAdmin](.../datenbankverbindung-server-bdd/#in der Praxis) angezeigt, wenn der angegebene Servername nicht korrekt ist.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Überprüfen Sie den Namen des in Ihrem [OVHcloud Kundencenter] zu registrierenden Servers(https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).

on-success:
>
> Wenn die Datenbank, mit der Sie sich verbinden möchten, im Tab Datenbanken {.action} in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) steht, wird der Name, der angegeben werden soll, in der Spalte Serveradresse angegeben.
>
> Wenn Sie sich mit einer Datenbank auf einem Server verbinden möchten (SQL Private)(.../erste-Schritte-mit-sql-private/) oder [Cloud Databases](https://www.ovh.com/fr/cloud-databases/), wird der einzugebende Server im Tab Allgemeine Informationen {.action}, Teil Verbindungsinformationen {.action}, SQL {.action} und im Bereich Hostname {.action}.
>

### Keine Verbindung auf einer Cloud Databases Datenbank möglich

Mit einem Server [Cloud Databases](https://docs.ovh.com/fr/clouddb/) können Sie sich [mit Ihren Datenbanken verbinden](.../datenbankverbindung-server-bdd/) von Ihrem Computer oder einem Server außerhalb der Infrastruktur von OVHcloud aus verbinden.

Sollte diese Verbindung nicht möglich sein, überprüfen Sie zunächst, ob Sie sich mit dem Datenbankserver verbinden können (Ihre öffentliche IP-Adresse autorisiert)(https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/#autoriser-une-adresse-ip).

Wenn diese Operation erfolgreich durchgeführt wurde, wenden Sie sich bitte an Ihren Internetprovider oder die [OVHcloud Partner](https://partner.ovhcloud.com/fr/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.

## Mehr <a name="Mehr"></a>

[erste Schritte mit dem SQL Private](.../erste Schritte mit-sql-private/)

[erste Schritte mit CloudDB](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/)

Für spezialisierte Dienstleistungen (Referenzierung, Entwicklung etc.) kontaktieren Sie die [OVHcloud Partner](https://partner.ovhcloud.com/fr/).

„Für den Austausch mit unserer User Community gehen Sie auf https://community.ovh.com/en/.“
