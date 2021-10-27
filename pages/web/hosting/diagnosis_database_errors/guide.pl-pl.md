---
title: Rozwiąż najczęstsze błędy związane z bazami danych 
excerpt: "Zdiagnozuj najczęstsze przypadki błędów związanych z bazami danych"
slug: blad-baz-danych
section: Diagnostyka
order: 4
---

> [!primary]
> Tłumaczenie zostało wygenerowane automatycznie przez system naszego partnera SYSTRAN. W niektórych przypadkach mogą wystąpić nieprecyzyjne sformułowania, na przykład w tłumaczeniu nazw przycisków lub szczegółów technicznych. W przypadku jakichkolwiek wątpliwości zalecamy zapoznanie się z angielską/francuską wersją przewodnika. Jeśli chcesz przyczynić się do ulepszenia tłumaczenia, kliknij przycisk „Zaproponuj zmianę” na tej stronie.
>

**Ostatnia aktualizacja z dnia 08/10/2021**

## Wprowadzenie

Korzystanie z baz danych może spowodować pewne nieprawidłowości na Twojej stronie WWW lub w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), jak również w interfejsie [phpMyAdmin](../creer-bazy-danych/#acceder-a-interfejs-phpmyadmin).

**Dowiedz się, jak usunąć błędy związane z bazami danych na hostingu www OVHcloud.**

> [!warning]
>
> OVHcloud udostępnia różnorodne usługi, jednak to Ty odpowiadasz za ich konfigurację i zarządzanie nimi. Ponosisz więc odpowiedzialność za ich prawidłowe funkcjonowanie.
>
> Oddajemy w Twoje ręce niniejszy przewodnik, którego celem jest pomoc w wykonywaniu bieżących zadań. W przypadku trudności zalecamy skorzystanie z pomocy wyspecjalizowanego webmastera lub kontakt z producentem oprogramowania. Niestety firma OVH nie będzie mogła udzielić wsparcia w tym zakresie. Więcej informacji znajduje się w sekcji [Sprawdź również](#gofurther) ten przewodnik.
>

## Wymagania początkowe

- Posiadanie [hostingu](https://www.ovh.com/fr/hebergement-web/) OVHcloud
- Dostęp do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.pl/&ovhSubsidiary=pl).
- Korzystanie z jednej z naszych ofert baz danych [Web Cloud](https://www.ovh.com/fr/hebergement-web/options-sql.xml), [SQL prywatny](../pierwsze-kroki-z-sql-prive/) lub [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).

W praktyce

### "Błąd podczas logowania do bazy danych"

##### Zweryfikuj zdarzenia w trakcie

Sprawdź najpierw na stronie [http://travaux.ovh.com/](http://travaux.ovh.com/), że Twoje centrum danych, klaster hostingu, Twój prywatny serwer SQL lub Cloud Databases nie są związane z awariami infrastruktury OVHcloud.

[!primary]
>
> Aby odnaleźć te informacje, zaloguj się do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), w części `Web Cloud`{.action} :
>
> - Aby znaleźć `Datacenter` Twojego hostingu, wraz z `Filer` (serwer plików), w menu po lewej stronie wybierz `Hosting{.action}, a następnie wybierz odpowiedni hosting. Informacje te można znaleźć w zakładce `Informacje ogólne`{.action}.
> - Aby odnaleźć **klaster** serwerów, na których hostowany jest Twój hosting, kliknij zakładkę `FTP-SSH`{.action}. Informacja ta pojawi się w nazwie Twojego `Serwera FTP`.
> - Aby odnaleźć nazwę serwera **Private SQL** lub **Cloud Databases**, kliknij przycisk `Bazy danych`{.action} w menu po lewej stronie, a następnie wybierz odpowiednią ofertę. Informacja ta znajduje się w polu 'Host` w zakładce 'Informacje ogólne{.action}.
>

#### Sprawdź dane do logowania do bazy danych <a name="config_file"></a>

Zaloguj się przez [FTP](../połączenie-przestrzeń-ftp-hosting-web/) do przestrzeni dyskowej plików na Twoim hostingu i znajdź plik konfiguracyjny Twojej strony (np. w przypadku strony Wordpress plik **wp-config.php** znajduje się w folderze zawierającym Twoją stronę).

Warning
>
> Wybór i konfiguracja pliku zawierającego dane do logowania do bazy danych jest ściśle związana z wybranym edytorem treści, a nie z OVHcloud.
>
> Zalecamy zatem skontaktowanie się z wydawcą [CMS](../moduły-en-1-clic/) używanym do założenia strony lub do skorzystania z pomocy [wyspecjalizowanego usługodawcy] (https://partner.ovhcloud.com/fr/) w razie potrzeby. Nie będziemy w stanie udzielić wsparcia w tym zakresie.
>

Następnie sprawdź zgodność **dokładna** między identyfikatorami logowania do [PhpMyAdmin](../creer-base-de-danych/#acceder-a-interface-phpmyadmin) a danymi w pliku konfiguracyjnym Twojej strony.

W razie potrzeby zmień [hasło do Twojej bazy danych](../zmień-hasło-do-bazy-danych/).

##### Przykład dla Wordpress

Jeśli Twoja strona wyświetla komunikat **"Błąd podczas logowania do bazy danych"** i nie dotyczy jej [problem](http://travaux.ovh.com/), zaloguj się przez [FTP](.../połączenie-przestrzeń-ftp-hosting-web/) do hostingu, a następnie otwórz katalog zawierający Twoją stronę (domyślnie jest to folder `www`).

Jeśli jest to strona Wordpress, otwórz plik `wp-config.php`.

PHP
define('DB_NAME', 'my_database');
 
/* MySQL database username */
define('DB_USER', 'my_user');
 
/** MySQL database password */
define('DB_PASSWORD', 'my_password');
 
/* MySQL hostname */
define('DB_HOST', 'my_server.mysql.db:port');
```

W [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), w części 'Hosting{.action}, kliknij zakładkę 'Bazy danych`{.action}, następnie sprawdź zgodność między elementami wyświetlanymi i znajdującymi się w pliku `wp-config.php`:

- **my_database** musi odpowiadać temu, co jest zapisane w `Nazwa bazy`;
- **my_user** musi odpowiadać temu, co jest zapisane w `Nazwa użytkownika`;
- **my_password** odnosi się do [hasło do bazy danych](../zmiana-hasła-bazy-danych/);
- **my_server.mysql.db** musi odpowiadać temu, co jest zapisane w `Adres serwera`.

[!primary]
>
> Jeśli operacje te nie pozwalają przywrócić dostępu do Twojej strony WWW, [zapisz bazę danych](../eksport-bazy-danych/), a następnie [przywróć ją w wcześniejszej dacie](.../przywrócić-importować-bazę-danych/#1-przywrócić-istniejącą-kopię zapasową) w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).
>
> W razie potrzeby należy skontaktować się z [wyspecjalizowanym dostawcą usług] (https://partner.ovhcloud.com/fr/). Nie będziemy w stanie udzielić wsparcia w tym zakresie.
>

### Przekroczenie dozwolonego rozmiaru bazy danych

Otrzymałeś e-mail z naszych usług informujący, że ilość danych na Twojej bazie przekracza dozwolony limit. Twoja baza została przeczytana w trybie tylko do odczytu. Dzięki temu nie można wprowadzać modyfikacji na Twojej stronie WWW.

![mail_overquota](images/mail_overquota.png){.thumbnail}

Odblokuj bazę danych na trzy sposoby:

#### Metoda 1: przejdź na wyższą ofertę

Jeśli posiadasz wzór **Perso2014** lub **Pro2014**, w tej sytuacji zalecamy przejście na[górną ofertę hostingową](https://www.ovh.com/fr/hebergement-web/). Zmiana abonamentu zwiększy rozmiar bazy danych, dzięki czemu będzie ona automatycznie odnawiana. Metoda ta jest najprostsza i nie wymaga szczególnych kompetencji technicznych.

Warning
>
> Zwiększenie rozmiaru bazy danych może być związane z nieprawidłowym działaniem wewnętrznego kodu Twojej strony WWW.
>
> Nieprawidłowości mogą spowodować stały wzrost rozmiaru bazy danych. W takim przypadku zmiana oferty hostingowej byłaby nieskuteczna.
>
> Zalecamy zatem, aby w przypadku zaobserwowania nagłego wzrostu rozmiaru bazy danych lub gdy posiadasz stronę typu "blog", która w normalnych warunkach nie jest konsumentem danych, niezwłocznie skontaktował się z [wyspecjalizowanym dostawcą] (https://partner.ovhcloud.com/fr/). Nie będziemy w stanie udzielić Ci wsparcia w tym zakresie.
>

W celu dokonania tej zmiany zaloguj się do [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), następnie kliknij przycisk 'Hosting{.action}, a następnie wybierz odpowiedni hosting. Kliknij przycisk `...`{.action} w rubryce `Offre` po prawej stronie ekranu, a następnie kliknij `Zmień ofertę{.action}.

Jeśli korzystasz z oferty **Performance**, sprawdź [metoda 2](#methode2).

#### Metoda 2: migracja danych na wyższą bazę danych <a name="methode2"></a>

Możesz również przenieść dane na nową bazę:

- Zamów (w razie potrzeby bazę danych)(https://www.ovh.com/fr/hebergement-web/options-sql.xml) o wyższej wielkości, a następnie uruchom [kreacja](../tworzenie-bazy-danych/);
- Wykonaj [eksport swoich danych](../eksport-bazy-danych/), następnie [je importować](.../hosting-guide-import-bazy-danych-mysql/) w nowej bazie;
- Wprowadź dane dostępowe nowej bazy danych do [pliku konfiguracyjnego] (#config_file) swojej strony.

[!primary]
>
> Jeśli dysponujesz hostingiem **Performance**, możesz również [włączyć za darmo prywatny serwer SQL](../pierwsze-kroki-z-sql-prive/#aktywacja-serwera-sql-prive-zawartego w-ofercie-hostingu).
>

#### Metoda 3: usuń niepotrzebne dane

Po utworzeniu [kopii zapasowej bazy danych](../eksport-bazy-danych/) zaloguj się do swojego interfejsu [PhpMyAdmin](../tworzenie-bazy-danych/#acceder-a-interface-phpmyadmin), aby usunąć niepotrzebne dane za pomocą poleceń Drop, Delete i Truncate.

Następnie upamiętaj obliczenie rozmiaru używanego w zakładce 'Bazy danych{.action} dla wybranego hostingu: kliknij przycisk `...`{.action} a następnie na 'Przelicz rozmiar`{.action}.

Warning
>
> Operacja ta wymaga wysokich umiejętności technicznych. W razie potrzeby zalecamy skorzystanie z pomocy [wyspecjalizowanego usługodawcy](https://partner.ovhcloud.com/fr/). Nie będziemy w stanie udzielić wsparcia w tym zakresie.
>

#### Metoda 4: zoptymalizuj bazę danych

Aby zoptymalizować bazę danych, postępuj zgodnie z instrukcjami zawartymi w przewodniku "[Konfiguracja serwera baz danych](../konfiguracja-optymalizacja-serwera-bazy-danych/#optymalizacja-baz-danych_1)". Następnie ponownie zastosuj rozmiar w zakładce 'Bazy danych{.action} Twojego hostingu, klikając przycisk `...`{.action} odpowiedniej bazy danych

Warning
>
> Jeśli dostarczone porady dotyczące optymalizacji Twojej bazy danych nie wystarczą, aby odblokować dostęp do Twojej strony, zalecamy kontakt z naszym [społecznością użytkowników](https://community.ovh.com) lub [partnerami OVHcloud](https://partner.ovhcloud.com/fr/). Niestety firma OVH nie będzie mogła udzielić wsparcia w tym zakresie.
>

Przekroczenie pojemności pamięci RAM

Poniższy komunikat w części `Bazy danych`{.action} Twojego [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr) wskazuje, że Twój serwer [Prywatny SQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) lub [Cloud Databases](https://www.ovh.com/fr/cloud-databases/) wykorzystał zbyt dużą ilość zasobów w infrastrukturze OVHcloud:

![quota_exceeding](images/quota_exceeding.png){.thumbnail}

W tej sytuacji możesz zwiększyć [ilość pamięci RAM](.../ustawić-optymalizować-serwer-bazy-danych/#śledzić-la-ram-konsumee) dostępny w części `Bazy danych`{.action} [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). W karcie `Informacje ogólne{.action} kliknij przycisk `...`{.action} w rubryce `RAM`.

Możesz również zoptymalizować bazę danych, postępując zgodnie z instrukcjami zawartymi w przewodniku "[Konfiguracja serwera baz danych](.../konfiguracja-optymalizacja-serwera-bazy-danych/#optymalizacja-baz-danych_1)".

[!primary]
>
> Jeśli napotkasz trudności z ograniczeniem wykorzystania zasobów na serwerze baz danych i nie chcesz ich zwiększać, skontaktuj się z naszym [społecznością użytkowników](https://community.ovh.com) lub [partnerami OVHcloud](https://partner.ovhcloud.com/fr/). Nie będziemy w stanie udzielić wsparcia w tym zakresie.
>

### Błędy w imporcie baz danych

#### "Access denied for user to database"

>
> **"#1044 - Access denied for user to database"**
>

Upewnij się, że baza danych jest pusta w zakładce 'Bazy danych{.action} odpowiedniego hostingu (kliknij przycisk `...`{.action} a następnie na 'Przelicz kwotę`{.action}) w celu [zapisz obecne dane](../eksport-bazy-danych/).

Możesz również zaznaczyć kratkę `Wyczyść aktualną bazę danych`{.action} tuż przed [uruchomieniem importu](../hostingu-przewodnika-importu-bazy-danych-mysql/#zaimportować-kopię-zapasową-z-panelu klienta):

![database-import-empty](images/database-import-empty.png){.thumbnail}

Ten komunikat błędu oznacza, że baza danych, którą chcesz importować zawiera nieautoryzowane elementy na infrastrukturze współdzielonej OVHcloud. W razie potrzeby skontaktuj się z [społecznością użytkowników](https://community.ovh.com) lub [wyspecjalizowanym dostawcą](https://partner.ovhcloud.com/fr/). Nie będziemy w stanie udzielić wsparcia w zakresie korekty tej nieprawidłowości.

on-success:
>
> Posiadanie **"trigger"** w skrypcie importu bazy danych nie jest dozwolone na serwerach hostingu www OVHcloud. W takiej sytuacji zaimportuj bazę danych na serwer [prywatny SQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml) lub [Cloud Databases](https://www.ovh.com/fr/cloud-databases/).
>
> Ponadto nie zezwala się na następujące zapytanie:
>
>```bash
>CREATE DATABASE IF NOT EXISTS `Database-Name` DEFAULT CHARACTER SET LATIN1 COLLATE LATIN1_swedish_ci; 
>```
>
> Zastąp ją:
>
>```bash
SaaS DataBase {{name}}
>```
>
>( Database-Name`: wpisz nazwę bazy danych (Panel klienta OVHcloud)(https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr)
>

#### "MySQL server has gone away"

>
ERROR MySQL server has gone away"*
>

Ten komunikat błędu pojawia się podczas [importu bazy danych](../przywracania-importowania-bazy-danych/#2-importowania-lokalnej-kopii-zapasowej) na serwerze [Prywatny SQL](../pierwsze-kroki-z-sql-prive/). Wiąże się to głównie z zbyt dużą ilością danych do importu lub z brakiem optymalizacji zapytań SQL w skrypcie importu.

Aby usunąć tę anomalię, możesz:

- Zwiększyć [ilość pamięci RAM](.../skonfigurować-optymalizować-serwer-bazy-danych/#śledzić-la-ram-zużycie). W tym celu przejdź do [prywatny serwer SQL](../pierwsze-kroki-z-sql-prive/) w sekcji `Bazy danych` Twojego [Panel klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr). Następnie kliknij przycisk `...`{.action} w części `RAM`, a następnie na 'Zmień ilość RAM`{.action}.

- Podziel bazę danych, aby ją importować na kilka operacji zamiast jednej (w przypadku pytań dotyczących operacji, które należy przeprowadzić, skontaktuj się z naszą [społecznością użytkowników](https://community.ovh.com) lub [partnerami OVHcloud](https://partner.ovhcloud.com/fr/). Niestety firma OVH nie będzie mogła udzielić wsparcia w tym zakresie.)

- [Zoptymalizuj bazę danych](.../ustawić-optymalizować-serwer-bazy-danych/#optymalizować-bazy-danych_1), a następnie powtórzyć operacje eksportu / importu.

### Nie można uzyskać dostępu do PhpMyAdmin

#### "Access denied for user"

>
> **« mysqli::real_connect(): (HY000/1045): Access denied for user"*
>

Ten komunikat błędu może pojawić się podczas logowania do bazy danych przez [PhpMyAdmin](../creer-bazy-danych/#acceder-a-interfejs-phpmyadmin). Wskazuje ona, że dane identyfikacyjne są błędne.

![access_denied_for_user](images/access_denied_for_user.png){.thumbnail}

W takiej sytuacji [sprawdź wpisane dane](../logowanie-bazy-danych-serwer-bdd/#en-praktyka) i w razie potrzeby zmień [hasło do bazy danych](../zmiana-hasła-bazy-danych/).

#### "Too many connections"

>
> **« mysqli_real_connect(): (HY000/1040): Too many connections"**
>

Maksymalna liczba aktywnych połączeń dla baz danych dostarczanych na hostingu ([StartSQL](https://www.ovh.com/fr/hebergement-web/options-sql.xml)) wynosi **30**.

Liczba ta wynosi **200** dla baz serwerów [SQL prywatny](../pierwsze-kroki-z-sql-prive/) i [Cloud Databases](https://www.ovh.com/fr/cloud-databases/). (Ten parametr można zmienić w części `Konfiguracja`{.action} Twojego serwera bazy danych).

Wiadomość ta pojawia się podczas [logowania do phpMyAdmin](../creer-base-de-danych/#acceder-a-interface-phpmyadmin), gdy ta maksymalna liczba połączeń jest przekroczona.

W takiej sytuacji powinieneś [zoptymalizować bazy danych](../skonfigurować-optymalizować-serwer-bazy-danych/#optymalizować-bazy-danych_1), aby zmniejszyć liczbę aktywnych połączeń.

Warning
>
> W przypadku pytań dotyczących operacji, które należy przeprowadzić, aby zmniejszyć liczbę aktywnych połączeń na Twojej bazie danych, skontaktuj się z naszą [społecznością użytkowników](https://community.ovh.com) lub [partnerami OVHcloud](https://partner.ovhcloud.com/fr/). Niestety firma OVH nie będzie mogła udzielić wsparcia w tym zakresie.
>

#### "Name or service not known"

>
> **« mysqli::real_connect(): (HY000/2002): php_network_getaddresses: getaddrinfo failed: Name or service not known"**
>

Ten komunikat błędu pojawia się podczas [logowania do PhpMyAdmin](../logowanie-bazy-danych-serwer-bd/#en-praktyka), gdy podana nazwa serwera jest nieprawidłowa.

![name_or_service_not_known](images/name_or_service_not_known.png){.thumbnail}

Sprawdź nazwę serwera, który chcesz zarejestrować w [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr).

on-success:
>
> Jeśli baza danych, do której chcesz się zalogować, wyświetla się w zakładce 'Bazy danych{.action} w części 'Hosting{.action} w Twoim [Panelu klienta OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.com/fr/&ovhSubsidiary=fr), nazwa, którą należy wpisać jest wpisana w kolumnie 'Adres serwera`.
>
> Jeśli chcesz zalogować się do bazy danych na serwerze [Prywatny SQL](../pierwsze-kroki-z-sql-prive/) lub [Cloud Databases](https://www.ovh.com/fr/cloud-databases/), nazwa serwera, która ma zostać wprowadzona jest w zakładce `Informacje ogólne{.action}, w części `Informacje o połączeniach{.action}, `SQL{.action} i w sekcji Nazwa hosta{.action}.
>

### Nie można połączyć z bazą danych Cloud Databases

Posiadanie serwera [Cloud Databases](https://docs.ovh.com/fr/clouddb/) pozwala na [zalogowanie się do baz danych](../połączenie-bazy-danych-serwer-bdd/) z komputera lub serwera zewnętrznego do infrastruktury OVHcloud.

Jeśli połączenie to okaże się niemożliwe, sprawdź, czy (autoryzacja publicznego adresu IP) (https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/#autoriser-une-adresse-ip) połączyłeś się z serwerem baz danych.

Jeśli operacja ta została pomyślnie wykonana, skontaktuj się z dostawcą dostępu do Internetu lub [partnerami OVHcloud](https://partner.ovhcloud.com/fr/). W takiej sytuacji nie będziemy w stanie udzielić wsparcia.

## Przejdź dalej <a name="idź dalej"></a>

[Pierwsze kroki z usługą Prywatnego SQL](../pierwsze-kroki-z-sql-prive/)

[Pierwsze kroki z usługą CloudDB](https://docs.ovh.com/fr/clouddb/debuter-avec-clouddb/)

W przypadku wyspecjalizowanych usług (pozycjonowanie, rozwój, etc.) skontaktuj się z [partnerami OVHcloud](https://partner.ovhcloud.com/fr/).

Przyłącz się do społeczności naszych użytkowników na stronie.
