---
title: Risolvi gli errori più frequenti associati ai database 
excerpt: "Diagnostica i casi di errore più frequenti associati ai database"
slug: errori-frequenti-database
section: Diagnostica
ordine 4
---

Ultimo aggiornamento: 08/10/2021

Obiettivo**

L'utilizzo dei database può provocare alcune anomalie sul tuo sito o sul tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), così come sull'interfaccia [PhpMyAdmin](../creer-database/#acceder-a-linterface-phpmyadmin).

**Scopri come risolvere gli errori associati ai database sugli hosting condivisi OVHcloud.**

> [!warning]
>
> OVHcloud mette a tua disposizione servizi di cui tu sei responsabile per la configurazione e la gestione. Assicurarne il corretto funzionamento è quindi responsabilità dell'utente.
>
Questa guida ti aiuta a eseguire le operazioni necessarie sul tuo VPS. Tuttavia, in caso di difficoltà o dubbi, ti consigliamo di rivolgerti a un provider specializzato o contattare l'amministratore del servizio. OVH non potrà fornirti assistenza. Per maggiori informazioni consulta la sezione “Per saperne di più” di questa guida.
>

Prerequisiti

- Disporre di una [offerta di hosting Web](https://www.ovh.com/fr/hebergement-web/) OVHcloud
https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr
- Utilizzare una delle nostre offerte di database [Web Cloud](https://www.ovh.com/fr/hebergement-web/options-sql.xml), [SQL privato](.../primi-passi-con-sql-privato/) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).

Procedura

### "Errore durante la connessione al database"

#### Verifica gli incidenti in corso

Per prima cosa verifica su [http://travaux.ovh.com/](http://travaux.ovh.com/) che il tuo datacenter, il tuo cluster di hosting, il tuo server SQL privato o Cloud Database non sia interessato da un incidente sull'infrastruttura OVHcloud.

[!primary]
>
> Per maggiori informazioni, accedi allo Spazio Cliente OVHcloud (https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), sezione `Web Cloud`{.action}:
>
> - Per recuperare la `Datacenter` del tuo hosting e la `Filer` (server di file), seleziona `Hosting`{.action} nel menu di sinistra e poi l'hosting interessato. Queste informazioni sono disponibili nella scheda `Informazioni generali`{.action}.
> - Per recuperare il **cluster** di server su cui è ospitato il tuo hosting, clicca su `FTP-SSH`{.action}. Questa informazione verrà mostrata nella `Server FTP`
> - Per recuperare il nome del tuo server **Private SQL** o **Cloud Databases**, clicca su `Database`{.action} nel menu a sinistra e seleziona l'offerta corrispondente. Questa informazione è disponibile nella scheda `Host`{.action}.
>

#### Verifica le credenziali di connessione al tuo database <a name="config_file"></a>

Accedi in [FTP](../connessione-spazio-archiviazione-ftp-hosting-web/) allo spazio di archiviazione dei file sul tuo hosting e ritrova il file di configurazione del tuo sito (ad esempio, per un sito Wordpress, si tratta del file **wp-config.php***, che contiene il tuo sito).

> [!warning]
>
> La scelta e la configurazione del file contenente le informazioni di connessione al database sono inerenti al mittente del contenuto (CMS) interessato e non a OVHcloud.
>
> In caso di necessità, ti consigliamo di rivolgerti all'editor del [CMS](.../moduli-in-1-click/) utilizzato per creare il tuo sito o di rivolgerti a uno specialista del settore(https://partner.ovhcloud.com/fr/). Non saremo in grado di fornirti assistenza al riguardo.
>

Verifica la corrispondenza **esatta** tra le credenziali di connessione a [PhpMyAdmin](.../creer-database/#acceder-a-linterface-phpmyadmin) e quelle del file di configurazione del tuo sito.

Modifica, se necessario, la [password del tuo database](../modifica-password-database/).

##### Esempio per Wordpress

Se il tuo sito visualizza un messaggio **"Errore durante la connessione al database"** e non è interessato da un [incidente](http://travaux.ovh.com/), accedi al tuo hosting e apri la directory contenente il tuo sito (di default la cartella `wwww`) ...

Se il tuo sito è Wordpress, apri il file `wp-config.php`

```php
define('DB_NAME', 'my_database');
 
/** MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

Nello Spazio Cliente OVHcloud (https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), sezione `Hosting`{.action}, clicca su `Database`{.action} e verifica la corrispondenza tra gli elementi visualizzati e quelli presenti nel file `wp-config.php`:

- **my_database** deve corrispondere a quanto indicato in `Nome del database`
- **my_user** deve corrispondere a quanto riportato nella `Nome utente`
- **my_password** corrisponde alla [password del tuo database](.../modificare-password-database/);
- **my_server.mysql.db* deve corrispondere a quanto riportato su `Indirizzo del server`.

[!primary]
>
> Se queste operazioni non ti permettono di ripristinare l'accesso al tuo sito, [salva il tuo database](../esportazione-database/) e [ripristina il database](.../ripristina-importa-database/#1-ripristina-backup-esistente) dal tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).
>
> Contatta uno specialista del settore (https://partner.ovhcloud.com/fr/) se necessario. Non saremo in grado di fornirti assistenza al riguardo.
>

### Superamento della quota autorizzata del database

Hai ricevuto un'email dai nostri servizi che indica che la quantità di dati sul tuo database supera il limite autorizzato. Il tuo database è quindi passato in sola lettura. In questo modo il sito non può essere modificato.

![mail_overquota](images/mail_overquota.png){.thumbnail}

Tre metodi ti permettono di sbloccare il tuo database:

##### Metodo 1: attiva il tuo abbonamento su un'offerta superiore

Se disponi di una formula **Personale2014** o **Pro2014***, ti consigliamo di passare all'[offerta di hosting superiore](https://www.ovh.com/fr/hebergement-web/). La modifica dell'abbonamento aumenterà la dimensione del tuo database e la riaprirà automaticamente. Si tratta del metodo più semplice e non richiede particolari competenze tecniche.

> [!warning]
>
> L'aumento della dimensione del tuo database può essere associato a malfunzionamenti nel codice interno del tuo sito.
>
> Un'anomalia può provocare un aumento permanente della dimensione del tuo database, nel qual caso la modifica dell'offerta di hosting risulterebbe inefficace.
>
> Ti consigliamo quindi di contattare immediatamente uno specialista (https://partner.ovhcloud.com/fr/) se riscontri un improvviso aumento nella dimensione del tuo database o se disponi di un sito di tipo "blog" normalmente a basso consumo di dati. Non saremo in grado di fornirti assistenza in merito.
>

Accedi allo Spazio Cliente OVHcloud (https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) e clicca su `Hosting`{.action} > 'hosting interessato'. Clicca sul pulsante `...`{.action} nella sezione `Offre` sulla destra dello schermo e su `Modifica dell'offerta`{.action}.

Se utilizzi un'offerta **Performance**, consulta la sezione [metodo 2](#methode2).

#### Metodo 2: migrare i tuoi dati su un database di dimensione superiore <a name="methode2"></a>

Puoi anche migrare i tuoi dati su un nuovo database:

- Ordinare, se necessario, una [database](https://www.ovh.com/fr/hebergement-web/options-sql.xml) di dimensione superiore e avviarne la [creazione](.../creer-database/);
- Effettua un [export dei tuoi dati](../esportazione-database/), poi [importali](.../condiviso-guida-importazione-di-un-database-mysql/) nel nuovo database;
- Inserisci gli identificativi del nuovo database nel [file di configurazione](#config_file) del tuo sito.

[!primary]
>
> Se disponi di un hosting **Performance**, puoi anche [attivare gratuitamente un server SQL Privato](.../primi-passi-con-sql-privato/#attivazione-del-tuo-server-sql-privato-incluso-con-la-tua-offerta-di-hosting-web).
>

##### Metodo 3: eliminare i dati non necessari

Dopo aver effettuato un [backup del tuo database](.../esportazione-database/), accedi alla tua interfaccia [PhpMyAdmin](.../creer-database/#acceder-a-linterface-phpmyadmin) per eliminare i dati inutili grazie ai comandi Drop, Delete e Truncate.

Esegui il calcolo della quota utilizzando la scheda `Database`{.action} dell'hosting in questione: clicca sul pulsante `...`{.action} interessata e seleziona `Ricalcola la quota`{.action}.

> [!warning]
>
> Questa operazione richiede competenze tecniche molto elevate. In caso di necessità, ti consigliamo di rivolgerti a uno specialista del settore (https://partner.ovhcloud.com/fr/). Non saremo in grado di fornirvi assistenza in merito.
>

#### Metodo 4: ottimizzare il tuo database

Per ottimizzare il tuo database, segui le istruzioni della nostra guida "Configura il tuo server di database"(.../configurare-ottimizzare-il-tuo-server-di-database/#ottimizza-i-tuoi-database_1)". Clicca sulla scheda `Database`{.action} del tuo hosting e poi riavvia il calcolo della quota...`{.action} del database in questione.

> [!warning]
>
> Se i consigli forniti sull'ottimizzazione del database non sono sufficienti per sbloccare l'accesso al tuo sito, ti consigliamo di contattare la nostra [Community di utenti](https://community.ovh.com) o i [partner OVHcloud](https://partner.ovhcloud.com/fr/). OVH non potrà fornirti alcuna assistenza al riguardo.
>

Superamento della capacità della RAM

Nella sezione `Database`{.action} del tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) è riportato che il tuo server [SQL Privato](https://www.ovh.com/fr/hebergement-web/options-sql.xml) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) ha consumato troppe risorse sull'infrastruttura OVHcloud:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

In questa situazione è possibile aumentare la [quantità di memoria RAM](.../configurare-ottimizzare-il-tuo-server-database/#segui-la-ram-consumer) disponibile nella sezione `Database`{.action} del tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). Nella scheda `Informazioni generali`{.action}, clicca sul pulsante `.`{.action} nella sezione `RAM`.

Per ottimizzare il tuo database, segui le istruzioni della nostra guida "Configurare il tuo server di database"(.../configurare-ottimizzare-il-tuo-server-di-database/#ottimizzare-i-tuoi-database_1)".

[!primary]
>
> Se riscontri difficoltà nell'utilizzo delle risorse sul tuo server di database e non desideri aumentarle, contatta la nostra [Community di utenti](https://community.ovh.com) o i [partner OVHcloud](https://partner.ovhcloud.com/fr/). Non saremo in grado di fornirti assistenza al riguardo.
>

### Errori di importazione di database

#### "Access denied for user to database"

>
> **"#1044 - Access denied for user to database**
>

Per prima cosa, assicurati che il database sia vuoto dalla scheda `Database`{.action} dell'hosting interessato (clicca sul pulsante `...`{.action} in questione e su `Ricalcola la quota`{.action}) per [salvare i dati presenti](.../esportazione-database/).

Seleziona la casella `Svuota il database attuale`{.action} immediatamente prima di [avviare l'importazione](.../gestisci_la_guida_importazione_di_un_database_mysql/#importare_il_tuo_backup_dallo_Spazio_Cliente OVH):

![database-import-empty](images/database-import-empty.png){.thumbnail}

Questo messaggio di errore significa che il database che stai cercando di importare contiene elementi non autorizzati sull'infrastruttura condivisa OVHcloud. Contatta, se necessario, la nostra [Community di utenti](https://community.ovh.com) o un [provider specializzato](https://partner.ovhcloud.com/fr/). Non saremo in grado di fornirti assistenza sulla correzione di questa anomalia.

> [!success]
>
> Avere un **"trigger"** nello script di importazione del tuo database non è autorizzato sui server di hosting condiviso OVHcloud. importa il tuo database su un server [SQL privato](https://www.ovh.com/fr/hebergement-web/options-sql.xml) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).
>
> Inoltre, la seguente richiesta non è autorizzata:
>
>```bash
>CREATE DATABASE IF NOT ESISTENTI `Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
>```
>
> Sostituiscila con:
>
>```bash
SaaS DataBase {{name}}
>```
>
>(`Database-Name` : inserisci il nome del database indicato nel tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr)
>

##### "MySQL server has gone away"

>
ERROR MySQL server has gone away »**
>

Questo messaggio di errore compare durante l'[importazione di un database](.../ripristina-database/#2-importare-un-backup-locale) su un server [SQL Privato](.../primi-passi-con-sql-privato/). È legato per la maggior parte del tempo alla quantità troppo elevata di dati da importare o alla mancanza di ottimizzazione delle richieste SQL nello script di importazione.

Per risolvere questa anomalia, puoi:

- Aumentare la [quantità di RAM](../configurare-ottimizzare-il-tuo-server-database/#segui-la-ram-consumer). accedendo alla sezione `Database` del tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). Clicca sul pulsante `...`{.action} nella sezione `RAM` e clicca su `Modifica la quantità di RAM`{.action}.

- Per importare il tuo database in più operazioni anziché in una sola pagina (per maggiori informazioni sulle operazioni da effettuare, contatta la nostra [Community di utenti](https://community.ovh.com) o i [partner OVHcloud](https://partner.ovhcloud.com/fr/) OVH non potrà fornirti alcuna assistenza al riguardo).

- [Ottimizza il tuo database](.../configura-ottimizza-il-tuo-server-di-database/#ottimizza-i-tuoi-database_1) e ripeti le operazioni di esportazione/importazione.

### Impossibile accedere a PhpMyAdmin

##### "Access denied for user"

>
> **« mysqli::real_connect(): (HY000/1045): Access denied for user"**
>

Questo messaggio di errore può comparire durante la connessione al tuo database da [PhpMyAdmin](.../creer-database/#acceder-a-linterface-phpmyadmin). Essa indica che gli identificativi indicati sono errati.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

In questa situazione, [verifica le credenziali inserite](.../connessione-database-di-dati-server-bdd/#en-pratico) e, se necessario, modifica la [password del tuo database](.../modifica-password-database/).

#### "Too many connections"

>
> **« mysqli_real_connect(): (HY000/1040): Too many connections"**
>

Il numero massimo di connessioni attive per i database consegnati con hosting condivisi ([StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) è di **30**.

Questo numero è di **200** per i database dei server [SQL privato](.../primi-passi-con-sql-privato/) e [Cloud Databases](https://www.ovh.com/fr/cloud-databases/). (Questo parametro è modificabile nella sezione `Configuration`{.action} del tuo server database).

Questo messaggio compare durante la [connessione a PhpMyAdmin](../creer-database/#acceder-a-linterface-phpmyadmin) quando viene superato il numero massimo di connessioni.

Per ridurre il numero di connessioni attive, è necessario [ottimizzare i tuoi database](../configurare-ottimizzare-il-tuo-server-di-database/#ottimizzare-i-tuoi-database_1).

> [!warning]
>
> Per maggiori informazioni sulle operazioni da effettuare per ridurre il numero di connessioni attive sul database, contatta la nostra [Community di utenti](https://community.ovh.com) o i [partner OVHcloud](https://partner.ovhcloud.com/fr/). OVH non potrà fornirti alcuna assistenza al riguardo.
>

#### "Name or service not known"

>
> **« mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known"**
>

Questo messaggio di errore compare durante la [connessione a PhpMyAdmin](.../connessione-database-database-server-bdd/#en-pratici) quando il nome del server inserito non è corretto.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Verifica il nome del server da iscrivere nel tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).

> [!success]
>
> Se il database a cui vuoi connetterti compare nella scheda `Database`{.action} della sezione `Hosting`{.action} del tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), il nome da inserire è indicato nella colonna `Indirizzo del server`.
>
> Se vuoi connetterti a un database su un server [SQL Privato](.../primi-passi-con-sql-privato/) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/), il nome del server da inserire è iscritto nella scheda `Informazioni generali`{.action}, `Informazioni di connessione`{.action}, `SQL`{.action} e nella sezione `Nome host`{.action}.
>

### Connessione impossibile su un database Cloud Databases

Disporre di un server [Cloud Databases](https://docs.ovh.com/fr/clouddb/) permette di accedere ai database(../connessione-database-server-bdd/) dal proprio computer o da un server esterno all'infrastruttura OVHcloud.

Se questa connessione non è possibile, verifica prima di tutto che tu abbia [autorizzato il tuo indirizzo IP pubblico](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/#autoriser-une-adresse-ip) a connettersi al server di database.

Se l'operazione è stata effettuata correttamente, contatta il tuo provider Internet o i [partner OVHcloud](https://partner.ovhcloud.com/fr/). In questa situazione non saremo in grado di fornirti assistenza.

## Aller plus loin <a name="aller-plus-loin"></a>

[Iniziare a utilizzare il servizio SQL Privato](...iniziare-a-utilizzare-sql-privato/)

[Iniziare a utilizzare il servizio CloudDB](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/)

Per prestazioni specializzate (referenziamento, sviluppo, ecc...), contatta i [partner OVHcloud](https://partner.ovhcloud.com/fr/).

Contatta la nostra Community di utenti all’indirizzo https://www.ovh.it/community/{.external}.
