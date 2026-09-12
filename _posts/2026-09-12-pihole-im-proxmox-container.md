---
layout: beitrag
title: "Pi-hole im Container – Werbefilter für das ganze Heimnetz"
date: 2026-09-12 14:00:00 +0200
tags: [Elektronik, Linux]
---

Werbeblocker im Browser helfen genau einem Browser. Der Fernseher, das
Tablet der Kinder, die Wetter-App auf dem Handy – die filtert niemand.
**Pi-hole** setzt eine Ebene tiefer an: Es beantwortet die Namensauflösung
für das gesamte Netz und lässt Anfragen an bekannte Werbe- und
Tracking-Domains ins Leere laufen. Ein Gerät, ein Filter, alle profitieren.

Das läuft in einem Container auf der Proxmox-Installation aus dem
[vorigen Beitrag](/2026/proxmox-ein-alter-rechner-viele-server/). Ein Container
statt eines Raspberry Pi, so wie dort beschrieben.

Die Adressen hier sind der FritzBox-Standard `192.168.178.x`. Im
Proxmox-Beitrag stand beispielhaft `192.168.1.x` – wer das übernommen hat,
ersetzt im Folgenden entsprechend.

## Wie das im Netz aussieht

Der entscheidende Punkt: Die FritzBox verteilt weiterhin die Adressen, sagt den
Geräten dabei aber, dass Pi-hole für DNS zuständig ist. Die Geräte fragen
danach direkt beim Pi-hole an.

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 580 300" role="img"
         aria-label="Ablauf einer Namensauflösung: Die FritzBox teilt den
                     Geräten per DHCP mit, dass 192.168.178.5 der DNS-Server
                     ist. Laptop, Handy und Fernseher fragen deshalb direkt
                     beim Pi-hole an. Erlaubte Anfragen reicht Pi-hole an Quad9
                     weiter, geblockte beantwortet es selbst mit 0.0.0.0.">
      <g font-family="system-ui, sans-serif" font-size="12" fill="#555">

        <rect x="196" y="12" width="188" height="36" rx="5"
              fill="#f0efec" stroke="#8a8a85"/>
        <text x="290" y="35" text-anchor="middle" font-weight="600"
              fill="#333">FritzBox · 192.168.178.1</text>

        <path d="M196 32H96v58" stroke="#8a8a85" stroke-width="1.4" fill="none"
              stroke-dasharray="4 3" marker-end="url(#pf)"/>
        <text x="104" y="66">per DHCP: „DNS ist die .5“</text>

        <g>
          <rect x="26" y="96" width="140" height="34" rx="4"
                fill="#fff" stroke="#333"/>
          <text x="96" y="118" text-anchor="middle">Laptop</text>
          <rect x="26" y="140" width="140" height="34" rx="4"
                fill="#fff" stroke="#333"/>
          <text x="96" y="162" text-anchor="middle">Handy</text>
          <rect x="26" y="184" width="140" height="34" rx="4"
                fill="#fff" stroke="#333"/>
          <text x="96" y="206" text-anchor="middle">Fernseher</text>
        </g>

        <g stroke="#8a8a85" stroke-width="1.4" fill="none">
          <path d="M166 113h32v44h14" marker-end="url(#pf)"/>
          <path d="M166 157h46" marker-end="url(#pf)"/>
          <path d="M166 201h32v-44h14" marker-end="url(#pf)"/>
        </g>

        <rect x="216" y="126" width="148" height="62" rx="5"
              fill="#f6efe2" stroke="#b98a3c"/>
        <text x="290" y="150" text-anchor="middle" font-weight="600"
              fill="#333">Pi-hole · .5</text>
        <text x="290" y="172" text-anchor="middle">prüft jeden Namen</text>

        <path d="M364 146h40v-34h22" stroke="#8a8a85" stroke-width="1.4"
              fill="none" marker-end="url(#pf)"/>
        <text x="372" y="106">erlaubt</text>
        <rect x="428" y="92" width="126" height="42" rx="5"
              fill="#fff" stroke="#333"/>
        <text x="491" y="112" text-anchor="middle">Quad9</text>
        <text x="491" y="128" text-anchor="middle">9.9.9.9</text>

        <path d="M364 168h40v44h22" stroke="#b3541e" stroke-width="1.4"
              fill="none" marker-end="url(#pfO)"/>
        <text x="372" y="206" fill="#b3541e">geblockt</text>
        <rect x="428" y="192" width="126" height="42" rx="5"
              fill="#fff" stroke="#b3541e"/>
        <text x="491" y="212" text-anchor="middle" fill="#b3541e">Antwort:</text>
        <text x="491" y="228" text-anchor="middle" fill="#b3541e">0.0.0.0</text>

        <text x="290" y="272" text-anchor="middle">Die FritzBox verteilt weiter
          die Adressen – gefragt wird aber der Pi-hole.</text>
      </g>
      <defs>
        <marker id="pf" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#8a8a85"/>
        </marker>
        <marker id="pfO" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#b3541e"/>
        </marker>
      </defs>
    </svg>
  </div>
  <figcaption>Geblockte Namen beantwortet Pi-hole selbst, der Rest geht nach
  draußen.</figcaption>
