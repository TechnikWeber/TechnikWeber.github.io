---
layout: beitrag
title: "Ein alter Fuchsjagd-Empfänger mit TCA440 – wer kennt den Bausatz?"
date: 2026-11-20 15:30:00 +0100
tags: [Amateurfunk]
---

Ein Arbeitskollege hat mir einen selbst gebauten **Peilempfänger fürs
80-m-Band** mitgebracht – gebaut für die Fuchsjagd (ARDF), bei der man im
Gelände versteckte Sender aufspürt. Blechgehäuse, Rohr als Griff, Stabantenne
obendrauf, zwei Drehknöpfe. Woher der Bausatz stammt, weiß niemand mehr.

<figure class="abb klein">
  <a href="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/01-in-der-hand.jpg">
    <img src="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/01-in-der-hand.jpg"
         alt="Blaugraues Blechkästchen in der Hand gehalten, oben ein dunkles Rohr als Griff und eine lange dünne Stabantenne, rechts zwei Drehknöpfe">
  </a>
  <figcaption>Handlich: Kästchen, Griff, Stabantenne.</figcaption>
</figure>

## So wird gepeilt

Im Rohr über dem Gehäuse steckt vermutlich die Ferritantenne. Sie hat ein
scharfes **Minimum**, wenn sie in Richtung Sender zeigt – das ergibt die
Richtung, aber nicht, ob der Fuchs vorne oder hinten sitzt. Dafür ist die
Stabantenne da: Per Taster zugeschaltet, wird aus der Acht eine Herzkurve, und
die Seite ist eindeutig. Einer der Knöpfe regelt die Empfindlichkeit, damit man
das Minimum auch direkt neben dem Sender noch hört.

<figure class="abb klein">
  <a href="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/02-gehaeuse-mit-griff.jpg">
    <img src="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/02-gehaeuse-mit-griff.jpg"
         alt="Das geschlossene Gehäuse liegend: vorne zwei Aluminium-Drehknöpfe mit roten Markierungen, hinten das Griffrohr mit Kupferring in der Mitte, daneben ein schwarzer Taster und die Antennenbuchse">
  </a>
  <figcaption>Geschlossen, mit Griffrohr und Taster.</figcaption>
</figure>

## Das Herz: der TCA440

Fast die ganze Empfangstechnik steckt in einem 16-Pin-Chip: geregelte
HF-Vorstufe, Mischer, eigener Oszillator und ZF-Verstärker. Das Besondere ist
der **Regelumfang von über 100 dB** – genau das braucht man beim Peilen, vom
kaum hörbaren Fuchs in der Ferne bis zum Sender direkt vor der Nase. Er läuft
mit 4,5 bis 15 V und reicht bis etwa 50 MHz.

Gedacht war der TCA440 eigentlich für AM-Radios der 1970er. Valvo (Philips)
führte ihn schon 1974, Siemens noch Ende der 1980er in seinen Datenbüchern;
wer ihn ursprünglich entwickelt hat, konnte ich nicht sicher klären. In der DDR
gab es ihn als **A244D**. Der Peiler-Konstrukteur Nick Roethe, DF1FO, schreibt,
er stecke in fast allen 80-m-Peilempfängern – in seiner Version 4 hat er ihn
trotzdem ersetzt, weil gute Exemplare kaum noch zu bekommen sind.

<figure class="abb klein">
  <a href="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/03-geoeffnet.jpg">
    <img src="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/03-geoeffnet.jpg"
         alt="Geöffnetes Gehäuse: links ein Schaumstoffblock als Batteriefach, rechts die grüne Platine mit dem TCA440 in einer Fassung, Trimmern, Widerständen und den zwei Potis an der Gehäusewand">
  </a>
  <figcaption>Geöffnet: Platine, Potis, Schaumstoff fürs Batteriefach.</figcaption>
</figure>

<figure class="abb klein">
  <a href="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/04-platine-tca440.jpg">
    <img src="/assets/2026-11-20-fuchsjagd-peilempfaenger-mit-tca440/04-platine-tca440.jpg"
         alt="Nahaufnahme der Platine: TCA440 im DIP-16-Gehäuse, daneben ein 12-k-Widerstand, darunter Widerstände mit 3k3 und 8k2, ein Transistor T1, ein grüner Trimmkondensator und ein 220-µF-Elko">
  </a>
  <figcaption>TCA440, daneben der 12-k-Widerstand.</figcaption>
</figure>

## Welcher Bausatz ist das?

Am nächsten kommt der **„Foxy“ (AS064)** des
[AATiS e.V.](https://www.aatis.de/content/baus%C3%A4tze/tipps/AS064_Fuchsjagdempf%C3%A4nger-Foxy-Tipps)
– Schaltplan und Bestückungsplan stehen dort. Vieles passt: TCA440, zwei
22-k-Potis, 3,3 k und 8,2 k, der 220-µF-Elko und vor allem der **12-k-Widerstand**,
den der AATiS nachträglich statt 22 k empfiehlt. Die Platine ist aber anders
aufgeteilt, und statt des Verstärker-ICs LM386 sitzt ein einzelner Transistor
drauf. Vielleicht ein Vorgänger oder eine Abwandlung.

Im Netz werden noch der **PRX80S** von Dieter Schwider, DF7XU, und die
FJRX-Peiler von DF1FO genannt, zu denen Harald Gosch, OE6GC, eine
Aufbauanleitung geschrieben hat. Einen Bausatz „ARDF80“ habe ich nicht
gefunden.

Wer das Gerät erkennt: Ich freue mich über einen Hinweis.

## Quellen

- [AATiS: Fuchsjagdempfänger „Foxy“ – Tipps, Schaltung, Bestückungsplan](https://www.aatis.de/content/baus%C3%A4tze/tipps/AS064_Fuchsjagdempf%C3%A4nger-Foxy-Tipps)
- [OE6GC: Empfehlungen zum Aufbau des DF1FO-80-m-Peilers FJRX84 (PDF)](https://workplace.oevsv.at/export/oevsv/.galleries/ARDF/PDF-ARDF/2016-Empfehlungen-von-OE6GC-zum-Aufbau-des-DF1FO-80m-Peilers-FJRX84.pdf)
- [hamwaves.com: ARDF-Ausrüstung, u. a. PRX80S und HRX80](https://hamwaves.com/ardf.equipment/en)
- [TCA440-Datenblatt (Kurzfassung)](https://pe2bz.philpem.me.uk/Misc/-%20Animals/-%20Bat/TCA440-Chip/tca440.htm)
