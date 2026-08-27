---
layout: post
title: "TITEL HIER EINTRAGEN"
date: 2026-08-27 09:00:00 +0200
tags: [Elektronik]
# categories: [anleitungen]
---

Hier den Beitrag schreiben.

<!--
  ANLEITUNG – dieser Kommentar taucht auf der fertigen Seite nicht auf
  und kann im echten Beitrag einfach stehen bleiben oder gelöscht werden.

  WICHTIG: Das Datum oben muss in der VERGANGENHEIT liegen, sonst baut
  Jekyll den Beitrag nicht mit. Dateiname immer JJJJ-MM-TT-titel.md

  Kompletter Veröffentlichungs-Ablauf: siehe _drafts/ANLEITUNG.md


  ── TAGS ──────────────────────────────────────────────────────────

  Tags sind die Themen-Schubladen. Jeder Beitrag kann in mehreren
  gleichzeitig liegen – anders als bei echten Ordnern. Alle Tags samt
  ihrer Beiträge erscheinen automatisch auf der Seite /themen/.

      tags: [Amateurfunk]
      tags: [Amateurfunk, Antennenbau]
      tags: [Elektronik, "Raspberry Pi"]     <- mehrere Wörter in "..."

  Bewährte Tags (bitte genau so weiterverwenden):

      Amateurfunk · Antennenbau · Elektronik · Embedded · Löten
      Messtechnik · PCB-Design · Python · C# · Werkstatt · Alltag

  WICHTIG – Groß-/Kleinschreibung zählt: "Amateurfunk" und "amateurfunk"
  landen in zwei getrennten Schubladen. Der Tag erscheint auf /themen/
  exakt so, wie er hier geschrieben steht. Also lieber einmal oben in
  der Liste nachsehen als neu tippen.

  Zwei bis vier Tags pro Beitrag sind ein guter Schnitt. Ein Tag, den
  nur ein einziger Beitrag benutzt, bringt niemandem etwas.


  ── CATEGORIES ────────────────────────────────────────────────────

  Braucht man hier eigentlich nicht – die Zeile ist deshalb oben
  auskommentiert. Kategorien sind für die grobe Einteilung gedacht
  (Anleitung / Projekt / Notiz), Tags für die Themen. Wenn Tags reichen,
  einfach nur Tags benutzen.


  ── BILDER: WOHIN UND WIE BENENNEN ────────────────────────────────

  REGEL: Pro Beitrag ein eigener Ordner unter assets/, benannt exakt
  wie die Beitragsdatei (ohne .md).

      _posts/2026-09-14-antenne-fuer-2m.md      <- der Beitrag
      assets/2026-09-14-antenne-fuer-2m/        <- seine Bilder
          01-material.jpg
          02-aufbau-strahler.jpg
          03-swr-messung.jpg
          04-fertig-am-mast.jpg

  Warum Ordner und nicht alles in assets/ mit langen Namen: nach
  dreißig Beiträgen liegen sonst dreihundert Dateien nebeneinander.
  So gehört zu jedem Beitrag genau ein Ordner – Beitrag gelöscht,
  Ordner gelöscht, fertig, nichts bleibt übrig.

  Zur Frage vorne oder hinten anhängen: bei einem Ordner erübrigt sich
  das. Innerhalb des Ordners kommt die NUMMER nach VORNE (01-, 02-, ...),
  dann stehen die Bilder im Dateimanager schon in der Reihenfolge, in
  der sie im Beitrag vorkommen.

  Für Dateinamen gilt:
    - klein schreiben, keine Leerzeichen, keine Umlaute
      also 02-loetstation.jpg statt "02 Lötstation.JPG"
    - sagen, was drauf ist: 03-swr-messung.jpg statt 03-img4711.jpg
      (der Name hilft später beim Wiederfinden – und mir, wenn ich
       aus deinen Bildern einen Beitrag zusammenbauen soll)

  Bilder, die zu keinem einzelnen Beitrag gehören (Logo, Profilbild),
  kommen nach assets/allgemein/.


  ── BILDER EINBINDEN ──────────────────────────────────────────────

  Pfad beginnt immer mit einem Schrägstrich:

      ![Fertige Antenne am Mast](/assets/2026-09-14-antenne-fuer-2m/04-fertig-am-mast.jpg)

  Der Text in den eckigen Klammern ist der Alternativtext. Den bitte
  immer ausfüllen: Screenreader lesen ihn vor, und er erscheint, falls
  das Bild nicht lädt.

  Nicht vergessen, die Bilder mit einzuchecken – am einfachsten der
  ganze Ordner auf einmal:

      git add assets/2026-09-14-antenne-fuer-2m/


  ── BILD MIT BILDUNTERSCHRIFT ─────────────────────────────────────

      <figure>
        <img src="/assets/2026-09-14-antenne-fuer-2m/03-swr-messung.jpg"
             alt="SWR-Messung am Antennenanalysator">
        <figcaption>SWR bei 145,5 MHz – nah genug an 1:1.</figcaption>
      </figure>


  ── BILD ALS LINK / KLEINER DARGESTELLT ───────────────────────────

  Klick öffnet das Bild in voller Größe:

      [![Beschreibung](/assets/BEITRAG/02-aufbau.jpg)](/assets/BEITRAG/02-aufbau.jpg)

  Feste Breite in Pixeln:

      <img src="/assets/BEITRAG/02-aufbau.jpg" alt="Beschreibung" width="400">


  ── GRÖSSE UND FORMAT ─────────────────────────────────────────────

  Fotos direkt aus der Kamera sind für eine Website viel zu groß.
  Vor dem Ablegen auf etwa 1600 Pixel Breite verkleinern, Ziel sind
  ungefähr 300 KB pro Bild.

      Fotos              -> .jpg
      Screenshots,       -> .png
      Zeichnungen, Logos

  Wichtig: Was einmal committet ist, bleibt für immer in der
  Repo-Historie – auch nach dem Löschen. Also lieber vorher
  verkleinern als nachher ärgern.

  Verkleinern auf der Kommandozeile (ImageMagick):

      magick original.jpg -resize 1600x -quality 82 01-aufbau.jpg


  ── PDF ODER ANDERE DATEI ZUM DOWNLOAD ────────────────────────────

      [Schaltplan als PDF](/assets/BEITRAG/schaltplan.pdf)


  ── VIDEO ─────────────────────────────────────────────────────────

  Achtung: große Dateien blähen das Repo dauerhaft auf.
  Ab ca. 20 MB besser bei YouTube o. ä. hochladen und verlinken.

      <video controls width="600">
        <source src="/assets/BEITRAG/aufbau.mp4" type="video/mp4">
      </video>


  ── WENN ICH (CLAUDE) DEN BEITRAG SCHREIBEN SOLL ──────────────────

  Am besten so vorbereiten:

    1. Ordner assets/JJJJ-MM-TT-thema/ anlegen
    2. Bilder in der gewünschten Reihenfolge hineinlegen (01-, 02-, ...)
       mit sprechenden Namen
    3. Stichpunkte dazuschreiben – entweder im Chat oder als
       notizen.txt in denselben Ordner

  Aus Reihenfolge, Namen und Stichpunkten baue ich den Beitrag und
  setze die Bilder an die passenden Stellen. Die notizen.txt lösche
  ich am Ende wieder.

-->

## Zwischenüberschrift

Text mit **fett**, *kursiv* und [einem Link](https://example.com).

Codeblöcke mit Syntax-Highlighting:

```python
print("Hallo Welt")
```
