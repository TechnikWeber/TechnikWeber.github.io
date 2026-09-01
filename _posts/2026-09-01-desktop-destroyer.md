---
layout: beitrag
title: "Desktop Destroyer – welches Kind aus den 90ern kennt das noch?"
date: 2026-09-01 11:00:00 +0200
tags: [Allgemeines]
---

Hammer, Kettensäge und Flammenwerfer auf dem eigenen Desktop – der Zeitvertreib
der 90er. Den gibt es jetzt für Linux.

<figure class="abb klein">
  <a href="/assets/2026-09-01-desktop-destroyer/01-desktop-destroyer.png">
    <img src="/assets/2026-09-01-desktop-destroyer/01-desktop-destroyer.png"
         alt="Zerlegter Linux-Desktop: Einschusslöcher und Brandspuren in einem
              Tabellenfenster, Termitengänge, ein Farbklecks und ein Kratzer
              quer über den Hintergrund, dazu der Werkzeugkasten mit neun
              Waffen von Hammer bis Waschpistole">
  </a>
  <figcaption>Neun Werkzeuge, ein Nachmittag Schadenfreude.</figcaption>
</figure>

Beim Start wird ein Standbild des Desktops aufgenommen und als Vollbild wieder
angezeigt – zerlegt wird also nur das Foto. `R` repariert alles, `Esc` beendet.
Läuft unter X11 und Wayland.

```bash
git clone https://github.com/TechnikWeber/linux-desktop-destroyer.git
cd linux-desktop-destroyer
./install.sh
```

Code und Anleitung:
[github.com/TechnikWeber/linux-desktop-destroyer](https://github.com/TechnikWeber/linux-desktop-destroyer)
