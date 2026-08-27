---
layout: beitrag
title: "Drei DC-DC-Wandler am Prüfstand – nur einer hält, was draufsteht"
date: 2026-08-26 19:30:00 +0200
tags: [Elektronik, Messtechnik]
---

Fünf Volt aus einem Akku zu machen, klingt nach einem gelösten Problem. Drei
Module lagen vergangenes Wochenende auf meinem Tisch, alle beworben mit **5 V**
und **5 A**. Mich hat dabei nicht interessiert, ob exakt 5,00 V herauskommen –
4,7 V wären für die meisten Verbraucher völlig in Ordnung. Mich hat
interessiert, ob überhaupt stimmt, was in der Artikelbeschreibung steht.

Zwei der Module sind **UBECs**, also reine Abwärtswandler: Sie können eine
Spannung nur herunterregeln, niemals hinauf. Das dritte ist ein
**Buck-Boost-Wandler** und kann beides.

## Der Prüfstand

Jedes Modul bekam 5,5 V, 6,6 V, 7,4 V, 11,1 V und 26 V vorgesetzt und wurde
dabei mit 1 A, 2 A, 3 A und – wo das ging – mit 5 A belastet. Die 6,6 V sind
kein Zufall: Da ist ein 2S-LiPo leer. Als bestanden zähle ich alles ab
**4,7 V** am Ausgang. Das ist großzügiger als die Toleranz, die Modul 2 selbst
angibt (5,25 V ± 0,5 V).

In den Messwert-Tabellen bedeutet **\*** „hält nur wenige Sekunden, dann
schaltet das Modul wegen Übertemperatur ab“, **✕** „kein Ausgang, das Modul
läuft gar nicht erst an“ und **–** „nicht gemessen“.

Gemessen habe ich direkt am Modulausgang. Ein Teil des Spannungsabfalls steckt
nämlich gar nicht im Regler: Der Lastabfall entspricht bei Modul 1 und 3 rund
0,1 bis 0,2 Ω, der Größenordnung von Litze und Steckern. Wer die letzten
Millivolt braucht, misst am Verbraucher.

## Modul 1 – Hobbywing UBEC

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg"
         alt="Hobbywing UBEC im silbernen Blechgehäuse mit angelöteten
              Leitungen und einem grünen Ferritringkern im Ausgangskabel">
  </a>
  <figcaption>„5V/6V 3A … MAX 5A“. Als einziges im Blechgehäuse, mit
  Ferritringkern im Kabel. Welcher Regler darin steckt, bleibt
  verborgen.</figcaption>
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

Ab 7,4 V Eingang und bis etwa 2 A ist das ein ordentlicher Regler. Er ist nur
eben ein 2-A-Regler.

## Modul 2 – UBEC-Platine 5 A

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg"
         alt="Kleine blaue Platine im durchsichtigen Schrumpfschlauch, zwei
              Elkos, Schaltregler-IC mit der Aufschrift LM2596S und
              Speicherdrossel mit Aufkleber UBEC 5A">
  </a>
  <figcaption>Nackte Reglerplatine, Aufkleber „UBEC 5A“. Auf dem IC steht gut
  lesbar <strong>LM2596S</strong>.</figcaption>
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

Der Aufdruck auf dem IC erklärt das Ganze: Ein **LM2596S** ist laut Datenblatt
ein 3-A-Schaltregler. Auf dem Aufkleber daneben steht „UBEC 5A“.

## Modul 3 – Buck-Boost-Modul

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg"
         alt="Blaue Platine mit geschirmter Speicherdrossel, unbeschriftetem
              QFN-Chip, zwei Elkos und Lötpads für IN plus, IN minus, OUT plus,
              OUT minus und EN">
  </a>
  <figcaption>Buck-Boost-Modul mit Enable-Eingang. Der QFN in der Mitte ist
  blank: die Beschriftung ist abgeschliffen.</figcaption>
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

Die Beschreibung schränkt selbst ein: Die 5 A gelten im Boost-Betrieb für den
*Eingangs*strom, nicht für den Ausgang. Genau am unteren Ende wird es eng – bei
5,5 V bricht das Modul schon unter 2 A nach Sekunden ein.

## Fazit

Nur **Modul 3** hält im Wesentlichen, was seine Beschreibung verspricht – der
einzige mit echten 5 V und der einzige, der 5 A überhaupt liefert. Ab 6,6 V
Eingang ohne Einschränkung brauchbar. Wer aus 2S oder 3S ordentlich Strom bei
5 V braucht, nimmt den.

**Modul 1** ist solide gebaut und ab 7,4 V für kleine Lasten brauchbar; die 5 A
auf dem Aufkleber sind Fiktion. Ich behalte es trotzdem: Es ist das einzige mit
Blechgehäuse und Ferritringkern, und für einen Empfänger direkt daneben kann
das mehr wert sein als das letzte halbe Volt. Ob es wirklich leiser ist, weiß
ich allerdings nicht – gemessen habe ich hier nur Spannungen, keine Störungen.

**Modul 2** verfehlt jede seiner drei Kernangaben. Ich werde es nicht einbauen.

---

Die drei Module bei AliExpress, ohne Affiliate-Kram und ohne Empfehlung – nur
damit nachvollziehbar ist, was gemessen wurde:
[Modul 1](https://de.aliexpress.com/item/1005010265933337.html) ·
[Modul 2](https://de.aliexpress.com/item/1005009444909052.html) ·
[Modul 3](https://de.aliexpress.com/item/1005008431252487.html)
