---
layout: beitrag
title: "Drei DC-DC-Wandler am Prüfstand – nur einer hält, was draufsteht"
date: 2026-08-26 19:30:00 +0200
tags: [Elektronik, Messtechnik]
---

Fünf Volt aus einem Akku zu machen, klingt nach einem gelösten Problem. Auf
allen drei Modulen, die vergangenes Wochenende bei mir auf dem Tisch lagen,
steht auch souverän **5 V** und **bis 5 A**. Nachgemessen liefert davon genau
**einer** verlässlich fünf Volt.

## Die drei Kandidaten

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/01-hobbywing-ubec.jpg"
         alt="Hobbywing UBEC im silbernen Blechgehäuse mit angelöteten
              Leitungen und einem grünen Ferritringkern im Ausgangskabel">
  </a>
  <figcaption>Modul 1 – Hobbywing UBEC, 3 A Dauerstrom, „MAX 5A“. Als einziges
  im Blechgehäuse, mit Ferritringkern im Kabel.</figcaption>
</figure>

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/02-ubec-5a-platine.jpg"
         alt="Kleine blaue Platine im durchsichtigen Schrumpfschlauch, zwei
              Elkos, Schaltregler-IC und Speicherdrossel mit Aufdruck UBEC 5A">
  </a>
  <figcaption>Modul 2 – nackte Reglerplatine im Schrumpfschlauch, Aufkleber
  „UBEC 5A“ auf der Drossel.</figcaption>
</figure>

<figure class="abb klein">
  <a href="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg">
    <img src="/assets/2026-08-26-dc-dc-wandler-im-test/03-buck-boost-modul.jpg"
         alt="Blaue Platine mit geschirmter Speicherdrossel, QFN-Chip,
              zwei Elkos und Lötpads für IN plus, IN minus, OUT plus,
              OUT minus und EN">
  </a>
  <figcaption>Modul 3 – Buck-Boost-Modul mit geschirmter Drossel und
  Enable-Eingang.</figcaption>
</figure>

Module 1 und 2 sind **UBECs**, also reine Abwärtswandler: Sie können eine
Spannung nur herunterregeln, niemals hinauf. Modul 3 ist ein
**Buck-Boost-Wandler** und kann beides. Genau das war die Frage.

## Gemessen

Jedes Modul bekam 5,5 V, 6,6 V, 7,4 V, 11,1 V und 26 V vorgesetzt und wurde
dabei mit 1 A, 2 A, 3 A und – wo das ging – mit 5 A belastet. Die 6,6 V sind
kein Zufall: Da ist ein 2S-LiPo leer. Modul 3 lief zusätzlich an 3,6 V, also
einer einzelnen Li-Ion-Zelle.

<figure class="abb">
  <div class="rahmen">
