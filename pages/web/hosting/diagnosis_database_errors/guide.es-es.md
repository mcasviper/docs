---
title: Resolver los errores más frecuentes asociados a las bases de datos 
excerpt: Diagnóstico de los errores más comunes relacionados con las bases de datos
slug: error-requentes-base-de-datos
section: Diagnóstico OVH
Order 4
---

Última actualización: 08/10/2021

Objetivo²

El uso de sus bases de datos puede dar lugar a una serie de anomalías en su sitio web o su [área de cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), así como en la interfaz [PhpMyAdmin](../crear-base-de-datos/#acceder-a-la-interfaz-phpmyadmin).

**Descubra cómo solucionar los errores relacionados con las bases de datos de los alojamientos compartidos de OVHcloud.**

> [!warning]
>
La configuración, la gestión y la responsabilidad de los servicios que OVHcloud pone a su disposición recaen sobre usted. Por lo tanto, usted deberá asegurarse de que estos funcionan correctamente.
>
Le ofrecemos esta guía para ayudarle a completar mejor las tareas más comunes. Sin embargo, le recomendamos que, si necesita ayuda, contacte con un proveedor de servicios especializado o con el editor del programa o la interfaz. Nosotros no podremos asistirle. Más información en la sección "Uso avanzado" de esta guía.
>

Requisitos

- Disponer de un [plan de hosting](https://www.ovh.com/fr/hebergement-web/) OVHcloud.
https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.es/&ovhSubsidiary=es
- Utilizar uno de nuestros productos de bases de datos [Web Cloud](https://www.ovh.com/fr/hebergement-web/options-sql.xml), [SQL Privado](.../primeros-pasos-con-sql-privado/) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).

Procedimiento

### "Error al conectar a la base de datos"

#### Comprobar los incidentes en curso

En primer lugar, compruebe en [http://travaux.ovh.com/](http://travaux.ovh.com/) que su datacenter, su cluster de alojamiento, su servidor SQL privado o Cloud Databases no se ven afectados por ningún incidente en la infraestructura de OVHcloud.

> [!primary]
>
> Para encontrar esta información, conéctese a su [área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), en la sección "Web Cloud" {.action} :
>
> Para encontrar el ' Datacenter` de su alojamiento, así como su ' Filer` (servidor de archivos), seleccione el menú de la izquierda "Alojamientos {.action}" y, seguidamente, el alojamiento correspondiente. Puede consultar esta información en la pestaña "Información general" {.action}.
> - Para consultar el **cluster** de servidores en el que se encuentra el alojamiento, abra la pestaña "FTP-SSH" {.action}. Esta información aparecerá en el nombre del servidor FTP.
> - Para encontrar el nombre de su servidor **Private SQL** o **Cloud Databases**, haga clic en " Bases de datos " {.action} en el menú de la izquierda y seleccione el servicio correspondiente. Puede consultar esta información en la pestaña "Información general" {.action}.
>

#### Comprobar las claves de conexión a su base de datos <a name="config_file"></a>

Conéctese al espacio de almacenamiento de archivos de su alojamiento mediante [FTP](../conecte-espacio-almacenamiento-ftp-alojamiento-web/) y consulte el archivo de configuración de su sitio web (por ejemplo, para un sitio web WordPress, se trata del archivo **wp-config.php* situado en el directorio que contiene su sitio web).

> [!warning]
>
> La elección y configuración del archivo que contiene la información de conexión a la base de datos es inherente al editor de contenidos (CMS) correspondiente y no a OVHcloud.
>
Si necesita ayuda, le recomendamos que se ponga en contacto con el editor del [CMS](../modulos-en-1-clic/) utilizado para crear su sitio web o con un [proveedor especializado](https://partner.ovhcloud.com/fr/). No podremos asistirle en este asunto.
>

Compruebe la coincidencia **exacta** entre los identificadores de conexión a [PhpMyAdmin](../crear-base-de-datos/#acceso-a-la-interfaz-phpmyadmin) y los del fichero de configuración de su sitio web.

Cambie, si es necesario, la [contraseña de su base de datos](../cambiar-contraseña-base-de-datos/).

##### Ejemplo para Wordpress

Si su sitio web muestra un mensaje ** "Error al conectarse a la base de datos"** y no se ve afectado por un [incidente](http://travaux.ovh.com/), conéctese a [FTP](../conexión-espacio-almacenamiento-ftp-alojamiento-web/) a su alojamiento y abra el directorio que contiene su sitio web (por defecto es el directorio " www").

Si se trata de un sitio web WordPress, abra el archivo `wp-config.php`.

PHP
define('DB_NAME', 'my_database');
 
/** MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

En el área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), haga clic en la pestaña "Bases de datos"{.action} y compruebe la correspondencia entre los elementos mostrados y los presentes en el archivo `wp-config.php`.

- **my_database** debe coincidir con lo que se indica en el símbolo " Nombre de la base de datos " ;
- **my_user** debe coincidir con lo que se indica en ' Nombre de usuario`;
- **my_password** corresponde a [contraseña de la base de datos](../cambiar-contraseña-base-de-datos/);
- **my_server.mysql.db** debe coincidir con lo que se indica en `Dirección del servidor`.

> [!primary]
>
> Si esta operación no le permite restablecer el acceso a su sitio web, [guarde su base de datos] (../exportar-bases de datos/) y después [restablezca-la a una fecha anterior](../restaurar-importar-base de datos/#1-restaurar-una-copia de seguridad-existente) desde su [área de cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).
>
> Contacte a continuación con un [proveedor especializado](https://partner.ovhcloud.com/fr/) si es necesario. No podremos asistirle en este asunto.
>

### Superación del límite autorizado de la base de datos

Nuestros servicios le han enviado por correo electrónico un mensaje indicándole que la cantidad de datos en la base de datos supera el límite autorizado. La base de datos ha pasado a ser de solo lectura. Esto impide realizar cambios en el sitio web.

![mail_overquota](images/mail_overquota.png){.thumbnail}

Desbloquee la base de datos de tres formas distintas:

#### Método 1: cambiar la suscripción a un plan superior

Si dispone de una fórmula **Perso2014** o **Pro2014**, le recomendamos que cambie a[plan de hosting superior](https://www.ovh.com/fr/hebergement-web/). Este cambio de suscripción aumentará el tamaño de la base de datos, lo que la reabrirá automáticamente. Este método es el más sencillo y no necesita conocimientos técnicos específicos.

> [!warning]
>
> El aumento del tamaño de la base de datos puede deberse a un fallo de funcionamiento en el código interno del sitio web.
>
> Una anomalía puede conllevar un aumento permanente del tamaño de la base de datos, en cuyo caso el cambio de plan de hosting sería ineficaz.
>
Si detecta un aumento repentino en el tamaño de su base de datos o si tiene un sitio web de tipo "blog" que normalmente no consume datos, le recomendamos que contacte inmediatamente con un [proveedor especializado](https://partner.ovhcloud.com/fr/). No podremos ofrecerle soporte sobre este tema.
>

Para ello, conéctese a su [área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), haga clic en "Alojamientos {.action}" y seleccione el alojamiento correspondiente. Haga clic en el botón "..."`{.action} en el epígrafe `Oferta` situado a la derecha de su pantalla y, seguidamente, en `Cambiar de producto' {.action}.

Si utiliza un plan **Performance**, consulte el [método 2](#methode2).

#### Método 2: migrar sus datos a una base de datos de tamaño superior <a name="methode2"></a>

También puede migrar sus datos a una nueva base de datos:

- Contrate, si es necesario, una [base de datos](https://www.ovh.com/fr/hebergement-web/options-sql.xml) de mayor tamaño y lance su [creación](../crear-base-de-datos/).
- Realice un [exportar sus datos](../exportar-bases de datos/) y a continuación [importar los](../mutualizar-guía-importación-de-base-de-datos-mysql/) en la nueva base de datos;
- Integre las claves de la nueva base de datos en el [archivo de configuración](#config_file) de su sitio web.

> [!primary]
>
> Si dispone de un alojamiento **Performance**, también puede [activar gratis un servidor SQL Privado](.../primeros-pasos-con-sql-privado/#activar-su-servidor-sql-privado-incluido-con-su-producto-alojamiento-web).
>

#### Método 3: eliminar datos innecesarios

Una vez realizada la [copia de seguridad de su base de datos](../exportación-bases de datos/), conéctese a su interfaz [PhpMyAdmin](../base-de-datos/#acceder-a-la-interfaz-phpmyadmin) para eliminar los datos innecesarios con los comandos Drop, Delete y Truncate.

Abra la pestaña "Bases de datos" {.action} del alojamiento correspondiente e inicie el cálculo de la cuota utilizada. pulse el botón "..."`{.action} correspondiente y luego `Recalcular la cuota {.action}.

> [!warning]
>
> Esta operación requiere fuertes conocimientos técnicos. Le recomendamos que, si lo necesita, contacte con un [proveedor especializado](https://partner.ovhcloud.com/fr/). No podremos asistirle en este asunto.
>

#### Método 4: optimizar la base de datos

Para optimizar su base de datos, siga las instrucciones de nuestra guía "[Configurar su servidor de bases de datos](.../configurar-optimizar-su-servidor-de-base de datos/#optimizar-sus-bases de datos_1)". Abra la pestaña `Bases de datos {.action} de su alojamiento y haga clic en el botón "...`{.action} de la base de datos en cuestión.

> [!warning]
>
Si el asesoramiento ofrecido sobre la optimización de su base de datos no bastaba para desbloquear el acceso a su sitio web, le recomendamos que se ponga en contacto con nuestra [comunidad de usuarios](https://community.ovh.com) o con los [partners de OVHcloud](https://partner.ovhcloud.com/fr/). Nosotros no podremos asistirle en este asunto.
>

Memoria RAM rebasada

El siguiente mensaje, situado en la sección "Bases de datos" {.action} de su [área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), indica que su servidor [SQL privado](https://www.ovh.com/fr/hebergement-web/options-sql.xml) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) ha consumido una cantidad de recursos demasiado grande en la infraestructura de OVHcloud:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

En ese caso, puede aumentar la [cantidad de memoria RAM](../configurar-optimizar-su-servidor-de-base-de-datos/#seguir-la-ram-consumo) disponible desde la sección "Bases de datos" {.action} de su [área de cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). En la pestaña "Información general {.action}", haga clic en el botón "..."`{.action} en la sección `RAM`.

También puede optimizar su base de datos siguiendo las instrucciones de nuestra guía "[Configurar su servidor de bases de datos](.../configurar-optimizar-su-servidor-de-base-de-datos/#optimizar-sus-bases de datos_1)".

> [!primary]
>
> Si tiene dificultades para reducir el uso de los recursos en su servidor de bases de datos y no quiere aumentarlos, contacte con nuestra [comunidad de usuarios](https://community.ovh.com) o con los [partners de OVHcloud](https://partner.ovhcloud.com/fr/). No podremos asistirle en este asunto.
>

## errores de importación de bases de datos

#### "Access denied for user to database"

>
> **"#1044 - Access denied for user to database"**
>

En primer lugar, asegúrese de que la base de datos esté vacía en la pestaña `Bases de datos {.action} del alojamiento correspondiente (haga clic en el botón...).`{.action} correspondiente y, seguidamente, `Recalcular el límite {.action}' para [guardar la información presente](../exportar-bases de datos/).

También puede marcar la casilla "Vaciar la base de datos actual {.action} justo antes de [iniciar la importación](../mutualizar-guía-importación-de-una-base-de-datos-mysql/#importar-su-propia-copia-desde el área de cliente):

![database-import-empty](images/database-import-empty.png){.thumbnail}

Este mensaje de error significa que la base de datos que está intentando importar contiene elementos no autorizados en la infraestructura compartida de OVHcloud. Si lo necesita, puede ponerse en contacto con nuestra [comunidad de usuarios](https://community.ovh.com) o con un [proveedor especializado](https://partner.ovhcloud.com/fr/). No podremos asistirle en la corrección de esta anomalía.

on-success:
>
> Tener un **"trigger"* en el script de importación de su base de datos no está autorizado en los servidores de alojamiento compartido de OVHcloud. En ese caso, importe la base de datos en un servidor [SQL Privado](https://www.ovh.com/fr/hebergement-web/options-sql.xml) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).
>
> Por otro lado, no está permitida la siguiente petición:
>
>```bash
>CREATE DATABASE IF NOT EXISTS` Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
>```
>
> Sustituya por:
>
>```bash
SaaS DataBase {{name}}
>```
>
>(`Database-Name` : indique el nombre de la base de datos indicada en su [área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr)
>

#### "MySQL server has gone away"

>
ERROR MySQL server has gone away"**
>

Este mensaje de error aparece durante [la importación de una base de datos](.../restaurar-importar-base-de-datos/#2-importar-una-copia de seguridad-local) en un servidor [SQL Privado](../primeros-pasos-con-sql-privado/). La mayor parte del tiempo se debe a la cantidad excesiva de datos que se van a importar o a la falta de optimización de las peticiones SQL en el script de importación.

Para resolver esta anomalía, puede:

- Aumentar la [cantidad de memoria RAM](../configurar-optimizar-su-servidor-base-de-datos/#seguir-la-ram-consumo). Para ello, acceda al [servidor SQL privado](../primeros-pasos-con-sql-privado/) correspondiente en la sección "Bases de datos" de su [área de cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). Haga clic en el botón "...""{.action}" en la sección "RAM" y, seguidamente, en "Cambiar la cantidad de RAM {.action}".

- Fraccione su base de datos para importarla en varias operaciones en lugar de una (para cualquier duda sobre las operaciones a realizar, contacte con nuestra [comunidad de usuarios](https://community.ovh.com) o con los [partners de OVHcloud](https://partner.ovhcloud.com/fr/). Nosotros no podremos asistirle en este asunto.)

- [Optimice su base de datos](../configurar-optimizar-su-servidor-de-base-de-datos/#optimizar-sus-bases de datos_1) y luego repite las operaciones de exportación/importación.

### No se ha podido acceder a PhpMyAdmin.

#### "Access denied for user"

>
> **« mysqli::real_connect(): (HY000/1045): Access denied for user"**
>

Este mensaje de error puede aparecer al conectarse a la base de datos por [PhpMyAdmin](../crear-base-de-datos/#acceder-a-la-interfaz-phpmyadmin). Indica que los identificadores introducidos son incorrectos.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

En ese caso, [compruebe los identificadores indicados](../conectar-base-de-datos-servidor-bdd/#en-práctica) y cambie si es necesario la [contraseña de su base de datos](../cambiar-contraseña-base-de-datos/).

#### « Too many connections »

>
> **« mysqli_real_connect(): (HY000/1040): Too many connections"**
>

El número máximo de conexiones activas para las bases de datos entregadas con los alojamientos compartidos ([StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) es de **30**.

Este número es de **200** para las bases de servidores [SQL Privado](.../primeros-pasos-con-sql-privado/) y [Cloud Databases](https://www.ovh.com/fr/cloud-databases/). (Puede cambiar este parámetro en la sección "Configuración {.action}" del servidor de la base de datos.)

Este mensaje aparece durante [conexión a PhpMyAdmin](../crear-base-de-datos/#acceder-a-la-interfaz-phpmyadmin) cuando se supera el número máximo de conexiones.

En ese caso, deberá [optimizar las bases de datos](../configurar-optimizar-su-servidor-de-base-de-datos/#optimizar-sus-bases de datos_1) para reducir el número de conexiones activas.

> [!warning]
>
> Para más información sobre las operaciones que debe realizar para reducir el número de conexiones activas a la base de datos, contacte con nuestra [comunidad de usuarios](https://community.ovh.com) o con los [partners de OVHcloud](https://partner.ovhcloud.com/fr/). Nosotros no podremos asistirle en este asunto.
>

#### "Name or service not known"

>
> **« mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known"**
>

Este mensaje de error aparece durante [conexión a PhpMyAdmin](.../conexión-base-de-datos-servidor-bdd/#en-práctica) cuando el nombre del servidor introducido es incorrecto.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Compruebe el nombre del servidor que quiera registrar en su [área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).

on-success:
>
> Si la base de datos a la que desea conectarse aparece en la pestaña `Bases de datos {.action} de la parte `Alojamientos' {.action} de su [área de cliente de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), el nombre que debe introducir se indica en la columna `Dirección del servidor.
>
> Si desea conectarse a una base de datos en un servidor [SQL Privado](.../primeros-pasos-con-sql-prive/) o [Cloud Databases](https://www.ovh.com/fr/cloud-databases/), el nombre del servidor a introducir se inscribe en la pestaña "Información general" {.action}, parte `Información de conexiones' {.action}, `SQL`{.action} y en el nombre de host {.action} ...
>

### No se ha podido conectar a una base de datos Cloud Databases.

Disponer de un servidor [Cloud Databases](https://docs.ovh.com/fr/clouddb/) le permite [conectarse a sus bases de datos](../conexión-base-de-datos-servidor-bdd/) desde su ordenador o un servidor externo a la infraestructura de OVHcloud.

Si esta conexión no es posible, compruebe que [ha autorizado la dirección IP pública](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/#autoriser-une-adresse-ip) a conectarse al servidor de bases de datos.

Si la operación se ha realizado correctamente, póngase en contacto con su proveedor de acceso a internet o con los [partners de OVHcloud](https://partner.ovhcloud.com/fr/). No podremos asistirle en esta situación.

## Ir más lejos <a name="ir más lejos"></a>

[Primeros pasos con el servicio SQL Privado](.../primeros-pasos-con-sql-privado/)

[Primeros pasos con el servicio CloudDB](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/)

Para servicios especializados (posicionamiento, desarrollo, etc.), contacte con [partners de OVHcloud](https://partner.ovhcloud.com/fr/).

Interactúe con nuestra comunidad de usuarios en ovh.es/community.
