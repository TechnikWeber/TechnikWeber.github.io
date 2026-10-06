---
layout: beitrag
title: "Genstrio – Generatoren für den 3D-Druck im Browser"
date: 2026-10-06 22:00:00 +0200
tags: [Allgemeines]
---

Für ein Gehäuse, einen Schlauchadapter oder einen Schubladeneinsatz jedes Mal
das CAD-Programm öffnen? **Genstrio** nimmt ein paar Maße entgegen, baut das
Modell sichtbar in 3D auf und gibt es als STL, 3MF oder STEP heraus – direkt im
Browser, auf Deutsch und Englisch.

<figure class="abb klein">
  <a href="/assets/2026-10-06-genstrio-generatoren-fuer-den-3d-druck/01-gehaeuse-mit-deckeltext.jpg">
    <img src="/assets/2026-10-06-genstrio-generatoren-fuer-den-3d-druck/01-gehaeuse-mit-deckeltext.jpg"
         alt="Genstrio im Browser: links die Maße, rechts ein Elektronikgehäuse
              mit dem vertieften Schriftzug „Genstrio“ auf dem Deckel">
  </a>
  <figcaption>Elektronikgehäuse mit Text auf dem Deckel.</figcaption>
</figure>

## Sechs Generatoren

- **Elektronikgehäuse:** eckig, rund oder vieleckig, mit Vorlagen für
  Raspberry Pi, Arduino und ESP32, Öffnungen für Stecker, Lüftung,
  verschraubtem, geklipstem oder klappbarem Deckel und Hutschienen-Clip
- **Rohradapter:** Reduzierstücke und Bögen zwischen Rohren, Schläuchen und
  G-Gewinden
- **Schubladen-Organizer:** Boxen, die eine Schublade lückenlos füllen –
  gleich groß oder zufällig gemischt, bis die Aufteilung gefällt
- **Gridfinity:** Behälter, Halter für Bits und Batterien sowie Grundplatten
- **Haken & Halter:** Wandhaken, Schlüsselleisten, Regalwinkel – zum
  Schrauben, Kleben, für Tür oder Lochwand
- **Text & Schilder:** Schilder, Anhänger, Stempel und Schablonen in neun
  freien Schriften

<figure class="abb klein">
  <a href="/assets/2026-10-06-genstrio-generatoren-fuer-den-3d-druck/02-gridfinity-grundplatten.jpg">
    <img src="/assets/2026-10-06-genstrio-generatoren-fuer-den-3d-druck/02-gridfinity-grundplatten.jpg"
         alt="Gridfinity-Grundplatte mit 9 × 6 Feldern, die eine Schublade von
              400 × 260 mm füllt und in sechs Platten geteilt ist">
  </a>
  <figcaption>Schubladenmaß eingeben, Platten fürs Druckbett bekommen.</figcaption>
</figure>

## Was es besonders macht

Die Geometrie rechnet ein echter CAD-Kern (OpenCascade als WebAssembly) auf
dem eigenen Rechner. Deshalb gibt es neben STL auch STEP zum Weiterbearbeiten,
und nichts wird hochgeladen – kein Konto, kein Server.

Zu jedem Modell sagt Genstrio dazu, was man zum Bauen braucht: welche
Schrauben, wie oft welches Teil zu drucken ist, wie es auf dem Druckbett liegt.
Maße gehen in Millimetern, Zentimetern oder Zoll, und fertige Einstellungen
lassen sich als Vorlage speichern oder per Link teilen.

<figure class="abb klein">
  <a href="/assets/2026-10-06-genstrio-generatoren-fuer-den-3d-druck/03-schluesselleiste.jpg">
    <img src="/assets/2026-10-06-genstrio-generatoren-fuer-den-3d-druck/03-schluesselleiste.jpg"
         alt="Schlüsselleiste mit fünf Haken und zwei Schraubenlöchern in der
              3D-Vorschau">
  </a>
  <figcaption>Schlüsselleiste aus dem Haken-Generator.</figcaption>
</figure>

Ausprobieren:
[technikweber.github.io/Genstrio](https://technikweber.github.io/Genstrio/) ·
Code: [github.com/TechnikWeber/Genstrio](https://github.com/TechnikWeber/Genstrio)
