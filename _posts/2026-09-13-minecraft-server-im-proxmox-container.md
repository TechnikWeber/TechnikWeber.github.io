---
layout: beitrag
title: "Minecraft-Server im Container – einer, der sich selbst pflegt"
date: 2026-09-13 19:00:00 +0200
tags: [Elektronik, Linux]
---

Dritter Teil der Reihe um den [Proxmox-Kasten im Keller](/2026/proxmox-ein-alter-rechner-viele-server/):
ein Minecraft-Server für die Familie, als Container neben
[Pi-hole](/2026/pihole-im-proxmox-container/) – im Netzwerkplan dort schon mit
der Adresse `192.168.178.12` eingezeichnet.

Einen Minecraft-Server zum Laufen zu bringen dauert zehn Minuten. Ihn so
aufzusetzen, dass man ihn danach **vergessen kann**, ist die eigentliche
Arbeit. Genau darum geht es hier. Die Schritt-für-Schritt-Anleitung liegt
komplett auf GitHub:
[TechnikWeber/minecraft-server-guide](https://github.com/TechnikWeber/minecraft-server-guide).

## Zwei Wege

| | A – Bedrock | B – Crossplay |
|---|---|---|
| Wer spielt? | Handy, Tablet, Windows | zusätzlich Java am PC |
| Plugins | – | Grundstücksschutz, `/home`, Rollback von Schäden |
| RAM im Container | 2 GB | 8 GB |
{: .messwerte}

Jede Anleitung ist komplett – von der leeren LXC bis zur Fehlersuche:
[A – Bedrock](https://github.com/TechnikWeber/minecraft-server-guide/tree/main/docs/a-bedrock) ·
[B – Crossplay](https://github.com/TechnikWeber/minecraft-server-guide/tree/main/docs/b-crossplay)

## Was eine Standardinstallation nicht kann

Server herunterladen, starten, fertig – so sehen die meisten Anleitungen aus.
Das funktioniert genau bis zum ersten Problem:

| | Standardinstallation | mit der Anleitung |
|---|---|---|
| Neue Minecraft-Version | Die Handys aktualisieren sich, der Server nicht – niemand kommt mehr rein | nachts automatisch, mit Backup und Rollback |
| Absturz | Server bleibt aus, bis sich ein Kind beschwert | Watchdog startet neu, Meldung aufs Handy |
| Backup | keins | täglich, sieben Tage zurück |
| Sicherheitsupdates | wenn man dran denkt | täglich, Neustart-Hinweis per Nachricht |
| Läuft als | oft root | eigener Benutzer ohne Passwort |
| Logs | wachsen endlos | werden rotiert |

Der erste Punkt ist der wichtigste. Bedrock-Clients aktualisieren sich
selbst, und ein veralteter Server lässt sie nicht mehr herein. Ohne
Automatik heißt das: Nach jedem Minecraft-Update steht jemand vor einem
Server, der „veraltet“ meldet.

## Update mit doppeltem Boden

Das Update-Script ist das Herzstück. Es aktualisiert nicht einfach, sondern
geht so vor, dass im schlimmsten Fall der alte Stand wieder läuft:

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 580 290" role="img"
         aria-label="Ablauf des Auto-Updates: Neue Version über die Mojang-API
                     prüfen, herunterladen und prüfen während der Server
                     weiterläuft, Backup und Snapshot vom gestoppten Server,
                     entpacken und starten. Dann die Frage, ob der Server sauber
                     startet. Wenn ja, Meldung Update erfolgreich. Wenn nein,
                     Rollback auf den Snapshot und Meldung, dass die alte
                     Version wieder läuft.">
      <g font-family="system-ui, sans-serif" font-size="12" fill="#555">

        <!-- Reihe 1 -->
        <rect x="20" y="20" width="160" height="50" rx="5" fill="#fff" stroke="#333"/>
        <text x="100" y="42" text-anchor="middle" font-weight="600" fill="#333">Neue Version?</text>
        <text x="100" y="59" text-anchor="middle">Mojang-API, 04:30</text>

        <rect x="210" y="20" width="160" height="50" rx="5" fill="#fff" stroke="#333"/>
        <text x="290" y="42" text-anchor="middle" font-weight="600" fill="#333">Laden und prüfen</text>
        <text x="290" y="59" text-anchor="middle">Server läuft weiter</text>

        <rect x="400" y="20" width="160" height="50" rx="5" fill="#fff" stroke="#333"/>
        <text x="480" y="42" text-anchor="middle" font-weight="600" fill="#333">Backup + Snapshot</text>
        <text x="480" y="59" text-anchor="middle">vom gestoppten Server</text>

        <!-- Reihe 2 -->
        <rect x="400" y="120" width="160" height="50" rx="5" fill="#fff" stroke="#333"/>
        <text x="480" y="150" text-anchor="middle" font-weight="600" fill="#333">Entpacken, starten</text>

        <rect x="210" y="120" width="160" height="50" rx="5" fill="#f6efe2" stroke="#b98a3c"/>
        <text x="290" y="142" text-anchor="middle" font-weight="600" fill="#333">Startet sauber?</text>
        <text x="290" y="159" text-anchor="middle">Log + Port, max. 120 s</text>

        <rect x="20" y="120" width="160" height="50" rx="5" fill="#f0efec" stroke="#8a8a85"/>
        <text x="100" y="142" text-anchor="middle" font-weight="600" fill="#333">Meldung:</text>
        <text x="100" y="159" text-anchor="middle">Update erfolgreich</text>

        <!-- Reihe 3 -->
        <rect x="210" y="220" width="160" height="50" rx="5" fill="#fff" stroke="#b3541e"/>
        <text x="290" y="250" text-anchor="middle" font-weight="600" fill="#b3541e">Rollback auf Snapshot</text>

        <rect x="20" y="220" width="160" height="50" rx="5" fill="#fff" stroke="#b3541e"/>
        <text x="100" y="242" text-anchor="middle" font-weight="600" fill="#b3541e">Meldung:</text>
        <text x="100" y="259" text-anchor="middle" fill="#b3541e">alte Version läuft</text>

        <g stroke="#8a8a85" stroke-width="1.4" fill="none">
          <path d="M180 45H206" marker-end="url(#mcPf)"/>
          <path d="M370 45H396" marker-end="url(#mcPf)"/>
          <path d="M480 70V116" marker-end="url(#mcPf)"/>
          <path d="M400 145H374" marker-end="url(#mcPf)"/>
          <path d="M210 145H184" marker-end="url(#mcPf)"/>
        </g>
        <g stroke="#b3541e" stroke-width="1.4" fill="none">
          <path d="M290 170V216" marker-end="url(#mcPfO)"/>
          <path d="M210 245H184" marker-end="url(#mcPfO)"/>
        </g>
        <text x="195" y="137" text-anchor="middle">ja</text>
        <text x="300" y="198" fill="#b3541e">nein</text>
      </g>
      <defs>
        <marker id="mcPf" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#8a8a85"/>
        </marker>
        <marker id="mcPfO" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#b3541e"/>
        </marker>
      </defs>
    </svg>
  </div>
  <figcaption>Das Bedrock-Update: Erst wenn der neue Server wirklich antwortet, gilt es als geschafft.</figcaption>
</figure>

Drei Details machen den Unterschied:

- **Herunterladen, bevor gestoppt wird.** Ist der Download kaputt, merkt es
  niemand – der Server lief ja die ganze Zeit.
- **„Gestartet“ heißt nicht „läuft“.** Das Script wartet, bis der Server im
  Log seine Bereitschaft meldet *und* der Port offen ist. Ein Prozess, der
  sofort wieder abstürzt, zählt nicht.
- **Der Snapshot entsteht vom gestoppten Server.** Eine Kopie der laufenden
  Welt kann halb geschriebene Dateien enthalten – dann wäre der Rollback
  selbst kaputt.

Beim Crossplay-Weg kommt eine Bremse dazu: Paper ist auf eine Version
**festgenagelt** (26.1.2). Automatisch kommen nur Patch-Builds dieser Version
sowie Geyser und Floodgate. Einen Versionssprung gibt es erst, wenn Geyser
*und* alle Plugins mitziehen – sonst kommen morgens die Bedrock-Spieler nicht
mehr rein. Neu gestartet wird nur, wenn sich eine Datei tatsächlich geändert
hat.

## Überwachung, die nicht nervt

Alle fünf Minuten prüft ein Watchdog, ob der Server antwortet. Wenn nicht,
startet er ihn neu. Die Kunst liegt darin, **wann er schweigt**:

- **Nur bei Zustandswechseln.** Eine Meldung, wenn der Server ausfällt, eine,
  wenn er wieder da ist – nicht alle fünf Minuten dieselbe.
- **Nicht während der Wartung.** Backup und Update setzen ein Wartungs-Flag,
  sonst würde der Watchdog den absichtlich gestoppten Server mitten im Backup
  „retten“.
- **Geduld beim Neustart.** Paper braucht mit allen Plugins oft deutlich
  länger als eine halbe Minute. Der Watchdog wartet aufs Log statt auf die Uhr
  und schlägt keinen falschen Alarm.

Gemeldet wird über [ntfy](https://ntfy.sh) direkt aufs Handy. Jede Nachricht
sagt, was passiert ist und was zu tun ist – im Normalfall: nichts. So sieht die
seltene schlechte Nachricht aus:

```
Bedrock: Update fehlgeschlagen (Rollback)
Version 1.26.50.1 startete nicht. Alte Version 1.26.45.1 wurde
wiederhergestellt und laeuft wieder.
```

## Einstellungen für einen Kinderserver

Ein offener Survival-Server ist für kleine Kinder das Falsche: Ein falscher
Klick, und das Haus des Bruders ist weg. Das Kinderserver-Profil setzt auf
**kontrolliertes Bauen**:

- `gamemode=adventure` als Standard – jeder kann herumlaufen, Türen öffnen
  und Kisten benutzen, aber nichts abbauen.
- Wer bauen darf, wird einzeln freigeschaltet: `/gamemode creative Name`.
- `force-gamemode=false` – ohne diese Zeile wäre die Freischaltung beim
  nächsten Login wieder weg. Das ist der Fehler, über den die meisten
  stolpern.
- `difficulty=peaceful` und ein paar Gamerules: immer Tag, kein Feuerschaden,
  TNT explodiert nicht.

Beim Crossplay-Weg kommen Plugins dazu: **GriefPrevention** – jedes Kind
schützt sein Grundstück mit einer goldenen Schaufel – und **CoreProtect**, das
jeden Block protokolliert. Geht doch etwas kaputt, macht
`/co rollback u:Name t:1h r:20` genau diesen Schaden rückgängig, ohne den Rest
der Welt zurückzusetzen. Eine kindgerechte
[Spieler-Anleitung](https://github.com/TechnikWeber/minecraft-server-guide/blob/main/docs/b-crossplay/spieler-anleitung.md)
zum Weitergeben liegt bei, auch als Discord-Version.

## Was Proxmox beisteuert

Die Anleitung setzt auf den Container aus dem
[Proxmox-Beitrag](/2026/proxmox-ein-alter-rechner-viele-server/) und nutzt
dessen Stärken:

- **Start at boot** und **feste IP** – nach einem Stromausfall ist der Server
  von allein wieder da, und die Portweiterleitung im Router zeigt immer auf
  `192.168.178.12`.
- **Zwei Sicherheitsleinen.** Das Backup-Script sichert die *Welt* – schnell
  zurückgespielt, wenn nur sie kaputt ist. Das Proxmox-Backup sichert den
  *ganzen Container* – für den Fall, dass die Platte stirbt.
- **Snapshot vor großen Schritten.** Vor einem Paper-Versionssprung einmal
  `pct snapshot <CTID> vor-update` auf dem Host – die Weltumwandlung ist
  unumkehrbar, der Snapshot nicht.

Die Anleitung ist bewusst ausführlich. Der Aufwand steckt einmal am Anfang –
danach meldet sich der Server nur noch, wenn er etwas zu sagen hat.

Anleitung und Scripts:
[github.com/TechnikWeber/minecraft-server-guide](https://github.com/TechnikWeber/minecraft-server-guide)
