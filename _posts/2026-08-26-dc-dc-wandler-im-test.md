---
layout: beitrag
title: "Drei DC-DC-Wandler am Prüfstand – nur einer hält, was draufsteht"
date: 2026-08-26 19:30:00 +0200
tags: [Elektronik, Messtechnik]
---

Fünf Volt aus einem Akku zu machen, klingt nach einem gelösten Problem: Modul
für ein paar Euro bestellen, dazwischenlöten, fertig. Auf allen dreien, die
vergangenes Wochenende bei mir auf dem Tisch lagen, steht auch souverän
**5 V** und **bis 5 A**. Nachgemessen habe ich es trotzdem – und von den dreien
liefert genau **einer** verlässlich fünf Volt.

## Die drei Kandidaten

<figure class="abb">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg"
         alt="Hobbywing UBEC im silbernen Blechgehäuse mit angelöteten
              Leitungen und einem grünen Ferritringkern im Ausgangskabel">
  </a>
  <figcaption>Modul 1 – Hobbywing UBEC, 3 A Dauerstrom, „MAX 5A“, 2–6S LiPo.
  Als einziges im geschirmten Blechgehäuse, mit Ferritringkern im Kabel.
  </figcaption>
</figure>

<figure class="abb">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg"
         alt="Kleine blaue Platine im durchsichtigen Schrumpfschlauch, zwei
              Elkos, Schaltregler-IC und Speicherdrossel mit Aufdruck UBEC 5A">
  </a>
  <figcaption>Modul 2 – nackte Reglerplatine im Schrumpfschlauch, Aufkleber
  „UBEC 5A“ auf der Drossel.</figcaption>
</figure>

<figure class="abb">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg"
         alt="Blaue Platine mit geschirmter Speicherdrossel, QFN-Chip,
              zwei Elkos und Lötpads für IN plus, IN minus, OUT plus,
              OUT minus und EN">
  </a>
  <figcaption>Modul 3 – Buck-Boost-Modul mit geschirmter Drossel, QFN-Regler
  und Enable-Eingang.</figcaption>
</figure>

Der entscheidende Unterschied steckt schon in den Namen. Module 1 und 2 sind
**UBECs**, also reine Abwärtswandler: Sie können eine Spannung nur
herunterregeln, niemals hinauf. Modul 3 ist ein **Buck-Boost-Wandler** und
kann beides – der sollte also auch dann noch fünf Volt liefern, wenn vorne
weniger anliegt. Genau das war die Frage.

## Wie gemessen wurde

Jedes Modul bekam nacheinander 5,5 V, 6,6 V, 7,4 V, 11,1 V und 26 V vorgesetzt
und wurde dabei mit 1 A, 2 A, 3 A und – wo das ging – mit 5 A belastet. Die
6,6 V sind kein Zufall: Da ist ein 2S-LiPo leer. 7,4 V ist dessen
Nennspannung, 11,1 V die eines 3S. Modul 3 habe ich zusätzlich mit 3,6 V
gefüttert, also einer einzelnen Li-Ion-Zelle – ein Buck-Boost muss das
eigentlich können.

## Die Messwerte im Bild

