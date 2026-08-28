---
layout: beitrag
title: "Drei DC-DC-Wandler am Prüfstand – nur einer hält, was draufsteht"
date: 2026-08-26 19:30:00 +0200
tags: [Elektronik]
---

Drei Module, alle beworben mit **5 V** und **5 A**. Exakte 5,00 V erwarte ich
nicht, 4,7 V täten es auch – mich interessierte nur, ob stimmt, was in der
Artikelbeschreibung steht. Zwei sind **UBECs**, also reine Abwärtswandler, das
dritte ein **Buck-Boost-Wandler**.

## Das Prüfverfahren

Jedes Modul bekam 5,5 V, 6,6 V, 7,4 V, 11,1 V und 26 V vorgesetzt, belastet mit
1 A, 2 A, 3 A und – wo das ging – 5 A. Die 6,6 V sind kein Zufall: Da ist ein
2S-LiPo leer. Als bestanden zähle ich alles ab **4,7 V** am Modulausgang; in
Litze und Steckern stecken noch einmal 0,1 bis 0,2 Ω.

## Modul 1 – Hobbywing UBEC

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg"
         alt="Hobbywing UBEC im silbernen Blechgehäuse mit angelöteten
              Leitungen und einem grünen Ferritringkern im Ausgangskabel">
  </a>
  <figcaption>„5V/6V 3A … MAX 5A“, Blechgehäuse mit
  Ferritringkern.</figcaption>
</figure>

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/04-hobbywing-geoeffnet.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/04-hobbywing-geoeffnet.jpg"
         alt="Geöffneter Hobbywing UBEC: grüne Platine mit der Aufschrift
              HW212V1.2, einem SOIC-8 mit der Beschriftung MP1593DN, zwei
              Schottky-Dioden SS34, einer Drossel mit Aufdruck 150 und einem
              blauen Jumper auf einer Stiftleiste">
  </a>
  <figcaption>Geöffnet: <strong>MP1593DN</strong>, zwei SS34, 15-µH-Drossel,
  Jumper für 5 V/6 V.</figcaption>
</figure>

| Aus der Artikelbeschreibung | Gemessen |
|---|---|
| Eingang 5,5 V–26 V (2–6S) | **Nein.** Bei 5,5 V kommen selbst mit nur 1 A Last bloß 3,77 V heraus. Sauber wird er erst ab 7,4 V. |
| Dauerausgangsstrom 3 A | **Nur ab 11 V.** Darunter fällt die Spannung bei 3 A auf 2,5 bis 3,6 V und das Modul schaltet nach wenigen Sekunden thermisch ab. |
| „MAX 5A“ | **Nein.** Wenn schon 3 A nicht dauerhaft gehen, habe ich 5 A gar nicht erst versucht. |

| Last | 5,5 V | 6,6 V | 7,4 V | 11,1 V | 26 V |
|---|---|---|---|---|---|
| 1 A | 3,77 V | 4,80 V | 5,12 V | 5,12 V | 5,12 V |
| 2 A | 3,05 V | 4,10 V | 4,80 V | 4,93 V | 4,93 V |
| 3 A | 2,50 V \* | 3,20 V \* | 3,60 V \* | 4,75 V | 4,75 V |
{: .messwerte}

\* hält nur Sekunden, dann Abschaltung wegen Übertemperatur
{: .legende}

Ungeprüft: Abschirmung, „niedrigstes RF-Rauschen“, Welligkeit unter
50 mV<sub>pp</sub> bei 2 A und 12 V. Bei den Maßen widerspricht sich der
Verkäufer: 51 × 16,6 × 8,5 mm laut Beschreibung, 43 × 17 × 7 mm auf der
AliExpress-Seite.

Ab 7,4 V Eingang und bis etwa 2 A ist das ein ordentlicher Regler. Warum nicht
mehr, steht auf dem Chip: Ein **MP1593DN** von Monolithic Power Systems liefert
laut Datenblatt 3 A und verträgt 4,75 bis 28 V am Eingang. Er bringt außerdem
eine Übertemperaturabschaltung mit – genau die, die bei 3 A nach Sekunden
zuschlägt. „MAX 5A“ steht also auf dem Gehäuse, aber in keinem Datenblatt.

## Modul 2 – UBEC-Platine 5 A

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg"
         alt="Kleine blaue Platine im durchsichtigen Schrumpfschlauch, zwei
              Elkos, Schaltregler-IC mit der Aufschrift LM2596S und
              Speicherdrossel mit Aufkleber UBEC 5A">
  </a>
  <figcaption>Aufkleber „UBEC 5A“, auf dem IC:
  <strong>LM2596S</strong>.</figcaption>
</figure>

