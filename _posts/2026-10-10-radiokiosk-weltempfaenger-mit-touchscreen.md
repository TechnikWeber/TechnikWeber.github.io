---
layout: beitrag
title: "RadioKiosk – der Weltempfänger mit Touchscreen"
date: 2026-10-10 07:30:00 +0200
tags: [Amateurfunk, "Raspberry Pi"]
---

Ein Raspberry Pi, ein Touch-Display und ein RTL-SDR-Stick: **RadioKiosk**
macht daraus ein Radio für alles – Webradio, DAB+, UKW, Kurzwelle, Amateurfunk,
Flugzeugkarte, Podcasts und einiges mehr in einer Oberfläche, die sich mit dem
Finger bedienen lässt.

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/01-radiokiosk-auf-dem-raspberry-pi.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/01-radiokiosk-auf-dem-raspberry-pi.jpg"
         alt="Raspberry Pi mit 7-Zoll-Touch-Display, darauf der Startbildschirm
              von RadioKiosk mit Kacheln für Webradio, DAB+, UKW, Empfänger,
              Flugzeuge, Bluetooth und Wetter; davor ein RTL-SDR-Stick">
  </a>
  <figcaption>Raspberry Pi 3 mit 7-Zoll-Display und RTL-SDR-Stick.</figcaption>
</figure>

## Was dahintersteckt

Ein kleiner Python-Dienst steuert die Empfänger und liefert eine
Weboberfläche aus, die ein Browser im Vollbild zeigt. Den Stick kann immer nur
ein Empfänger nutzen, also beendet der Dienst den laufenden, bevor er den
nächsten startet.

## Die Kacheln

- **Hören:** Webradio, DAB+ mit Lauftext und Senderbildern, UKW mit Stereo,
  RDS und Wasserfall, Podcasts mit Vorschlägen aus den aktuellen Charts
- **Empfänger:** freies Abstimmen in FM, AM und Seitenband – Kurzwelle,
  Amateurfunk, PMR446, Freenet, CB
- **Mitlesen:** Flugzeuge (ADS-B) und Schiffe (AIS) auf der Karte,
  Funk-Thermometer und Wetterstationen der Umgebung auf 433 MHz
- **Für Funkamateure:** Funkwetter mit Bandbedingungen und MUF, DX-Cluster und
  POTA, ein QSO-Log mit ADIF-Export und eine Funk-Analyse, die einen Bereich
  über eine gewählte Zeit beobachtet und berichtet, was auf Sendung war
- **Dazu:** Nachrichten per RSS, Wetter mit Mondphase, Galerie, Timer,
  Wecker, Aufnahme und Favoriten quer über alle Quellen
- **Seit dem Update unten:** Kalender, Notizen, Erinnerungen, Smart Home,
  Musik, Hörbücher und Online-Medien

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/02-ukw-mit-wasserfall.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/02-ukw-mit-wasserfall.jpg"
         alt="UKW-Ansicht auf 88,30 MHz mit Spektrum und Wasserfall, darunter
              Tasten zum Abstimmen; in der unteren Leiste der Sendername SWR1 BW">
  </a>
  <figcaption>UKW mit Wasserfall und Sendername.</figcaption>
</figure>

UKW und der freie Empfänger laufen über einen eigenen Empfänger in Python mit
NumPy: Er demoduliert, dekodiert RDS und zeichnet den Wasserfall, ohne den
Stick beim Umstimmen neu zu starten. DAB+, ADS-B, AIS und die Funksensoren
übernehmen bewährte Programme wie `welle-cli`, `readsb`, `rtl_ais` und
`rtl_433`. Der Ruhebildschirm zeigt wahlweise die Uhr, eine Diashow, die
neuesten Nachrichten oder den DX-Cluster.

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/03-funkaktivitaet-dx-cluster.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/03-funkaktivitaet-dx-cluster.jpg"
         alt="Kachel Funkaktivität mit den Reitern DX-Cluster und POTA, einem
              Bandfilter und einer Liste aktueller Meldungen mit Rufzeichen,
              Frequenz und Kommentar">
  </a>
  <figcaption>DX-Cluster: ein Tipp stimmt den Empfänger dorthin ab.</figcaption>
</figure>

## Ausprobieren

Eine Zeile installiert alles, auf Fedora, Debian, Ubuntu und Raspberry Pi OS:

```sh
curl -fsSL https://raw.githubusercontent.com/TechnikWeber/RadioKiosk/main/install.sh | bash
```

Mit `--kiosk` startet die Oberfläche nach jeder Anmeldung im Vollbild, mit
`--ham` kommen die Funk-Kacheln und ihre Programme dazu. Ohne Stick läuft
alles weiter, was keinen braucht; Kurzwelle braucht einen Stick, der unter
24 MHz abstimmt, und eine lange Drahtantenne. Gebaut ist alles, aber noch
nicht auf jeder Hardware ausprobiert.

Code und Anleitung:
[github.com/TechnikWeber/RadioKiosk](https://github.com/TechnikWeber/RadioKiosk)

## Update vom 11. Oktober 2026

Aus dem Weltempfänger ist mehr geworden: Version 0.24 ist auch Küchenradio und
digitaler Bilderrahmen, und sie läuft ohne Touchscreen genauso auf einem
Laptop.

Der Raspberry Pi vom Foto oben steht inzwischen in der Küche, ohne Stick und
mit ausgeblendeten Funk-Kacheln:

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/04-kuechenradio.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/04-kuechenradio.jpg"
         alt="Startbildschirm mit Favoritenzeile und zwölf Kacheln: Webradio,
              Podcasts, Musik, Hörbücher, Online-Medien, Bluetooth,
              Nachrichten, Wetter, Wecker, Timer, Notizen und Erinnerungen;
              in der Kopfzeile das Wetter, rechts Uhrzeit und Datum">
  </a>
  <figcaption>Der Pi als Küchenradio.</figcaption>
</figure>

Die Vollversion mit allen Kacheln steht neben dem Funkgerät:

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/05-alle-kacheln.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/05-alle-kacheln.jpg"
         alt="Startbildschirm mit 28 Kacheln in fünf Reihen: zuerst alles zum
              Hören, dann Nachrichten, Wetter, Kalender, Galerie, Smart Home,
              Wecker, Timer, Notizen und Erinnerungen, zuletzt die
              Funk-Kacheln von Flugzeuge bis SDR++">
  </a>
  <figcaption>Alle Kacheln, mit <code>--ham</code> installiert.</figcaption>
</figure>

Neu seit dem Beitrag:

- **Bilderrahmen:** Die Galerie füllt freie Ränder mit dem unscharfen Bild,
  schwenkt über beschnittene Bilder und wechselt mit Überblenden, Wischen
  oder Blättern. Bilder lassen sich vom Handy hochladen.
- **Alltag:** Kalender über iCal-Adressen, Notizen, Erinnerungen, Wecker mit
  wählbarem Ton und amtliche Warnungen von DWD und NINA.
- **Hören:** eigene Musik, Hörbücher, Online-Medien über yt-dlp, Pause und
  Stummschaltung.
- **Smart Home:** Schalter und Werte über HTTP, etwa Webhooks von Home
  Assistant; umgekehrt lässt sich RadioKiosk von außen steuern.
- **Updates:** ein Knopf in den Einstellungen, auf Wunsch nachts von selbst,
  mit Rückfall auf die alte Version, wenn die neue nicht startet.