</figure>

## Zwei Entscheidungen vorweg

**Kein Docker.** Der LXC *ist* schon der Container. Docker darin bedeutet
`nesting=1`, eine weitere Netzwerkschicht vor Port 53 und `pihole`-Befehle nur
noch über `docker exec`. Der einzige echte Vorteil wäre ein sauberes Rollback
über Image-Tags – und das erledigt das Proxmox-Backup besser.

**Debian statt Ubuntu.** Ubuntu belegt Port 53 mit `systemd-resolved`, den man
erst abschalten muss. Debian 13 bringt das Problem nicht mit.

## Schritt 1 – Template holen

Auf dem **Proxmox-Host** (nicht im Container), in der Shell:

```bash
pveam update
pveam list local
```

Die zweite Zeile zeigt die vorhandenen Vorlagen mit genau dem Namen, den der
nächste Befehl braucht. Fehlt Debian 13 noch:

```bash
pveam available --section system | grep debian-13
pveam download local debian-13-standard_13.1-2_amd64.tar.zst
```

Die Versionsnummer im Dateinamen ändert sich – immer die aus der Ausgabe
nehmen, nicht die hier abgetippte.

## Schritt 2 – Container anlegen

Ebenfalls auf dem Host. `110` ist die Container-Nummer, frei wählbar:

```bash
pct create 110 local:vztmpl/debian-13-standard_13.1-2_amd64.tar.zst \
  --hostname pihole \
  --cores 2 --memory 2048 --swap 512 \
  --rootfs local-lvm:8 \
  --net0 name=eth0,bridge=vmbr0,ip=192.168.178.5/24,gw=192.168.178.1 \
  --nameserver 192.168.178.1 \
  --features nesting=1 \
  --onboot 1 --unprivileged 1 \
  --password
```

Vier Angaben sind keine Geschmacksfrage:

- **Feste IP**, kein DHCP. Ein DNS-Server, dessen Adresse wandert, ist keiner.
- **`--onboot 1`**, sonst steht nach einem Neustart des Hosts das halbe Netz
  ohne Namensauflösung da.
- **`--nameserver`** ist nur der Start-DNS für die Installation. Pi-hole
  schreibt sich das später selbst um.
- **`--unprivileged 1`** ist richtig, solange die FritzBox DHCP macht. Nur wenn
  Pi-hole auch DHCP übernehmen soll, bräuchte es mehr Rechte.

Starten und hineinwechseln:

```bash
pct start 110
pct enter 110
```

Ab hier sind alle Befehle **im Container**.

## Schritt 3 – System vorbereiten

```bash
apt update && apt full-upgrade -y
apt install -y curl ca-certificates sudo
```

## Schritt 4 – Pi-hole installieren

```bash
curl -sSL https://install.pi-hole.net | bash
```

Im Installer vier Antworten, die zählen:

| Frage | Antwort |
|---|---|
| Upstream DNS | Quad9 oder Cloudflare |
| Interface | `eth0` |
| Query Logging | an |
| Privacy Level | 0 – Show everything |
{: .messwerte}

**Nicht die FritzBox als Upstream eintragen** – das gibt eine Schleife, sobald
die FritzBox ihrerseits auf Pi-hole zeigt.

Danach das Passwort für die Oberfläche setzen:

```bash
pihole setpassword
```

Die Oberfläche liegt unter `http://192.168.178.5/admin`.

## Schritt 5 – Erst testen, dann umstellen

Von einem anderen Rechner aus, **bevor** die FritzBox angefasst wird:

```bash
nslookup heise.de 192.168.178.5
nslookup doubleclick.net 192.168.178.5
```

Der erste Name muss eine richtige Adresse liefern, der zweite `0.0.0.0`. Wenn
das nicht stimmt, ist die FritzBox der falsche Ort zum Suchen.

## Schritt 6 – Automatische Updates

Für das Betriebssystem übernimmt das Debian selbst:

```bash
apt install -y unattended-upgrades apt-listchanges
dpkg-reconfigure -plow unattended-upgrades
```

Dann in `/etc/apt/apt.conf.d/50unattended-upgrades` die beiden Zeilen
aktivieren – der Neustart eines Containers dauert zwei Sekunden:

```
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "04:30";
```