<figure class="abb">
  <div class="rahmen">
    <svg viewBox="0 0 760 850" xmlns="http://www.w3.org/2000/svg" role="img" aria-labelledby="diagTitel diagDesc" class="messdiagramm">
    <title id="diagTitel">Ausgangsspannung der drei Wandler über der Eingangsspannung, je Laststrom eine Linie</title>
    <desc id="diagDesc">Dieselben Zahlen stehen in der Tabelle weiter unten im Beitrag.</desc>
    <style>.messdiagramm{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif}.messdiagramm text{fill:#52514e}.d-legtext{font-size:12.5px}.d-muted{fill:#7c7b77;font-size:12px}.d-ptitel{font-size:13.5px;font-weight:600;fill:#1a1a19}.d-grid{stroke:#e6e6e3;stroke-width:1}.d-soll{stroke:#a9a8a3;stroke-width:1.5;stroke-dasharray:6 4}.d-vgrid{stroke:#f1f1ee;stroke-width:1}.d-axis{stroke:#c4c3bf;stroke-width:1}.d-ytext{font-size:11px;fill:#8a8985;text-anchor:end}.d-xtext{font-size:11.5px;text-anchor:middle}.d-fuss{font-size:11.5px;fill:#7c7b77}.d-open{fill:#ffffff;stroke-width:2.5}.messdiagramm g[data-p]{cursor:help}.messdiagramm g[data-p]:hover circle,.messdiagramm g[data-p]:hover path{opacity:.55}</style>
    <text x="76" y="20" class="d-legtext d-muted">Laststrom</text>
    <line x1="146" y1="16" x2="168" y2="16" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <circle cx="157" cy="16" r="4.5" fill="#86b6ef" stroke="#fff" stroke-width="2"/>
    <text x="174" y="20" class="d-legtext">1 A</text>
    <line x1="218" y1="16" x2="240" y2="16" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <circle cx="229" cy="16" r="4.5" fill="#3987e5" stroke="#fff" stroke-width="2"/>
    <text x="246" y="20" class="d-legtext">2 A</text>
    <line x1="290" y1="16" x2="312" y2="16" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <circle cx="301" cy="16" r="4.5" fill="#1c5cab" stroke="#fff" stroke-width="2"/>
    <text x="318" y="20" class="d-legtext">3 A</text>
    <line x1="362" y1="16" x2="384" y2="16" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round"/>
    <circle cx="373" cy="16" r="4.5" fill="#0d366b" stroke="#fff" stroke-width="2"/>
    <text x="390" y="20" class="d-legtext">5 A</text>
    <text x="434" y="20" class="d-legtext d-muted">(hell = wenig Last, dunkel = viel Last)</text>
    <text x="76" y="46" class="d-legtext d-muted">Lesehilfe</text>
    <line x1="146" y1="42" x2="168" y2="42" class="d-soll"/>
    <text x="174" y="46" class="d-legtext">5 V Sollwert</text>
    <circle cx="284" cy="42" r="4.5" class="d-open" stroke="#1c5cab"/>
    <text x="296" y="46" class="d-legtext">hält nur Sekunden, dann Abschaltung</text>
    <path d="M542 37 l9 9 M551 37 l-9 9" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" fill="none"/>
    <text x="560" y="46" class="d-legtext">kein Ausgang</text>
    <g>
    <text x="68" y="92" class="d-ptitel">Modul 1 · Hobbywing UBEC 3 A (max. 5 A)</text>
    <line x1="76" y1="252.0" x2="676" y2="252.0" class="d-grid"/>
    <text x="67" y="256.0" class="d-ytext">0</text>
    <line x1="76" y1="225.1" x2="676" y2="225.1" class="d-grid"/>
    <text x="67" y="229.1" class="d-ytext">1</text>
    <line x1="76" y1="198.2" x2="676" y2="198.2" class="d-grid"/>
    <text x="67" y="202.2" class="d-ytext">2</text>
    <line x1="76" y1="171.3" x2="676" y2="171.3" class="d-grid"/>
    <text x="67" y="175.3" class="d-ytext">3</text>
    <line x1="76" y1="144.4" x2="676" y2="144.4" class="d-grid"/>
    <text x="67" y="148.4" class="d-ytext">4</text>
    <line x1="76" y1="117.5" x2="676" y2="117.5" class="d-soll"/>
    <text x="67" y="121.5" class="d-ytext">5</text>
    <line x1="76.0" y1="104.0" x2="76.0" y2="252.0" class="d-vgrid"/>
    <text x="76.0" y="273" class="d-xtext">5,5 V</text>
    <line x1="226.0" y1="104.0" x2="226.0" y2="252.0" class="d-vgrid"/>
    <text x="226.0" y="273" class="d-xtext">6,6 V</text>
    <line x1="376.0" y1="104.0" x2="376.0" y2="252.0" class="d-vgrid"/>
    <text x="376.0" y="273" class="d-xtext">7,4 V</text>
    <line x1="526.0" y1="104.0" x2="526.0" y2="252.0" class="d-vgrid"/>
    <text x="526.0" y="273" class="d-xtext">11,1 V</text>
    <line x1="676.0" y1="104.0" x2="676.0" y2="252.0" class="d-vgrid"/>
    <text x="676.0" y="273" class="d-xtext">26 V</text>
    <line x1="76" y1="252.0" x2="676" y2="252.0" class="d-axis"/>
    <line x1="76.0" y1="150.6" x2="226.0" y2="122.8" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="122.8" x2="376.0" y2="114.2" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="114.2" x2="526.0" y2="114.2" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="114.2" x2="676.0" y2="114.2" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 1 A: 3,77 V</title><circle cx="76.0" cy="150.6" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 1 A: 4,80 V</title><circle cx="226.0" cy="122.8" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 1 A: 5,12 V</title><circle cx="376.0" cy="114.2" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 1 A: 5,12 V</title><circle cx="526.0" cy="114.2" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 1 A: 5,12 V</title><circle cx="676.0" cy="114.2" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="169.9" x2="226.0" y2="141.7" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="141.7" x2="376.0" y2="122.8" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="122.8" x2="526.0" y2="119.3" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="119.3" x2="676.0" y2="119.3" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 2 A: 3,05 V</title><circle cx="76.0" cy="169.9" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 2 A: 4,10 V</title><circle cx="226.0" cy="141.7" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 2 A: 4,80 V</title><circle cx="376.0" cy="122.8" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 2 A: 4,93 V</title><circle cx="526.0" cy="119.3" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 2 A: 4,93 V</title><circle cx="676.0" cy="119.3" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="184.7" x2="226.0" y2="165.9" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="226.0" y1="165.9" x2="376.0" y2="155.1" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="376.0" y1="155.1" x2="526.0" y2="124.2" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="526.0" y1="124.2" x2="676.0" y2="124.2" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 3 A: 2,50 V, fällt nach Sekunden ab</title><circle cx="76.0" cy="184.7" r="4.5" class="d-open" stroke="#1c5cab"/></g>
    <g data-p="1"><title>6,6 V bei 3 A: 3,20 V, fällt nach Sekunden ab</title><circle cx="226.0" cy="165.9" r="4.5" class="d-open" stroke="#1c5cab"/></g>
    <g data-p="1"><title>7,4 V bei 3 A: 3,60 V, fällt nach Sekunden ab</title><circle cx="376.0" cy="155.1" r="4.5" class="d-open" stroke="#1c5cab"/></g>
    <g data-p="1"><title>11,1 V bei 3 A: 4,75 V</title><circle cx="526.0" cy="124.2" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 3 A: 4,75 V</title><circle cx="676.0" cy="124.2" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    </g>
    <g>
    <text x="68" y="334" class="d-ptitel">Modul 2 · UBEC-Platine 5 A</text>
    <line x1="76" y1="494.0" x2="676" y2="494.0" class="d-grid"/>
    <text x="67" y="498.0" class="d-ytext">0</text>
    <line x1="76" y1="467.1" x2="676" y2="467.1" class="d-grid"/>
    <text x="67" y="471.1" class="d-ytext">1</text>
    <line x1="76" y1="440.2" x2="676" y2="440.2" class="d-grid"/>
    <text x="67" y="444.2" class="d-ytext">2</text>
    <line x1="76" y1="413.3" x2="676" y2="413.3" class="d-grid"/>
    <text x="67" y="417.3" class="d-ytext">3</text>
    <line x1="76" y1="386.4" x2="676" y2="386.4" class="d-grid"/>
    <text x="67" y="390.4" class="d-ytext">4</text>
    <line x1="76" y1="359.5" x2="676" y2="359.5" class="d-soll"/>
    <text x="67" y="363.5" class="d-ytext">5</text>
    <line x1="76.0" y1="346.0" x2="76.0" y2="494.0" class="d-vgrid"/>
    <text x="76.0" y="515" class="d-xtext">5,5 V</text>
    <line x1="226.0" y1="346.0" x2="226.0" y2="494.0" class="d-vgrid"/>
    <text x="226.0" y="515" class="d-xtext">6,6 V</text>
    <line x1="376.0" y1="346.0" x2="376.0" y2="494.0" class="d-vgrid"/>
    <text x="376.0" y="515" class="d-xtext">7,4 V</text>
    <line x1="526.0" y1="346.0" x2="526.0" y2="494.0" class="d-vgrid"/>
    <text x="526.0" y="515" class="d-xtext">11,1 V</text>
    <line x1="676.0" y1="346.0" x2="676.0" y2="494.0" class="d-vgrid"/>
    <text x="676.0" y="515" class="d-xtext">26 V</text>
    <line x1="76" y1="494.0" x2="676" y2="494.0" class="d-axis"/>
    <line x1="76.0" y1="384.5" x2="226.0" y2="368.9" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="368.9" x2="376.0" y2="366.5" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="366.5" x2="526.0" y2="361.3" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 1 A: 4,07 V</title><circle cx="76.0" cy="384.5" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 1 A: 4,65 V</title><circle cx="226.0" cy="368.9" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 1 A: 4,74 V</title><circle cx="376.0" cy="366.5" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 1 A: 4,93 V</title><circle cx="526.0" cy="361.3" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="399.8" x2="226.0" y2="369.9" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="369.9" x2="376.0" y2="367.5" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="367.5" x2="526.0" y2="371.3" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 2 A: 3,50 V</title><circle cx="76.0" cy="399.8" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 2 A: 4,61 V</title><circle cx="226.0" cy="369.9" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 2 A: 4,70 V</title><circle cx="376.0" cy="367.5" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 2 A: 4,56 V</title><circle cx="526.0" cy="371.3" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="418.7" x2="226.0" y2="389.6" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="389.6" x2="376.0" y2="384.5" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="384.5" x2="526.0" y2="377.2" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="377.2" x2="676.0" y2="374.5" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 3 A: 2,80 V</title><circle cx="76.0" cy="418.7" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 3 A: 3,88 V</title><circle cx="226.0" cy="389.6" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 3 A: 4,07 V</title><circle cx="376.0" cy="384.5" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 3 A: 4,34 V</title><circle cx="526.0" cy="377.2" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 3 A: 4,44 V</title><circle cx="676.0" cy="374.5" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>5,5 V bei 5 A: kein Ausgang</title><path d="M71.5 482.5 l9 9 M80.5 482.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>6,6 V bei 5 A: kein Ausgang</title><path d="M221.5 482.5 l9 9 M230.5 482.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>7,4 V bei 5 A: kein Ausgang</title><path d="M371.5 482.5 l9 9 M380.5 482.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>11,1 V bei 5 A: kein Ausgang</title><path d="M521.5 482.5 l9 9 M530.5 482.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>26 V bei 5 A: kein Ausgang</title><path d="M671.5 482.5 l9 9 M680.5 482.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    </g>
    <g>
    <text x="68" y="576" class="d-ptitel">Modul 3 · Buck-Boost-Modul</text>
    <line x1="76" y1="736.0" x2="676" y2="736.0" class="d-grid"/>
    <text x="67" y="740.0" class="d-ytext">0</text>
    <line x1="76" y1="709.1" x2="676" y2="709.1" class="d-grid"/>
    <text x="67" y="713.1" class="d-ytext">1</text>
    <line x1="76" y1="682.2" x2="676" y2="682.2" class="d-grid"/>
    <text x="67" y="686.2" class="d-ytext">2</text>
    <line x1="76" y1="655.3" x2="676" y2="655.3" class="d-grid"/>
    <text x="67" y="659.3" class="d-ytext">3</text>
    <line x1="76" y1="628.4" x2="676" y2="628.4" class="d-grid"/>
    <text x="67" y="632.4" class="d-ytext">4</text>
    <line x1="76" y1="601.5" x2="676" y2="601.5" class="d-soll"/>
    <text x="67" y="605.5" class="d-ytext">5</text>
    <line x1="76.0" y1="588.0" x2="76.0" y2="736.0" class="d-vgrid"/>
    <text x="76.0" y="757" class="d-xtext">5,5 V</text>
    <line x1="226.0" y1="588.0" x2="226.0" y2="736.0" class="d-vgrid"/>
    <text x="226.0" y="757" class="d-xtext">6,6 V</text>
    <line x1="376.0" y1="588.0" x2="376.0" y2="736.0" class="d-vgrid"/>
    <text x="376.0" y="757" class="d-xtext">7,4 V</text>
    <line x1="526.0" y1="588.0" x2="526.0" y2="736.0" class="d-vgrid"/>
    <text x="526.0" y="757" class="d-xtext">11,1 V</text>
    <line x1="676.0" y1="588.0" x2="676.0" y2="736.0" class="d-vgrid"/>
    <text x="676.0" y="757" class="d-xtext">26 V</text>
    <line x1="76" y1="736.0" x2="676" y2="736.0" class="d-axis"/>
    <line x1="76.0" y1="599.0" x2="226.0" y2="599.0" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="599.0" x2="376.0" y2="599.0" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="599.0" x2="526.0" y2="599.0" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 1 A: 5,09 V</title><circle cx="76.0" cy="599.0" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 1 A: 5,09 V</title><circle cx="226.0" cy="599.0" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 1 A: 5,09 V</title><circle cx="376.0" cy="599.0" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 1 A: 5,09 V</title><circle cx="526.0" cy="599.0" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="679.5" x2="226.0" y2="602.0" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="226.0" y1="602.0" x2="376.0" y2="602.0" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="602.0" x2="526.0" y2="602.0" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 2 A: 2,10 V, fällt nach Sekunden ab</title><circle cx="76.0" cy="679.5" r="4.5" class="d-open" stroke="#3987e5"/></g>
    <g data-p="1"><title>6,6 V bei 2 A: 4,98 V</title><circle cx="226.0" cy="602.0" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 2 A: 4,98 V</title><circle cx="376.0" cy="602.0" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 2 A: 4,98 V</title><circle cx="526.0" cy="602.0" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="736.0" x2="226.0" y2="605.2" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="226.0" y1="605.2" x2="376.0" y2="605.0" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="605.0" x2="526.0" y2="605.0" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 3 A: kein Ausgang</title><path d="M71.5 724.5 l9 9 M80.5 724.5 l-9 9" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>6,6 V bei 3 A: 4,86 V</title><circle cx="226.0" cy="605.2" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 3 A: 4,87 V</title><circle cx="376.0" cy="605.0" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 3 A: 4,87 V</title><circle cx="526.0" cy="605.0" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="226.0" y1="736.0" x2="376.0" y2="611.4" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="376.0" y1="611.4" x2="526.0" y2="611.7" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="611.7" x2="676.0" y2="611.7" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 5 A: kein Ausgang</title><path d="M86.5 724.5 l9 9 M95.5 724.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>6,6 V bei 5 A: kein Ausgang</title><path d="M221.5 724.5 l9 9 M230.5 724.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>7,4 V bei 5 A: 4,63 V</title><circle cx="376.0" cy="611.4" r="4.5" fill="#0d366b" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 5 A: 4,62 V</title><circle cx="526.0" cy="611.7" r="4.5" fill="#0d366b" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 5 A: 4,62 V</title><circle cx="676.0" cy="611.7" r="4.5" fill="#0d366b" stroke="#ffffff" stroke-width="2"/></g>
    </g>
    <text x="76" y="824" class="d-fuss">waagerecht: angelegte Eingangsspannung (Abstände nicht maßstäblich) · senkrecht: Ausgangsspannung in Volt</text>
    <text x="76" y="842" class="d-fuss">Fehlt am rechten Rand ein Punkt, wurde dort nicht gemessen.</text>
    </svg>
  </div>
  <figcaption>Ausgangsspannung über der Eingangsspannung, je Laststrom eine
  Linie. Die gestrichelte graue Linie ist der Sollwert von 5 V – je näher eine
  Kurve an ihr klebt, desto besser. Mit dem Mauszeiger auf einem Punkt gibt es
  den genauen Wert.</figcaption>
</figure>

Die Form der Kurven erzählt die Geschichte schon ohne Zahlen: Bei den beiden
UBECs oben laufen die Linien von links unten nach rechts oben – ihre
Ausgangsspannung hängt an der Eingangsspannung. Beim Buck-Boost unten liegt
alles von Anfang an flach oben am Sollwert, bis auf die gestrichelten Stücke
links, wo er aussteigt.

## Alle Messwerte

**Modul 1 – Hobbywing UBEC 3 A (max. 5 A)**

| Last | 5,5 V | 6,6 V | 7,4 V | 11,1 V | 26 V |
|---|---|---|---|---|---|
| 1 A | 3,77 V | 4,80 V | 5,12 V | 5,12 V | 5,12 V |
| 2 A | 3,05 V | 4,10 V | 4,80 V | 4,93 V | 4,93 V |
| 3 A | 2,50 V \* | 3,20 V \* | 3,60 V \* | 4,75 V | 4,75 V |
| 5 A | – | – | – | – | – |
{: .messwerte}

**Modul 2 – UBEC-Platine 5 A**

| Last | 5,5 V | 6,6 V | 7,4 V | 11,1 V | 26 V |
|---|---|---|---|---|---|
| 1 A | 4,07 V | 4,65 V | 4,74 V | 4,93 V | – |
| 2 A | 3,50 V | 4,61 V | 4,70 V | 4,56 V | – |
| 3 A | 2,80 V | 3,88 V | 4,07 V | 4,34 V | 4,44 V |
| 5 A | ✕ | ✕ | ✕ | ✕ | ✕ |
{: .messwerte}

**Modul 3 – Buck-Boost-Modul**

| Last | 5,5 V | 6,6 V | 7,4 V | 11,1 V | 26 V |
|---|---|---|---|---|---|
| 1 A | 5,09 V | 5,09 V | 5,09 V | 5,09 V | – |
| 2 A | 2,10 V \* | 4,98 V | 4,98 V | 4,98 V | – |
| 3 A | ✕ | 4,86 V | 4,87 V | 4,87 V | – |
| 5 A | ✕ | ✕ | 4,63 V | 4,62 V | 4,62 V |
{: .messwerte}

\* hält nur wenige Sekunden, dann schaltet das Modul wegen Übertemperatur ab
· ✕ kein Ausgang, das Modul läuft gar nicht erst an
· – nicht gemessen
{: .legende}

Bei 3,6 V tut sich bei Modul 3 unter Last überhaupt nichts mehr. Startet man
ihn dagegen **ohne** Last bei 3,8 V und belastet erst danach, hält er 1 A und
2 A bei rund 5 V. Ein Verhalten, mit dem man im Betrieb nicht plant.

## Was auffällt

**Ein Buck kann nicht hochsetzen.** Bei 5,5 V Eingang liefert Modul 1 gerade
noch 3,77 V, Modul 2 immerhin 4,07 V – und das schon bei gemütlichem 1 A.
Sauber wird Modul 1 erst ab 7,4 V.

**„MAX 5A“ ist bei beiden UBECs eine Behauptung.** Modul 2 liefert bei 5 A an
keiner einzigen Eingangsspannung noch etwas. Modul 1 schaltet schon bei 3 A
thermisch ab, sobald weniger als 11 V anliegen.

**Auch der Buck-Boost hat eine Grenze – sie liegt am Eingang.** Je niedriger
die Eingangsspannung, desto höher der Eingangsstrom für dieselbe Leistung. Bei
5,5 V und 2 A steigt er thermisch aus, bei 3,6 V geht unter Last gar nichts.

**Ein Teil des Spannungsabfalls steckt nicht im Regler.** Der Abfall über der
Last entspricht bei Modul 1 und 3 rund 0,1 bis 0,2 Ω – das ist die
Größenordnung von dünner Litze, Steckern und Klemmen, nicht von schlechter
Regelung. Wer die letzten Millivolt braucht, misst am Verbraucher, nicht am
Modul.

## Fazit

| Modul | Urteil |
|---|---|
| **Modul 3**<br>Buck-Boost | **Der Sieger.** Der einzige, der wirklich 5 V macht, und der einzige, der 5 A schafft. Ab 6,6 V Eingang ohne Einschränkung brauchbar. |
| **Modul 1**<br>Hobbywing | Brauchbar für kleine Lasten ab 7,4 V aufwärts. Solide gebaut, aber lastschwach – und die 5 A auf dem Aufkleber sind Fiktion. |
| **Modul 2**<br>UBEC-Platine | Erreicht in keiner einzigen Messung 5 V. Bester Wert überhaupt: 4,93 V. Ich werde ihn nicht einbauen. |

Wer aus einem 2S- oder 3S-Akku ordentlich Strom bei 5 V braucht, nimmt den
Buck-Boost – der ist auch der einzige, der noch mitmacht, wenn die Zelle auf
dem Rückweg vom Berg langsam leer wird.

Modul 1 behalte ich trotzdem: Es ist das einzige mit Blechgehäuse und
Ferritringkern, also das einzige, bei dem sich jemand Gedanken über die
abgestrahlte Störung gemacht hat. Für einen Empfänger direkt daneben kann das
mehr wert sein als das letzte halbe Volt. Ob es wirklich leiser ist, weiß ich
allerdings nicht – gemessen habe ich hier nur Spannungen, keine Störungen. Das
wäre ein eigener Nachmittag mit dem SDR.

---

Die drei Module bei AliExpress, ohne Affiliate-Kram und ohne Empfehlung – nur
damit nachvollziehbar ist, was gemessen wurde:
[Modul 1](https://de.aliexpress.com/item/1005010265933337.html) ·
[Modul 2](https://de.aliexpress.com/item/1005009444909052.html) ·
[Modul 3](https://de.aliexpress.com/item/1005008431252487.html)
