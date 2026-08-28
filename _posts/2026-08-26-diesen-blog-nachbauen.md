---
layout: beitrag
title: "So baust du dir diesen Blog nach – kostenlos und ohne Server"
date: 2026-08-26 09:00:00 +0200
tags: [Alltag, Webseite]
---

Diese Seite kostet nichts. Kein Server, keine Datenbank, kein WordPress,
keine monatliche Rechnung. Geschrieben wird in einfachen Textdateien, den
Rest erledigt GitHub. Wer sich dasselbe bauen will: hier ist der komplette
Weg. Gebraucht werden ein GitHub-Konto und ein Browser.

Dahinter steckt **Jekyll**: ein Programm, das aus Markdown-Textdateien
fertige HTML-Seiten baut. **GitHub Pages** lässt Jekyll nach jedem Hochladen
automatisch laufen und veröffentlicht das Ergebnis. Lokal muss dafür nichts
installiert werden.

## Schritt 1 – Konto und Repository

Auf [github.com](https://github.com) ein Konto anlegen. Der Benutzername
wird Teil der Adresse, also mit Bedacht wählen.

Dann ein neues Repository anlegen – so heißt bei GitHub ein Projektordner.
Der Name muss **exakt** `benutzername.github.io` lauten, sonst funktioniert
der Rest nicht:

- Name: `benutzername.github.io`
- Sichtbarkeit: **Public**
- Haken bei „Add a README file"

## Schritt 2 – Seite einschalten

Im Repository auf **Settings → Pages**, dann unter *Source* auswählen:
**Deploy from a branch**, Branch `main`, Ordner `/ (root)`, speichern.

Ein bis zwei Minuten später ist die Seite unter
`https://benutzername.github.io` erreichbar.

## Schritt 3 – Die Dateien anlegen

Alle Dateien lassen sich direkt im Browser anlegen: **Add file → Create new
file**. Ordner entstehen dabei von selbst, indem man einen Schrägstrich in
den Dateinamen schreibt, also `_layouts/beitrag.html`.

Das ist das ganze Gerüst:

```
_config.yml       Grundeinstellungen
index.md          Startseite mit der Beitragsliste
themen.md         Übersicht aller Tags, füllt sich von selbst
ueber-mich.md     Über mich
impressum.md      Impressum
datenschutz.md    Datenschutzerklärung
_posts/           die Beiträge, Dateiname JJJJ-MM-TT-titel.md
_layouts/         beitrag.html – Beitragslayout
assets/           Bilder, ein Unterordner je Beitrag
```

<details markdown="1">
<summary><strong>_config.yml</strong> – zum Kopieren</summary>

Nur die ersten vier Zeilen anpassen.

```yaml
title: Mein Blog
description: Worum es hier geht
author: Vorname Nachname
url: https://benutzername.github.io
lang: de
timezone: Europe/Berlin
permalink: /:year/:title/
show_excerpts: true
theme: minima

# Datumsformat deutsch statt "Aug 25, 2026"
minima:
  date_format: "%d.%m.%Y"

header_pages:
  - index.md
  - themen.md
  - ueber-mich.md
  - impressum.md
  - datenschutz.md

exclude:
  - README.md

# Beiträge nutzen automatisch das Layout "beitrag"
defaults:
  - scope:
      path: ""
      type: posts
    values:
      layout: beitrag

plugins:
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-sitemap
```

`theme: minima` ist das Standard-Theme von GitHub Pages – schlicht, schnell
und ohne Installation nutzbar.

</details>

<details markdown="1">
<summary><strong>index.md</strong> und <strong>themen.md</strong> – zum Kopieren</summary>

`index.md` – die Startseite mit der Beitragsliste:

```markdown
---
layout: home
title: Beiträge
list_title: Beiträge
---

<style>
  /* Das Theme setzt hier zwei gleiche Überschriften. Die zweite weg. */
  .home > .post-list-heading { display: none; }
</style>
```

`themen.md` – die Themenübersicht. Sie füllt sich automatisch aus den Tags
aller Beiträge, es ist also nie etwas nachzupflegen:

{% raw %}
```liquid
---
layout: page
title: Themen
permalink: /themen/
---

{% assign alle_tags = site.tags | sort %}
{% if alle_tags.size == 0 %}

Hier sammeln sich die Beiträge nach Themen, sobald die ersten
geschrieben sind.

{% else %}

<p>
{% for tag in alle_tags %}
  <a href="#{{ tag[0] | slugify }}">{{ tag[0] }}</a> ({{ tag[1].size }}){% unless forloop.last %} · {% endunless %}
{% endfor %}
</p>

{% for tag in alle_tags %}
<h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
<ul>
  {% for post in tag[1] %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <small>– {{ post.date | date: "%d.%m.%Y" }}</small>
  </li>
  {% endfor %}
</ul>
{% endfor %}

{% endif %}
```
{% endraw %}

Eine eigene Seite wie `ueber-mich.md` besteht nur aus diesem Kopf und dem
Text darunter:

```markdown
---
layout: page
title: Über mich
permalink: /ueber-mich/
---

Hier steht der Text.
```

</details>

<details markdown="1">
<summary><strong>_layouts/beitrag.html</strong> – Bilder mit Rahmen und die Tag-Zeile</summary>

Das ist das normale Beitragslayout plus zwei Zutaten: Bilder in einem
Rahmen samt automatisch durchnummerierter Bildunterschrift und die Zeile
`Themen: …` am Ende jedes Beitrags, die auf die Themenseite zurückverlinkt.

{% raw %}
```html
---
layout: post
---
<style>
  /* Bilder mit Rahmen und Bildunterschrift. Im Beitrag:

       <figure class="abb klein">
         <a href="/assets/BEITRAG/01-bild.jpg">
           <img src="/assets/BEITRAG/01-bild.jpg" alt="Alternativtext">
         </a>
         <figcaption>Beschreibung.</figcaption>
       </figure>

     Die Nummer "Abb. 1", "Abb. 2" … setzt der Browser selbst davor.  */

  .post-content { counter-reset: abb; }
  .abb { margin: 2.2em 0; }

  /* "klein" = schmaler und mittig statt über die volle Textbreite */
  .abb.klein { max-width: 440px; margin-left: auto; margin-right: auto; }

  .abb > a {
    display: block;
    padding: 8px;
    background: #fff;
    border: 1px solid #e0e0dd;
    border-radius: 6px;
    line-height: 0;
  }
  .abb img { display: block; width: 100%; height: auto; border-radius: 3px; }

  .abb figcaption {
    margin-top: .75em;
    font-size: .88em;
    line-height: 1.5;
    color: #828282;
    text-align: center;
  }
  .abb figcaption::before {
    counter-increment: abb;
    content: "Abb. " counter(abb) " · ";
    font-weight: 600;
    color: #424242;
  }

  /* Tabellen: nur so breit wie nötig, seitlich scrollbar.
     Im Beitrag  {: .messwerte}  direkt unter die Tabelle schreiben. */
  .post-content .messwerte {
    display: block;
    width: max-content;
    max-width: 100%;
    overflow-x: auto;
    font-size: .92em;
  }
  .messwerte td, .messwerte th { white-space: nowrap; }
  .messwerte td + td, .messwerte th + th { text-align: right; }

  /* Kleingedruckte Zeile unter einer Tabelle:  {: .legende}  */
  .post-content .legende {
    margin-top: -1.4em;
    font-size: .88em;
    line-height: 1.5;
    color: #828282;
  }
</style>

{{ content }}

{%- if page.tags.size > 0 %}
<p class="post-tags">
  Themen:
  {%- for tag in page.tags %}
  <a href="{{ '/themen/' | relative_url }}#{{ tag | slugify }}">{{ tag }}</a>
  {%- unless forloop.last %} · {% endunless -%}
  {%- endfor %}
</p>

<style>
  .post-tags {
    margin-top: 2em;
    padding-top: 1em;
    border-top: 1px solid #e8e8e8;
    font-size: 0.9em;
    color: #828282;
  }
</style>
{%- endif %}
```
{% endraw %}

</details>

## Schritt 4 – Der erste Beitrag

Beiträge liegen in `_posts/` und heißen **immer** `JJJJ-MM-TT-titel.md`,
zum Beispiel `_posts/2026-08-26-mein-erster-beitrag.md`. Oben im Kopf
stehen Titel, Datum und Tags, darunter der Text in Markdown.

Zwei Stolpersteine, die jeden einmal erwischen:

- **Das Datum muss in der Vergangenheit liegen.** Jekyll überspringt
  zukünftig datierte Beiträge stillschweigend – der Build meldet trotzdem
  „erfolgreich", die Seite ist aber nicht da.
- **Der Dateiname muss dem Muster folgen.** Alles andere wird nicht als
  Beitrag erkannt.

<details markdown="1">
<summary><strong>Vorlage für einen Beitrag</strong> – zum Kopieren</summary>

Diese Datei einmal als `_drafts/vorlage.md` ablegen und für jeden neuen
Beitrag nach `_posts/` kopieren. Der Kommentarblock erscheint auf der
fertigen Seite nicht und kann stehen bleiben.

````markdown
---
layout: beitrag
title: "TITEL HIER EINTRAGEN"
date: 2026-08-26 09:00:00 +0200
tags: [Elektronik]
---

Hier den Beitrag schreiben.

<!--
  WICHTIG: Das Datum oben muss in der VERGANGENHEIT liegen, sonst baut
  Jekyll den Beitrag nicht mit. Dateiname immer JJJJ-MM-TT-titel.md


  ── TAGS ──────────────────────────────────────────────────────────

  Tags sind die Themen-Schubladen. Jeder Beitrag kann in mehreren
  gleichzeitig liegen. Alle Tags samt ihrer Beiträge erscheinen
  automatisch auf der Seite /themen/.

      tags: [Amateurfunk]
      tags: [Amateurfunk, Antennenbau]
      tags: [Elektronik, "Raspberry Pi"]     <- mehrere Wörter in "..."

  Groß-/Kleinschreibung zählt: "Amateurfunk" und "amateurfunk" landen in
  zwei getrennten Schubladen. Zwei bis vier Tags pro Beitrag sind ein
  guter Schnitt. Am besten eine feste Liste bewährter Tags führen und
  von dort abschreiben.


  ── BILDER ────────────────────────────────────────────────────────

  Pro Beitrag ein eigener Ordner unter assets/, benannt exakt wie die
  Beitragsdatei ohne .md:

      _posts/2026-09-14-antenne-fuer-2m.md
      assets/2026-09-14-antenne-fuer-2m/01-material.jpg
      assets/2026-09-14-antenne-fuer-2m/02-aufbau.jpg

  Dateinamen klein schreiben, keine Leerzeichen, keine Umlaute, und
  sagen, was drauf ist. Die Nummer nach vorne, dann stimmt die
  Reihenfolge schon im Dateimanager.

  Einbinden mit führendem Schrägstrich, Alternativtext immer ausfüllen:

      ![Fertige Antenne am Mast](/assets/2026-09-14-antenne-fuer-2m/02-aufbau.jpg)

  Mit Rahmen und Bildunterschrift, Klick öffnet das Bild groß:

      <figure class="abb klein">
        <a href="/assets/BEITRAG/01-bild.jpg">
          <img src="/assets/BEITRAG/01-bild.jpg" alt="Alternativtext">
        </a>
        <figcaption>Beschreibung des Bildes.</figcaption>
      </figure>

  Fotos aus der Kamera sind viel zu groß. Vorher auf etwa 1600 Pixel
  Breite verkleinern, Ziel sind rund 300 KB je Bild:

      magick original.jpg -resize 1600x -quality 82 01-aufbau.jpg

  Fotos als .jpg, Screenshots und Zeichnungen als .png.

  Achtung: Was einmal hochgeladen ist, bleibt für immer in der
  Historie – auch nach dem Löschen. Also vorher verkleinern.
-->

## Zwischenüberschrift

Text mit **fett**, *kursiv* und [einem Link](https://example.com).

```python
print("Hallo Welt")
```
````

</details>

## Schritt 5 – Die Adresse

Drei Wege, vom einfachsten zum aufwendigsten.

**a) Alles so lassen.** Die Seite läuft unter
`https://benutzername.github.io`. Nichts zu tun, HTTPS ist inklusive,
kostet nichts. Für die meisten reicht das.

**b) Eigene Domain als Weiterleitung.** So läuft es hier: Die Domain
`online-weber.de` liegt bei einem Anbieter, der sie per **HTTP-Weiterleitung**
auf `technikweber.github.io` schickt. Beim Anbieter dafür „Weiterleitung"
oder „Redirect" einrichten, Ziel ist die vollständige Adresse mit `https://`.
Vorteil: geht mit jedem Billig-Tarif und ohne DNS-Gefummel. Nachteil: In der
Adresszeile steht nach dem Sprung wieder `benutzername.github.io`. In
`_config.yml` bleibt `url:` deshalb auf der github.io-Adresse.

