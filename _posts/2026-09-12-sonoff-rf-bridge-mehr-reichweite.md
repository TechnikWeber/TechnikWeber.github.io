---
layout: beitrag
title: "Sonoff RF Bridge: 17,3 cm Draht, doppelte Reichweite"
date: 2026-09-12 21:00:00 +0200
tags: [Amateurfunk, Elektronik]
---

{% include hinweis-strom.html %}

Die Sonoff RF Bridge setzt 433-MHz-Funksignale ins WLAN um – mit ihren
winzigen Spiralantennen aber nur über kurze Strecken. Also runter damit und
durch zwei gestreckte Drähte ersetzt.

Zwei Antennen, weil Sender und Empfänger getrennte Bausteine sind – billiger
als ein kombinierter Chip mit Antennenumschalter. Gesendet und empfangen wird
trotzdem abwechselnd auf derselben Frequenz, also **Simplex**. Duplex hieße
gleichzeitig senden und empfangen.

> **Nur ein Experiment.** Die Bridge funkt im ISM-Band, und dort gelten
> strenge Regeln: höchstens 10 mW Strahlungsleistung, nur zugelassene Geräte
> mit Originalantenne. Mit dem Umbau ist beides dahin – daran ändert auch eine
> Amateurfunklizenz nichts.

<figure class="abb klein">
  <a href="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/01-rf-bridge-geschlossen.jpg">
    <img src="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/01-rf-bridge-geschlossen.jpg"
         alt="Schwarze Sonoff RF Bridge auf einem Karoblock am Fenster, aus dem
              Gehäuse ragen oben ein grüner und ein weißer Draht senkrecht nach
              oben">
  </a>
  <figcaption>Zusammengebaut: zwei Drähte durch zwei gebohrte Löcher im Gehäuse.</figcaption>
</figure>

<figure class="abb klein">
  <a href="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/02-rf-bridge-geoeffnet-drahtantenne.jpg">
    <img src="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/02-rf-bridge-geoeffnet-drahtantenne.jpg"
         alt="Geöffnete RF Bridge: grüne Platine mit leuchtender Anzeige,
              an zwei Ecken sind ein grüner und ein weißer Draht angelötet,
              daneben die kleinen Kupferspiralen der Originalantennen">
  </a>
  <figcaption>Geöffnet: Drähte an den Antennenanschlüssen angelötet.</figcaption>
</figure>

## Warum 17,3 cm

Ein Viertel der Wellenlänge bei 433,92 MHz:

```
λ   = 300 000 km/s / 433,92 MHz ≈ 69,1 cm
λ/4 ≈ 17,3 cm
```

Ein Draht mit λ/4 ist ein einfacher, aber brauchbarer Monopol – deutlich
besser als die aufgewickelte Spirale, die vor allem klein sein soll.

## Ergebnis

Im Test kamen Signale **doppelt so weit** wie mit den Originalantennen.

## Im Einsatz mit Tasmota

Auf der Bridge läuft **Tasmota** statt der Sonoff-Firmware. Damit schalte ich
meine 433-MHz-Geräte per Knopf im Browser – Funksteckdosen gingen genauso, bei
mir sind es Rollläden, Markisen und das Garagentor.

<figure class="abb klein">
  <a href="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/03-tasmota-oberflaeche.png">
    <img src="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/03-tasmota-oberflaeche.png"
         alt="Tasmota-Weboberfläche der Sonoff Bridge auf dem Handy: blaue
              Knöpfe für Markise links und rechts rein und raus, Rolladen
              runter und hoch, Garage sowie freie Knöpfe 8 bis 16, darunter
              Configuration, Information, Firmware Upgrade, Console und
              Restart">
  </a>
  <figcaption>Tasmota auf dem Handy: ein Knopf pro Funkbefehl.</figcaption>
</figure>
