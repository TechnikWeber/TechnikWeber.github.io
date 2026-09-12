---
layout: beitrag
title: "Proxmox – ein alter Rechner, viele Server"
date: 2026-09-12 09:00:00 +0200
tags: [Elektronik, Linux]
---

Im Keller steht ein Rechner, der zu schade zum Wegwerfen und zu langsam für
den Schreibtisch ist. Genau der richtige Kandidat für **Proxmox VE**: ein
kostenloses Betriebssystem, das nichts anderes tut, als andere Betriebssysteme
laufen zu lassen – mehrere gleichzeitig, sauber getrennt, alle über eine
Weboberfläche im Browser bedienbar.

Statt fünf Geräten für fünf Aufgaben läuft ein Kasten, auf dem fünf Maschinen
wohnen. Jede lässt sich anlegen, sichern, zurückrollen und wieder wegwerfen,
ohne dass die anderen etwas davon merken.

Diese Anleitung führt von der leeren Festplatte bis zum ersten laufenden
Dienst. Was man anschließend daraufsetzt – Pi-hole, Paperless, ein
Minecraft-Server – kommt in eigenen Beiträgen.

## Was Proxmox eigentlich macht

Unter der Haube ist Proxmox VE ein **Debian** mit zwei Zusatztechniken und
einer Weboberfläche darüber:

- **KVM** für virtuelle Maschinen – ein kompletter, simulierter Rechner mit
  eigenem Kernel. Darin läuft alles, auch Windows.
- **LXC** für Container – ein abgeschotteter Bereich, der sich den Kernel des
  Wirts teilt. Nur für Linux, dafür sparsam und in Sekunden gestartet.

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 580 300" role="img"
         aria-label="Schichtenbild: unten der Rechner mit CPU, RAM, SSD und
                     Netzwerkkarte, darüber Proxmox VE als Debian mit KVM und
                     LXC. Darauf drei Gäste nebeneinander: zwei virtuelle
                     Maschinen mit jeweils eigenem Kernel und ein Container
                     ohne eigenen Kernel, der den darunterliegenden mitbenutzt.">
      <g font-family="system-ui, sans-serif" font-size="12" fill="#555">

        <!-- Gaeste -->
        <g>
          <rect x="26" y="40" width="164" height="132" rx="5"
                fill="#fff" stroke="#333"/>
          <text x="108" y="62" text-anchor="middle" font-weight="600"
                fill="#333">VM · Windows</text>
          <rect x="40" y="76" width="136" height="28" rx="3"
                fill="#f0efec" stroke="#8a8a85"/>
          <text x="108" y="95" text-anchor="middle">eigener Kernel</text>
          <rect x="40" y="112" width="136" height="46" rx="3"
                fill="#fbfaf8" stroke="#c9c8c3"/>
          <text x="108" y="140" text-anchor="middle">Programme</text>
        </g>

        <g>
          <rect x="208" y="40" width="164" height="132" rx="5"
                fill="#fff" stroke="#333"/>
          <text x="290" y="62" text-anchor="middle" font-weight="600"
                fill="#333">VM · Debian</text>
          <rect x="222" y="76" width="136" height="28" rx="3"
                fill="#f0efec" stroke="#8a8a85"/>
          <text x="290" y="95" text-anchor="middle">eigener Kernel</text>
          <rect x="222" y="112" width="136" height="46" rx="3"
                fill="#fbfaf8" stroke="#c9c8c3"/>
          <text x="290" y="140" text-anchor="middle">Programme</text>
        </g>

        <g>
          <rect x="390" y="40" width="164" height="132" rx="5"
                fill="#fff" stroke="#b3541e"/>
          <text x="472" y="62" text-anchor="middle" font-weight="600"
                fill="#b3541e">Container · Pi-hole</text>
          <rect x="404" y="76" width="136" height="28" rx="3"
                fill="none" stroke="#b3541e" stroke-dasharray="4 3"/>
          <text x="472" y="95" text-anchor="middle" fill="#b3541e">kein eigener</text>
          <rect x="404" y="112" width="136" height="46" rx="3"
                fill="#fbfaf8" stroke="#c9c8c3"/>
          <text x="472" y="140" text-anchor="middle">Programme</text>
          <!-- teilt sich den Kernel unten -->
          <path d="M472 104v76" stroke="#b3541e" stroke-width="1.4"
                stroke-dasharray="4 3" fill="none" marker-end="url(#pfeilO)"/>
        </g>

        <!-- Proxmox -->
        <rect x="26" y="190" width="528" height="44" rx="5"
              fill="#f6efe2" stroke="#b98a3c"/>
        <text x="290" y="217" text-anchor="middle" font-weight="600"
              fill="#333">Proxmox VE · Debian mit KVM und LXC</text>

        <!-- Blech -->
        <rect x="26" y="246" width="528" height="42" rx="5"
              fill="#f0efec" stroke="#8a8a85"/>
        <text x="290" y="272" text-anchor="middle">der alte Rechner · CPU · RAM · SSD · Netzwerkkarte</text>
      </g>
      <defs>
        <marker id="pfeilO" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#b3541e"/>
        </marker>
      </defs>
    </svg>
  </div>
  <figcaption>Oben die Gäste, unten das Blech. Der Container spart sich den
  eigenen Kernel und nimmt den darunter.</figcaption>
