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


  ── BILDER EINBINDEN ──────────────────────────────────────────────

  1. Bild nach assets/ kopieren, z. B. assets/loetstation.jpg
     (Dateinamen klein, ohne Leerzeichen und ohne Umlaute halten –
     also loetstation.jpg statt "Lötstation Bild.JPG")
  2. Im Text so einbinden – der Pfad beginnt mit einem Schrägstrich:

         ![Kurze Bildbeschreibung](/assets/loetstation.jpg)

     Der Text in den eckigen Klammern ist der Alternativtext. Den bitte
     immer ausfüllen: Screenreader lesen ihn vor, und er erscheint, falls
     das Bild nicht lädt.

  3. Nicht vergessen, das Bild mit einzuchecken:

         git add assets/loetstation.jpg


  ── BILD MIT BILDUNTERSCHRIFT ─────────────────────────────────────

      <figure>
        <img src="/assets/loetstation.jpg" alt="Kurze Bildbeschreibung">
        <figcaption>Die Unterschrift unter dem Bild.</figcaption>
      </figure>


  ── BILD ALS LINK / KLEINER DARGESTELLT ───────────────────────────

      [![Beschreibung](/assets/loetstation.jpg)](/assets/loetstation.jpg)

      <img src="/assets/loetstation.jpg" alt="Beschreibung" width="400">


  ── PDF ODER ANDERE DATEI ZUM DOWNLOAD ────────────────────────────

      [Schaltplan als PDF](/assets/schaltplan.pdf)


  ── VIDEO ─────────────────────────────────────────────────────────

  Eigenes Video (Achtung: große Dateien blähen das Repo auf,
  ab ca. 20 MB besser bei YouTube o. ä. hochladen):

      <video controls width="600">
        <source src="/assets/aufbau.mp4" type="video/mp4">
      </video>


  ── UNTERORDNER ───────────────────────────────────────────────────

  Bei vielen Medien lohnen sich Unterordner, der Pfad wächst dann mit:

      assets/2026-08-loetstation/bild1.jpg
      →  ![Beschreibung](/assets/2026-08-loetstation/bild1.jpg)
-->

## Zwischenüberschrift

Text mit **fett**, *kursiv* und [einem Link](https://example.com).

Codeblöcke mit Syntax-Highlighting:

```python
print("Hallo Welt")
```
