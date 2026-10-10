---
layout: beitrag
title: "RadioKiosk – der Weltempfänger mit Touchscreen"
date: 2026-10-10 07:30:00 +0200
tags: [Amateurfunk, "Raspberry Pi"]
---

Ein Raspberry Pi, ein Touch-Display und ein RTL-SDR-Stick: **RadioKiosk**
macht daraus ein Radio für alles – Webradio, DAB+, UKW, Kurzwelle, Amateurfunk
und eine Flugzeugkarte in einer Oberfläche, die sich mit dem Finger bedienen
lässt.

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

- **Webradio:** Sendersuche über radio-browser.info, mit Senderlogos
- **DAB+:** Suchlauf, Lauftext und die Bilder, die die Sender mitschicken
- **UKW:** Stereo, Sendername und Radiotext (RDS), Suchlauf, Wasserfall
- **Empfänger:** freies Abstimmen in FM, AM und Seitenband – Kurzwelle,
  Amateurfunk, PMR446, Freenet, CB; auf Kurzwelle steht dabei, wer gerade sendet
- **Flugzeuge:** Live-Karte der Maschinen in der Umgebung (ADS-B)
- **Dazu:** Bluetooth, Wetter, Wecker, Sleep-Timer, Aufnahme und Favoriten
  quer über alle Quellen

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/02-ukw-mit-wasserfall.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/02-ukw-mit-wasserfall.jpg"
         alt="UKW-Ansicht auf 103,40 MHz mit Spektrum und Wasserfall, darunter
              Tasten zum Abstimmen und der Radiotext des Senders">
  </a>
  <figcaption>UKW mit Wasserfall und Radiotext.</figcaption>
</figure>

UKW und der freie Empfänger laufen über einen eigenen Empfänger in Python mit
NumPy: Er demoduliert, dekodiert RDS und zeichnet den Wasserfall, ohne den
Stick beim Umstimmen neu zu starten. DAB+ und ADS-B übernehmen bewährte
Programme wie `welle-cli` und `readsb`.

<figure class="abb klein">
  <a href="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/03-flugzeugkarte.jpg">
    <img src="/assets/2026-10-10-radiokiosk-weltempfaenger-mit-touchscreen/03-flugzeugkarte.jpg"
         alt="Karte von Südwestdeutschland mit einem Flugzeug in 37000 Fuß,
              rechts die Liste der empfangenen Maschinen">
  </a>
  <figcaption>Flugzeuge über Süddeutschland, direkt vom Stick.</figcaption>
</figure>

## Ausprobieren

Eine Zeile installiert alles, auf Fedora, Debian, Ubuntu und Raspberry Pi OS:

```sh
curl -fsSL https://raw.githubusercontent.com/TechnikWeber/RadioKiosk/main/install.sh | bash
```

Mit `--kiosk` startet die Oberfläche nach jeder Anmeldung im Vollbild. Ohne
Stick läuft das Webradio trotzdem; Kurzwelle braucht einen Stick, der unter
24 MHz abstimmt, und eine lange Drahtantenne. Das Projekt steht bei Version
0.10 – gebaut ist alles, aber noch nicht auf jeder Hardware ausprobiert.

Code und Anleitung:
[github.com/TechnikWeber/RadioKiosk](https://github.com/TechnikWeber/RadioKiosk)
