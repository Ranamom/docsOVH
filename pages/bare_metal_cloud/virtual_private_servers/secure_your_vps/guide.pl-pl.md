---
title: "Zabezpieczenie serwera VPS"
excerpt: "Dowiedz się, jak wdrożyć podstawowe środki bezpieczeństwa, aby chronić Twój serwer VPS przed atakami i nieautoryzowanym dostępem"
updated: 2024-10-07
---

> [!primary]
> Tłumaczenie zostało wygenerowane automatycznie przez system naszego partnera SYSTRAN. W niektórych przypadkach mogą wystąpić nieprecyzyjne sformułowania, na przykład w tłumaczeniu nazw przycisków lub szczegółów technicznych. W przypadku jakichkolwiek wątpliwości zalecamy zapoznanie się z angielską/francuską wersją przewodnika. Jeśli chcesz przyczynić się do ulepszenia tłumaczenia, kliknij przycisk "Zgłóś propozycję modyfikacji" na tej stronie.
> 

## Wprowadzenie

Kiedy zamawiasz serwer VPS, możesz wybrać dystrybucję lub system operacyjny do pre-instalowania. Serwer jest więc gotowy do użytku po zainstalowaniu serwera. Jednakże, jako administrator, musisz wdrożyć środki gwarantujące bezpieczeństwo i stabilność systemu.

**Niniejszy przewodnik wyjaśnia, jak zabezpieczyć serwer oparty na GNU/Linux.**

> [!warning]
> OVHcloud świadczy usługi, za które jesteś odpowiedzialny w związku z ich konfiguracją i zarządzaniem. Jesteś więc odpowiedzialny za ich prawidłowe funkcjonowanie.
>
>Jeśli napotkasz trudności z przeprowadzeniem tych operacji, skontaktuj się z wyspecjalizowanym dostawcą usług i/lub przedyskutuj problem z naszą społecznością użytkowników na stronie https://community.ovh.com/en/. OVHcloud nie może udzielić Ci wsparcia technicznego w tym zakresie.
>

## Wymagania początkowe

