---
layout: beitrag
title: "So abonnierst du einen RSS-Feed"
date: 2026-08-26 14:00:00 +0200
tags: [Allgemeines]
---

Eine Seite regelmäßig auf neue Beiträge abzuklappern, vergisst man. Ein
Newsletter will die E-Mail-Adresse. RSS dreht das um: Die Seite meldet sich bei
dir, ohne Konto, ohne Adresse, ohne Algorithmus, der entscheidet, was du zu
sehen bekommst.

Fast jeder Blog bietet einen **Feed** an – eine Datei, in der die letzten
Beiträge stehen und die sich bei jedem neuen Beitrag ändert. Ein **Feedreader**
sieht regelmäßig nach und legt dir vor, was dazugekommen ist. Wie ein
Posteingang, nur für Webseiten.

## Schritt 1 – Einen Reader aussuchen

| Wo | Womit |
|---|---|
| PC | Thunderbird kann es schon eingebaut. Sonst QuiteRSS oder Fluent Reader. |
| Android | Feeder oder FeedMe |
| iPhone | NetNewsWire oder Reeder |
| überall | Feedly oder Inoreader – laufen im Browser, wollen dafür ein Konto |

Die ersten drei Zeilen brauchen kein Konto: Die Abos liegen auf deinem Gerät.

## Schritt 2 – Die Adresse eintragen

Der Feed dieses Blogs ist:

```
https://technikweber.github.io/feed.xml
```

Die kopierst du in deinen Reader, fertig. Bei den meisten reicht sogar die
normale Blog-Adresse `https://technikweber.github.io` – der Reader sucht sich
den Feed dann selbst, weil er in jeder Seite vermerkt ist.

In **Thunderbird** sind es drei Schritte: *Datei → Neu → Feed-Konto* anlegen,
dann Rechtsklick auf dieses Konto → *Abonnements…* → *Hinzufügen* und die
Adresse einfügen. Neue Beiträge landen danach wie E-Mails im Posteingang.

## Der Feed sieht im Browser aus wie Kauderwelsch

Wer die Adresse direkt im Browser öffnet, bekommt eine Wand aus spitzen
Klammern und den Hinweis „This XML file does not appear to have any style
information". Das ist kein Fehler und nichts kaputt: Die Datei ist für
Programme geschrieben, nicht für Augen. Kopier die Adresse einfach in den
Reader, der macht eine Liste daraus.

## Und bei anderen Seiten?

Meistens versteckt sich der Feed hinter einem Symbol oder einem Link namens
„RSS" oder „Feed". Findest du keinen, gib deinem Reader einfach die Adresse der
Seite – oder häng probeweise `/feed`, `/rss` oder `/feed.xml` an. Erstaunlich
viele Seiten haben einen, auch ohne ihn zu bewerben.

---

Zum Ausprobieren gleich hier:
[technikweber.github.io/feed.xml](https://technikweber.github.io/feed.xml).
Ich erfahre davon nichts – kein Zähler, kein Konto, keine E-Mail-Adresse. Genau
das ist der Punkt.
