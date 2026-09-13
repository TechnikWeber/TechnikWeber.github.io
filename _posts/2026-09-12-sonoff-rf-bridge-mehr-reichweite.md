---
layout: beitrag
title: "Sonoff RF Bridge: 17,3 cm Draht, viermal Reichweite"
date: 2026-09-12 21:00:00 +0200
tags: [Elektronik]
---

Die Sonoff RF Bridge setzt 433-MHz-Funksignale ins WLAN um – mit ihren
winzigen Spiralantennen aber nur über kurze Strecken. Also runter damit und
durch zwei gestreckte Drähte ersetzt.

> **Nur ein Experiment.** Mit geänderter Antenne erlischt die Zulassung als
> Funkgerät (SRD), legal betreiben lässt sich die Bridge so nicht. Auch das
> Amateurfunkrufzeichen hilft nicht – Steckdosen schalten ist kein
> Amateurfunk. Der Umbau lief nur zu Testzwecken.

<figure class="abb">
  <a href="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/01-rf-bridge-geschlossen.jpg">
    <img src="/assets/2026-09-12-sonoff-rf-bridge-mehr-reichweite/01-rf-bridge-geschlossen.jpg"
         alt="Schwarze Sonoff RF Bridge auf einem Karoblock am Fenster, aus dem
              Gehäuse ragen oben ein grüner und ein weißer Draht senkrecht nach
              oben">
  </a>
  <figcaption>Zusammengebaut: zwei Drähte statt interner Antennen.</figcaption>
</figure>

<figure class="abb">
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

Im Test kamen Signale **fast viermal so weit** wie mit den Originalantennen.