</figure>

Im Zweifel: **Container nehmen.** Er braucht einen Bruchteil der Ressourcen,
und die meisten Heimdienste sind Linux.

| | Virtuelle Maschine | Container |
|---|---|---|
| Betriebssystem | beliebig, auch Windows | nur Linux |
| RAM im Leerlauf | ab ~1 GB | ab ~64 MB |
| Startzeit | wie ein echter PC | Sekunden |
| Trennung | vollständig | gut, aber gemeinsamer Kernel |
{: .messwerte}

## Was der Rechner mitbringen muss

Proxmox ist genügsam. Die harte Bedingung ist eine 64-Bit-CPU mit
Virtualisierungserweiterung – **Intel VT-x** oder **AMD-V**. Alles ab etwa
2012 hat das.

| | Minimum | Vernünftig |
|---|---|---|
| CPU | 64 Bit, VT-x / AMD-V | 4 Kerne |
| RAM | 4 GB | 16 GB |
| Systemplatte | 32 GB | 250 GB SSD |
| Netzwerk | LAN-Kabel | LAN-Kabel |
{: .messwerte}

RAM ist der Engpass, nicht die CPU – jede Maschine will ihren Teil und gibt
ihn nicht wieder her. **WLAN ist keine Option:** Proxmox baut eine Netzwerk-
brücke, und die funktioniert über WLAN nicht zuverlässig.

Ein Punkt für den Mini-PC statt des alten Towers: Der Kasten läuft rund um die
Uhr. Ein Tower zieht im Leerlauf leicht 80 W, ein NUC oder ein gebrauchter
Thin Client 10 W. Bei 30 ct/kWh sind das **210 € gegen 26 € im Jahr** – der
Mini-PC hat sich im ersten Jahr bezahlt.

Die Systemplatte wird bei der Installation **komplett gelöscht**. Nichts
draufliegen lassen, was noch gebraucht wird.

## Der Stapel Raspberry Pis im Regal

In der Bastler-Community sieht man das Muster ständig: ein Pi für Pi-hole,
einer für die Heimautomatisierung, einer für den Dateiserver, einer für das
Ding, dessen Zweck man selbst vergessen hat. Vier Netzteile, vier SD-Karten,
vier Kabel zum Switch – und jedes Mal, wenn eine SD-Karte stirbt, wird ein
Dienst neu aufgesetzt.

Auf einem Proxmox-Kasten sind das vier Container. Ein Netzteil, ein Kabel, eine
Oberfläche, ein Backup-Auftrag, der alle vier gemeinsam sichert. Wer neu anfängt
oder gerade wieder einen Pi kaufen wollte, fährt mit einem gebrauchten Mini-PC
meistens besser: Ein Thin Client mit 16 GB RAM kostet auf dem Gebrauchtmarkt
etwa so viel wie zwei Pis samt Zubehör und trägt ein Dutzend Dienste statt
einem.

Zwei Gründe bleiben trotzdem für den Pi: **GPIO-Pins**, wenn etwas an die
Stiftleiste soll, und **Standorte**, an denen 5 Watt und lautloser Betrieb den
Ausschlag geben. Alles andere kann der Kasten im Keller mitmachen.

