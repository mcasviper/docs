---
title: Die häufigsten Datenbankfehler beheben 
excerpt: Diagnose der häufigsten Fehler in Zusammenhang mit Datenbanken
slug: datenbanken-fehler
section: Diagnose
order: 4
---

> [!primary]
> Diese Übersetzung wurde durch unseren Partner SYSTRAN automatisch erstellt. In manchen Fällen können ungenaue Formulierungen verwendet worden sein, z.B. bei der Beschriftung von Schaltflächen oder technischen Details. Bitte ziehen Sie beim geringsten Zweifel die englische oder französische Fassung der Anleitung zu Rate. Möchten Sie mithelfen, diese Übersetzung zu verbessern? Dann nutzen Sie dazu bitte den Button “Mitmachen“ auf dieser Seite.
>

**Letzte Aktualisierung am 08.10.2021**

## Ziel

Die Nutzung Ihrer Datenbanken kann zu einer Reihe von Anomalien auf Ihrer Website oder in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) sowie im [PhpMyAdmin](../datenbank-erstellen/#auf-das-phpmyadmin-interface-zugreifen) führen.

**Erfahren Sie, wie Sie Fehler in Zusammenhang mit Datenbanken auf OVHcloud Webhostings beheben.**

> [!warning]
>
> OVHcloud stellt Ihnen Dienste zur Verfügung, deren Konfiguration, Verwaltung und Verantwortung Ihnen obliegen. Es liegt daher an Ihnen, dafür zu sorgen, dass sie ordnungsgemäß funktionieren.
>
> Wir stellen Ihnen diesen Leitfaden zur Verfügung, um Ihnen bei der Bewältigung alltäglicher Server-Verwaltungsaufgaben zu helfen. Wir empfehlen Ihnen, falls Sie Hilfe brauchen, einen spezialisierten Dienstleister zu kontaktieren und/oder sich auf der Website des Herausgebers zu informieren. Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten. Genauere Informationen finden Sie im Teil [Weiterführende Informationen](#gofurther) dieses Leitfadens.
>

## Voraussetzungen

- Sie verfügen über ein [Webhosting](https://www.ovh.de/hosting/) von OVHcloud.
- Sie sind in Ihrem [OVHcloud Kundencenter eingeloggt](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/de/&ovhSubsidiary=de).
- Sie verwenden eines unserer [Web Cloud](https://www.ovh.de/hosting/sql-optionen.xml) oder [SQL Private](../erste-schritte-mit-sql-private/) Datenbankangebote.

## In der praktischen Anwendung

### “Fehler beim Aufbau einer Datenbankverbindung“

#### Aktuelle Störungen überprüfen

Überprüfen Sie zunächst auf [http://travaux.ovh.com/](http://travaux.ovh.com/), dass Ihr Datacenter, Ihr Hosting-Cluster, Ihr SQL Private Server nicht von einer Störung auf der OVHcloud Infrastruktur betroffen sind.

> [!primary]
>
> Um zu diesen Informationen zu gelangen, loggen Sie sich in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) im Bereich `Web Cloud`{.action} ein:
>
> - Um zum **Datacenter** Ihres Webhostings zu gelangen, gehen Sie auf die Liste der Hostings im linken Menü und klicken Sie auf die entsprechenden Hosting-Pakete. Diese Informationen finden Sie im Tab `Allgemeine Informationen`{.action}.
> - Um zu dem **Cluster** der Server zu gelangen, auf denen sich Ihr Hosting befindet, klicken Sie auf den Tab `FTP-SSH`{.action}. Diese Information erscheint im Namen Ihres `FTP-Server`.
> - Um den Namen Ihres Servers wiederzufinden **Private SQL**, klicken Sie im linken Menü auf die `Datenbanken`{.action} und anschließend auf das entsprechende Angebot. Diese Information finden Sie unter dem Eintrag `Hostname` im Tab `Allgemeine Informationen`{.action}.
>

#### Überprüfen Sie die Verbindungsdaten zu Ihrer Datenbank <a name="config_file"></a>

Verbinden Sie sich über [FTP](../verbindung-ftp-speicher-webhosting/) mit dem Speicherplatz der Dateien auf Ihrem Hosting und finden Sie die Konfigurationsdatei Ihrer Website (zum Beispiel für eine WordPress-Seite die Datei **wp-config.php** in dem Ordner Ihrer Website).

> [!warning]
>
> Die Wahl und Konfiguration der Datei mit den Verbindungsinformationen zur Datenbank ist für den jeweiligen Content Editor (CMS) und nicht für OVHcloud relevant.
>
> Wir empfehlen Ihnen daher, sich an den Herausgeber des [CMS](../webhosting_installation_von_webhosting-modulen/) zu wenden, mit dem Sie Ihre Website erstellen können, oder bei Bedarf einen [spezialisierter Dienstleister](https://partner.ovhcloud.com/de/) zu kontaktieren. Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

Überprüfen Sie anschließend die Übereinstimmung **exakt** zwischen den Zugangsdaten zu [PhpMyAdmin](../datenbank-erstellen/#auf-das-phpmyadmin-interface-zugreifen) und denen der Konfigurationsdatei Ihrer Website.

Ändern Sie bei Bedarf das [Passwort Ihrer Datenbank](../datenbank-passwort-aendern/).

#### Beispiel für Wordpress

Wenn Ihre Website eine Nachricht **“Fehler beim Login in die Datenbank“** veröffentlicht und von einer [Störung](http://travaux.ovh.com/) nicht betroffen ist, loggen Sie sich in [FTP](../verbindung-ftp-speicher-webhosting/) ein und öffnen Sie dann das Verzeichnis mit Ihrer Website (standardmäßig der Ordner www) .

Wenn es sich um eine WordPress Website handelt, öffnen Sie die Datei **wp-config.php**.

```php
define('DB_NAME', 'my_database');
 
/** MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

In Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) klicken Sie im Bereich `Hosting-Pakete`{.action} auf den Tab `Datenbanken`{.action} und überprüfen Sie anschließend die Übereinstimmung der angezeigten Elemente mit den in der Datei **wp-config.php** enthaltenen Elementen:

- **my_database** muss dem im Namen der Datenbank hinterlegten Wert entsprechen;
- **my_user** muss dem entsprechen, was in `Benutzername` notiert wird;
- **my_password** entspricht dem [Passwort Ihrer Datenbank](../datenbank-passwort-aendern/);
- **my_server.mysql.db** muss dem entsprechen, was in der `Server-Adresse` angegeben ist.

> [!primary]
>
> Wenn Sie mit diesen Änderungen den Zugriff auf Ihre Website nicht wiederherstellen können, [Datenbank-Backup](../webhosting_hilfe_zum_export_von_datenbanken/) und [Wiederherstellen zu einem früheren Zeitpunkt](../datenbank-importieren/#datenbank-uber-das-kundencenter-wiederherstellen-und-importieren) von Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) aus.
>
> Kontaktieren Sie gegebenenfalls einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/de/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

### Überschreitung des erlaubten Quotas der Datenbank

Sie haben eine E-Mail von unseren Diensten erhalten, in der angegeben wird, dass die Datenmenge auf Ihrer Datenbank die erlaubte Grenze überschreitet. Ihre Datenbank wurde also nur gelesen. Dies verhindert jede Änderung Ihrer Website.

![mail_overquota](images/mail_overquota.png){.thumbnail}

Mit drei Methoden können Sie Ihre Datenbank entsperren:

#### Methode 1: Ihr Abo auf ein höheres Angebot umstellen

Wenn Sie über eine Formel **Basic** oder **Pro** verfügen, empfehlen wir Ihnen in dieser Situation, auf das [höhere Hosting-Angebot](https://www.ovh.de/hosting/) umzustellen. Diese Änderung des Abonnements erhöht die Größe Ihrer Datenbank, was sie automatisch wieder öffnet. Diese Methode ist die einfachste und erfordert keine besondere technische Kompetenz.

> [!warning]
>
> Die Vergrößerung Ihrer Datenbank kann auf eine Fehlfunktion im internen Code Ihrer Website zurückzuführen sein.
>
> Eine Anomalie kann zu einer dauerhaften Vergrößerung Ihrer Datenbank führen, da ein Wechsel des Webhosting Angebots nicht funktioniert.
>
> Daher empfehlen wir Ihnen, wenn Sie eine plötzliche Vergrößerung Ihrer Datenbank feststellen oder wenn Sie über eine Seite vom Typ “Blog“ verfügen, die normalerweise keine Daten verbraucht, sofort einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/de/) zu kontaktieren. Wir werden Sie in dieser Angelegenheit nicht unterstützen können.
>

Loggen Sie sich hierfür zunächst in Ihr [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) ein, klicken Sie dann auf `Hosting-Pakete`{.action} und anschließend auf das betreffende Hosting. Klicken Sie auf den Button `...`{.action} in der Rubrik `Angebot`{.action} in `Abo`{.action} rechts auf Ihrem Bildschirm, dann auf `Upgraden`{.action}.

Wenn Sie ein Angebot **Performance** verwenden, lesen Sie [Methode 2](#methode2).

#### Methode 2: Ihre Daten auf eine größere Datenbank übertragen <a name="methode2"></a>

Sie können Ihre Daten auch auf eine neue Datenbank migrieren:

- Wenn nötig, bestellen Sie eine [Datenbank](https://www.ovh.de/hosting/sql-optionen.xml) höherer Größe und starten Sie die [Erstellung](../datenbank-erstellen/).
- Führen Sie einen [Export Ihrer Daten](../webhosting_hilfe_zum_export_von_datenbanken/) durch und [importieren Sie diese](../webhosting_import_einer_mysql-datenbank/) in die neue Datenbank.
- Integrieren Sie die Login-Daten der neuen Datenbank in die [Konfigurationsdatei](#config_file) Ihrer Website.

> [!primary]
>
> Wenn Sie über ein Hosting-Paket verfügen **Performance**, können Sie auch [kostenlos einen SQL Private Server aktivieren](../erste-schritte-mit-sql-private/#aktivierung-des-in-ihrem-webhosting-angebot-enthaltenen-private-sql-servers).
>

#### Methode 3: Unnötige Daten löschen

Loggen Sie sich nach einer [Sicherung Ihrer Datenbank](../webhosting_hilfe_zum_export_von_datenbanken/) mit Ihrem [PhpMyAdmin](../datenbank-erstellen/#auf-das-phpmyadmin-interface-zugreifen) ein, um unnötige Daten mithilfe der Befehle Drop, Delete und Truncate zu löschen.

Starten Sie anschließend die Berechnung des verwendeten Quotas über den Tab `Datenbanken`{.action} des betreffenden Hostings neu: klicken Sie auf die Schaltfläche `...`{.action} betroffen und dann auf `Das Quota neu berechnen`{.action}.

> [!warning]
>
> Dieser Vorgang erfordert umfangreiche technische Kenntnisse. Wir empfehlen Ihnen, falls nötig einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/de/) zu kontaktieren. Wir werden Ihnen in dieser Angelegenheit nicht helfen können.
>

#### Methode 4: Ihre Datenbank optimieren

Um Ihre Datenbank zu optimieren, folgen Sie den Anweisungen in unserer Anleitung “[Konfigurieren Ihres Datenbankservers](../konfigurieren-ihres-datenbank-servers/#ihre-datenbanken-optimieren_1)“. Beginnen Sie anschließend mit der Berechnung des verwendeten Quotas im Tab `Datenbanken`{.action} Ihres Hostings, indem Sie auf den Button klicken `...`{.action} aus der betreffenden Datenbank.

> [!warning]
>
> Wenn die Tipps zur Optimierung Ihrer Datenbank nicht ausreichen, um den Zugriff auf Ihre Website zu entsperren, empfehlen wir Ihnen, unsere [User Community](https://community.ovh.com/en/) oder die [OVHcloud Partner](https://partner.ovhcloud.com/de/) zu kontaktieren. Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

### Überschreitungen der RAM-Kapazität

In der folgenden Nachricht im Bereich `Datenbanken`{.action} in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) wird darauf hingewiesen, dass Ihr [Server SQL Private](https://www.ovh.de/hosting/sql-optionen.xml) zu viele Ressourcen auf der OVHcloud Infrastruktur verbraucht hat:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

In diesem Fall können Sie die [RAM-Menge](../konfigurieren-ihres-datenbank-servers/#wechseln-des-datenbank-angebots_1), die im Bereich `Datenbanken`{.action} Ihres [OVHcloud Kundencenters](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) verfügbar ist, erhöhen. Klicken Sie im Tab `Allgemeine Informationen`{.action} auf die Schaltfläche `...`{.action} im Bereich `RAM`.

Sie können Ihre Datenbank auch weiter optimieren, indem Sie die Anweisungen in unserer Anleitung “[Ihren Datenbankserver konfigurieren](../konfigurieren-ihres-datenbank-servers/#uberprufung-der-ram-nutzung)“ befolgen.

[!primary]
>
> Wenn Sie Schwierigkeiten haben, die Nutzung von Ressourcen auf Ihrem Datenbankserver zu reduzieren, und diese nicht erhöhen möchten, kontaktieren Sie unsere [User Community](https://community.ovh.com/en/) oder die [OVHcloud Partner](https://partner.ovhcloud.com/de/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

### Fehler beim Import von Datenbanken

#### “Access denied for user to database“

>
> **“#1044 - Access denied for user to database“**
>

Vergewissern Sie sich zunächst, dass Ihre Datenbank im Tab `Datenbanken`{.action} des betreffenden Webhostings leer ist (klicken Sie auf die Schaltfläche `...`{.action} betroffen und dann auf `Das Quota neu berechnen`{.action}, um [vorhandene Daten zu sichern](../webhosting_hilfe_zum_export_von_datenbanken/).

Sie können auch das Kästchen leerung die aktuelle `Datenbanken`{.action} kurz vor der [Import starten](../webhosting_import_einer_mysql-datenbank/#eigene-backup-datei-uber-das-kundencenter-importieren) ankreuzen:

![database-import-empty](images/database-import-empty.png){.thumbnail}

Diese Fehlermeldung bedeutet, dass die Datenbank, die Sie importieren möchten, unberechtigte Elemente auf der Shared Hosting Infrastruktur von OVHcloud enthält. Kontaktieren Sie gegebenenfalls unsere [Community](https://community.ovh.com/en/) oder einen [spezialisierten Dienstleister](https://partner.ovhcloud.com/de/). Wir werden Ihnen keine Hilfe bei der Behebung dieser Anomalie bieten können.

> [!success]
>
> Es ist nicht erlaubt, einen **“Trigger“** im Importskript Ihrer Datenbank zu haben. Importieren Sie in diesem Fall Ihre Datenbank auf einen [SQL Private Server](https://www.ovh.de/hosting/sql-optionen.xml).
>
> Außerdem ist folgender Antrag nicht zulässig:
>
>```bash
>CREATE DATABASE IF NOT EXISTS `Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
>```
>
> Ersetzen Sie sie durch:
>
>```bash
>USE `Database-Name`;
>```
>
> (`Database-Name`: Geben Sie den Namen der Datenbank in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) an)
>

#### “MySQL server has gone away“

>
> **ERROR MySQL server has gone away“**
>

Diese Fehlermeldung wird bei der [Import einer Datenbank](../datenbank-importieren/#eine-lokale-sicherung-importieren) auf einem Server [SQL Private](../erste-schritte-mit-sql-private/) angezeigt. Die Migration hängt meist mit der zu großen Datenmenge zusammen, die importiert werden soll, oder mit einer fehlenden Optimierung der SQL-Anfragen im Importskript.

Um diese Anomalie zu beheben können Sie:

- Erhöhung der [Arbeitsspeicherkapazität (RAM)](../konfigurieren-ihres-datenbank-servers/#wechseln-des-datenbank-angebots_1). Gehen Sie hierzu auf den [SQL Private Server](../erste-schritte-mit-sql-private/), der im Bereich Datenbanken Ihres [OVHcloud Kundencenters](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) betroffen ist. Klicken Sie dann auf die Schaltfläche `...`{.action} im Bereich `RAM`, dann wird der Arbeitsspeicher `RAM-Menge ändern`{.action} bearbeitet.

- Teilen Sie Ihre Datenbank auf, um sie in mehrere Operationen zu importieren und nicht in einen (für alle Fragen zu den durchzuführenden Operationen kontaktieren Sie bitte unsere [User Community](https://community.ovh.com/en/) oder die [OVHcloud Partner](https://partner.ovhcloud.com/de/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.

- [Optimieren Sie Ihre Datenbank](../konfigurieren-ihres-datenbank-servers/#ihre-datenbanken-optimieren_1) und wiederholen Sie die Export/Import-Operationen.

### Kein Zugriff auf PhpMyAdmin

#### “Access denied for user“

>
> **“ mysqli::real_connect(): (HY000/1045): Access denied for user“**
>

Diese Fehlermeldung kann bei der Verbindung zu Ihrer Datenbank durch [PhpMyAdmin](../datenbank-erstellen/#auf-das-phpmyadmin-interface-zugreifen) angezeigt werden. Sie gibt an, dass die eingegebenen Login-Daten falsch sind.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

Überprüfen Sie in diesem Fall [die eingegebenen Kennungen überprüfen](../datenbank-verbindung-auf-bdd/#in-der-praktischen-anwendung) und ändern Sie bei Bedarf das [Passwort Ihrer Datenbank](../datenbank-passwort-aendern/).

#### “Too many connections“

>
> **“mysqli_real_connect(): (HY000/1040): Too many connections“**
>

Die maximale Anzahl an aktiven Verbindungen für die mit den Shared Hosting Angeboten gelieferten Datenbanken ([StartSQL](https://www.ovh.de/hosting/sql-optionen.xml)) beträgt **30**.

Diese Zahl beträgt **200** für die Datenbanken der Server [SQL Private](../erste-schritte-mit-sql-private/). (Diese Einstellung kann im Bereich `Konfiguration`{.action} Ihres Datenbankservers geändert werden).

Diese Nachricht erscheint bei der [Verbindung zu PhpMyAdmin](../datenbank-erstellen/#auf-das-phpmyadmin-interface-zugreifen), wenn diese maximale Anzahl an Verbindungen überschritten wird.

In dieser Situation müssen Sie [Ihre Datenbanken optimieren](../konfigurieren-optimieren-ihres-datenbank-servers/#optimieren-ihrer-datenbanken_1), um die Anzahl der aktiven Verbindungen zu reduzieren.

> [!warning]
>
> Wenn Sie Fragen zu den notwendigen Schritten zur Reduzierung der Anzahl aktiver Verbindungen auf Ihrer Datenbank haben, kontaktieren Sie unsere [User Community](https://community.ovh.com/en/) oder die [OVHcloud Partner](https://partner.ovhcloud.com/de/). Für externe Dienstleistungen können wir Ihnen leider keine Unterstützung anbieten.
>

#### “Name or service not known“

>
> **“mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known“**
>

Diese Fehlermeldung wird bei der [Verbindung zu PhpMyAdmin](../datenbank-erstellen/#auf-das-phpmyadmin-interface-zugreifen) angezeigt, wenn der angegebene Servername nicht korrekt ist.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Überprüfen Sie den Namen des Servers in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) zu registrierenden.

> [!success]
>
> Wenn die Datenbank, mit der Sie sich verbinden möchten, im Tab `Datenbanken`{.action} in `Web Cloud`{.action} in Ihrem [OVHcloud Kundencenter](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.de/&ovhSubsidiary=de) steht, wird der Name, der angegeben werden soll, in der Spalte `Server-Adresse` angegeben.
>
> Wenn Sie sich mit einer Datenbank auf einem Server verbinden möchten [SQL Private](../erste-schritte-mit-sql-private/), wird der einzugebende Server im Tab `Allgemeine Informationen`{.action}, Teil `Verbindungsinformationen`{.action}, `SQL`{.action} und im Bereich `Hostname`{.action}.
>

## Weiterführende Informationen <a name="gofurther"></a>

[erste Schritte mit dem SQL Private](../erste-schritte-mit-sql-private/)

Für spezialisierte Dienstleistungen (Referenzierung, Entwicklung etc.) kontaktieren Sie die [OVHcloud Partner](https://partner.ovhcloud.com/de/).

Für den Austausch mit unserer User Community gehen Sie auf https://community.ovh.com/en/.
