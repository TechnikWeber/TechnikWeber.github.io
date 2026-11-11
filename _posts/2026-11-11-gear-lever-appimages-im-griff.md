---
layout: beitrag
title: "Gear Lever – AppImages endlich ordentlich im System"
date: 2026-11-11 20:00:00 +0100
tags: [Allgemeines, Linux]
---

AppImages sind praktisch: eine Datei herunterladen, ausführbar machen, starten
– ohne Installation, auf fast jeder Distribution. Der Haken: Sie liegen dann
irgendwo in `Downloads`, tauchen nicht im Startmenü auf und aktualisieren sich
nicht. **Gear Lever** löst genau das.

## Was Gear Lever macht

- **Ins Startmenü mit einem Klick.** AppImage per Drag & Drop ins Fenster
  ziehen, auf *Integrieren* klicken – Gear Lever legt Starter und Icon an, die
  App erscheint im Menü wie jede andere.
- **Ordnung statt Download-Chaos.** Integrierte AppImages landen in einem
  festen Ordner statt verstreut auf der Platte.
- **Updates.** Gear Lever sucht nach neuen Versionen und ersetzt die alte –
  oder behält sie auf Wunsch daneben, falls die neue zickt.
- **Sauber entfernen.** Beim Löschen verschwinden AppImage, Starter und Icons
  zusammen in den Papierkorb.
- **Kommandozeile.** Wer lieber tippt, bekommt alles auch als Befehl, z.B.
  `--list-updates` für anstehende Updates.

## Installieren

Gear Lever gibt es als Flatpak auf
[Flathub](https://flathub.org/apps/it.mijorus.gearlever) – unter KDE also
einfach in Discover suchen, oder im Terminal:

```bash
flatpak install flathub it.mijorus.gearlever
```

Danach öffnet ein Doppelklick auf eine AppImage-Datei direkt Gear Lever.

## Warum ich das gut finde

AppImages sind die einfachste Art, ein Programm unabhängig von der
Distribution weiterzugeben – gerade für kleine Projekte ohne Paketbetreuer.
Gear Lever schließt die Lücke zum „richtigen“ Installieren, ohne die
Einfachheit kaputtzumachen. Kostenlos, Open Source (GPL-3.0), entwickelt von
Lorenzo Paderi. Verdient mehr Aufmerksamkeit.

Projekt: [github.com/mijorus/gearlever](https://github.com/mijorus/gearlever)
