---
title: "Anleitung: Wie ich einen Beitrag veröffentliche"
---

Interne Notiz für mich selbst. Liegt in `_drafts/`, wird also **nie**
veröffentlicht – Jekyll baut Entwürfe nur mit `--drafts`.

## Die wichtigsten Begriffe

| Befehl       | Bedeutung                                                    |
|--------------|--------------------------------------------------------------|
| `git pull`   | Änderungen von GitHub **holen**                              |
| `git add`    | Datei für den nächsten Commit **vormerken**                  |
| `git commit` | Lokal **speichern** – GitHub sieht davon noch nichts         |
| `git push`   | Commits zu GitHub **hochladen** → Seite geht live            |

Merksatz: **committen ist speichern, pushen ist veröffentlichen.**

## Neuer Beitrag – der komplette Ablauf

```bash
cd ~/TechnikWeber.github.io

# 1. Aktuellen Stand holen (wichtig, falls online etwas geändert wurde)
git pull

# 2. Beitrag anlegen – Vorlage kopieren und umbenennen
cp _drafts/vorlage.md _posts/2026-08-27-mein-thema.md

# 3. Datei bearbeiten: Titel, Datum, Text
#    (Dateiname MUSS dem Muster JJJJ-MM-TT-titel.md folgen)

# 4. Vormerken, speichern, hochladen
git add _posts/2026-08-27-mein-thema.md
git commit -m "Neuer Beitrag: Mein Thema"
git push
```

Nach dem Push baut GitHub Pages automatisch neu – nach ein bis zwei Minuten
ist der Beitrag online unter `https://technikweber.github.io/2026/mein-thema/`.

Kurzform, wenn alles geändert werden soll, was gerade offen ist:

```bash
git add -A && git commit -m "Beschreibung" && git push
```

## Beitrag ändern

Datei bearbeiten, dann derselbe Dreisatz:

```bash
git add _posts/2026-08-27-mein-thema.md
git commit -m "Beitrag überarbeitet: Mein Thema"
git push
```

## Beitrag löschen

```bash
git rm _posts/2026-08-27-mein-thema.md
git commit -m "Beitrag entfernt: Mein Thema"
git push
```

## Zwischendurch nachsehen

```bash
git status          # Was ist geändert / vorgemerkt?
git diff            # Was genau habe ich geändert?
git log --oneline   # Welche Commits gibt es?
```

## Wenn der Beitrag nach dem Push nicht auftaucht

In dieser Reihenfolge prüfen:

1. **Datum in der Zukunft?** Das ist mit Abstand der häufigste Grund.
   Jekyll überspringt zukünftig datierte Beiträge stillschweigend – der Build
   meldet trotzdem „erfolgreich", die Seite ist aber nicht da.
   `date:` muss vor dem jetzigen Zeitpunkt liegen.
2. **Dateiname falsch?** Muster `JJJJ-MM-TT-titel.md`, nichts anderes wird
   als Beitrag erkannt.
3. **Liegt die Datei in `_posts/`** und nicht versehentlich in `_drafts/`?
4. **Wirklich gepusht?** `git status` zeigt sonst „Ihr Branch ist X Commits
   voraus".
5. **Build-Fehler?** Sichtbar unter
   <https://github.com/TechnikWeber/TechnikWeber.github.io/actions>
   oder per `gh api repos/TechnikWeber/TechnikWeber.github.io/pages/builds/latest`.

## Was wo liegt

```
_posts/       veröffentlichte Beiträge (JJJJ-MM-TT-titel.md)
_drafts/      Entwürfe + diese Anleitung – wird NICHT veröffentlicht
assets/       Bilder, PDFs und andere Medien
_includes/    Bausteine des Themes, z. B. footer.html
_config.yml   Grundeinstellungen der Seite
```
