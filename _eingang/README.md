# Arbeitsordner für den nächsten Beitrag

Hier kommt alles rein, woraus ein Beitrag werden soll. Was in diesem Ordner
liegt, ist **nur lokal** – er ist in `.gitignore` eingetragen und wird nicht
zu GitHub hochgeladen. Nur diese README ist eine Ausnahme.

## So läuft es

1. Fotos hier ablegen. Namen egal, Größe egal – Originale aus der Kamera
   sind genau richtig.
2. In welcher Reihenfolge sie im Beitrag vorkommen sollen: einfach
   `01-`, `02-`, ... voranstellen. Wenn die Reihenfolge egal ist, weglassen.
3. `notizen.txt` danebenlegen (Vorlage unten).
4. Claude Bescheid geben: *"Im Eingang liegt was, mach einen Beitrag draus."*

## Was dann passiert

- Titel und Dateiname werden aus den Notizen abgeleitet
- Beitrag entsteht unter `_posts/JJJJ-MM-TT-titel.md`
- Bilder werden auf ca. 1600 px verkleinert, umbenannt und nach
  `assets/JJJJ-MM-TT-titel/` einsortiert
- Tags werden gesetzt, der Beitrag landet damit auch unter /themen/
- committen und pushen erst nach Rückfrage
- **danach wird dieser Ordner geleert** – es liegt also immer nur der
  Beitrag darin, an dem gerade gearbeitet wird

## notizen.txt – Vorlage

Alles darf formlos sein, Stichpunkte reichen völlig.

    Worum geht es?
      -

    Was ist passiert / was habe ich gebaut?
      -
      -

    Was war das Ergebnis, was habe ich gelernt?
      -

    Zu den Bildern:
      01 -
      02 -

    Tags (falls schon klar):

    Sonstiges (Links, Bauteile, Messwerte):