**c) Eigene Domain richtig einhängen.** Dann bleibt die Domain in der
Adresszeile. Beim Domain-Anbieter im DNS anlegen:

- für `www.beispiel.de` einen **CNAME** auf `benutzername.github.io`
- für `beispiel.de` ohne www vier **A-Records** auf `185.199.108.153`,
  `185.199.109.153`, `185.199.110.153` und `185.199.111.153`

Danach im Repository unter **Settings → Pages → Custom domain** die Domain
eintragen und, sobald der Haken anwählbar ist, **Enforce HTTPS**
ankreuzen – das Zertifikat stellt GitHub kostenlos aus. In `_config.yml`
dann `url: https://beispiel.de` setzen. Die aktuellen Adressen und
AAAA-Records stehen in der
[GitHub-Dokumentation](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site).

## Schritt 6 – Impressum und Datenschutz

Ein Blog aus Deutschland braucht beides, auch privat. Die folgenden Fassungen
sind meine – als Ausgangspunkt gedacht, nicht als Vorlage von der Stange.

> **Wichtig: rechtlich nicht geprüft.** Das ist kein Rechtsrat, sondern das,
> was ich für meine eigene statische Seite ohne Kommentare und ohne Tracking
> zusammengestellt habe. Jede Seite liegt anders. Wer sichergehen will, lässt
> es prüfen.

