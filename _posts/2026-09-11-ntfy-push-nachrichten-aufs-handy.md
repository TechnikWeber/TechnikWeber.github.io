---
layout: beitrag
title: "ntfy – Push-Nachrichten vom Server aufs Handy"
date: 2026-09-11 18:00:00 +0200
tags: [Elektronik, Linux]
---

Ein Backup ist schiefgegangen, ein Dienst abgestürzt, die Festplatte fast
voll – und niemand merkt es. **ntfy** (gesprochen „notify") schickt so etwas
direkt aufs Handy. Eine Zeile im Script genügt.

## Warum ntfy

- **Kein Konto, keine Anmeldung.** App installieren, Thema abonnieren, fertig.
- **Ein einziger `curl`-Befehl** zum Senden – funktioniert aus jedem Script,
  jedem Cronjob, von jedem Gerät im Netz.
- **Kostenlos und Open Source.** Der öffentliche Server `ntfy.sh` reicht für
  zu Hause; wer will, betreibt einen eigenen.
- **Kein Umweg** über E-Mail-Server oder Telegram-Bots.

## Einrichten

**1. App installieren** – ntfy gibt es für Android (Google Play, F-Droid) und
iOS, alternativ im Browser unter [ntfy.sh/app](https://ntfy.sh/app).

**2. Thema ausdenken und abonnieren.** Das Thema (*Topic*) ist nichts weiter
als ein Name. In der App auf **+** tippen und ihn eintragen, z.B.
`mein-server-x7k2q9`.

**3. Nachricht schicken:**

```bash
curl -d "Backup fertig" ntfy.sh/mein-server-x7k2q9
```

Sekunden später klingelt das Handy. Mit Titel, Priorität und Emoji:

```bash
curl -H "Title: Backup fehlgeschlagen" \
     -H "Priority: high" \
     -H "Tags: warning" \
     -d "Bitte /var/log/backup.log prüfen" \
     ntfy.sh/mein-server-x7k2q9
```

Prioritäten gehen von `min` bis `urgent` – `urgent` klingelt auch dann
eindringlich, wenn das Handy stumm ist.

## Wichtig: Der Name ist das Passwort

Auf `ntfy.sh` kann **jeder** ein Thema lesen und hineinschreiben, der den Namen
kennt. Also nie `backup` oder `minecraft` nehmen, sondern einen zufälligen
Anhang wie oben. Keine Passwörter oder persönlichen Daten verschicken.

Mehr Schutz bietet ein **eigener ntfy-Server** mit Benutzern und
Access-Tokens – er passt als kleiner Container auf den
[Proxmox-Kasten](/2026/proxmox-ein-alter-rechner-viele-server/).

## Im Einsatz

Der [Minecraft-Server](/2026/minecraft-server-im-proxmox-container/) meldet
über ntfy Updates, Abstürze und fehlgeschlagene Backups – und schweigt, solange
alles läuft.

Doku: [docs.ntfy.sh](https://docs.ntfy.sh)
