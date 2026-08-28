# Philipps Blog – technikweber.github.io

Jekyll-Blog mit Theme `minima`, gehostet auf GitHub Pages.
Repo: https://github.com/TechnikWeber/TechnikWeber.github.io

Sprache im Blog und in der Kommunikation: **Deutsch**.
Philipp ist Funkamateur, Rufzeichen **DL4PW**.

## Schreibstil

**Kurz und auf den Punkt, nicht ausschweifend.** Gilt für Beiträge,
Anleitungen und Erklärungen gleichermaßen – Einleitung, Fließtext,
Bildunterschriften und Erläuterungen unter Tabellen. Nichts wiederholen, was
Bild oder Tabelle schon zeigt. Ausdrücklich so gewünscht.

## Commits

**Niemals `Co-Authored-By: Claude` an Commits anhängen.** Philipp möchte
ausschließlich sich selbst als Autor sehen. Ausdrücklich so gewünscht.

**Fertige Beiträge sofort committen und pushen – keine Rückfrage.** Philipp
kontrolliert nicht vorab, er liest den Beitrag auf der Live-Seite und sagt
hinterher Bescheid. Ausdrücklich so gewünscht.

## Auslöser: "Dateien liegen in Eingang, mache den Beitrag"

Heißt: in `_eingang/` liegen Fotos und eine `notizen.txt`. Daraus einen
fertigen Beitrag bauen. Ablauf:

1. `_eingang/notizen.txt` und die Bilder ansehen (Bildnamen mit `01-`,
   `02-` … geben die Reihenfolge im Beitrag vor)
2. Titel und Slug selbst aus dem Inhalt ableiten – Philipp erwartet
   ausdrücklich einen eigenen, ansprechenden Vorschlag, keine Rückfrage
3. Beitrag anlegen: `_posts/JJJJ-MM-TT-slug.md`
   - `layout: beitrag` (nicht `post`) – das ist minimas Beitragslayout
     plus der Tag-Zeile am Ende, die auf /themen/ zurückverlinkt
   - Datum **muss in der Vergangenheit liegen**, sonst baut Jekyll ihn
     stillschweigend nicht mit (häufigste Fehlerquelle)
   - `tags:` setzen – Liste bewährter Tags steht in `_drafts/vorlage.md`,
     Groß-/Kleinschreibung zählt
4. Bilder aufbereiten nach `assets/JJJJ-MM-TT-slug/`:
   - verkleinern: `magick original.jpg -resize 1600x -quality 82 01-name.jpg`
   - sprechende Namen, `01-`, `02-` … voranstellen
   - Alternativtexte im Beitrag immer ausfüllen
5. Beitrag committen und pushen (ohne Rückfrage, siehe oben). Nicht auf den
   GitHub-Pages-Build warten – der läuft nach jedem Push automatisch
6. **`_eingang/` leeren** (README.md dort behalten) – dort soll immer nur
   der Beitrag liegen, an dem gerade gearbeitet wird

## Ordner

```
_posts/       veröffentlichte Beiträge (JJJJ-MM-TT-titel.md)
_layouts/     beitrag.html – Beitragslayout inkl. Tag-Zeile
_drafts/      ANLEITUNG.md (Philipps Nachschlagewerk) + vorlage.md
_eingang/     Arbeitsordner, per .gitignore NICHT in Git (Originalfotos)
assets/       ein Unterordner je Beitrag, benannt wie die Beitragsdatei
              assets/allgemein/ für Bilder ohne Beitragsbezug
themen.md     Tag-Übersicht, füllt sich automatisch aus site.tags
```

## Kontext

Philipp lernt Git gerade erst. Begriffe wie commit/push kurz einordnen
statt sie vorauszusetzen, und Befehle zum Kopieren mitgeben.
Ausführliche Erklärungen für ihn stehen in `_drafts/ANLEITUNG.md`.

Ruby/Jekyll sind lokal **nicht** installiert – Änderungen lassen sich nur
nach dem Push an der Live-Seite prüfen. ImageMagick (`magick`) ist da.