<details markdown="1">
<summary><strong>Impressum</strong> – zum Kopieren (rechtlich nicht geprüft)</summary>

Als `impressum.md` anlegen, Platzhalter ersetzen.

```markdown
---
layout: page
title: Impressum
permalink: /impressum/
---

## Angaben gemäß § 5 DDG

Vorname Nachname<br>
Straße Hausnummer<br>
PLZ Ort<br>
Deutschland

## Kontakt

E-Mail: mail@beispiel.de

## Verantwortlich für den Inhalt nach § 18 Abs. 2 MStV

Vorname Nachname<br>
Straße Hausnummer<br>
PLZ Ort<br>
Deutschland

## Haftung für Inhalte

Die Inhalte dieser Seiten wurden mit größter Sorgfalt erstellt. Für die
Richtigkeit, Vollständigkeit und Aktualität der Inhalte kann ich jedoch
keine Gewähr übernehmen. Als Diensteanbieter bin ich gemäß § 7 Abs. 1 DDG
für eigene Inhalte auf diesen Seiten nach den allgemeinen Gesetzen
verantwortlich. Nach §§ 8 bis 10 DDG bin ich als Diensteanbieter jedoch
nicht verpflichtet, übermittelte oder gespeicherte fremde Informationen zu
überwachen oder nach Umständen zu forschen, die auf eine rechtswidrige
Tätigkeit hinweisen.

## Haftung für Links

Mein Angebot enthält Links zu externen Websites Dritter, auf deren Inhalte
ich keinen Einfluss habe. Deshalb kann ich für diese fremden Inhalte auch
keine Gewähr übernehmen. Für die Inhalte der verlinkten Seiten ist stets der
jeweilige Anbieter oder Betreiber der Seiten verantwortlich. Bei
Bekanntwerden von Rechtsverletzungen werde ich derartige Links umgehend
entfernen.

## Haftung für Anleitungen und Code-Beispiele

Sämtliche auf dieser Website veröffentlichten Anleitungen, Code-Beispiele und
technischen Hinweise werden ohne Gewähr bereitgestellt. Die Umsetzung erfolgt
auf eigene Verantwortung und eigenes Risiko. Für etwaige Schäden, die aus der
Nutzung oder Nichtnutzung der dargestellten Informationen entstehen, wird
keine Haftung übernommen.

## Urheberrecht

Die durch den Seitenbetreiber erstellten Inhalte und Werke auf diesen Seiten
unterliegen dem deutschen Urheberrecht. Beiträge Dritter sind als solche
gekennzeichnet. Sofern nicht anders angegeben, dürfen Code-Beispiele im
Rahmen der jeweils angegebenen Lizenz verwendet werden.
```

