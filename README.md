# Ein Homeserver mit NixOS, der einfach zu warten ist und wenig Zeit braucht - Von der Idee bis zum fertigen Server

## Zusammenfassung:
In diesem Workshop zeigen wir dir, wie du einen Homeserver mit NixOS aufsetzt, der einfach zu warten ist und wenig Zeit benötigt. Du lernst, wie du den Server in einer virtuellen Maschine unter VirtualBox installierst und verschiedene wichtige Komponenten wie OpenSSH, Nginx, Nextcloud und Samba einrichtest. Wir erklären auch, wie du deinen Server verschlüsselst, Backups machst und Cronjobs zur Automatisierung nutzt. Der Workshop richtet sich an alle, die sich für NixOS interessieren, und ist auch für Linux-Neulinge geeignet. Am Ende des Workshops hast du das Wissen, deinen eigenen Homeserver zu betreiben.

## Beschreibung:
In diesem spannenden Workshop zeigen wir dir, wie du einen leistungsfähigen Homeserver mit NixOS aufsetzen kannst, der nicht nur einfach zu warten ist, sondern auch wenig Zeit in Anspruch nimmt. Wir beginnen mit der Installation des Servers in einer virtuellen Maschine (VM) unter VirtualBox, sodass du die Schritte direkt mitverfolgen und selbst umsetzen kannst.

Im Laufe des Workshops werden wir verschiedene wichtige Komponenten installieren und konfigurieren, darunter:

* OpenSSH für sicheren Remote-Zugriff
* Verschlüsselung des Servers zum Schutz deiner Daten
* Backup-Lösungen, um deine Informationen zu sichern
* Firewall-Einstellungen für mehr Sicherheit
* Nginx als Webserver
* Nginx Proxy für die Anbindung von IoT-Geräten
* Nextcloud für deine persönliche Cloud-Lösung
* Samba für die Dateifreigabe im Netzwerk
* Cronjobs zur Automatisierung von Aufgaben
* Du solltest ein Notebook mitbringen, auf dem VirtualBox installiert ist, um aktiv am Workshop teilzunehmen.

Durch die Verwendung von NixOS lernst du die Vorteile eines systemspezifischen Ansatzes kennen, der dir nicht nur Zeit bei der Wartung spart, sondern auch die Reproduzierbarkeit deines Servers gewährleistet. Am Ende des Workshops hast du nicht nur einen voll funktionsfähigen Server in einer VM eingerichtet, sondern auch das Wissen, um zu Hause deinen eigenen Homeserver zu betreiben.

Der Workshop richtet sich an alle, die sich für NixOS interessieren. Er ist so gestaltet, dass auch Personen teilnehmen können, die sich mit Linux noch nicht so gut auskennen. Wir freuen uns darauf, gemeinsam mit dir zu lernen und die Grundlagen von NixOS zu erkunden!


## NixOS Nachteile

### Komplett anders als klassisches Linux
* Die Nix-Sprache ist funktional und unterscheidet sich stark von klassischen Konfigurationsformaten
* Man muss Nix einmal verstanden haben sonst kommt man nicht weiter
* Eigene Nixpkgs schreiben - Kein Standard Linux Paket (steam-run)
* Änderungen müssen immer gebaut werden (teils länger als Installation auf anderen Systemen)
* Plattenplatz
      
### Kompatibilitätsprobleme
* Einige Closed-Source-Programme oder proprietäre Treiber (z.B. Nvidia, Steam, Zoom) brauchen zusätzliche Konfiguration.
* Nicht alles ist als Nix-Paket vorhanden (kann aber selbst gebaut werden).
      
### Probleme während Update
* Manchmal gibt es ein Ruckeln oder Aussetzer auf meinem System während Updates vor allem beim kompilieren


## NixOS - Wird oft als Nachteil genannt - Sehe ich nicht als Nachteil
### Community-getrieben
* Kein kommerzieller Support wie bei RedHat oder Ubuntu LTS.
* Hilfe ist stark von der aktiven, aber kleinen Community abhängig.
### Weniger out-of-the-box Komfort
* Für Einsteiger ist NixOS nicht so "plug & play" wie Ubuntu oder Fedora.
* Konfiguration von z.B. WLAN, GUI, Druckern ist oft Handarbeit.
Systemverwaltung erfordert Umdenken
* Kein typisches apt install - alles wird deklarativ in der Konfigurationsdatei definiert.
* Spontane Systemänderungen verschwinden beim nächsten Rebuild, wenn sie nicht in der Config stehen.



## NixOS Vorteile
### Reproduzierbare Systemkonfiguration
* Die gesamte Systemkonfiguration wird in einer einzigen Konfigurationsdatei (configuration.nix) beschrieben.
* Ideal für unsere Zwecke und auch (DevOps, Infrastruktur als Code)
  
### Rollbacks & Versionierung
* Du kannst das gesamte System oder einzelne Pakete auf einen früheren Zustand zurücksetzen - sogar nach einem fehlgeschlagenen Update.
* Bootloader zeigt mehrere Systemzustände an.
  
### Isolierte Pakete
* Keine "Abhängigkeits-Hölle": Pakete sind vollständig isoliert und können unterschiedliche Versionen gleichzeitig koexistieren.
* Kein "System verdreckt" durch manuelle Installationen.
### Updates
* Updates sind atomar: Sie schlagen entweder ganz fehl oder funktionieren vollständig - keine halbfertigen Systemzustände.
* Rolling Release / Versionen 2 mal im Jahr xx.05 und xx.11
* Geringe Probleme bei Updates
### Paketmanager Nix
* Funktioniert auch unter anderen Distributionen (z. B. Ubuntu).
* Ermöglicht saubere, nicht-invasive Software-Installationen und Entwicklungsumgebungen pro Projekt.
* Software ausprobieren
### Sicherheitsvorteile
* Da Pakete in isolierten Umgebungen laufen, sind Exploits durch System-Pakete schwerer.
* System ist im Auslieferungszustand minimalistisch.
* Read-Only






## NixOS - Quellen