| Aus der Artikelbeschreibung | Gemessen |
|---|---|
| Eingang 5,5 V–35 V (2–8S) | **Nein.** Bei 5,5 V und 1 A sind es 4,07 V. |
| Dauerstrom 5 A, kurzzeitig 6 A | **Nein.** Bei 5 A läuft das Modul an keiner einzigen Eingangsspannung überhaupt an. |
| Ausgang 5,25 V ± 0,5 V | **Nein.** Bestwert über alle Messungen: 4,93 V. Bei 3 A bleiben selbst an 26 V nur 4,44 V. |

| Last | 5,5 V | 6,6 V | 7,4 V | 11,1 V | 26 V |
|---|---|---|---|---|---|
| 1 A | 4,07 V | 4,65 V | 4,74 V | 4,93 V | – |
| 2 A | 3,50 V | 4,61 V | 4,70 V | 4,80 V | – |
| 3 A | 2,80 V | 3,88 V | 4,07 V | 4,34 V | 4,44 V |
| 5 A | ✕ | ✕ | ✕ | ✕ | ✕ |
{: .messwerte}

✕ kein Ausgang, das Modul läuft gar nicht erst an · – nicht gemessen
{: .legende}

Ungeprüft: Abschirmung und „niedrigstes HF-Rauschen“, eine Zahl zur Welligkeit
fehlt. Angegeben sind 43 × 21 × 1 mm – nachgemessen trägt das Modul 10 mm auf.

Der Aufdruck auf dem IC erklärt das Ganze: Ein **LM2596S** ist laut Datenblatt
ein 3-A-Schaltregler. Auf dem Aufkleber daneben steht „UBEC 5A“.

## Modul 3 – Buck-Boost-Modul

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg"
         alt="Blaue Platine mit geschirmter Speicherdrossel, blankem QFN-Chip
              ohne Beschriftung, zwei Elkos und Lötpads für IN plus, IN minus,
              OUT plus, OUT minus und EN">
  </a>
  <figcaption>Buck-Boost mit Enable-Eingang. Steuerchip abgelasert,
  Rückseite: <strong>CR-3050B</strong>.</figcaption>
</figure>

| Aus der Artikelbeschreibung | Gemessen |
|---|---|
| Eingang 3,6 V–32 V | **Teilweise.** Ab 6,6 V tadellos, aber bei 3,6 V läuft unter Last gar nichts. |
| 5 V Ausgang | **Ja.** 5,09 V bei 1 A, 4,98 V bei 2 A, 4,87 V bei 3 A – über den ganzen Eingangsbereich. |
| bis 5 A | **Fast.** Ab 7,4 V Eingang schafft er die 5 A, mit 4,62 V aber knapp unter meiner Grenze. |

| Last | 5,5 V | 6,6 V | 7,4 V | 11,1 V | 26 V |
|---|---|---|---|---|---|
| 1 A | 5,09 V | 5,09 V | 5,09 V | 5,09 V | – |
| 2 A | 2,10 V \* | 4,98 V | 4,98 V | 4,98 V | – |
| 3 A | ✕ | 4,86 V | 4,87 V | 4,87 V | – |
| 5 A | ✕ | ✕ | 4,63 V | 4,62 V | 4,62 V |
{: .messwerte}

\* hält nur Sekunden, dann Abschaltung wegen Übertemperatur
· ✕ kein Ausgang, das Modul läuft gar nicht erst an
· – nicht gemessen
{: .legende}

Ungeprüft: „geringe Welligkeit“ (ohne Zahl), Kurzschluss- und
Übertemperaturschutz, TVS-Diode, −40 bis +125 °C. Maße nennt der Verkäufer
keine – nachgemessen 31 × 22 × 7 mm.

Die Beschreibung schränkt selbst ein: Die 5 A gelten im Boost-Betrieb für den
*Eingangs*strom, nicht für den Ausgang. Genau am unteren Ende wird es eng – bei
5,5 V bricht das Modul schon unter 2 A nach Sekunden ein.

## Fazit

**Modul 3** hält im Wesentlichen, was draufsteht, und ist als einziges bei 5 A
überhaupt zu gebrauchen. Wer aus 2S oder 3S ordentlich Strom bei 5 V braucht,
nimmt den.

**Modul 1** taugt ab 7,4 V für kleine Lasten; die 5 A auf dem Aufkleber sind
Fiktion. Ich behalte es trotzdem – wegen Blechgehäuse und Ferritringkern, was
neben einem Empfänger mehr wert sein kann als das letzte halbe Volt.

**Modul 2** verfehlt jede seiner drei Kernangaben und kommt nicht zum Einsatz.

---

Die drei Module bei AliExpress, ohne Affiliate-Kram und ohne Empfehlung – nur
damit nachvollziehbar ist, was gemessen wurde:
[Modul 1](https://de.aliexpress.com/item/1005010265933337.html) ·
[Modul 2](https://de.aliexpress.com/item/1005009444909052.html) ·
[Modul 3](https://de.aliexpress.com/item/1005008431252487.html)
