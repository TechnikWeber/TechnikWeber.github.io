---
layout: beitrag
title: "YonderRC – Fernsteuern über IP"
date: 2026-08-28 08:00:00 +0200
tags: [Elektronik, "Raspberry Pi"]
---

Eine normale RC-Fernsteuerung endet dort, wo ihre Reichweite endet. **YonderRC**
ersetzt sie durch IP: Video, Steuerung und Konfiguration laufen über WLAN oder
LTE, bedient wird im Browser – am PC oder am Handy. Ein Raspberry Pi im Fahrzeug
macht daraus die Servosignale.

<figure class="abb">
  <a href="/assets/2026-08-28-yonderrc-fernsteuerung-ueber-lte/01-bodenstation-fpv-osd.png">
    <img src="/assets/2026-08-28-yonderrc-fernsteuerung-ueber-lte/01-bodenstation-fpv-osd.png"
         alt="Bodenstation von YonderRC im Browser: oben die Verbindungszeile zum
              Fahrzeug, darunter das FPV-Fenster mit dem Testbild des Simulators
              und eingeblendeten Werten – GPS, Home-Kompass, Strecke, Tempo,
              Akkubalken, Spannung, Strom, mAh und der Hinweis DISARMED">
  </a>
  <figcaption>Bodenstation mit FPV und OSD. Hier im Simulator, deshalb das
  Testbild.</figcaption>
</figure>

Dazu kommt das, was eine Fernsteuerung ausmacht: 16 Kanäle mit Trim, Expo,
Endpunkten und Kennlinien, Modellvorlagen für Auto, Boot, Flugzeug und Drohne,
Armen mit Halte-Knopf, Failsafe je Fahrzeugtyp und Telemetrie im Bild. Alles
läuft auch **komplett simuliert**, ganz ohne Hardware.

## Was man mindestens braucht

| Teil | Womit |
|---|---|
| Rechner | Raspberry Pi 4 oder Pi Zero 2 W – beide haben den H.264-Encoder fürs Video. Der Pi 5 hat ihn **nicht**. |
| Karte | microSD 32 GB mit Raspberry Pi OS Lite |
| Servosignale | PCA9685, 16 Kanal über I²C, auf Adresse 0x41 gelegt |
| Strom | UBEC 5 V / 3 A aus dem Fahrakku |

Das war es. Kamera und Stromsensor machen den Aufbau erst rund, nötig sind sie
nicht – ohne sie meldet sich die Simulation. Wer über die Sichtweite hinaus
will, steckt zusätzlich einen **USB-LTE-Stick** an; ein Huawei E3372h-320 tut
es. Am Ende eines Nachmittags im echten Netz standen 110 ms Steuer- und 128 ms
Video-Latenz.

## Installation mit einem Befehl

Auf dem frisch bespielten Pi:

```bash
curl -fsSL https://raw.githubusercontent.com/TechnikWeber/YonderRC/main/provisioning/bootstrap.sh | bash
```

Das holt das Projekt nach `/opt/yonderrc` und richtet den Dienst ein. Danach
`http://<pi-ip>:8080/setup` öffnen und **Detect hardware** drücken: Der Pi geht
den I²C-Bus ab, liest das Kennregister jedes Chips und trägt die Adressen selbst
in die Formulare ein. Auch die Treibermodule installiert diese Seite – kein SSH
nötig. Findet der Pi kein WLAN, macht er seinen eigenen Hotspot auf und schickt
das Handy per Captive Portal direkt auf die Seite.

Code, Teileliste und Verkabelung:
[github.com/TechnikWeber/YonderRC](https://github.com/TechnikWeber/YonderRC)
