---
layout: beitrag
title: "Ein Bibelvers auf dem Schreibtisch"
date: 2026-09-01 12:00:00 +0200
tags: [Glaube, Linux]
---

Jeden Tag ein Vers, direkt auf dem Desktop – ohne Fenster, ohne Konto, ohne
Internet. Als Plasmoid für **KDE Plasma 6** und als Desklet für **Cinnamon**.

<figure class="abb klein">
  <a href="/assets/2026-09-01-bibelvers-widget/01-bibelvers-plasmoid.png">
    <img src="/assets/2026-09-01-bibelvers-widget/01-bibelvers-plasmoid.png"
         alt="Das Widget auf dem Desktop: Hosea 6,3 in großer Schrift auf
              hellem Grund, darunter klein die Stellenangabe">
  </a>
  <figcaption>Vers des Tages, darunter die Stelle. Ein Klick kopiert
  beides.</figcaption>
</figure>

Zur Wahl stehen eine kuratierte Liste oder die **Herrnhuter Losungen**, dazu
Deutsch, Englisch oder Spanisch. Schrift, Farbe, Ausrichtung und Hintergrund
lassen sich einstellen.

Welcher Vers kommt, ergibt allein das lokale Datum: Die Liste wird pro Jahr
deterministisch gemischt und der Reihe nach durchlaufen. Kein Server, kein
gespeicherter Zustand – und auf jedem Gerät am selben Tag derselbe Vers.

```sh
make install-plasmoid   # KDE Plasma
make install-desklet    # Cinnamon
```

Code und Anleitung:
[github.com/TechnikWeber/bible-verse-widget](https://github.com/TechnikWeber/bible-verse-widget)
