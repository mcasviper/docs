---
title: Resolver os erros mais frequentes associados às bases de dados 
excerpt "Diagnosticar os casos mais comuns de erros associados às bases de dados"
slug: erros-frequentes-bases-de-dados
Secção: Diagnóstico
order 4
---

“Última atualização: 08/10/2021”.

Objetivo***

A utilização das suas bases de dados pode dar origem a um certo número de anomalias no seu site ou no seu [Área de Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), bem como na interface [PhpMyAdmin](.../criar-base-de-dados/#acaceder-à-interface-phpmyadmin).

**Descubra como resolver os erros associados às bases de dados sobre os alojamentos partilhados OVHcloud.**

Warning
>
A OVHcloud disponibiliza-lhe serviços cuja configuração e gestão são da responsabilidade do cliente. O cliente é o único responsável pelo seu bom funcionamento.
>
Este manual fornece as instruções necessárias para usar as funcionalidades básicas de um servidor. No entanto, caso encontre dificuldades, recomendamos que contacte um fornecedor especializado e/ou o editor do serviço. De facto, a OVHcloud não lhe poderá fornecer assistência. Para mais informações, aceda à secção deste manual intitulada: “Quer saber mais?”
>

Requisitos

- Ter um [serviço de alojamento web](https://www.ovh.com/fr/hebergement-web/) OVHcloud.
https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr
- Utilizar uma das nossas ofertas de bases de dados [Web Cloud](https://www.ovh.com/fr/hebergement-web/options-sql.xml), [SQL privado](.../primeiros-passos-com-sql-privado/) ou [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).

Instruções

## "Erro durante a ligação à base de dados"

##### Verificar os incidentes em curso

Em [http://travaux.ovh.com/](http://travaux.ovh.com/), verifique primeiro se o seu datacenter, cluster de alojamento, servidor SQL privado ou Cloud Databases não está afetado por um incidente na infraestrutura OVHcloud.

[!primary]
>
> Para encontrar estas informações, aceda à Área de Cliente OVHcloud (https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), na parte 'Web Cloud` {.action}:
>
> - Para encontrar o `Datacenter` do seu alojamento, bem como o seu `Filer` (servidor de ficheiro), escolha `os Alojamentos` {.action} no menu à esquerda e, a seguir, o alojamento em causa. Encontrará estas informações no separador `Informações gerais` {.action}.
> - Para encontrar o **cluster** de servidores em que se encontra o seu alojamento, clique no separador `FTP-SSH` {.action}. Esta informação aparecerá no nome do seu 'Server FTP`'.
> - Para encontrar o nome do seu servidor ***Private SQL* ou **Cloud Databases**, clique em 'Bases de dados` {.action} no menu à esquerda e, a seguir, na oferta em causa. Encontrará esta informação no separador `Informações gerais` {.action}.
>

##### Verificar os dados de acesso à sua base de dados <a name="config_file"></a>

Ligue-se ao espaço de armazenamento de ficheiros com [FTP](.../ligação-espaço-armazenamento-ftp-alojamento-web/) ao espaço de armazenamento de ficheiros no seu alojamento e encontre o ficheiro de configuração do seu site (por exemplo, para um site Wordpress, trata-se do ficheiro **wp-config.php** situado na pasta que contém o seu site).

Warning
>
> A escolha e a configuração do ficheiro com as informações de ligação à base de dados é inerente ao editor de conteúdo (CMS) em causa e não à OVHcloud.
>
> Recomendamos que contacte o editor do [CMS](.../módulos-en-1-clic/) utilizado para criar o seu site ou que recorra a um [fornecedor especializado](https://partner.ovhcloud.com/fr/) em caso de necessidade. De facto, a OVHcloud não lhe poderá fornecer assistência.
>

De seguida, verifique a correspondência **exata** entre os identificadores de ligação ao [PhpMyAdmin](.../criar-base-de-dados/#acaceder-à-interface-phpmyadmin) e os do ficheiro de configuração do seu site.

Altere, se necessário, a [palavra-passe da sua base de dados](.../alterar-palavra-passe-base-de-dados/).

###### Exemplo para Wordpress

Se o seu website apresentar uma mensagem **"Erro durante a ligação à base de dados"** e que este não é afetado por [incidente](http://travaux.ovh.com/), ligue-se em [FTP](.../ligação-espaço-armazenamento-ftp-alojamento-web/) ao seu alojamento e abra o diretório que contém o seu website (por predefinição, trata-se do dossier '`ww`).

Se se tratar de um site Wordpress, abra o ficheiro `wp-config.php`.

PHP
define('DB_NAME', 'my_database');
 
/** MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/** MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

No seu [Espaço Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), na parte `Alojamentos` {.ac}, clique no separador 'Bases de dados` {.action} e verifique a correspondência entre os elementos apresentados e os presentes no ficheiro `wp-config.php`:

- **my_database** deve corresponder ao que é notado no nome da base`;
- **my_user** deve corresponder ao que é notado no nome de utilizador`;
- **my_password** corresponde à [palavra-passe da sua base de dados](.../alterar-palavra-passe-base-de-dados/);
- **my_server.mysql.db** deve corresponder ao que é notado no endereço do servidor`.

[!primary]
>
> Se estas manipulações não lhe permitem restabelecer o acesso ao seu website, [salvaguarde a sua base de dados](.../exportação-bases-dados/) e depois [restaure-a numa data anterior](.../restaurar-importar-base-de-dados/#1-restaurar-uma-cópia de segurança existente) a partir do seu [Espaço Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).
>
> Contacte um [fornecedor especializado](https://partner.ovhcloud.com/fr/) se necessário. De facto, a OVHcloud não lhe poderá fornecer assistência.
>

#### Excesso do limite autorizado da base de dados

Recebeu um e-mail dos nossos serviços indicando que a quantidade de dados na sua base de dados ultrapassa o limite autorizado. A sua base de dados passou então a ler sozinha. Isto impede qualquer modificação do seu site.

![mail_overquota](images/mail_overquota.png){.thumbnail}

Três métodos irão permitir-lhe desbloquear a sua base de dados:

#### Método 1: passar a sua subscrição para uma oferta superior

Se dispõe de uma fórmula **Perso2014** ou **Pro2014**, aconselhamos-o a passar para a oferta de alojamento superior (https://www.ovh.com/fr/hebergement-web/). Esta alteração de subscrição irá aumentar o tamanho da sua base de dados, o que a irá reabrir automaticamente. Este método é o mais simples e não exige qualquer competência técnica específica.

Warning
>
> O aumento do tamanho da sua base de dados pode estar associado a uma falha no código interno do seu site.
>
> Uma anomalia pode provocar um aumento permanente do tamanho da sua base de dados, caso em que a alteração da oferta de alojamento não será eficaz.
>
> Se verificar um aumento súbito da dimensão da sua base de dados, ou se dispuser de um site do tipo "blog" normalmente pouco consumidor de dados, aconselhamos que contacte imediatamente um [fornecedor especializado](https://partner.ovhcloud.com/fr/). Não poderemos dar-lhe apoio nesta matéria.
>

Para efetuar esta alteração, aceda à Área de Cliente OVHcloud (https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) e clique em Alojamentos` {.action e no alojamento em causa. Clique no botão ^ o...{.action} na rubrica 'Oferta`, à direita do seu ecrã, e depois alterer d'oferta` {.action}.

Se utiliza uma oferta **Performance**, consulte o [método 2](#methode2).

#### Método 2: migrar os seus dados para uma base superior <a name="método2"></a>

Também pode migrar os seus dados para uma nova base:

- Encomende, se necessário, uma [base de dados](https://www.ovh.com/fr/hebergement-web/options-sql.xml) de tamanho superior e lance a sua [criação](.../criar-base-de-dados/);
- Efetue uma [exportação dos seus dados](.../exportação-bases-dados/) e depois [importe-os](.../mutualise-guia-importacao-de-uma-base-de-dados-mysql/) na nova base de dados;
- Integre os identificadores da nova base de dados no [ficheiro de configuração](#config_file) do seu site.

[!primary]
>
> Se dispõe de um alojamento **Performance**, pode igualmente [ativar gratuitamente um servidor SQL Privado](.../primeiros-passos-com-sql-privado/#ativação-do-seu-servidor-sql-privado-incluído-com-o-seu-alojamento-web).
>

#### Método 3: eliminar dados desnecessários

Depois de realizar um backup da sua base de dados, aceda à interface PhpMyAdmin(.../criar-base-de-dados/#acaceder-à-interface-phpmyadmin) para eliminar os dados inúteis graças aos comandos Drop, Delete e Truncate.

De seguida, volte a analisar o cálculo da quota utilizado a partir do separador `Bases de dados` {.action} do alojamento em causa: clique no botão ^ o...{.ação} em causa e depois 'Recalcular a quota` {.action}.

Warning
>
> Esta operação requer grandes competências técnicas. Se necessário, recomendamos que recorra a um prestador de serviços especializado (https://partner.ovhcloud.com/fr/). De facto, a OVHcloud não lhe poderá fornecer assistência.
>

#### Método 4: otimizar a sua base de dados

Para otimizar a sua base de dados, siga as instruções do nosso guia "[Configurar o seu servidor de bases de dados](.../configurar-otimizar-o-servidor-base-de-dados/#otimizar-as-bases-de-dados_1)". De seguida, volte a analisar o cálculo da quota utilizado a partir do separador `Bases de dados` {.action} do seu alojamento, clicando no botão ^...{.ação} da base de dados em questão.

Warning
>
> Se os conselhos fornecidos sobre a otimização da sua base de dados não bastam para desbloquear o acesso ao seu website, aconselhamos que contacte a nossa [comunidade de utilizadores](https://community.ovh.com) ou os [parceiros da OVHcloud](https://partner.ovhcloud.com/fr/). De facto, a OVHcloud não lhe poderá fornecer assistência.
>

Capacidade de RAM excedida

A seguinte mensagem na parte `Bases de dados` {.action} do seu [Área de Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) indica que o seu servidor [SQL privado](https://www.ovh.com/fr/hebergement-web/options-sql.xml) ou [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) consumiu uma quantidade de recursos demasiado importante na infraestrutura OVHcloud:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

Nesta situação, pode aumentar a [quantidade de memória RAM](.../configurar-otimizar-o-servidor-base-de-dados/#segregar-a-ram-consumo) disponível a partir da parte `Bases de dados` {.action} do seu [espaço cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). No separador `Informações gerais` {.action}, clique no botão ^ o...{.ação} na rubrica `RAM`.

Também pode otimizar a sua base de dados seguindo as instruções do nosso guia "[Configurar o seu servidor de bases de dados](.../configurar-otimizar-o-servidor-base-de-dados/#otimizar-as-bases-de-dados_1)".

[!primary]
>
> Se encontrar dificuldades em diminuir a utilização dos recursos no seu servidor de bases de dados e não pretender aumentá-las, contacte a nossa [comunidade de utilizadores](https://community.ovh.com) ou os [parceiros OVHcloud](https://partner.ovhcloud.com/fr/). De facto, a OVHcloud não lhe poderá fornecer assistência.
>

### Erros de importação de bases de dados

##### "Access denied for user to database"

>
> **"#1044 - Access denied for user to database"**
>

Em primeiro lugar, certifique-se de que a sua base de dados está vazia no separador `Bases de dados` {.action} do alojamento em causa (clique no botão ^....).{.ação} em causa e depois 'Recalculer a quota` {.action} para [salvaguardar os dados presentes](.../exportação-bases de dados/).

Também pode selecionar a casa `Vider a base de dados atual` {.action} imediatamente antes de [lançar a importação](.../mutualise-guia-importacao-de-uma-base-de-dados-mysql/#importar-o-seu-próprio-backup-a-partir do espaço-cliente):

![database-import-empty](images/database-import-empty.png){.thumbnail}

Esta mensagem de erro significa que a base de dados que está a tentar importar contém elementos não autorizados na infraestrutura partilhada da OVHcloud. Contacte, se necessário, a nossa [comunidade de utilizadores](https://community.ovh.com) ou um [fornecedor especializado](https://partner.ovhcloud.com/fr/) sobre este assumpto. Não poderemos prestar-lhe assistência na correção desta anomalia.

on-success:
>
> Ter um **"trigger"** no script de importação da sua base de dados não é autorizado nos servidores de alojamento partilhado OVHcloud. Para isso, importe a sua base de dados para um servidor [SQL privado](https://www.ovh.com/fr/hebergement-web/options-sql.xml) ou [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).
>
> Além disso, não é autorizado o seguinte pedido:
>
>```bash
>CREATE DATABASE IF NOT EXISTENTE `Database-Name` DEFAULT CHARACTER SET latin1 COLLATE latin1_swedish_ci; 
>```
>
> Substitua-a por:
>
>```bash
Paas DataBase {{name}}
>```
>
>( Database-Name` : indique o nome da base de dados indicado no seu [Área de Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr)
>

### "MySQL server has gone away"

>
ERRO MySQL server has gone away"**
>

Esta mensagem de erro aparece aquando da [importação de uma base de dados](.../restaurar-importar-base-de-dados/#2-importar-uma-cópia de segurança local) num servidor [SQL Privado](.../primeiros-passos-com-sql-privado/). Está ligado, na maior parte dos casos, à quantidade excessiva de dados a importar ou à falta de otimização dos pedidos SQL no script de importação.

Para resolver esta anomalia, pode:

- Aumentar a [quantidade de memória viva (RAM)](.../configurar-otimizar-o-servidor-base-de-dados/#seguir-a-ram-consumir). Para isso, aceda ao [servidor SQL privado](.../primeiros passos-com-sql-privado/) afetado na rubrica 'Bases de dados` do seu [Espaço Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). A seguir, clique no botão ^..{.ação} na parte `RAM`, e ``Alterar a quantidade de RAM` {.ação}.

- Transferir a base de dados para várias operações em vez de uma (para qualquer questão relativa às operações a realizar, contacte a nossa [comunidade de utilizadores](https://community.ovh.com) ou os parceiros da OVHcloud](https://partner.ovhcloud.com/fr/). De facto, a OVHcloud não lhe poderá fornecer assistência.

- [Otimize a sua base de dados](.../configure-otimize-o-seu-servidor-base-de-dados/#otimizar-as-suas-bases-de-dados_1) e depois repita as operações de exportação/importação.

### Não é possível aceder ao PhpMyAdmin

##### "Access denied for user"

>
> **« mysqli::real_connect(): (HY000/1045): Acesso denied for user**
>

Esta mensagem de erro pode aparecer no acesso à sua base de dados por [PhpMyAdmin](.../criar-base-de-dados/#acaceder-à-interface-phpmyadmin). Indica que os dados de identificação introduzidos estão errados.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

Nesta situação, [verifique os identificadores introduzidos](.../ligação-base-de-dados-servidor-bdd/#en-prático) e altere, se necessário, a [palavra-passe da sua base de dados](.../alterar-palavra-passe-base-de-dados/).

#### "Too many connections"

>
> **« mysqli_real_connect(): (HY000/1040): Too many connections"**
>

O número máximo de ligações ativas para as bases de dados entregues com os alojamentos partilhados ([StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml)) é de **30**.

Este número é de **200** para as bases dos servidores [SQL privado](.../primeiros-passos-com-sql-privado/) e [Cloud Databases](https://www.ovh.com/fr/cloud-databases/). (Este parâmetro pode ser modificado na secção 'Configuration` {.action} do seu servidor de base de dados).

Esta mensagem aparece na [ligação ao PhpMyAdmin](.../criar-base-de-dados/#acaceder-a-interface-phpmyadmin) quando o número máximo de ligações é ultrapassado.

Nesta situação, deverá [otimizar as suas bases de dados](.../configurar-otimizar-o-servidor-base-de-dados/#otimizar-as-bases-de-dados_1) de forma a reduzir o número de ligações ativas.

Warning
>
> Para qualquer questão relativa às operações a realizar para reduzir o número de ligações ativas na sua base de dados, contacte a nossa [comunidade de utilizadores](https://community.ovh.com) ou os [parceiros da OVHcloud](https://partner.ovhcloud.com/fr/). De facto, a OVHcloud não lhe poderá fornecer assistência.
>

#### "Name or service not known"

>
> **« mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known**
>

Esta mensagem de erro aparece na [ligação a PhpMyAdmin](.../ligação-base-de-dados-servidor-bdd/#en-prático) quando o nome do servidor indicado está incorreto.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Verifique o nome do servidor a inscrever no seu [Área de Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).

on-success:
>
> Se a base de dados à qual deseja aceder aparecer no separador `Bases de dados` {.action { da parte `Alojamentos`.action} do seu [Espaço Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), o nome a inserir está inscrito na coluna "Endereço do servidor`".
>
> Se pretender ligar-se a uma base de dados num servidor [SQL privado](.../primeiros-passos-com-sql-privado/) ou [Cloud Databases](https://www.ovh.com/fr/cloud-databases/), o nome do servidor a introduzir está inscrito no separador `Informações gerais` {.action}, parte `Informações` {.action, `SQL` {.action} e na rubrica `Nome de host` {.action}.
>

### Conexão impossível numa base de dados Cloud Databases

Ter um servidor [Cloud Databases](https://docs.ovh.com/fr/clouddb/) permite-lhe [ligar às suas bases de dados](.../ligação-base-de-dados-servidor-bdd/) a partir do seu computador ou de um servidor externo à infraestrutura da OVHcloud.

Se esta ligação for impossível, comece por verificar que [autorizou o seu endereço IP público](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/#autoriser-une-adresse-ip) está a aceder ao servidor de bases de dados.

Se esta operação for bem-sucedida, contacte o seu Fornecedor de Acesso à Internet ou os parceiros da OVHcloud (https://partner.ovhcloud.com/fr/). De facto, a OVHcloud não lhe poderá fornecer assistência.

# Quer ir mais longe <a name="ir mais longe"></a>

[Primeiros passos com o serviço SQL Privado](.../primeiros passos com-sql-privado/)

[Primeiros passos com o serviço CloudDB](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/)

Para serviços especializados (referenciamento, desenvolvimento, etc), contacte os [parceiros OVHcloud](https://partner.ovhcloud.com/fr/).

“Fale com a nossa comunidade de utilizadores em https://community.ovh.com/en/.”
