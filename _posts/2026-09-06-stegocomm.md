---
layout: beitrag
title: "StegoComm – verschlüsselte Nachrichten als harmloses Geplauder"
date: 2026-09-06 10:00:00 +0200
tags: [Amateurfunk]
---

**StegoComm** verschlüsselt eine Nachricht mit AES-256-GCM und verpackt den
Chiffretext anschließend in unauffällige Alltagssätze. Übertragen wird nur
Text aus Buchstaben und Leerzeichen – das übersteht jede Funk- oder
Chat-Strecke. Die Datei `cover_studio.html` macht das komplett im Browser,
ohne Installation und ohne Server.

<figure class="abb klein">
  <a href="/assets/2026-09-06-stegocomm/01-cover-studio.jpg">
    <img src="/assets/2026-09-06-stegocomm/01-cover-studio.jpg"
         alt="Cover Studio im Browser: links Nachricht, Schlüsselfeld und
              Einstellungen, rechts der erzeugte Cover-Text aus 60 Sätzen mit
              Kennzahlen zu Zeichen, Blöcken und Bits pro Satz">
  </a>
  <figcaption>Links die Eingabe, rechts der Text zum Senden.</figcaption>
</figure>

So geht es: HTML-Datei
[herunterladen](https://github.com/TechnikWeber/StegoComm) und doppelklicken.
Nachricht eintippen, Schlüssel eingeben – beide Seiten denselben –, Sprache
und Kanal wählen, **Copy all**. Die Gegenseite fügt den Text unten bei
*Receive & decrypt* ein und klickt **Decrypt**. Ob es funktioniert, zeigt
**Test with my own cover**: Der Knopf dekodiert den eben erzeugten Text, ganz
ohne zweiten Rechner.

Der Schlüssel ist standardmäßig maskiert, **🎲 Random** würfelt 25 Zeichen ohne
Verwechsler wie `l/1` und `o/0`, und das Schloss friert das Feld ein.
Gespeichert wird nichts – Tab zu, Schlüssel weg.

Für JS8Call gibt es einen Großbuchstaben-Modus, und wer keine Tarnung braucht,
schaltet auf **Numbers** oder **Base32** um: dieselbe Verschlüsselung, aber
vier- bis sechsmal kürzer.

**Rechtlicher Hinweis:** Im Amateurfunk ist verschlüsselter oder
verschleierter Funkverkehr nicht zulässig – der Inhalt einer Aussendung muss
offen und für jeden nachvollziehbar sein. In Deutschland untersagt die
Amateurfunkverordnung das Verschleiern von Aussendungen ausdrücklich. Andere
Länder regeln das jeweils selbst, deshalb vorher die eigenen Bestimmungen
prüfen. Auf den Amateurfunkbändern gehört StegoComm damit nicht aufs Band; für
Chat, Mail oder andere Wege gilt die Einschränkung nicht.

Ein Proof of Concept, kein auditiertes Sicherheitswerkzeug.

Code: [github.com/TechnikWeber/StegoComm](https://github.com/TechnikWeber/StegoComm)