Pi-hole selbst hat keinen offiziellen Auto-Updater. Mit Proxmox-Backups im
Rücken ist ein Cronjob vertretbar:

```bash
cat > /etc/cron.d/pihole-selfupdate <<'EOF'
30 4 * * 6 root /usr/local/bin/pihole -up >> /var/log/pihole-update.log 2>&1
EOF
```

Samstags um 4:30, also nach dem Fenster für die Systemupdates. Geht ein Update
schief, wird das Proxmox-Backup zurückgespielt – mehr Sicherung braucht es
nicht.

Die **Blocklisten** aktualisieren sich bereits von allein: Der Installer legt
`/etc/cron.d/pihole` an, das wöchentlich `pihole -g` ausführt.

## Schritt 7 – FritzBox umstellen

**Heimnetz → Netzwerk → Netzwerkeinstellungen → IPv4-Einstellungen**, dort das
Feld *Lokaler DNS-Server* auf `192.168.178.5` setzen.

Damit bekommt jedes Gerät Pi-hole als DNS, die FritzBox selbst behält ihren
eigenen Weg nach draußen. Das ist wichtig: Fällt Pi-hole aus, kommt man über
die FritzBox-Oberfläche weiterhin gegensteuern.

Der umgekehrte Weg – Pi-hole unter *Internet → Zugangsdaten → DNS-Server* als
Upstream der FritzBox – funktioniert zwar auch, kostet aber jede
Client-Statistik:

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 580 300" role="img"
         aria-label="Zwei Wege im Vergleich. Links der richtige: Das Gerät
                     fragt direkt beim Pi-hole an, der nach draußen
                     weiterleitet. Pi-hole sieht jedes Gerät einzeln. Rechts
                     der falsche: Das Gerät fragt die FritzBox, diese den
                     Pi-hole. Pi-hole sieht nur noch die FritzBox als einzigen
                     Fragesteller.">
      <g font-family="system-ui, sans-serif" font-size="12" fill="#555">

        <text x="146" y="26" text-anchor="middle" font-weight="600"
              fill="#333">So herum</text>
        <text x="434" y="26" text-anchor="middle" font-weight="600"
              fill="#b3541e">Nicht so herum</text>

        <!-- richtig -->
        <g stroke="#333">
          <rect x="66" y="96" width="160" height="34" rx="4" fill="#fff"/>
          <rect x="66" y="156" width="160" height="34" rx="4" fill="#f6efe2"/>
          <rect x="66" y="216" width="160" height="34" rx="4" fill="#fff"/>
        </g>
        <text x="146" y="118" text-anchor="middle">Gerät</text>
        <text x="146" y="178" text-anchor="middle" font-weight="600" fill="#333">Pi-hole</text>
        <text x="146" y="238" text-anchor="middle">Internet</text>
        <g stroke="#8a8a85" stroke-width="1.4" fill="none">
          <path d="M146 130v18" marker-end="url(#pf2)"/>
          <path d="M146 190v18" marker-end="url(#pf2)"/>
        </g>
        <text x="146" y="278" text-anchor="middle">sieht jedes Gerät einzeln</text>

        <!-- falsch -->
        <g stroke="#b3541e">
          <rect x="354" y="56" width="160" height="34" rx="4" fill="#fff"/>
          <rect x="354" y="116" width="160" height="34" rx="4" fill="#fff"/>
          <rect x="354" y="176" width="160" height="34" rx="4" fill="#f6efe2"/>
          <rect x="354" y="236" width="160" height="34" rx="4" fill="#fff"/>
        </g>
        <text x="434" y="78" text-anchor="middle">Gerät</text>
        <text x="434" y="138" text-anchor="middle">FritzBox</text>
        <text x="434" y="198" text-anchor="middle" font-weight="600" fill="#333">Pi-hole</text>
        <text x="434" y="258" text-anchor="middle">Internet</text>
        <g stroke="#b3541e" stroke-width="1.4" fill="none">
          <path d="M434 90v18" marker-end="url(#pfO2)"/>
          <path d="M434 150v18" marker-end="url(#pfO2)"/>
          <path d="M434 210v18" marker-end="url(#pfO2)"/>
        </g>
        <text x="434" y="290" text-anchor="middle" fill="#b3541e">sieht nur noch die FritzBox</text>
      </g>
      <defs>
        <marker id="pf2" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#8a8a85"/>
        </marker>
        <marker id="pfO2" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#b3541e"/>
        </marker>
      </defs>
    </svg>
  </div>
  <figcaption>Rechts ist jede Anfrage im Log von der FritzBox – einzelne Geräte
  lassen sich dann nicht mehr ausnehmen.</figcaption>
</figure>

