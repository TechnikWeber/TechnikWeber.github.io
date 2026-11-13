---
layout: beitrag
title: "IRescue: Die verlorene Fernbedienung per Brute Force wiederfinden"
date: 2026-11-13 07:00:00 +0100
tags: [Elektronik, ESP32]
---

{% include hinweis-strom.html %}

Die Fernbedienung der LED-Lampe ist weg, ein Ersatz nicht zu kaufen. Die Lampe
versteht aber weiter ihre Infrarot-Codes – man muss nur den richtigen finden.
**IRescue** probiert sie mit einem ESP32 und einer IR-LED der Reihe nach durch
und merkt an einem Lichtsensor, wann die Lampe reagiert.

<figure class="abb klein">
  <a href="/assets/2026-11-13-irescue-verlorene-fernbedienung/01-weboberflaeche.png">
    <img src="/assets/2026-11-13-irescue-verlorene-fernbedienung/01-weboberflaeche.png"
         alt="Dunkle Weboberfläche von IRescue: oben Live-Anzeige mit gerade gesendetem Code NEC addr 0 cmd 71, Fortschritt 81 Prozent und Protokoll mit einem Treffer, darunter Lichtsensor mit Kalibrieren-Knopf und die automatische Suche mit Start, Pause, Weiter und Stop">
  </a>
  <figcaption>Suche läuft, ein Treffer steht schon im Protokoll.</figcaption>
</figure>

## So sucht es

1. **Bekannte Codes zuerst:** Listen aus der freien Flipper-IRDB, passend für
   LED-Lampen und -Streifen. Oft ist der Code damit in Minuten gefunden.
2. **Alles durchprobieren:** Das häufigste Protokoll NEC hat 256 Adressen ×
   256 Befehle – rund zwei Stunden.
3. **Selbst erkennen:** Viele Lampen blinken kurz, wenn sie einen Befehl
   annehmen. Der Lichtsensor sieht das, IRescue hält an und grenzt den Code ein.

Ohne Sensor geht es auch (Blind-Modus): Man schaut selbst auf die Lampe.
Codes lassen sich außerdem einzeln von Hand senden. Später soll IRescue echte
Fernbedienungen anlernen und als Pakete im Flipper-Format teilen.

## Hardware

Ein ESP32-DevKit, eine IR-LED (940 nm) mit Transistor, ein Lichtsensor wie der
TEMT6000 und für das Anlernen ein IR-Empfänger. Kosten: wenige Euro.

<figure class="abb klein">
  <a href="/assets/2026-11-13-irescue-verlorene-fernbedienung/02-verdrahtung.png">
    <img src="/assets/2026-11-13-irescue-verlorene-fernbedienung/02-verdrahtung.png"
         alt="Verdrahtungsplan: ESP32 DevKit-C, an GPIO4 über 1 kOhm ein BC337, der die IR-LED mit 33 Ohm an 5 V schaltet, Lichtsensor TEMT6000 an GPIO34 und optionaler IR-Empfänger TSOP38238 an GPIO27">
  </a>
  <figcaption>Verdrahtung, GPIOs in config.h änderbar.</figcaption>
</figure>

Die LED hängt nicht direkt am Pin, sondern am Transistor: So fließen gepulst
rund 110 mA statt 20 mA, das bringt Reichweite.

## Ausprobieren

- Flashen im [Web-Flasher](https://technikweber.github.io/IRescue/) (Chrome
  oder Edge), ganz ohne Entwicklungsumgebung
- Danach ins offene WLAN `IRescue-XXXX`, die Seite öffnet sich von selbst
- Quellcode und Bauteilliste auf
  [GitHub](https://github.com/TechnikWeber/IRescue)

## Stand

Frühe Alpha: Die Firmware baut und lässt sich flashen, an einer echten Lampe
hat sie noch nicht gesucht.
