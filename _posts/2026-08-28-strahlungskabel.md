---
layout: beitrag
title: "Strahlungskabel – die Antenne, die 500 Meter lang ist"
date: 2026-08-28 08:30:00 +0200
tags: [Amateurfunk]
---

In einer Tiefgarage lief mir ein daumendickes Kabel über den Weg, das an der
Decke entlanglief und nirgends in eine Antenne mündete. Der Aufdruck:
**RLK78-50JFNA**. Es *ist* die Antenne – auf seiner ganzen Länge.

Ein Strahlungskabel (auch Schlitz- oder Leckkabel, englisch *leaky feeder*) ist
ein Koaxkabel, dessen Außenleiter in regelmäßigen Abständen geschlitzt ist.
Durch diese Schlitze tritt ein genau dosierter Teil der Leistung aus. Und weil
Antennen reziprok sind, koppelt umgekehrt auch ein Signal von außen wieder ein –
das Handfunkgerät im Tunnel sendet und empfängt gleichermaßen.

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 580 200" role="img"
         aria-label="Skizze: ein waagerechtes Koaxkabel mit Schlitzgruppen im
                     Außenleiter, links der Sender, rechts der 50-Ohm-Abschluss.
                     Entlang des Kabels die Längsdämpfung, nach unten zu einem
                     Handfunkgerät die Koppeldämpfung.">
      <g font-family="system-ui, sans-serif" font-size="12" fill="#555">
        <!-- Laengsdaempfung -->
        <line x1="60" y1="28" x2="520" y2="28" stroke="#999"
              stroke-width="1" marker-end="url(#pfeil)"/>
        <text x="290" y="20" text-anchor="middle">Längsdämpfung · 2,9 dB je 100 m</text>
        <!-- Kabel -->
        <rect x="40" y="52" width="500" height="20" rx="3"
              fill="#f0efec" stroke="#8a8a85"/>
        <line x1="40" y1="52" x2="540" y2="52" stroke="#8a8a85" stroke-width="2"/>
        <line x1="40" y1="62" x2="540" y2="62" stroke="#b98a3c" stroke-width="3"/>
        <!-- Schlitzgruppen im Aussenleiter -->
        <g stroke="#333" stroke-width="2">
          <path d="M110 72v-6M116 72v-6M122 72v-6
                   M200 72v-6M206 72v-6M212 72v-6
                   M290 72v-6M296 72v-6M302 72v-6
                   M380 72v-6M386 72v-6M392 72v-6
                   M470 72v-6M476 72v-6M482 72v-6"/>
        </g>
        <!-- Abstrahlung -->
        <g stroke="#b3541e" fill="none" stroke-width="1.4">
          <path d="M206 80q40 30 74 46" stroke-dasharray="4 3"/>
          <path d="M296 80q0 34 -4 46" stroke-dasharray="4 3"/>
          <path d="M386 80q-40 30 -74 46" stroke-dasharray="4 3"/>
        </g>
        <!-- Handfunkgeraet -->
        <rect x="278" y="128" width="26" height="42" rx="4"
              fill="#fff" stroke="#333"/>
        <line x1="291" y1="128" x2="291" y2="108" stroke="#333" stroke-width="2"/>
        <text x="316" y="152" fill="#b3541e">Koppeldämpfung · 56 dB in 2 m</text>
        <!-- Enden -->
        <text x="40" y="94">Sender</text>
        <text x="540" y="94" text-anchor="end">50 Ω Abschluss</text>
      </g>
      <defs>
        <marker id="pfeil" viewBox="0 0 10 10" refX="9" refY="5"
                markerWidth="6" markerHeight="6" orient="auto">
          <path d="M0 0 10 5 0 10z" fill="#999"/>
        </marker>
      </defs>
    </svg>
  </div>
  <figcaption>Zwei Dämpfungen, die gegeneinander laufen: die eine längs, die
  andere quer.</figcaption>
</figure>

## Wo es steckt

Überall dort, wo Funk nicht hinkommt, aber hinkommen muss: Straßen- und
Eisenbahntunnel, U-Bahnen, Bergwerke, Tiefgaragen, Einkaufszentren, Kliniken.
In Deutschland meist als **Objektfunk** für die BOS – ohne den findet die
Feuerwehr im Untergeschoss keine Verbindung. Das Kabel ist mit 30 bis 980 MHz so
breitbandig, dass BOS-Funk, Mobilfunk und Betriebsfunk gleichzeitig darüber
laufen.

## Die zwei Dämpfungen

| Frequenz | Längsdämpfung | Koppeldämpfung (95 %) |
|---|---|---|
| 150 MHz | 1,56 dB/100 m | 66 dB |
| 450 MHz | 2,90 dB/100 m | 56 dB |
| 900 MHz | 5,05 dB/100 m | 62 dB |
{: .messwerte}

Längsdämpfung ist, was auf dem Weg verlorengeht; Koppeldämpfung, was zwischen
Kabel und einem Empfänger in 2 m Abstand fehlt. Der 95-%-Wert heißt: An 95 % der
Messpunkte war es mindestens so gut. Beide zusammen bestimmen die nutzbare
Länge – und sie ziehen in verschiedene Richtungen, denn mehr Abstrahlung heißt
weniger Rest am Ende.

Ein Zahlenbeispiel im 70-cm-Bereich: 10 W am Anfang sind 40 dBm, nach 300 m
bleiben 31 dBm, nach der Kopplung landen −25 dBm im Handfunkgerät. Sehr laut.

## Was daran eigenartig ist

- **Sperrbänder.** Der regelmäßige Schlitzabstand macht das Kabel bei 300–375
  und 650–685 MHz weitgehend blind. Praktischerweise liegen 2 m und 70 cm
  außerhalb, aber ein 300-MHz-System kann man auf diesem Kabel vergessen.
- **Es hat eine Vorzugsrichtung.** Über den Schlitzen läuft ein Wulst im Mantel,
  damit man beim Montieren sieht, wohin sie zeigen – nämlich in den Raum. Und
  mindestens 8 cm Abstand zur Wand, sonst stimmt die Kopplung nicht mehr.
- **Der Mantel ist die halbe Miete.** JFN heißt halogenfrei, flammwidrig,
  raucharm. In einem Tunnelbrand darf ein Kabel keinen korrosiven Qualm
  beisteuern.
- **Das Ende gehört abgeschlossen**, sonst läuft die Welle zurück und die
  Versorgung bekommt Löcher im Meterabstand.

Der Typenschlüssel liest sich übrigens geradeheraus: **RLK** Kabeltyp, **78** für
7/8 Zoll, **50** Ohm, **JFN** der Mantel, **A** die Serie. 28,5 mm dick,
550 g pro Meter, kleinster Biegeradius 35 cm. Nichts, was man mal eben durchs
Treppenhaus zieht.

Quellen:
[RFS-Datenblatt RLK78-50JFNA](https://www.rfsworld.com/product/RLK78-50JFNA) ·
[Schlitzkabel bei Wikipedia](https://de.wikipedia.org/wiki/Schlitzkabel)