- Jeden [VPS](https://www.ovhcloud.com/pl/vps/) na Twoim koncie OVHcloud.
- Dostęp administratora (sudo) do serwera przez SSH.

## W praktyce

> [!primary]
>
> Pamiętaj, że jest to ogólny przewodnik przygotowany na podstawie systemów operacyjnych Ubuntu, Debian i CentOS. Niektóre polecenia należy dostosować do używanej dystrybucji, a niektóre z nich wymagają użycia narzędzi zewnętrznych. W razie potrzeby skorzystaj z oficjalnej dokumentacji dotyczącej tych aplikacji.
>
> Jeśli skonfigurujesz Twój pierwszy VPS OVHcloud, zapoznaj się [z przewodnikiem dotyczącym uruchomienia serwera VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps).
>

Poniższe przykłady zakładają, że jesteś zalogowany jako [użytkownik z dużymi uprawnieniami](/pages/bare_metal_cloud/dedicated_servers/changing_root_password_linux_ds).

### Aktualizacja systemu operacyjnego

Producenci dystrybucji i systemów operacyjnych proponują często aktualizacje pakietów ze względów bezpieczeństwa.<br>
Aktualizacja dystrybucji lub systemu operacyjnego jest kluczowa dla zabezpieczenia serwera VPS.

> [!tabs]
> Ubuntu
>>
>> Aktualizację tę przeprowadza się w dwóch krokach:
>> 
>> - Aktualizacja listy pakietów:
>> 
>> ```bash
>> sudo apt update
>> ```
>> 
>> - Aktualizacja aktualnych pakietów:
>> 
>> ```bash
>> sudo apt upgrade
>> ```
>>
> Debian
>> 
>> ```bash
>> sudo apt update && sudo apt upgrade
>> ```
>>
>> Polecenie jest identyczne z Ubuntu, ponieważ Debian i Ubuntu używają `apt`.
>>
> CentOS
>>
>> ```bash
>> sudo yum update
>> ```
>>
>> W przypadku CentOS polecenie aktualizacji systemu operacyjnego używa `yum` lub `dnf` w zależności od wersji.

Operacja ta musi być wykonywana regularnie, aby utrzymać system na bieżąco.

### Zmień domyślny port SSH <a name="changesshport"></a>

> [!primary]
>
> W tej sekcji poniższe wiersze poleceń są takie same w przypadku Ubuntu, Debiana i CentOS.
>

Jedna z pierwszych operacji, jakie należy przeprowadzić na serwerze, to konfiguracja portu wykorzystywanego do nasłuchiwania usługi SSH. Domyślnie jest on zdefiniowany na **porcie 22**, więc próby włamania na serwerze przez roboty będą wskazywać na ten port jako priorytet.
Zmiana tego parametru na inny port to prosty sposób na wzmocnienie ochrony serwera przed automatycznymi atakami.

W tym celu zmodyfikuj plik konfiguracyjny usługi za pomocą wybranego edytora tekstu (`nano` jest używany w tym przykładzie):

```bash
sudo nano /etc/ssh/sshd_config
```

Należy znaleźć następujące lub równoważne linie:

```console
#Port 49152
#AddressFamily any
#ListenAddress 0.0.0.0
```

Zamień liczbę **22** na wybrany numer portu.<br>
**Pamiętaj, aby nie wpisywać numeru portu już używanego w systemie**.
Aby zwiększyć bezpieczeństwo, wprowadź numer 49152 i 65535.<br>Zapisz i wyjdź z pliku konfiguracyjnego.

Jeśli linia jest "zakomentowana" (tj. poprzedzona znakiem "#"), jak w powyższym przykładzie, należy usunąć znak "#" przed zapisaniem pliku, aby zmiana została uwzględniona. Przykład:

```console
Port 49152
#AddressFamily any
#ListenAddress 0.0.0.0
```

Zrestartuj usługę:

```bash
sudo systemctl restart sshd
```

Powinno to wystarczyć do wdrożenia zmian. W przeciwnym razie zrestartuj serwer VPS (`sudo reboot`).

**Dla systemu Ubuntu 23.04 i nowszych wersji**

W przypadku najnowszych wersji Ubuntu, konfiguracja SSH jest zarządzana w pliku `ssh.socket`.

Aby zaktualizować port SSH, edytuj wiersz `ListenStream` w pliku konfiguracyjnym za pomocą wybranego edytora tekstu (`nano` użyty w tym przykładzie):

```console
[Socket]
ListenStream=49152
Accept=no
```

Zapisz zmiany i wykonaj następujące polecenia:

```bash
sudo systemctl daemon-reload
```

```bash
sudo systemctl restart ssh.service
```

Jeśli włączona jest zapora systemu operacyjnego, upewnij się, że zezwalasz na nowy port w regułach zapory.

Pamiętaj, że podczas każdego zlecenia [połączenia SSH z Twoim serwerem](/pages/bare_metal_cloud/dedicated_servers/ssh_introduction) należy wskazać nowy port:

```bash
ssh username@IPv4_VPS -p NewPortNumber
```

Przykład:

```bash
ssh ubuntu@203.0.113.100 -p 49152
```

### Utworzenie użytkownika z ograniczonymi prawami <a name="createuser"></a>

Zadania, które nie wymagają uprawnień root, powinny być wykonywane za pomocą standardowego użytkownika. Więcej informacji znajdziesz w [tym przewodniku](/pages/bare_metal_cloud/dedicated_servers/changing_root_password_linux_ds).

### Konfiguracja wewnętrznej zapory sieciowej (iptables)

Dystrybucje GNU/Linux są dostarczane wraz z zaporą sieciową o nazwie iptables. Usługa ta nie posiada domyślnie żadnej aktywnej reguły. Możesz się o tym przekonać, wpisując następującą komendę:

```bash
iptables -L
```

Więcej informacji na temat iptables znajdziesz w naszym [przewodniku](/pages/bare_metal_cloud/virtual_private_servers/firewall-Linux-iptable).

Zalecamy utworzenie reguł firewalla i dostosowanie ich do Twojego trybu użytkowania. Więcej informacji na temat różnych możliwych operacji znajdziesz w oficjalnej dokumentacji dotyczącej używanej dystrybucji.

### Zainstaluj Fail2ban

Fail2ban to oprogramowanie zapobiegające włamaniom, które blokuje adresy IP, z których atakujący lub bojownicy próbują dostać się do Twojego systemu.<br>
Pakiet ten jest zalecany, a w niektórych przypadkach nawet niezbędny, do ochrony Twojego serwera przed atakami typu *Brute Force* lub *Denial of Service*.

Aby zainstalować pakiet oprogramowania, użyj następującej komendy:

> [!tabs]
> Ubuntu i Debian
>> 
>> ```bash
>> sudo apt install fail2ban
>> ```
>>
> CentOS
>>
>> Na CentOS 7 i CentOS 8 (lub RHEL) najpierw zainstaluj repozytorium EPEL (**E**xtra **P**ackages for **E**nterprise **L**inux), a następnie Fail2ban:
>>
>> ```bash
>> sudo yum install epel-release
>> sudo yum install fail2ban
>> ```

Możesz spersonalizować pliki konfiguracyjne Fail2ban, aby chronić usługi wystawione na działanie publicznego internetu przed próbami wielokrotnego połączenia.

Jak zaleca Fail2ban, utwórz lokalny plik konfiguracyjny Twoich usług kopiując plik "jail.conf":

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Następnie otwórz plik za pomocą edytora tekstu:

```bash
sudo nano /etc/fail2ban/jail.local
```

Pamiętaj, aby przeczytać informacje na górze pliku, w tym komentarze pod `[DEFAULT]`.

Parametry `[DEFAULT]` są globalne i będą miały zastosowanie do wszystkich usług zdefiniowanych do włączenia (`enabled`) w tym pliku. 

Ważne jest, aby wiedzieć, że ogólne parametry będą brane pod uwagę tylko wtedy, gdy nie ma różnych wartości określonych w sekcjach usług (`JAILS`) poniżej w pliku.

Poniżej przedstawiamy przykładowe linie pod `[DEFAULT]`:

```console
bantime = 10m
maxretry = 5
enabled = false
```

Oznacza to, że adres IP, z którego host próbuje się połączyć, zostanie zablokowany przez dziesięć minut po piątej nieudanej próbie rozpoczęcia sesji.<br>
Ponadto wszystkie parametry określone przez `[DEFAULT]` i w kolejnych sekcjach pozostają wyłączone, chyba że `enabled = true` zostanie dodany do usługi (wymienione poniżej `# JAILS`).

Przykładowo, posiadanie następujących linii w sekcji `[sshd]` aktywuje ograniczenia tylko dla usługi OpenSSH:

```console
[sshd]
enabled = true
port = ssh
filter = sshd
maxretry = 3
findtime = 5m
bantime  = 30m
```

W tym przykładzie, jeśli próba połączenia SSH nie powiedzie się trzy razy w ciągu pięciu minut, okres, w którym IP nie będą aktywne, to wynosi 30 minut.

Możesz zmienić "ssh" na rzeczywisty numer portu, jeśli go zmieniłeś.

Najlepsze podejście polega na aktywowaniu Fail2ban tylko w przypadku usług, które są faktycznie wykonywane na serwerze. Każdy spersonalizowany parametr dodany w `# JAILS` będzie pierwszeństwo przed wartościami domyślnymi.

Po zakończeniu modyfikacji zapisz plik i zamknij edytor.

Zrestartuj usługę, aby upewnić się, że działa ona z zastosowanymi ustawieniami:

1\. Polecenie zalecane `systemctl`:

```bash
sudo systemctl restart fail2ban
```

2\. Polecenie z `service` (stara metoda, nadal kompatybilna):

```bash
sudo service fail2ban restart
```

Fail2ban ma wiele ustawień i filtrów personalizacji oraz wstępnie zdefiniowanych opcji, np. jeśli chcesz dodać warstwę ochronną do serwera Nginx.

W celu uzyskania dodatkowych informacji oraz uzyskania zaleceń dotyczących Fail2ban zapoznaj się [z oficjalną](https://www.fail2ban.org/wiki/index.php/Main_Page){.external} dokumentacją tego narzędzia.

### Konfiguracja Network Firewall OVHcloud 

Rozwiązania OVHcloud obejmują możliwość aktywacji firewalla w punkcie wejścia infrastruktury, zwanym Network Firewall. Prawidłowa konfiguracja zapory sieciowej pozwala zablokować połączenia jeszcze przed ich wejściem na Twój serwer.

Sprawdź przewodnik “[Konfiguracja Network Firewall](/pages/bare_metal_cloud/dedicated_servers/firewall_network)”, jeśli chcesz włączyć tą opcję.

### Tworzenie kopii zapasowej systemu i danych

Koncepcja bezpieczeństwa nie ogranicza się do ochrony systemu przed atakami.

Zabezpieczenie danych jest jednym z kluczowych czynników, dlatego OVHcloud oferuje kilka opcji tworzenia kopii zapasowych:

- Opcja `Snapshot` umożliwia tworzenie zrzutu ręcznego.
- Opcja automatycznej `kopii zapasowej` pozwala na zachowanie regularnych kopii zapasowych serwera VPS (z wyjątkiem dodatkowych dysków).

Wszystkie informacje na temat rozwiązań kopii zapasowych dostępnych dla Twojej usługi znajdują się na [stronie produktu](https://www.ovhcloud.com/pl/vps/options/) i w odpowiednich [przewodnikach](/products/bare-metal-cloud-virtual-private-servers).

## Sprawdź również

[Pierwsze kroki z serwerem VPS](/pages/bare_metal_cloud/virtual_private_servers/starting_with_a_vps) 

[Twórz i używaj kluczy SSH](/pages/bare_metal_cloud/dedicated_servers/creating-ssh-keys-dedicated)

[Konfiguracja firewalla w systemie Windows](/pages/bare_metal_cloud/virtual_private_servers/activate-port-firewall-soft-win)

[Konfiguracja firewalla w systemie Linux z systemem iptables](/pages/bare_metal_cloud/virtual_private_servers/firewall-Linux-iptable)

[Konfiguracja rozwiązania Network Firewall](/pages/bare_metal_cloud/dedicated_servers/firewall_network)

Przyłącz się do społeczności naszych użytkowników na stronie <https://community.ovh.com/en/>.