Wer über Elektronik oder Arbeiten an elektrischen Anlagen schreibt, sollte
zusätzlich einen deutlichen Sicherheits- und Haftungshinweis aufnehmen – auf
[meinem Impressum](/impressum/) steht er unter „Arbeiten an elektrischen
Anlagen".

</details>

<details markdown="1">
<summary><strong>Datenschutzerklärung</strong> – zum Kopieren (rechtlich nicht geprüft)</summary>

Als `datenschutz.md` anlegen. Abschnitt 4 nur übernehmen, wenn eine
Weiterleitung wie in Schritt 5b eingerichtet ist – sonst löschen.

```markdown
---
layout: page
title: Datenschutzerklärung
permalink: /datenschutz/
---

## 1. Verantwortlicher

Verantwortlich für die Datenverarbeitung auf dieser Website ist:

Vorname Nachname<br>
Straße Hausnummer<br>
PLZ Ort<br>
Deutschland<br>
E-Mail: mail@beispiel.de

## 2. Allgemeines zur Datenverarbeitung

Diese Website ist eine statische Website ohne eigene Datenbank, ohne
Nutzerkonten, ohne Kommentarfunktion und ohne Tracking- oder
Analyse-Werkzeuge. Es werden keine Cookies zu Analyse- oder
Marketingzwecken gesetzt. Eine Verarbeitung personenbezogener Daten findet
im Wesentlichen nur technisch bedingt durch den Hosting-Anbieter statt
(siehe Punkt 3).

## 3. Hosting über GitHub Pages und Datenübermittlung in die USA

Diese Website wird bei GitHub Pages gehostet, einem Dienst der GitHub Inc.,
88 Colin P. Kelly Jr. Street, San Francisco, CA 94107, USA, einer
Tochtergesellschaft der Microsoft Corporation.

Wenn Sie diese Website aufrufen, verarbeitet GitHub technisch notwendige
Daten, insbesondere Ihre IP-Adresse, um die Inhalte an Ihren Browser
auszuliefern und die Sicherheit und Stabilität des Dienstes zu
gewährleisten. Diese Daten können in Server-Logfiles gespeichert werden. Auf
Umfang und Dauer dieser Verarbeitung habe ich als Seitenbetreiber keinen
Einfluss.

Da GitHub ein US-amerikanisches Unternehmen ist, kann dabei eine
Übermittlung personenbezogener Daten in die USA erfolgen. Rechtsgrundlage
für die Verarbeitung ist das berechtigte Interesse an einer sicheren und
effizienten Bereitstellung dieser Website gemäß Art. 6 Abs. 1 lit. f DSGVO.

Weitere Informationen finden Sie in der Datenschutzerklärung von GitHub:
https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement

## 4. Domain-Weiterleitung über den Domain-Anbieter

Die Domain beispiel.de wird technisch über ANBIETER, Anschrift, per
HTTP-Weiterleitung auf die Adresse dieser Website
(benutzername.github.io) umgeleitet. Beim Aufruf über diese Domain kann der
Anbieter im Rahmen der Weiterleitung technisch bedingt Verbindungsdaten
(z. B. IP-Adresse) verarbeiten. Rechtsgrundlage ist Art. 6 Abs. 1 lit. f
DSGVO (berechtigtes Interesse an der Erreichbarkeit der Website unter dieser
Domain).

## 5. Server-Logfiles

Beim Zugriff auf die Website werden durch den Hosting-Anbieter automatisch
Informationen erfasst, die Ihr Browser übermittelt. Dies können
insbesondere sein:

- IP-Adresse des zugreifenden Geräts
- Datum und Uhrzeit des Zugriffs
- Name und URL der abgerufenen Datei
- übertragene Datenmenge
- verwendeter Browsertyp und Betriebssystem
- die Website, von der aus der Zugriff erfolgt (Referrer)

Diese Daten werden ausschließlich zur Auslieferung der Website sowie zur
Gewährleistung von Sicherheit und Stabilität verarbeitet. Rechtsgrundlage
ist Art. 6 Abs. 1 lit. f DSGVO.

## 6. Kontaktaufnahme per E-Mail

Wenn Sie mir per E-Mail schreiben, werden Ihre Angaben zum Zweck der
Bearbeitung der Anfrage und für mögliche Anschlussfragen gespeichert.
Rechtsgrundlage ist Art. 6 Abs. 1 lit. f DSGVO bzw. bei Vertragsbezug
Art. 6 Abs. 1 lit. b DSGVO. Diese Daten gebe ich nicht ohne Ihre
Einwilligung weiter und lösche sie, sobald sie nicht mehr benötigt werden
und keine gesetzlichen Aufbewahrungspflichten entgegenstehen.

## 7. Verschlüsselung (SSL/TLS)

Diese Website nutzt aus Sicherheitsgründen eine SSL-/TLS-Verschlüsselung.
Eine verschlüsselte Verbindung erkennen Sie an „https://" in der
Adresszeile Ihres Browsers.

## 8. Ihre Rechte

Sie haben im Rahmen der gesetzlichen Bestimmungen jederzeit das Recht auf:

- Auskunft über Ihre gespeicherten personenbezogenen Daten (Art. 15 DSGVO)
- Berichtigung unrichtiger Daten (Art. 16 DSGVO)
- Löschung (Art. 17 DSGVO)
- Einschränkung der Verarbeitung (Art. 18 DSGVO)
- Datenübertragbarkeit (Art. 20 DSGVO)
- Widerspruch gegen die Verarbeitung (Art. 21 DSGVO)

Zur Ausübung Ihrer Rechte genügt eine Nachricht an die oben genannte
Kontaktadresse.

## 9. Beschwerderecht bei der Aufsichtsbehörde

Sie haben das Recht, sich bei einer Datenschutz-Aufsichtsbehörde über die
Verarbeitung Ihrer personenbezogenen Daten zu beschweren (Art. 77 DSGVO).

## 10. Aktualität und Änderung dieser Datenschutzerklärung

Diese Datenschutzerklärung ist aktuell gültig. Durch die Weiterentwicklung
der Website oder aufgrund geänderter gesetzlicher bzw. behördlicher Vorgaben
kann es notwendig werden, diese Datenschutzerklärung anzupassen.
```