<svg viewBox="0 0 760 889" xmlns="http://www.w3.org/2000/svg" role="img" aria-labelledby="diagTitel diagDesc" class="messdiagramm">
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
    <line x1="76" y1="265.0" x2="676" y2="265.0" class="d-grid"/>
    <text x="67" y="269.0" class="d-ytext">0</text>
    <line x1="76" y1="238.2" x2="676" y2="238.2" class="d-grid"/>
    <text x="67" y="242.2" class="d-ytext">1</text>
    <line x1="76" y1="211.3" x2="676" y2="211.3" class="d-grid"/>
    <text x="67" y="215.3" class="d-ytext">2</text>
    <line x1="76" y1="184.5" x2="676" y2="184.5" class="d-grid"/>
    <text x="67" y="188.5" class="d-ytext">3</text>
    <line x1="76" y1="157.7" x2="676" y2="157.7" class="d-grid"/>
    <text x="67" y="161.7" class="d-ytext">4</text>
    <line x1="76" y1="130.8" x2="676" y2="130.8" class="d-soll"/>
    <text x="67" y="134.8" class="d-ytext">5</text>
    <line x1="76" y1="104.0" x2="676" y2="104.0" class="d-grid"/>
    <text x="67" y="108.0" class="d-ytext">6</text>
    <line x1="76.0" y1="104.0" x2="76.0" y2="265.0" class="d-vgrid"/>
    <text x="76.0" y="286" class="d-xtext">5,5 V</text>
    <line x1="226.0" y1="104.0" x2="226.0" y2="265.0" class="d-vgrid"/>
    <text x="226.0" y="286" class="d-xtext">6,6 V</text>
    <line x1="376.0" y1="104.0" x2="376.0" y2="265.0" class="d-vgrid"/>
    <text x="376.0" y="286" class="d-xtext">7,4 V</text>
    <line x1="526.0" y1="104.0" x2="526.0" y2="265.0" class="d-vgrid"/>
    <text x="526.0" y="286" class="d-xtext">11,1 V</text>
    <line x1="676.0" y1="104.0" x2="676.0" y2="265.0" class="d-vgrid"/>
    <text x="676.0" y="286" class="d-xtext">26 V</text>
    <line x1="76" y1="265.0" x2="676" y2="265.0" class="d-axis"/>
    <line x1="76.0" y1="163.8" x2="226.0" y2="136.2" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="136.2" x2="376.0" y2="127.6" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="127.6" x2="526.0" y2="127.6" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="127.6" x2="676.0" y2="127.6" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 1 A: 3,77 V</title><circle cx="76.0" cy="163.8" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 1 A: 4,80 V</title><circle cx="226.0" cy="136.2" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 1 A: 5,12 V</title><circle cx="376.0" cy="127.6" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 1 A: 5,12 V</title><circle cx="526.0" cy="127.6" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 1 A: 5,12 V</title><circle cx="676.0" cy="127.6" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="183.2" x2="226.0" y2="155.0" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="155.0" x2="376.0" y2="136.2" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="136.2" x2="526.0" y2="132.7" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="132.7" x2="676.0" y2="132.7" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 2 A: 3,05 V</title><circle cx="76.0" cy="183.2" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 2 A: 4,10 V</title><circle cx="226.0" cy="155.0" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 2 A: 4,80 V</title><circle cx="376.0" cy="136.2" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 2 A: 4,93 V</title><circle cx="526.0" cy="132.7" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 2 A: 4,93 V</title><circle cx="676.0" cy="132.7" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="197.9" x2="226.0" y2="179.1" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="226.0" y1="179.1" x2="376.0" y2="168.4" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="376.0" y1="168.4" x2="526.0" y2="137.5" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="526.0" y1="137.5" x2="676.0" y2="137.5" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 3 A: 2,50 V, fällt nach Sekunden ab</title><circle cx="76.0" cy="197.9" r="4.5" class="d-open" stroke="#1c5cab"/></g>
    <g data-p="1"><title>6,6 V bei 3 A: 3,20 V, fällt nach Sekunden ab</title><circle cx="226.0" cy="179.1" r="4.5" class="d-open" stroke="#1c5cab"/></g>
    <g data-p="1"><title>7,4 V bei 3 A: 3,60 V, fällt nach Sekunden ab</title><circle cx="376.0" cy="168.4" r="4.5" class="d-open" stroke="#1c5cab"/></g>
    <g data-p="1"><title>11,1 V bei 3 A: 4,75 V</title><circle cx="526.0" cy="137.5" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 3 A: 4,75 V</title><circle cx="676.0" cy="137.5" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    </g>
    <g>
    <text x="68" y="347" class="d-ptitel">Modul 2 · UBEC-Platine 5 A</text>
    <line x1="76" y1="520.0" x2="676" y2="520.0" class="d-grid"/>
    <text x="67" y="524.0" class="d-ytext">0</text>
    <line x1="76" y1="493.2" x2="676" y2="493.2" class="d-grid"/>
    <text x="67" y="497.2" class="d-ytext">1</text>
    <line x1="76" y1="466.3" x2="676" y2="466.3" class="d-grid"/>
    <text x="67" y="470.3" class="d-ytext">2</text>
    <line x1="76" y1="439.5" x2="676" y2="439.5" class="d-grid"/>
    <text x="67" y="443.5" class="d-ytext">3</text>
    <line x1="76" y1="412.7" x2="676" y2="412.7" class="d-grid"/>
    <text x="67" y="416.7" class="d-ytext">4</text>
    <line x1="76" y1="385.8" x2="676" y2="385.8" class="d-soll"/>
    <text x="67" y="389.8" class="d-ytext">5</text>
    <line x1="76" y1="359.0" x2="676" y2="359.0" class="d-grid"/>
    <text x="67" y="363.0" class="d-ytext">6</text>
    <line x1="76.0" y1="359.0" x2="76.0" y2="520.0" class="d-vgrid"/>
    <text x="76.0" y="541" class="d-xtext">5,5 V</text>
    <line x1="226.0" y1="359.0" x2="226.0" y2="520.0" class="d-vgrid"/>
    <text x="226.0" y="541" class="d-xtext">6,6 V</text>
    <line x1="376.0" y1="359.0" x2="376.0" y2="520.0" class="d-vgrid"/>
    <text x="376.0" y="541" class="d-xtext">7,4 V</text>
    <line x1="526.0" y1="359.0" x2="526.0" y2="520.0" class="d-vgrid"/>
    <text x="526.0" y="541" class="d-xtext">11,1 V</text>
    <line x1="676.0" y1="359.0" x2="676.0" y2="520.0" class="d-vgrid"/>
    <text x="676.0" y="541" class="d-xtext">26 V</text>
    <line x1="76" y1="520.0" x2="676" y2="520.0" class="d-axis"/>
    <line x1="76.0" y1="410.8" x2="226.0" y2="395.2" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="395.2" x2="376.0" y2="392.8" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="392.8" x2="526.0" y2="387.7" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 1 A: 4,07 V</title><circle cx="76.0" cy="410.8" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 1 A: 4,65 V</title><circle cx="226.0" cy="395.2" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 1 A: 4,74 V</title><circle cx="376.0" cy="392.8" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 1 A: 4,93 V</title><circle cx="526.0" cy="387.7" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="426.1" x2="226.0" y2="396.3" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="396.3" x2="376.0" y2="393.9" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="393.9" x2="526.0" y2="391.2" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 2 A: 3,50 V</title><circle cx="76.0" cy="426.1" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 2 A: 4,61 V</title><circle cx="226.0" cy="396.3" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 2 A: 4,70 V</title><circle cx="376.0" cy="393.9" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 2 A: 4,80 V</title><circle cx="526.0" cy="391.2" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="444.9" x2="226.0" y2="415.9" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="415.9" x2="376.0" y2="410.8" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="410.8" x2="526.0" y2="403.5" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="403.5" x2="676.0" y2="400.9" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 3 A: 2,80 V</title><circle cx="76.0" cy="444.9" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 3 A: 3,88 V</title><circle cx="226.0" cy="415.9" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 3 A: 4,07 V</title><circle cx="376.0" cy="410.8" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 3 A: 4,34 V</title><circle cx="526.0" cy="403.5" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 3 A: 4,44 V</title><circle cx="676.0" cy="400.9" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>5,5 V bei 5 A: kein Ausgang</title><path d="M71.5 508.5 l9 9 M80.5 508.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>6,6 V bei 5 A: kein Ausgang</title><path d="M221.5 508.5 l9 9 M230.5 508.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>7,4 V bei 5 A: kein Ausgang</title><path d="M371.5 508.5 l9 9 M380.5 508.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>11,1 V bei 5 A: kein Ausgang</title><path d="M521.5 508.5 l9 9 M530.5 508.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>26 V bei 5 A: kein Ausgang</title><path d="M671.5 508.5 l9 9 M680.5 508.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    </g>
    <g>
    <text x="68" y="602" class="d-ptitel">Modul 3 · Buck-Boost-Modul</text>
    <line x1="76" y1="775.0" x2="676" y2="775.0" class="d-grid"/>
    <text x="67" y="779.0" class="d-ytext">0</text>
    <line x1="76" y1="748.2" x2="676" y2="748.2" class="d-grid"/>
    <text x="67" y="752.2" class="d-ytext">1</text>
    <line x1="76" y1="721.3" x2="676" y2="721.3" class="d-grid"/>
    <text x="67" y="725.3" class="d-ytext">2</text>
    <line x1="76" y1="694.5" x2="676" y2="694.5" class="d-grid"/>
    <text x="67" y="698.5" class="d-ytext">3</text>
    <line x1="76" y1="667.7" x2="676" y2="667.7" class="d-grid"/>
    <text x="67" y="671.7" class="d-ytext">4</text>
    <line x1="76" y1="640.8" x2="676" y2="640.8" class="d-soll"/>
    <text x="67" y="644.8" class="d-ytext">5</text>
    <line x1="76" y1="614.0" x2="676" y2="614.0" class="d-grid"/>
    <text x="67" y="618.0" class="d-ytext">6</text>
    <line x1="76.0" y1="614.0" x2="76.0" y2="775.0" class="d-vgrid"/>
    <text x="76.0" y="796" class="d-xtext">5,5 V</text>
    <line x1="226.0" y1="614.0" x2="226.0" y2="775.0" class="d-vgrid"/>
    <text x="226.0" y="796" class="d-xtext">6,6 V</text>
    <line x1="376.0" y1="614.0" x2="376.0" y2="775.0" class="d-vgrid"/>
    <text x="376.0" y="796" class="d-xtext">7,4 V</text>
    <line x1="526.0" y1="614.0" x2="526.0" y2="775.0" class="d-vgrid"/>
    <text x="526.0" y="796" class="d-xtext">11,1 V</text>
    <line x1="676.0" y1="614.0" x2="676.0" y2="775.0" class="d-vgrid"/>
    <text x="676.0" y="796" class="d-xtext">26 V</text>
    <line x1="76" y1="775.0" x2="676" y2="775.0" class="d-axis"/>
    <line x1="76.0" y1="638.4" x2="226.0" y2="638.4" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="226.0" y1="638.4" x2="376.0" y2="638.4" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="638.4" x2="526.0" y2="638.4" stroke="#86b6ef" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 1 A: 5,09 V</title><circle cx="76.0" cy="638.4" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>6,6 V bei 1 A: 5,09 V</title><circle cx="226.0" cy="638.4" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 1 A: 5,09 V</title><circle cx="376.0" cy="638.4" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 1 A: 5,09 V</title><circle cx="526.0" cy="638.4" r="4.5" fill="#86b6ef" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="718.6" x2="226.0" y2="641.4" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="226.0" y1="641.4" x2="376.0" y2="641.4" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="641.4" x2="526.0" y2="641.4" stroke="#3987e5" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 2 A: 2,10 V, fällt nach Sekunden ab</title><circle cx="76.0" cy="718.6" r="4.5" class="d-open" stroke="#3987e5"/></g>
    <g data-p="1"><title>6,6 V bei 2 A: 4,98 V</title><circle cx="226.0" cy="641.4" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 2 A: 4,98 V</title><circle cx="376.0" cy="641.4" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 2 A: 4,98 V</title><circle cx="526.0" cy="641.4" r="4.5" fill="#3987e5" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="76.0" y1="775.0" x2="226.0" y2="644.6" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="226.0" y1="644.6" x2="376.0" y2="644.3" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="376.0" y1="644.3" x2="526.0" y2="644.3" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 3 A: kein Ausgang</title><path d="M71.5 763.5 l9 9 M80.5 763.5 l-9 9" stroke="#1c5cab" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>6,6 V bei 3 A: 4,86 V</title><circle cx="226.0" cy="644.6" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>7,4 V bei 3 A: 4,87 V</title><circle cx="376.0" cy="644.3" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 3 A: 4,87 V</title><circle cx="526.0" cy="644.3" r="4.5" fill="#1c5cab" stroke="#ffffff" stroke-width="2"/></g>
    <line x1="226.0" y1="775.0" x2="376.0" y2="650.8" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" stroke-dasharray="5 4"/>
    <line x1="376.0" y1="650.8" x2="526.0" y2="651.0" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round"/>
    <line x1="526.0" y1="651.0" x2="676.0" y2="651.0" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round"/>
    <g data-p="1"><title>5,5 V bei 5 A: kein Ausgang</title><path d="M86.5 763.5 l9 9 M95.5 763.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>6,6 V bei 5 A: kein Ausgang</title><path d="M221.5 763.5 l9 9 M230.5 763.5 l-9 9" stroke="#0d366b" stroke-width="2.5" stroke-linecap="round" fill="none"/></g>
    <g data-p="1"><title>7,4 V bei 5 A: 4,63 V</title><circle cx="376.0" cy="650.8" r="4.5" fill="#0d366b" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>11,1 V bei 5 A: 4,62 V</title><circle cx="526.0" cy="651.0" r="4.5" fill="#0d366b" stroke="#ffffff" stroke-width="2"/></g>
    <g data-p="1"><title>26 V bei 5 A: 4,62 V</title><circle cx="676.0" cy="651.0" r="4.5" fill="#0d366b" stroke="#ffffff" stroke-width="2"/></g>
    </g>
    <text x="76" y="863" class="d-fuss">waagerecht: angelegte Eingangsspannung (Abstände nicht maßstäblich) · senkrecht: Ausgangsspannung in Volt</text>
    <text x="76" y="881" class="d-fuss">Fehlt am rechten Rand ein Punkt, wurde dort nicht gemessen.</text>
    </svg>
  </div>
  <figcaption>Ausgangsspannung über der Eingangsspannung, je Laststrom eine
  Linie. Gestrichelt grau der 5-V-Sollwert – je näher eine Kurve an ihm klebt,
  desto besser. Mauszeiger auf einen Punkt gibt den genauen Wert.</figcaption>
