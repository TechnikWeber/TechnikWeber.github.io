---
layout: beitrag
title: "MobTag: Lebensanzeige über Mobs, nur wenn man kämpft"
date: 2026-11-17 14:00:00 +0100
tags: [Allgemeines]
---

Auf unserem
[Minecraft-Server]({% post_url 2026-09-13-minecraft-server-im-proxmox-container %})
fehlte eine Anzeige, wie viel Leben ein Mob noch hat. Das Plugin
[MobTag](https://github.com/Abood8001/MobTag) von Abood8001 kann das und ist
Open Source (MIT). Ich habe es geforkt, also eine eigene Kopie angelegt, und um
ein paar Einstellungen pro Spieler erweitert:
[TechnikWeber/MobTag](https://github.com/TechnikWeber/MobTag).

<figure class="abb klein">
  <a href="/assets/2026-11-17-mobtag-lebensanzeige-ueber-mobs/01-anzeige.png">
    <img src="/assets/2026-11-17-mobtag-lebensanzeige-ueber-mobs/01-anzeige.png"
         alt="Lama auf einer Weide, darüber ein halbtransparentes Herz mit 25/25">
  </a>
  <figcaption>Klassische Anzeige über einem Lama.</figcaption>
</figure>

## Was der Fork dazubringt

- **Design pro Spieler:** Klassisch (❤ 14/20), Balken, Balken mit Zahl oder
  nur ein Punkt in Grün, Gelb oder Rot.
- **Größe:** klein, mittel, groß. Die Anzeige ist leicht durchsichtig.
- **Wann:** immer, nur beim Anschauen oder nur bei Mobs, die man gerade
  getroffen hat. Letzteres ist bei uns Standard: Bei vielen Tieren auf der
  Weide war alles andere zu unruhig.
- **Zielanzeige:** auf Wunsch eine Bossleiste oben mit dem Mob, den man
  anschaut, gedacht für Bosskämpfe. Standardmäßig aus.
- **Aufgeräumte Config:** Bei Updates bleiben alle Erklärungen in der
  `config.yml` erhalten.

<figure class="abb klein">
  <a href="/assets/2026-11-17-mobtag-lebensanzeige-ueber-mobs/02-menue.png">
    <img src="/assets/2026-11-17-mobtag-lebensanzeige-ueber-mobs/02-menue.png"
         alt="Menü MobTag Settings: oben Schalter aus grüner und roter Wolle, darunter Namensschild, Fernrohr, Enderauge und Wassereimer">
  </a>
  <figcaption>Oben Schalter, unten Design, Größe, Wann und Zurücksetzen.</figcaption>
</figure>

<figure class="abb klein">
  <a href="/assets/2026-11-17-mobtag-lebensanzeige-ueber-mobs/03-designs.png">
    <img src="/assets/2026-11-17-mobtag-lebensanzeige-ueber-mobs/03-designs.png"
         alt="Tooltip Design: Classic mit Herz 14/20, Bar als grüner Balken, Bar + numbers mit 14/20 und Dot als grüner Punkt">
  </a>
  <figcaption>Die vier Designs mit Vorschau.</figcaption>
</figure>

Alles geht auch per Befehl, etwa `/mobtag style bar` oder `/mobtag show combat`.

## Installieren

Läuft auf Paper oder Spigot ab 1.21, getestet mit Paper 26.3.

1. `MobTag-….jar` von den
   [Releases](https://github.com/TechnikWeber/MobTag/releases) laden und in
   den Ordner `plugins/` legen.
2. Zusätzlich [PacketEvents](https://modrinth.com/plugin/packetevents) in
   `plugins/` legen. Ohne läuft MobTag auch, dann aber ohne eigene Designs und
   Größen pro Spieler.
3. Server neu starten, im Spiel `/mobtag` eingeben.

Standardwerte für neue Spieler stehen in `plugins/MobTag/config.yml`.
Geyser-Spieler auf Bedrock werden erkannt, getestet habe ich das aber noch
nicht.