Noch prüfen, dass `192.168.178.5` außerhalb des DHCP-Bereichs liegt oder fest
zugeordnet ist. Die Geräte übernehmen die neue Adresse erst mit der nächsten
DHCP-Erneuerung – WLAN einmal aus und an, oder `ipconfig /renew`.

### IPv6 nicht vergessen

Das ist die häufigste Fehlerquelle. Die FritzBox meldet sich per Router
Advertisement auch als IPv6-DNS-Server, und Windows wie Android bevorzugen
IPv6. Ergebnis: Pi-hole wird umgangen, und im Dashboard kommt fast nichts an.

Unter **Heimnetz → Netzwerk → Netzwerkeinstellungen → IPv6-Einstellungen** die
Option *„DNSv6-Server auch über Router Advertisement bekanntgeben (RFC 5006)"*
abschalten und auch über DHCPv6 keinen DNS-Server ankündigen lassen. Dann läuft
alles über IPv4 zum Pi-hole. Die Bezeichnungen wandern je nach FritzOS-Version
etwas, sinngemäß steht es aber dort.

### Lokale Namen behalten

Damit `nas.fritz.box` weiter funktioniert, im Pi-hole unter **Settings → DNS →
Conditional Forwarding** eintragen:

| Feld | Wert |
|---|---|
| Local network | `192.168.178.0/24` |
| IP of router | `192.168.178.1` |
| Local domain | `fritz.box` |
{: .messwerte}

## Welche Listen

Pi-hole v6 versteht Hosts-Format und Adblock-Syntax. Weniger ist mehr: Fünf
sich überlappende Listen blocken kaum zusätzlich, kosten aber RAM und
produzieren Fehlalarme.

Die Basis reicht für die meisten Haushalte:

| Liste | URL |
|---|---|
| HaGeZi Multi PRO | `…/hagezi/dns-blocklists/main/adblock/pro.txt` |
| HaGeZi Threat Intelligence | `…/hagezi/dns-blocklists/main/adblock/tif.txt` |

Sinnvolle Ergänzungen, wenn mehr sein darf:

| Liste | Zweck |
|---|---|
| HaGeZi Badware Hoster (`hoster.txt`) | Hoster, die fast nur Schadcode ausliefern |
| HaGeZi Popup Ads (`popupads.txt`) | Popup- und Weiterleitungs-Domains |
| Phishing Army | Phishing |
| URLhaus (abuse.ch) | aktive Malware-Verteilung |

Vollständig zum Kopieren:

```
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/hoster.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/popupads.txt
https://phishing.army/download/phishing_army_blocklist_extended.txt
https://urlhaus.abuse.ch/downloads/hostfile/
```

Dazu gehört zwingend eine **Allowlist**, sonst brechen Weiterleitungen in Shops
und Login-Abläufe weg. Unter *Lists* mit Typ **Allow** eintragen:

```
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/whitelist-referral.txt
```

HaGeZi Pro ersetzt die mitgelieferte Standardliste praktisch vollständig; sie
kann danach deaktiviert werden. Wovon ich abraten würde: die
*Ultimate*-Variante und die Native-Tracker-Listen für Apple, Amazon oder
Windows. Die blocken konsequent, aber man sucht danach regelmäßig, warum
irgendein Gerät klemmt.

Nach dem Hinzufügen **Tools → Update Gravity** oder `pihole -g`.

Der Arbeitsablauf, den man sich merken sollte: Wenn etwas nicht geht, Query Log
öffnen, Domain suchen, per Knopfdruck erlauben.

## Drei Stolpersteine

- **Pi-hole nicht als DNS des Proxmox-Hosts eintragen.** Sonst startet der Host,
  braucht Namensauflösung – und der Container, der sie liefern soll, läuft noch
  nicht. Beim Host die FritzBox oder einen externen Resolver eintragen. Dasselbe
  gilt für ein NAS.
- **Geräte mit eingebautem DNS umgehen den Filter.** Chromecasts und manche
  Fernseher fragen fest `8.8.8.8`, Browser mit DNS-over-HTTPS ebenfalls. Bei
  Android unter *Privates DNS* auf „Aus" oder „Automatisch" stellen.
- **iOS merkt sich die alte Einstellung hartnäckig.** Wenn das iPhone im
  Dashboard nicht auftaucht: einmal neu starten. Das räumt Cache und alte
  Konfiguration auf.

## Wie es weitergeht

Der Container läuft, die erste Woche mit dem Dashboard ist erfahrungsgemäß die
interessanteste – man sieht zum ersten Mal, was die Geräte im Hintergrund so
alles fragen.

Als Nächstes in dieser Reihe: **Paperless** für den Papierkram und ein
**Minecraft-Server** für die Familie, beide wieder als Container auf derselben
Installation.

Handbuch: [docs.pi-hole.net](https://docs.pi-hole.net) ·
Listen: [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists)