</figure>

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
| 2 A | 3,50 V | 4,61 V | 4,70 V | 4,80 V | – |
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

Bei 3,6 V tut sich bei Modul 3 unter Last nichts mehr. Ohne Last bei 3,8 V
gestartet hält er hinterher 1 A und 2 A bei rund 5 V – damit plant man nicht.

## Was auffällt

**Ein Buck kann nicht hochsetzen.** Bei 5,5 V Eingang liefert Modul 1 gerade
noch 3,77 V, Modul 2 4,07 V – und das schon bei gemütlichem 1 A. Sauber wird
Modul 1 erst ab 7,4 V.

**„MAX 5A“ ist bei beiden UBECs eine Behauptung.** Modul 2 liefert bei 5 A an
keiner Eingangsspannung noch etwas, Modul 1 schaltet schon bei 3 A thermisch
ab, sobald weniger als 11 V anliegen.

**Auch der Buck-Boost hat eine Grenze – sie liegt am Eingang.** Je niedriger
die Eingangsspannung, desto höher der Eingangsstrom für dieselbe Leistung. Bei
5,5 V und 2 A steigt er thermisch aus.

**Ein Teil des Abfalls steckt nicht im Regler.** Der Lastabfall entspricht bei
Modul 1 und 3 rund 0,1 bis 0,2 Ω – die Größenordnung von Litze und Steckern.
Wer die letzten Millivolt braucht, misst am Verbraucher.