## Schritt 1 – USB-Stick vorbereiten

Das ISO gibt es kostenlos bei
[proxmox.com/downloads](https://www.proxmox.com/en/downloads) unter *Proxmox
Virtual Environment*. Kein Konto nötig.

Unter Linux zuerst den Stick finden – die Ausgabe genau lesen, `dd`
überschreibt wortwörtlich alles:

```bash
lsblk
```

Dann schreiben, `sdX` durch den gefundenen Namen ersetzen (also `sdb`, nicht
`sdb1`):

```bash
sudo dd if=proxmox-ve_9.0-1.iso of=/dev/sdX bs=4M status=progress oflag=sync
```

<details markdown="1">
<summary><strong>Unter Windows</strong></summary>

[Rufus](https://rufus.ie) nehmen und beim Schreiben **DD-Modus** wählen, wenn
gefragt wird. Der voreingestellte ISO-Modus baut den Stick um, und der
Proxmox-Installer startet dann nicht. [balenaEtcher](https://etcher.balena.io)
macht es ohne Nachfrage richtig.

</details>

## Schritt 2 – BIOS einstellen

Beim Einschalten ins BIOS (meist `Entf`, `F2` oder `F10`) und drei Dinge
prüfen:

- **Virtualisierung an.** Heißt bei Intel *Intel Virtualization Technology*
  oder *VT-x*, bei AMD *SVM Mode*. Ohne das startet später keine einzige VM.
- **Boot vom USB-Stick.** Entweder in der Bootreihenfolge oder einmalig über
  das Bootmenü (`F8`, `F11`, `F12` – je nach Hersteller).
- **Secure Boot** notfalls aus. Aktuelle Proxmox-Versionen kommen damit klar;
  wenn der Stick partout nicht startet, ist das der erste Schalter.

## Schritt 3 – Installieren

Stick rein, Rechner an, im Menü **Install Proxmox VE (Graphical)** wählen. Der
Rest sind sieben Bildschirme:

1. **Lizenz** – zustimmen.
2. **Zielfestplatte** – hier wird gelöscht. Unter *Options* steht das
   Dateisystem: **ext4** ist für eine einzelne SSD genau richtig. ZFS lohnt
   erst mit mehreren Platten, will viel RAM und verschleißt billige SSDs
   schnell.
3. **Land, Zeitzone, Tastatur** – `Germany`, `Europe/Berlin`, `German`.
4. **Passwort und E-Mail.** Das Passwort ist das des Benutzers `root`. Eine
   echte Adresse eintragen, dorthin gehen später Warnungen über fehlge-
   schlagene Backups.
5. **Netzwerk.** Der wichtigste Bildschirm:
   - *Hostname* muss einen Punkt enthalten, z. B. `pve.heim.lan`
   - *IP-Adresse* **fest** vergeben, außerhalb des DHCP-Bereichs des Routers,
     z. B. `192.168.178.10/24`. Die FritzBox verteilt ab Werk erst ab `.20`,
     alles darunter ist also frei für feste Adressen
   - *Gateway* und *DNS* ist die Adresse des Routers, bei der FritzBox
     `192.168.178.1`
6. **Zusammenfassung** – prüfen, *Install*.
7. **Neustart** – und den Stick ziehen, sonst startet der Installer erneut.

Die feste IP ist kein Schönheitsfehler, sondern Pflicht: Wechselt die Adresse,
ist die Oberfläche weg und die Gäste verlieren ihren Anschluss.

Die Adressen `192.168.178.x` sind der Standard der FritzBox, weil die hier im
Netz hängt. Bei anderen Routern lautet er oft `192.168.0.x` oder
`192.168.1.x` – dann die ersten drei Zahlen überall entsprechend ersetzen.

## Schritt 4 – Der erste Login

Nach dem Neustart zeigt der Bildschirm nur noch eine Adresse. Ab jetzt bleibt
der Rechner zu – bedient wird er vom Sofa aus im Browser:

```
https://192.168.178.10:8006
```

Der Browser warnt vor dem Zertifikat. Das ist in Ordnung, Proxmox stellt sich
selbst eins aus; über *Erweitert* weiterklicken. Anmelden mit Benutzer `root`,
dem vergebenen Passwort und Realm **Linux PAM**. Die Sprache lässt sich im
selben Fenster auf Deutsch stellen – die Anleitung hier bleibt bei den
englischen Bezeichnungen, weil die Voreinstellung so ist.

Nach dem Login meldet ein Fenster „No valid subscription". Das ist die
Erinnerung an das kostenpflichtige Support-Abo. Wegklicken, alles funktioniert.

## Schritt 5 – Updates einschalten

Frisch installiert zeigt Proxmox bei jedem `apt update` einen Fehler: Es
fragt das Enterprise-Repository, und das gibt ohne Abo nichts heraus. Zwei
Klicks, dann stimmt es:

Links den Knoten anklicken (`pve`), dann **Updates → Repositories**:

- Die Zeile mit `enterprise` markieren und **Disable** – für `pve-enterprise`
  und, falls vorhanden, `ceph`.
- **Add** drücken und **No-Subscription** auswählen.

Danach in der Konsole (**Shell** im Menü links) das erste Update:

```bash
apt update && apt full-upgrade -y
reboot
```

Das No-Subscription-Repository liefert dieselben Pakete wie das Enterprise-
Repo, nur ohne die zusätzliche Testrunde. Für zu Hause ist das genau richtig.

## Schritt 6 – Das Netzwerk verstehen

Proxmox hat bei der Installation eine **Brücke** namens `vmbr0` angelegt. Sie
hängt an der Netzwerkkarte, und jeder Gast steckt virtuell dort ein. Für den
Router sieht das aus wie ein Switch mit vielen Geräten daran – jede Maschine
bekommt ihre eigene IP im Heimnetz und ist direkt erreichbar.

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 580 280" role="img"
         aria-label="Netzwerkplan: Der Router mit 192.168.178.1 ist per
                     LAN-Kabel mit dem Proxmox-Host 192.168.178.10 verbunden. Im
                     Host liegt die Brücke vmbr0, an der drei Gäste hängen:
                     Paperless mit .11, ein Minecraft-Server mit .12 und
                     Pi-hole mit .19.">
      <g font-family="system-ui, sans-serif" font-size="12" fill="#555">

        <rect x="200" y="14" width="180" height="38" rx="5"
              fill="#f0efec" stroke="#8a8a85"/>
        <text x="290" y="38" text-anchor="middle" font-weight="600"
              fill="#333">Router · 192.168.178.1</text>

        <line x1="290" y1="52" x2="290" y2="88" stroke="#8a8a85"
              stroke-width="2"/>
        <text x="300" y="74">LAN-Kabel</text>

        <rect x="20" y="88" width="540" height="176" rx="6"
              fill="#fbfaf8" stroke="#8a8a85"/>
        <text x="36" y="108" font-weight="600" fill="#333">Proxmox-Host · 192.168.178.10</text>

        <rect x="40" y="120" width="500" height="32" rx="4"
              fill="#f6efe2" stroke="#b98a3c"/>
        <text x="290" y="141" text-anchor="middle">vmbr0 · die Brücke im Host</text>

        <g stroke="#b98a3c" stroke-width="1.4">
          <path d="M120 152v34"/>
          <path d="M290 152v34"/>
          <path d="M460 152v34"/>
        </g>

        <g>
          <rect x="42" y="186" width="156" height="58" rx="5"
                fill="#fff" stroke="#333"/>
          <text x="120" y="209" text-anchor="middle" fill="#333">Paperless · CT</text>
          <text x="120" y="228" text-anchor="middle">192.168.178.11</text>
        </g>
        <g>
          <rect x="212" y="186" width="156" height="58" rx="5"
                fill="#fff" stroke="#333"/>
          <text x="290" y="209" text-anchor="middle" fill="#333">Minecraft · VM</text>
          <text x="290" y="228" text-anchor="middle">192.168.178.12</text>
        </g>
        <g>
          <rect x="382" y="186" width="156" height="58" rx="5"
                fill="#fff" stroke="#333"/>
          <text x="460" y="209" text-anchor="middle" fill="#333">Pi-hole · CT</text>
          <text x="460" y="228" text-anchor="middle">192.168.178.19</text>
        </g>
      </g>
    </svg>
  </div>
  <figcaption>Ein Kabel, viele Adressen: Jeder Gast hängt über vmbr0 direkt
  im Heimnetz.</figcaption>
</figure>

An der Netzwerkkonfiguration des Hosts danach nichts mehr ändern, solange
alles läuft. Ein Tippfehler dort sperrt einen aus – dann hilft nur noch
Tastatur und Bildschirm am Gerät selbst.

## Schritt 7 – Der erste Container

Zum Ausprobieren ein Debian-Container. Erst die Vorlage holen: links auf
`local (pve)`, dann **CT Templates → Templates**, in der Liste
`debian-13-standard` suchen und **Download**.

Dann oben rechts **Create CT**:

- *Hostname*: `test`, Passwort vergeben
- *Template*: die eben geladene Vorlage
- *Disk*: 8 GB reichen
- *CPU*: 1 Kern
- *Memory*: 512 MB
- *Network*: Bridge `vmbr0`, bei IPv4 entweder `DHCP` oder fest
  `192.168.178.13/24` mit Gateway `192.168.178.1`
- *DNS*: leer lassen, dann gilt die Einstellung des Hosts

**Finish**, dann links den Container anklicken, **Start**, **Console**. Nach
ein paar Sekunden steht dort ein Login-Prompt: `root` und das vergebene
Passwort. Das ist ein vollwertiges Debian – nur eben eines, das man ohne
schlechtes Gewissen wieder löscht.

Genau das ist der Sinn der Sache: ausprobieren, kaputtmachen, wegwerfen,
neu anlegen. Der echte Rechner merkt nichts davon.

## Backups und Snapshots

Zwei verschiedene Dinge, beide unverzichtbar:

**Snapshot** ist ein Standbild von jetzt. Vor jedem Update einer Maschine
einen anlegen (VM anklicken → *Snapshots* → *Take Snapshot*), und wenn das
Update schiefgeht, ist man in zehn Sekunden wieder im Zustand davor. Snapshots
liegen auf derselben Platte – gegen einen Plattenausfall helfen sie nicht.

**Backup** ist eine vollständige Kopie, die woanders liegen sollte. Unter
**Datacenter → Backup → Add** einen Zeitplan anlegen: alle Gäste, einmal
nachts, Modus *Snapshot*, und unter *Retention* etwa `keep-last 3`. Sonst
läuft die Platte irgendwann voll.

Der Ernstfall ist damit kein Drama mehr: neue Platte, Proxmox neu
installieren, Backup zurückspielen.

## Stolpersteine

- **Keine VM startet.** Virtualisierung ist im BIOS aus. Häufigster Fehler.
- **Die Oberfläche ist plötzlich weg.** Der Host hat per DHCP eine neue
  Adresse bekommen. Feste IP vergeben, oder im Router eine Reservierung
  eintragen.
- **`apt update` meldet einen Fehler.** Das Enterprise-Repository ist noch
  an – siehe Schritt 5.
- **Die Platte ist voll.** `local-lvm` hält die Plattenabbilder der Gäste,
  `local` die ISOs, Vorlagen und Backups. Alte ISOs und Backups löschen.
- **ZFS frisst den RAM.** ZFS nimmt sich standardmäßig einen erheblichen Teil
  des Arbeitsspeichers als Cache. Auf einem 8-GB-Rechner lieber ext4.
- **Der Gast hat kein Netz.** Meist eine falsche Bridge oder eine IP, die im
  Netz schon jemand anderem gehört.

## Wie es weitergeht

Der Kasten läuft, und er tut noch nichts Nützliches. Das ändert sich in den
nächsten Beiträgen – geplant sind **Pi-hole** als Werbefilter fürs ganze
Heimnetz, **Paperless** als Ablage für Papierkram und ein **Minecraft-Server**
für die Familie. Alle drei landen in je einem eigenen Container auf genau
dieser Installation.

Handbuch und Quelle für alles Weitere:
[pve.proxmox.com/pve-docs](https://pve.proxmox.com/pve-docs/) ·
[Proxmox-Forum](https://forum.proxmox.com)