</details>

## Schritt 7 – Am eigenen Rechner arbeiten

Im Browser zu tippen geht, macht aber auf Dauer keinen Spaß. Mit Git holt man
sich das Repository auf den Rechner, schreibt im gewohnten Editor und lädt
fertige Beiträge hoch:

```bash
git clone https://github.com/benutzername/benutzername.github.io.git
cd benutzername.github.io
```

Für jede Änderung immer derselbe Dreisatz:

```bash
git add -A                              # Änderungen vormerken
git commit -m "Neuer Beitrag: Titel"    # lokal speichern
git push                                # hochladen, Seite geht live
```

Merksatz: **committen ist speichern, pushen ist veröffentlichen.** Ein bis
zwei Minuten nach dem Push ist der Beitrag online – GitHub baut die Seite
nach jedem Push von selbst neu.

## Drei Dinge, die gut zu wissen sind

**Alles ist öffentlich.** Das Repository ist Public, und was einmal
hochgeladen wurde, bleibt in der Historie – auch nach dem Löschen. Also
keine privaten Fotos, keine Zugangsdaten, keine halbfertigen Gedanken.

**Der Beitrag taucht nicht auf?** In dieser Reihenfolge prüfen: Datum in der
Zukunft (mit Abstand der häufigste Grund), Dateiname nicht nach Muster,
Datei nicht in `_posts/`, gar nicht gepusht. Build-Fehler zeigt der Reiter
**Actions** im Repository.

**Bilder vorher verkleinern**, auf etwa 1600 Pixel Breite. Sonst wird das
Repository nach dreißig Beiträgen unhandlich – und die Seite langsam.

---

Der komplette Quelltext dieser Seite liegt offen:
[github.com/TechnikWeber/TechnikWeber.github.io](https://github.com/TechnikWeber/TechnikWeber.github.io).
Wer lieber abschreibt als tippt, findet dort jede Datei im Original.