[NixOS Wiki](https://nixos.wiki/)

[NixOS Manual](https://nixos.org/manual/nixos/stable/)

[Download bei NixOS.org](https://nixos.org/)

[GitHub](https://github.com/nixos)

[Search Packages](https://search.nixos.org/packages)

```
nix --extra-experimental-features "nix-command flakes" search nixpkgs firefox
```


## NixOS - Installationmethoden


### Minimal ISO Image

https://nixos.wiki/wiki/NixOS_Installation_Guide

https://channels.nixos.org/nixos-24.11/latest-nixos-minimal-x86_64-linux.iso


### Graphical ISO Image
Unsere Variante in diesem Workshop

https://channels.nixos.org/nixos-24.11/latest-nixos-plasma6-x86_64-linux.iso





## Installieren in VirtualBox

### VirtualBox mit NixOS erstellen
![VirtualBox mit NixOS erstellen](img/VirtualBox1.png) 
### Hauptspeicher und Prozessoren auswählen
![Hauptspeicher und Prozessoren auswählen](img/VirtualBox2.png) 
### Festplatte auswählen
![Festplatte auswählen](img/VirtualBox3.png) 
### Zusammenfassung
![Zusammenfassung](img/VirtualBox4.png) 
### Starten
![Starten](img/VirtualBox5.png)
### NixOS startet - Installer auswählen
![NixOS startet - Installer auswählen](img/VM01.png) 
### Sprache
![Sprache](img/VM02.png) 
### Zeitzone
![Zeitzone](img/VM03.png) 
### Tastatur
![Tastatur](img/VM04.png) 
### Benutzer
![Benutzer](img/VM05.png) 
### Desktop - Plasma (wer eine Grafische Oberfläche will)
![Desktop - KDE](img/VM06.png) 
### ohne Desktop
![ohne Desktop](img/VM07.png) 
### Unfree Software
![Unfree Software](img/VM08.png) 
### Partitionen
![Partitionen](img/VM09.png) 
Festplatte verschlüsseln?
### Richtige Festplatte gewählt?
![Richtige Festplatte gewählt?](img/VM10.png) 
### Zusammenfassung
![Zusammenfassung](img/VM11.png) 
### Installation fertig
![Installation fertig](img/VM12.png) 
### ISO ausgehängt?
![ISO ausgehängt?](img/VM13.png) 
### Zweite Netzwerkkarte für Login per SSH
Damit wir uns direkt von unserem Rechner auf die VM einloggen können und nicht über das Netz der Technische Hochschule Augsburg müssen
![Zweite Netzwerkkarte für Login per SSH](img/VM14.png)
### Unser Installiertes NixOS startet in der VirtualBox
![Unser Installiertes NixOS startet in der VirtualBox](img/VM15.png)


## Wie funktioniert NixOS


### Grundprinzip: Deklarative Konfiguration

In NixOS wird das komplette System - also Pakete, Dienste, Benutzer, Netzwerkeinstellungen, etc. - in einer Konfigurationsdatei beschrieben, meist in 
```
/etc/nixos/configuration.nix
# wird bei Installation automatisch angelegt
/etc/nixos/hardware.conf
```

Du sagst dem System also:
"So soll mein System aussehen", und NixOS baut es daraus automatisch zusammen.

Funktioniert auch wenn Programme, Dienste oder User entfernt werden!

### Paketmanager "Nix"

NixOS basiert auf dem Paketmanager Nix, der:

* Reproduzierbare Builds erlaubt (z.B. zwei Maschinen mit exakt gleichem Setup)
* Pakete in isolierten Pfaden installiert (z.B. /nix/store/...)
* Rollbacks ermöglicht (du kannst jederzeit auf frühere Systemzustände zurückspringen)


Statt ```apt install``` (wie bei Ubuntu) schreibst du z.B. in deine Konfiguration:
```
environment.systemPackages = with pkgs; [
  firefox
  vim
  htop
];
```
Dann führst du einfach aus:
```
sudo nixos-rebuild switch -–upgrade
```

Und NixOS:

* baut dein System gemäß der Konfiguration
* aktiviert alle Dienste und Einstellungen
* lässt dich sofort damit arbeiten



### Rollbacks

Wenn nach dem Update etwas kaputt ist:
Kein Problem - du kannst beim Booten einfach eine ältere Generation auswählen, oder mit:
```
sudo nixos-rebuild switch --rollback
```
zurückspringen.


### Dienste verwalten

Statt manuell wie z.B. in Ubuntu systemctl enable zu machen, schreibst du z. B.:
```
services.openssh.enable = true;
```
in die ```/etc/nixos/configuration.nix```

Dann wird der Dienst beim nächsten ```nixos-rebuild``` automatisch konfiguriert, aktiviert und gestartet.



### Wie funktioniert die Verlinkung bei NixOS?
Pakete liegen im ```/nix/store```

Alle Pakete werden nicht wie üblich in ```/usr/bin```, ```/lib```, etc. installiert, sondern sauber getrennt im Store, z. B.:
```
/nix/store/abc123-firefox-123.0/
/nix/store/xyz789-vim-9.1/
```

Diese Pfade sind unveränderlich und beinhalten genau diese Version.
Der Nix Store ist Read-Only, dass kein Programm dort rein schreiben kann.
Symlinks machen das System benutzbar

NixOS verlinkt (symbolische Verknüpfungen!) die benötigten Programme in eine Umgebung, z. B.:

```
/run/current-system/sw/bin/firefox -> /nix/store/abc123-firefox-123.0/bin/firefox
```
Das sieht für dich aus wie ein normales System – aber es ist alles verlinkt.

```
/nix/store
  ├── abc123-firefox-123.0
  └── xyz789-vim-9.1

/run/current-system/sw/bin/
  ├── firefox  ->  /nix/store/abc123-firefox-123.0/bin/firefox
  └── vim      ->  /nix/store/xyz789-vim-9.1/bin/vim
```

Nix Store (```/nix/store```) Kann geprüft und repariert werden (falls doch mal jemand rein schreibt)

```
nix-store --verify --check-contents --repair
```

Nix Store (```/nix/store```) ist Read-Only - das können wir auch testen
```
touch /nix/store/test
```

## NixOS kennen lernen

SSH einschalten in - ```/etc/nixos/configuration```
```
nano /etc/nixos/configuration.nix
```
 Die Zeile auskommentieren
```
services.openssh.enable = true;
```
Kann auch anders geschrieben werden
```
services.openssh = {
    enable = true;
};
```
Dem User lit den Login erlauben
```
services.openssh = {
    enable = true;
    settings.AllowUsers = [ "lit" ];
};
```
Wenn mehrere User erlaubt sind wir das wie folgt geschrieben
```
settings.AllowUsers = [ "lit" "user1" "user2" "user3" ];
```

### SSH Port

Am besten in der Fritzbox einen anderen Port frei geben und dann auf 22 weiter leiten


### Update & Upgrade
```
nix-channel -–update

# Ändert das System in dem ich bin aber nicht das, das beim nächsten Booten hochfährt – steht in manchen Anleitungen
nixos-rebuild switch

# ich empfehle immer, da ich meine Änderungen nach einem Reboot wieder habe
nixos-rebuild switch -–upgrade
```

### Garbagecollector
```
nix-collect-garbage -d
```

### Gesamter Update Prozess
```
#So habe ich immer den letzten Stand aber trotzdem die Platte frei
nix-collect-garbage -d && nix-channel -–update && nixos-rebuild switch -–upgrade
```

### Programm Ausprobieren

Was läuft auf meinem System
```
htop
```
Mit folgendem Befehl kann ich Programme temporär installieren
```
nix-shell -p [Paket] 
```
Wir installieren htop
```
nix-shell -p htop
```
Jetzt geht htop
```
htop
```

### Welche IP hat unsere VM
Wir lassen uns die IP auf dem Host-System anzeigen, dass wir uns im nächsten Schritt darüber per SSH Einloggen können
z.B. 192.168.56.xxx
```
ip a
```

### Reboot oder Shutdown
Wir starten neu damit wir uns über SSH einloggen können
```
reboot
```
Wir fahren NixOS runter damit wir uns über SSH einloggen können
```
shutdown -h now
```

### SSH-Login
```
ssh lit@192.168.56.xxx
```

### htop ist wieder verschwunden
```
htop
```

## Skript für Updates ```/root/nixjobs.sh```
```
# !/bin/sh
case "$1" in
--update_delete)

nice -n 19 /run/current-system/sw/bin/nix-collect-garbage -d
nice -n 19 /run/current-system/sw/bin/nix-channel --update
nice -n 19 /run/current-system/sw/bin/nixos-rebuild switch --upgrade

;;
--update)

nice -n 19 /run/current-system/sw/bin/nix-channel --update
nice -n 19 /run/current-system/sw/bin/nixos-rebuild switch --upgrade

;;
--verify)

nice -n 19 /run/current-system/sw/bin/nix-store --verify --check-contents --repair

;;
*)

  echo ""
  echo "============ Befehle ==========================================="
  echo "--update_delete  Garbage Collector + Update"
  echo "--update         Update"
  echo "--verify         Repair Packages"
  echo "================================================================"
  echo ""

;;
esac
```

## Programm dauerhaft installieren
```
nano /etc/nixos/configuration.nix
```
Die Zeile auskommentieren und htop installieren
```
environment.systemPackages = with pkgs; [
  htop
];
```

## User definieren und Programme nur für diesen User installieren
iotop nur für User lit installieren
```
users.users.lit = {
    isNormalUser = true;
    description = "User Linux Info Tag";
    extraGroups = [ "wheel" "dialout" "cdrom" ];
    packages = with pkgs; [
	    iotop
    ];
  };
```
## Rollback - Booten in alte Version

Geht im Bootmanager 

Rollback - Wir Booten in alte Version

## Rollback - Dauerhaft rückgängig machen
```
nixos-rebuild switch --rollback
```
Kann auch beim Booten einmalig temporär ausgewählt werden
```
nix-env --list-generations --profile /nix/var/nix/profiles/system
```
```
nix-env --switch-generation NRXXXX -p /nix/var/nix/profiles/system
```

## KDE
Enable the KDE Plasma Desktop Environment.
```
services.displayManager.sddm.enable = true;
services.xserver.desktopManager.plasma5.enable = true;
```

## Firewall
```
networking.firewall.enable = true;
#22 ssh
#80 http
#443 https
networking.firewall.allowedTCPPorts = [ 22 80 443 ];
networking.firewall.allowPing = true;
services.samba.openFirewall = true;
```

## Fail2Ban
```
 services.fail2ban = {
    enable = true;
    # Ban IP after 5 failures
    maxretry = 5;
    ignoreIP = [
      # Whitelist – Eigene IP im Netz
      "192.168.178.0/24"
      "deine.domain.de" # resolve the IP via DNS
    ];
    bantime = "24h"; # Ban IPs for one day on the first ban
  };
```

### Fail2Ban - Config anschauen
```
ls -la /nix/store/*fail2ban*
```
```
ls -la /nix/store/3wk3val49hxqbpdi4d0m3fd6d7vr062r-fail2ban-1.1.0
```


## Imports in /etc/nixos/configuration.nix
```
imports =
    [
      ./hardware-configuration.nix
      ./inc_samba.nix
      ./inc_webserver.nix
    ];
```

## Samba

inc_samba.nix

```
{ config, pkgs, ... }:
{
  services.samba = {
    enable = true;
    settings = {
      global.security = "user";
      www = {
        path = "/var/www";
        browseable = "yes";
        "writeable" = "yes";
        "valid users" = "lit";
        "read only" = "no";
        "guest ok" = "no";
        "create mask" = "0660";
        "directory mode" = "0770";
        "directory mask" = "0770";
        "force user" = "lit";
        "force group" = "nginx";
      };
    };
  };
}
```

### Samba user anzeigen
```
pdbedit -L -w
```

### User anlegen
```
smbpasswd -a lit
```

### User PWD ändern
```
smbpasswd -a <username> 
```

### User löschen
```
smbpasswd -x lit
```

## Domain und Zertifikate

### INWX

[INWX](https://www.inwx.de/)

[INWX - Preisliste](https://www.inwx.de/de/domain/pricelist)

* DNS 1,20€ im Jahr [Stand April 2025]
* DE-Domain 4,65€ im Jahr (erstes Jahr 5,97€) [Stand April 2025]

#### INWX Einstellungen
* Unter: _Registrierung_ kann die Domain beantragt werden
* Unter: _Domainliste -> Zahnrad -> DNS Einträge_ können die Subdomains eingetragen werden
* Subdomain anlegen z.B. dyndns.domain.net
  * Name: dyndns
  * Typ: A
  * Wert: (ist egal, da dieser dann vom DynDNS gesetzt wird)
  * TTL: 60
* Weitere Subdomains für z.B. IoT-Geräte
  * Name: iot1 (Subdomain)
  * Typ: CNAME
  * Wert: dyndns.domain.de
  * TTL: 300

Unter: DynDNS
Den DynDNS Zugang einrichten. Hierfür braucht ihr dann die Subdomain z.B. dyndns.domain.net

#### Fritz.Box Einstellungen
Unter: Internet -> Freigaben -> DynDNS
* Update-URL: ```https://dyndns.inwx.com/nic/update?myip=<ipaddr>```
* Domainname: DynDNS Domainname
* Benutzername: DynDNS Benutzername
* Kennwort: MeinPasswort


### Selfe Signed SSL 
Wir brauchen dieses [Selfe Signed SSL](#selfe-signed-ssl) zum Testen im Workshop. Später wenn Ihr eine Domain habt dann bitte [SSL Root Zertifikat für DE-Domain](#ssl-root-zertifikat-für-de-domain) verwenden.

```
mkdir /var/letsencrypt/
cd /var/letsencrypt/
```

#### Private Key generieren
```
openssl genrsa -out nixos_ca.key 2048
```

#### Root Cert
```
openssl req -new -x509 -days 3650 -key nixos_ca.key -subj "/C=DE/ST=BY/L=AUX/O=nixos/CN=nixos Root CA" -out nixos_ca.crt
```

#### Server Cert Private Key
```
openssl req -newkey rsa:2048 -nodes -keyout nixos_server.key -subj "/C=DE/ST=BY/L=AUX/O=nixos/CN=nixos" -out nixos_server.csr
```

#### Server Cert
```
openssl x509 -req -extfile <(printf "subjectAltName=DNS:nixos,DNS:nixos.local") -days 3650 -in nixos_server.csr -CA nixos_ca.crt -CAkey nixos_ca.key -CAcreateserial -out nixos_server.crt
```



### SSL Root Zertifikat für DE-Domain

#### CertBot installieren

```
environment.systemPackages = with pkgs; [
  ...
  python311Packages.certbot
  python311Packages.certbot-dns-inwx
  ...
];
```

#### Python - PIP
```
python3 -m venv certbot
source certbot/bin/activate
pip install certbot-dns-inwx
```

#### CertBot Secrets für INWX
```
mkdir /var/letsencrypt/
cd /var/letsencrypt/
toch /var/letsencrypt/inwx.cfg
chmod 700 /var/letsencrypt/inwx.cfg
nano /var/letsencrypt/inwx.cfg
```
```
dns_inwx_url           = https://api.domrobot.com/xmlrpc/
dns_inwx_username      = your_username
dns_inwx_password      = """your_password"""
# Entweder secret setzten oder auf "optional" setzen
dns_inwx_shared_secret = optional
```

#### Neues Zertifikat

```
cd /var/letsencrypt/
source certbot/bin/activate
certbot certonly --config-dir . --logs-dir . --work-dir . --agree-tos \
--email <EMAIL> --no-eff-email --authenticator dns-inwx \
--dns-inwx-credentials ./inwx.cfg --dns-inwx-propagation-seconds 30 \
--cert-name <DOMAIN> -d *.<DOMAIN> --no-eff-email
```

#### Renew Zertifikat

```
cd /var/letsencrypt/
source certbot/bin/activate
certbot renew --config-dir . --logs-dir . --work-dir . --agree-tos \
--email <EMAIL> --no-eff-email --authenticator dns-inwx \
--dns-inwx-credentials ./inwx.cfg --noninteractive --force-renewal

sudo systemctl restart nginx 
```

#### CertBot Parameter


* ```certbot renew``` Versucht alle installierten (bzw. im Konfigurationsverzeichnis vorhandenen) SSL-Zertifikate zu erneuern, deren Ablauf in Kürze bevorsteht.

Verzeichnisse:

* ```--config-dir``` Verwendet das aktuelle Verzeichnis (.) als Konfigurationsverzeichnis, statt das standardmäßige (/etc/letsencrypt).

* ```--logs-dir``` Speichert Protokolldateien im aktuellen Verzeichnis.
* ```--work-dir``` Nutzt das aktuelle Verzeichnis für temporäre Arbeitsdateien.

Zustimmung & Kontakt:

* ```--agree-tos``` Du stimmst den Nutzungsbedingungen von Let's Encrypt automatisch zu (Pflicht für die automatische Ausführung).
* ```--email <EMAIL>``` Gibt die Kontakt-E-Mail-Adresse an, z. B. für Benachrichtigungen bei Ablauf eines Zertifikats.
* ```--no-eff-email``` Verhindert, dass deine E-Mail-Adresse an die Electronic Frontier Foundation (EFF) weitergegeben wird.

Authentifizierung via DNS:

* ```--authenticator dns-inwx``` Wählt den Authentifizierungsmethoden-Plugin dns-inwx, um über INWX DNS-Einträge zu setzen (DNS-01 Challenge).
* ```--dns-inwx-credentials ./inwx.cfg``` Gibt den Pfad zur Konfigurationsdatei mit den INWX-Zugangsdaten an. Diese Datei enthält üblicherweise Benutzernamen und Passwort oder Token.

Ausführungsverhalten:
* ```--noninteractive``` Führt Certbot ohne interaktive Abfragen aus – wichtig für Automatisierung (z. B. per Cronjob).
* ```--force-renewal``` Erzwingt die Verlängerung, auch wenn das Zertifikat eigentlich noch nicht abläuft.

## Nextcloud Webserver mit NGINX und MySQL

Nur zur Info: Es gibt von [NixOS ein Paket für Nextcloud](https://nixos.wiki/wiki/Nextcloud)

Wir konfigurieren aber einen eigenen NGINX Server wie auf der Seite von Nextcloud beschrieben.

* [NGINX Config für Nextcloud](https://docs.nextcloud.com/server/latest/admin_manual/installation/nginx.html)

**Hinweis:** Ist die Firewall schon konfiguriert? Sonst haben wir später keinen Zugriff auf den NGINX-Server.

inc_webserver.nix
```
{ config, pkgs, ... }:
{

  services.memcached.enable = true;

# MYSQL ======================================================================
  services.mysql = {
    enable = true;
    package = pkgs.mariadb;
  };
# MYSQL ================================================================== END

# PHP ========================================================================
  services.phpfpm.phpOptions = ''
    extension=${pkgs.phpExtensions.imagick}/lib/php/extensions/imagick.so
    extension=${pkgs.phpExtensions.opcache}/lib/php/extensions/opcache.so
    extension=${pkgs.phpExtensions.bz2}/lib/php/extensions/bz2.so
    extension=${pkgs.phpExtensions.apcu}/lib/php/extensions/apcu.so
  '';

  services.phpfpm.pools.mypool = {                                                                                                                                                                                                             
    user = "lit";
    group = "nginx";                                                                                                                                                                                                                           
    phpPackage = pkgs.php83.buildEnv {
      extensions = {enabled, all}: enabled ++ (with all; [
        apcu
        bcmath
        gmp
        imagick
        opcache
        pdo
        pdo_pgsql
        memcached
      ]);
      extraConfig = ''
        output_buffering = off
        memory_limit = 1G
        apc.enable_cli = 1
        opcache.memory_consumption=256
        opcache.interned_strings_buffer=64
        opcache.max_accelerated_files=32531
        opcache.validate_timestamps=0
        opcache.enable_cli=1
      '';
    };
    settings = {                                                                                                                                                                                                                               
      "clear_env" = "no";
      "pm" = "dynamic";            
      "listen.owner" = config.services.nginx.user;                                                                                                                                                                                                              
      "pm.max_children" = 5;                                                                                                                                                                                                                   
      "pm.start_servers" = 2;                                                                                                                                                                                                                  
      "pm.min_spare_servers" = 1;                                                                                                                                                                                                              
      "pm.max_spare_servers" = 3;                                                                                                                                                                                                              
      "pm.max_requests" = 500;                                                                                                                                                                                                                 
    };
  };
# PHP ==================================================================== END

# NGINX ======================================================================
  services.nginx = {
    enable = true;
    user = "lit";
    group = "nginx";
    recommendedProxySettings = true;
    recommendedTlsSettings = true;
    commonHttpConfig = ''
        # Set the `immutable` cache control options only for assets with a cache busting `v` argument
        map $arg_v $asset_immutable {
            "" "";
            default "immutable";
        }
    ''; 

    virtualHosts."cloud.domain.de" = {
      root = "/var/www/nextcloud/";
      forceSSL = true;
      sslCertificate = "/var/letsencrypt/nixos_server.crt";
      sslCertificateKey = "/var/letsencrypt/nixos_server.key";
      extraConfig = ''
        listen 443 ssl http2;
        server_tokens off;
        ########## SSL Configuration ######################################################
        #ssl_certificate           /var/letsencrypt/domain.de/fullchain.crt;
        #ssl_certificate_key       /var/letsencrypt/domain.de/domain.de.key;
        #ssl_session_cache  builtin:1000  shared:SSL:10m;
        #ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
        #ssl_ciphers HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4;
        #ssl_prefer_server_ciphers on;
        ########## SSL Configuration ###################################################END
        
        ########## Header configuration ###################################################
        # HSTS (ngx_http_headers_module is required) In order to be recoginzed by SSL test, there must be an index.hmtl in the server's root
        add_header Strict-Transport-Security "max-age=63072000; includeSubdomains; preload;" always; 
        add_header X-Content-Type-Options "nosniff" always;
        add_header X-XSS-Protection "1; mode=block" always;
        add_header X-Robots-Tag "noindex, nofollow" always;
        add_header X-Download-Options noopen always;
        add_header X-Permitted-Cross-Domain-Policies none always;
        add_header Referrer-Policy no-referrer always;
        add_header X-Frame-Options "SAMEORIGIN" always;
        # Disable FLoC
        add_header Permissions-Policy "interest-cohort=()";
        # Remove X-Powered-By, which is an information leak
        fastcgi_hide_header X-Powered-By;
        ########## Header configuration ################################################END

        # set max upload size and increase upload timeout:
        client_max_body_size 10G;
        client_body_timeout 300s;
        fastcgi_buffers 64 4K;
        
        # Enable gzip but do not remove ETag headers
        gzip on;
        gzip_vary on;
        gzip_comp_level 4;
        gzip_min_length 256;
        gzip_proxied expired no-cache no-store private no_last_modified no_etag auth;
        gzip_types application/atom+xml application/javascript application/json application/ld+json application/manifest+json application/rss+xml application/vnd.geo+json application/vnd.ms-fontobject application/wasm application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/bmp image/svg+xml image/x-icon text/cache-manifest text/css text/plain text/vcard text/vnd.rim.location.xloc text/vtt text/x-component text/x-cross-domain-policy;
        # Specify how to handle directories -- specifying `/index.php$request_uri`
        # here as the fallback means that Nginx always exhibits the desired behaviour
        # when a client requests a path that corresponds to a directory that exists
        # on the server. In particular, if that directory contains an index.php file,
        # that file is correctly served; if it doesn't, then the request is passed to
        # the front-end controller. This consistent behaviour means that we don't need
        # to specify custom rules for certain paths (e.g. images and other assets,
        # `/updater`, `/ocm-provider`, `/ocs-provider`), and thus
        # `try_files $uri $uri/ /index.php$request_uri`
        # always provides the desired behaviour.
        index index.php index.html /index.php$request_uri;
        # Rule borrowed from `.htaccess` to handle Microsoft DAV clients
        location =  {
            if ( $http_user_agent ~ ^DavClnt ) {
                return 302 /remote.php/webdav/$is_args$args;
            }
        }
        # Make a regex exception for `/.well-known` so that clients can still
        # access it despite the existence of the regex rule
        # `location ~ /(\.|autotest|...)` which would otherwise handle requests
        # for `/.well-known`.
        location ^~ /.well-known {
            # The rules in this block are an adaptation of the rules
            # in `.htaccess` that concern `/.well-known`.
            location = /.well-known/carddav { return 301 /remote.php/dav/; }
            location = /.well-known/caldav  { return 301 /remote.php/dav/; }
            location = /.well-known/webfinger  { return 301 /index.php/.well-known/webfinger; }
            location = /.well-known/nodeinfo  { return 301 /index.php/.well-known/nodeinfo; }
            location /.well-known/acme-challenge    { try_files $uri $uri/ =404; }
            location /.well-known/pki-validation    { try_files $uri $uri/ =404; }
            # Let Nextcloud's API for `/.well-known` URIs handle all other
            # requests by passing them to the front-end controller.
            return 301 /index.php$request_uri;
        }
        # Rules borrowed from `.htaccess` to hide certain paths from clients
        location ~ /\.h {
          deny all;
        }
        location ~ \.tpl(?:$|/) { return 404; }
        location ~ \.log(?:$|/) { return 404; }
        location ~ ^/(?:build|tests|config|lib|3rdparty|templates|data)(?:$|/)  { return 404; }
        location ~ ^/(?:\.|autotest|occ|issue|indie|db_|console)                { return 404; }
        # Ensure this block, which passes PHP files to the PHP process, is above the blocks
        # which handle static assets (as seen below). If this block is not declared first,
        # then Nginx will encounter an infinite rewriting loop when it prepends `/index.php`
        # to the URI, resulting in a HTTP 500 error response.
        location ~ \.php(?:$|/) {
        # Required for legacy support
            rewrite ^/(?!index|remote|public|cron|core\/ajax\/update|status|ocs\/v[12]|updater\/.+|oc[ms]-provider\/.+|.+\/richdocumentscode\/proxy) /index.php$request_uri;
            fastcgi_split_path_info ^(.+?\.php)(/.*)$;
            set $path_info $fastcgi_path_info;
            try_files $fastcgi_script_name =404;
            include ${pkgs.nginx}/conf/fastcgi_params;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param PATH_INFO $path_info;
            fastcgi_param HTTPS on;
            fastcgi_param modHeadersAvailable true;         # Avoid sending the security headers twice
            fastcgi_param front_controller_active true;     # Enable pretty urls
            fastcgi_pass  unix:${config.services.phpfpm.pools.mypool.socket};
            fastcgi_intercept_errors on;
            fastcgi_request_buffering off;
            fastcgi_max_temp_file_size 0;
            fastcgi_read_timeout 600;
            fastcgi_send_timeout 600;
            fastcgi_connect_timeout 600;
            fastcgi_param PHP_VALUE "upload_max_filesize = 10G
            memory_limit = 1G
            post_max_size = 10G
            max_execution_time = 3600
            output_buffering = off";
            fastcgi_split_path_info ^(.+\.php)(/.*)$;
            fastcgi_param DOCUMENT_ROOT $document_root;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
        location ~ \.(?:css|js|svg|gif|png|jpg|ico|wasm|tflite|map)$ {
            try_files $uri /index.php$request_uri;
            #add_header Cache-Control "public, max-age=15778463, $asset_immutable";
            access_log off;     # Optional: Don't log access to assets
            location ~ \.wasm$ {
                default_type application/wasm;
            }
        }
        location ~ \.woff2?$ {
            try_files $uri /index.php$request_uri;
            expires 7d;         # Cache-Control policy borrowed from `.htaccess`
            access_log off;     # Optional: Don't log access to assets
        }
        # Rule borrowed from `.htaccess`
        location /remote {
            return 301 /remote.php$request_uri;
        }
        location / {
            try_files $uri $uri/ /index.php$request_uri;
        }
    '';
    };
  };
  # NGINX ================================================================== END
  # Weitere virtualHosts =======================================================
  # Webserver
  # IoT
  # Weitere virtualHosts =================================================== END
}

```

### MySQL vorbereiten

```
mysql -uroot
```
```
CREATE USER 'nextcloud'@'localhost' IDENTIFIED BY 'password';
CREATE DATABASE IF NOT EXISTS nextcloud CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
GRANT ALL PRIVILEGES on nextcloud.* to 'nextcloud'@'localhost';
FLUSH privileges;
quit
```


### Nextcloud Installieren

#### Benötigte Programme
```
environment.systemPackages = with pkgs; [
  outils
  
  (pkgs.php83.buildEnv {
    extensions = ({enabled, all}: enabled ++ (with all; [
      apcu
      bcmath
      gmp
      imagick
      opcache
      pdo
      pdo_pgsql
      memcached
    ]));
    extraConfig = ''
      apc.enable_cli = 1
    '';
  })
 
  unp
  wget
];
```

#### Installation in Konsole

**Nur zur Info:** Kann auch über Samba-Freigabe auf den NGINX-Webserver kopiert werden

```
mkdir -p /var/www/
mkdir -p /var/www/nextcloud_data
cd /var/www/
wget https://download.nextcloud.com/server/releases/nextcloud-31.0.4.tar.bz2
wget https://download.nextcloud.com/server/releases/nextcloud-31.0.4.tar.bz2.sha256
sha256 nextcloud-31.0.4.tar.bz2 -C nextcloud-31.0.4.tar.bz2.sha256
unp nextcloud-31.0.4.tar.bz2
chown lit:nginx -R /var/www/
chown lit:nginx -R /var/www/nextcloud_data
chown lit:nginx -R /var/letsencrypt
```

#### Installation im Browser

https://192.168.56.xxx im Browser aufrufen

##### Installation Starten
![Installation Starten](img/Nextcloud01.png) 
##### Datenbank auswählen
![Datenbank auswählen](img/Nextcloud02.png) 
##### Apps Installieren
![Apps Installieren](img/Nextcloud03.png) 
##### Nextcloud läuft
![Nextcloud](img/Nextcloud04.png) 

#### Nextcloud Config

```
  $CONFIG = array (
  'instanceid' => 'oc9668j0e3y2',
  'passwordsalt' => '60wu3x5K0tiVDf79CkwDEXKWmwhzNe',
  'secret' => 'DMlzRztG2LA+mCsXR5xnGdjouXc3drgv8LmnZcJy/pM09GZa',
  'trusted_domains' => 
  array (
    0 => '192.168.56.102',
  ),
  'datadirectory' => '/var/www/nextcloud_data',
  'dbtype' => 'mysql',
  'version' => '31.0.4.1',
  'overwrite.cli.url' => 'https://192.168.56.102',
  'dbname' => 'nextcloud',
  'dbhost' => 'localhost',
  'dbport' => '',
  'dbtableprefix' => 'oc_',
  'mysql.utf8mb4' => true,
  'dbuser' => 'nextcloud',
  'dbpassword' => 'password',
  'installed' => true,
  
  // Add to config
  'mail_from_address' => 'mail',
  'mail_smtpmode' => 'smtp',
  'mail_sendmailmode' => 'smtp',
  'mail_domain' => 'domain.de',
  'mail_smtphost' => 'mail.domain.de',
  'mail_smtpport' => '25',
  'mail_smtpauth' => 1,
  'mail_smtpname' => 'mail@domain.de',
  'mail_smtppassword' => 'password', 
  'installed' => true,
  'maintenance' => false,
  'maintenance_window_start' => 1,
  'default_phone_region' => 'DE',
  'filelocking.enabled' => true,
  'theme' => '',
  'memcache.local' => '\OC\Memcache\APCu',
  'memcache.distributed' => '\OC\Memcache\Memcached',
  'memcache.locking' => '\OC\Memcache\Memcached',
  'memcached_servers' => [
    [ 'localhost', 11211 ],
  ],
  'updater.release.channel' => 'stable',
);

```
_Im Livesystem die IP durch die Domain ersetzten, oder gleich mit der Domain den Web-Installer ausführen._

#### Wartung 

[Sicherheitsscanner von Nextcloud](https://scan.nextcloud.com/)

Verwaltungseinstellungen -> https://192.168.56.102/settings/admin/overview

Gehe auch auf deine Nextcloud mit dem Handy und erlaube Benachrichtigungen, dann erhältst du auch eine Info, wenn es eine neue Version gibt und du updaten kannst.

##### OCC ausführen
```
# z.B.
/run/current-system/sw/bin/php -d memory_limit=2G /var/www/nextcloud/occ db:add-missing-indices
/run/current-system/sw/bin/php -d memory_limit=2G /var/www/nextcloud/occ maintenance:repair --include-expensive

```

### Zusätzlicher Webserver
```
virtualHosts."www.domain.de" = {
  forceSSL = true;
  sslCertificate = "/var/letsencrypt/domain.de/domain.de.crt";
  sslCertificateKey = "/var/letsencrypt/domain.de/domain.de.key";
  root = "/var/www/htdocs_webserver/";
  locations."~ \\.php$".extraConfig = ''
    fastcgi_index index.php;
  '';
};
```

### Internet of Things sicher im Internet frei geben
```
virtualHosts."iot.domain.de" =  {
  basicAuth = { user = "Passwort"; };
  forceSSL = true;
  sslCertificate = "/var/letsencrypt/domain.de/domain.de.crt";
  sslCertificateKey = "/var/letsencrypt/domain.de/domain.de.key";
  locations."/" = {
    proxyPass = "https://IoT-IP";
    proxyWebsockets = true; # needed if you need to use WebSocket
    extraConfig =
      # required when the target is also TLS server with multiple hosts
      "proxy_ssl_server_name on;" +
      # required when the server wants to use HTTP Authentication
      "proxy_pass_header Authorization;"
      ;
  };
};
```

## Systemd
```
systemd.services.NameVomDienst = {
      wantedBy = [ "multi-user.target" ];
      after = [ "network.target" ];
      description = "Start NameVomDienst";
      serviceConfig = {
        Type = "oneshot";
        RemainAfterExit = "yes";
        User = "lit";
        ExecStart = ''/home/lit/DienstStartStop.sh --start''; 
        ExecStop = ''/home/lit/DienstStartStop.sh --stop'';
      };
   };
```

## CronJob
```
services.cron = {
  enable = true;
  systemCronJobs = [
      # Min  Hour  day  month   day_of_week
      "@reboot  root . /etc/profile; /root/BeimStarten.sh"
      "0   1  *  *  *   root  . /etc/profile; /root/backup.sh"
      "*/5   *  *  *  *   lit  . /etc/profile; /run/current-system/sw/bin/php -d memory_limit=2G /var/www/nextcloud/cron.php"
    ];
  };
```

## Backup

Du brauchst nur die nixos Konfigurationsdateien (da diese das ganze System beschreiben)
```
/etc/nixos/configuration.nix
/etc/nixos/inc_samba.nix
/etc/nixos/inc_webserver.nix
```
**Info:** Einige NixOS User verwenden zum sichern der Configs GitHub. Hier muss unbedingt darauf geachtet werden, dass du dann keine Passwörter in die Config schreibst, wie z.B. im Kapitel [Internet of Things sicher im Internet frei geben](#internet-of-things-sicher-im-internet-frei-geben) 

Und natürlich sicherst du deine Eigene Daten z.B. in
```
/home/*
/var/*
/var/www
/var/lib/mysql/

```

## Restore

NixOS einfach wie zu Anfang mit dem [ISO Image](#graphical-iso-image) installieren, dann die NixOS Konfigurationsdateien einspielen und einen Rebuild auslösen ```nix-channel -–update && nixos-rebuild switch -–upgrade``` schon habt Ihr euer System wieder so wie es war.

```
/etc/nixos/configuration.nix
/etc/nixos/inc_samba.nix
/etc/nixos/inc_webserver.nix
```

Jetzt fehlen nur noch die eigenen Dateien. Hier ggf. wieder die Verzeichnisse anlegen und die Daten rein kopieren.
```
/home/*
/var/*
/var/www
/var/lib/mysql/

```

**Nur zur Info:** in der ```configuration.nix``` könnte man auch Verzeichnisse anlegen lassen. Das mache ich der Übersichtlichkeit halber lieber selber. Da ich nach einem Restore die Daten ja auch wieder einspielen muss und dabei die Verzeichnisse anlege.

## Code Beispiele für Backup

Hier bitte selber anhand der Beispiele ein passende backup.sh erstellen

backup.sh


```
#!/run/current-system/sw/bin/bash

heute=`date -d "now" +Y-%m-%d`
gestern=`date -d "1 day ago" +Y-%m-%d`
loeschen=`date -d "7 day ago" +Y-%m-%d`
backup_ziel='/mnt/backup/'
exclude='--exclude=/mnt --exclude=/media --exclude=/proc --exclude=/sys --exclude=/tmp –exclude=/dev'

# Auf gleichem Server aber andere Platte
rsync -a --link-dest=$backup_ziel$gestern/ $exclude / $backup_ziel$heute

rm -R $backup_ziel$loeschen

# Beispiel für Backup auf anderen Server
# rsync -a -e 'ssh -p 2222' --rsync-path="sudo rsync" --exclude=/mnt --exclude=/media --exclude=/proc --exclude=/sys --exclude=/tmp –exclude=/dev / lit@mein.server.net:/mnt/backup/YYYY-mm-dd/

```

* ```#!/run/current-system/sw/bin/bash``` unter NixOS nicht ```#!/bin/bash```
* ```rsync```: Archiv-Modus - Kopiert Dateien rekursiv und bewahrt Berechtigungen, Zeitstempel, Symbolische Links, etc. – sehr wichtig für Backups.
* ```-a```: Ist das Synchronisations-Tool, ideal für Backups oder zum syncen von 2 Verzeichnissen
* ```--link-dest```: Hardlinks - Wenn eine Datei nicht verändert wurde, wird kein neuer Speicherplatz belegt, sondern es wird ein Hardlink auf die Datei im $gestern-Verzeichnis erstellt.
* ```--exclude```: Ausschluss-Optionen für Verzeichnisse
* ```/```: Das Quellverzeichnis
* ```$backup_ziel$heute```: Zielverzeichnis für das heutige Backup – z. B. /mnt/backup/xxxx-xx-xx.


## MySQL-Dump

Hat den Vorteil, dass man vorher die DB nicht anhalten muss
```
mysqldump --single-transaction --no-tablespaces -all -C -c -e --host=localhost --user=DeinUserFürDieDB --password=DeinPasswortFürDieDB --all-databases | gzip --rsyncable -c > /mnt/DB/db.sql.gz
```

* ```--single-transaction```:
Macht ein konsistentes Backup (wichtig bei InnoDB), ohne die Datenbank zu sperren. Ideal für Live-Systeme.

* ```--no-tablespaces```:
Ignoriert Informationen über Tablespaces, was besonders bei InnoDB wichtig ist (z.B. wenn man nicht den gleichen Speicherpfad beim Restore hat).

* ```--all```:
Dump enthält auch alle Trigger. (Hinweis: -a ist eigentlich kein offizieller Mysqldump-Schalter, möglicherweise ist hier --all gemeint oder ein Alias je nach System).

* ```-C```:
Aktiviert Komprimierung der Verbindung zum Server (nicht zu verwechseln mit Datei-Komprimierung).

* ```-c```:
Verwendet vollständige INSERT-Statements (z. B. INSERT INTO t (a,b) VALUES (1,2) statt INSERT INTO t VALUES (1,2)).

* ```-e```:
Verwendet erweiterte INSERT-Statements für bessere Performance (mehrere Werte in einem INSERT).

* ```--host=localhost```:
Verbindet sich mit dem lokalen MySQL-Server.

* ```--user=DeinUserFürDieDB```:
Gibt den Benutzernamen an.

* ```--password=DeinPasswortFürDieDB```:
Gibt das Passwort an

* ```--all-databases```:
Sichert alle Datenbanken auf dem MySQL-Server auf die der Benutzer zugriff hat.


## Release Upgrade

[Release Notes lesen](https://nixos.org/nixos/manual/release-notes.html)
Aktuelles Release anzeigen
```
nix-channel --list
```

Neues Release hinzufügen
```
nix-channel --add https://nixos.org/channels/nixos-xx.xx nixos
```

Schauen ob es geklappt hat
```
nix-channel --list
```

System mit neuem Release bauen
```
nix-channel --update
nixos-rebuild --upgrade boot
```

Hinweise beachten die bei ```nixos-rebuild --upgrade boot``` auftreten. Manchmal ändert sich das ein oder andere an der Konfiguration. Meist kommt dann ein Hinweis, dass folgenden Konfiguration durch eine andere ersetzt wurde. Dann bitte die ```/etc/nixos/configuration.nix``` dementspreichend anpassen.

# Alle wichtigen Befehle noch mal kurz im Überblick

## Update & Upgrade
```
nix-channel -–update

nixos-rebuild switch -–upgrade
```

## Garbagecollector
```
nix-collect-garbage -d
```

## Gesamter Update Prozess
```
nix-collect-garbage -d && nix-channel -–update && nixos-rebuild switch -–upgrade
```

## Programm Ausprobieren
```
nix-shell -p [Paket]
```

## Repair Packages
```
nix-store --verify --check-contents --repair
```

## Rolback
Kann auch beim Booten einmalig temporär ausgewählt werden

```
nix-env --list-generations --profile /nix/var/nix/profiles/system
```

```
nix-env --switch-generation NRXXXX -p /nix/var/nix/profiles/system
```