## Fazit

| Modul | Urteil |
|---|---|
| **Modul 3**<br>Buck-Boost | **Der Sieger.** Der einzige mit echten 5 V, der einzige mit 5 A. Ab 6,6 V Eingang ohne Einschränkung brauchbar. |
| **Modul 1**<br>Hobbywing | Brauchbar für kleine Lasten ab 7,4 V. Solide gebaut, aber lastschwach – die 5 A auf dem Aufkleber sind Fiktion. |
| **Modul 2**<br>UBEC-Platine | Erreicht in keiner Messung 5 V, bester Wert 4,93 V. Ich werde ihn nicht einbauen. |

Wer aus 2S oder 3S ordentlich Strom bei 5 V braucht, nimmt den Buck-Boost.
Modul 1 behalte ich trotzdem: Es ist das einzige mit Blechgehäuse und
Ferritringkern, und für einen Empfänger direkt daneben kann das mehr wert sein
als das letzte halbe Volt. Ob es wirklich leiser ist, weiß ich allerdings
nicht – gemessen habe ich hier nur Spannungen, keine Störungen.

---

Die drei Module bei AliExpress, ohne Affiliate-Kram und ohne Empfehlung – nur
damit nachvollziehbar ist, was gemessen wurde:
[Modul 1](https://de.aliexpress.com/item/1005010265933337.html) ·
[Modul 2](https://de.aliexpress.com/item/1005009444909052.html) ·
[Modul 3](https://de.aliexpress.com/item/1005008431252487.html)
