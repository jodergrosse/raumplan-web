# RaumPlan – Produktwebseite und Infomaterial

Statische Webseite ohne Baukasten, ohne Cookies, ohne externe Schriften oder Skripte. Läuft auf jedem Webspace.

```
index.html            Startseite (deutsch)
support.html          Häufige Fragen und Kontakt
datenschutz.html      Datenschutzerklärung (App + Webseite)
impressum.html        Impressum nach § 5 DDG
kurzinfo.html         Eine Seite zum Drucken/Weitergeben (Strg/⌘ + P)
RaumPlan-Kurzinfo.pdf dieselbe Seite als PDF (noch mit Platzhaltern)
en/                   englische Fassung: index, support, privacy, imprint
assets/               style.css, App-Symbol, Favicon
store/appstore-texte.md  Name, Untertitel, Stichwörter, Beschreibung DE/EN, Screenshot-Plan, Hinweise für die Prüfung
```

## 1. Platzhalter ersetzen

Alle Platzhalter stehen in eckigen Klammern und sind auf der Seite gelb markiert. Suchen und Ersetzen über alle Dateien (in VS Code: ⇧⌘F, „Ersetzen“) erledigt die meisten auf einmal:

| Platzhalter | Was hinein muss |
| --- | --- |
| Anschrift (später) | Zum Start ohne Adresse. In impressum.html, datenschutz.html, en/imprint.html und en/privacy.html steht an der Stelle ein HTML-Kommentar `<!-- Anschrift hier ergänzen … -->`: Kommentarzeichen entfernen und echte Anschrift eintragen. **Kein Postfach**, c/o-Adresse möglich |
| `[HOSTER: …]` und die zwei Sätze danach in datenschutz.html / en/privacy.html | Anbieter, bei dem die Seite liegt (bei GitHub Pages stimmt der Text schon), Übermittlungsgrundlage (bei GitHub: prüfen, ob GitHub unter dataprivacyframework.gov gelistet ist) und Link zur Datenschutzerklärung des Hosters (GitHub: docs.github.com/de/site-policy/privacy-policies/github-general-privacy-statement) |
| `[APP-STORE-LINK]` | nach der Freigabe der Link zur App (apps.apple.com/…). Bis dahin den Knopf stehen lassen oder entfernen |
| `[APP-ID]` | in einem auskommentierten Block im Kopf jeder Seite: Zahl aus dem App-Store-Link, dann Kommentar entfernen. Zeigt in Safari den App-Banner |

Wenn alles ersetzt ist, verschwinden die gelben Markierungen nicht von selbst: die `<mark class="ph">…</mark>`-Hülle kann bleiben (sieht dann nur gelb aus) oder per Suchen/Ersetzen entfernt werden: `<mark class="ph">` und `</mark>` durch nichts ersetzen. Außerdem die gelben Hinweiskästen mit „Platzhalter:“ in index.html und en/index.html löschen.

## 2. Screenshots

Die Bilder auf der Seite sind echte Aufnahmen aus dem Simulator bzw. der Mac-App mit einer Beispielwohnung, verkleinert als JPEG unter `assets/shots/de|en/`. Die Originale in voller Store-Größe (40 PNGs, iPhone, iPad, Mac, Vision Pro) liegen auf dem Mac unter `~/Projects/RaumPlanner/marketing/screenshots/`.

Nur das Bild zum Scannen ist noch eine gezeichnete Illustration (SVG im HTML, Schild „Illustration“). Für ein echtes Scan-Bild: Datei als `assets/shots/de/iphone-scan.jpg` (660 px breit) ablegen und in index.html den Block `<div class="device shot" data-ph="Illustration">…</div>` durch `<div class="device"><img src="assets/shots/de/iphone-scan.jpg" alt="Scan-Ansicht"></div>` ersetzen (englisch entsprechend mit `../assets/shots/en/…`).

## 3. Hosten mit GitHub Pages unter raumplan-app.de

Die Datei `CNAME` (Inhalt `raumplan-app.de`) und die leere Datei `.nojekyll` liegen schon im Ordner und müssen mit hochgeladen werden.

**Repository**
1. Auf github.com ein neues **öffentliches** Repository anlegen, z. B. `raumplan-website` (Pages ist im kostenlosen Konto nur für öffentliche Repositories verfügbar).
2. Den Inhalt dieses Ordners hochladen, inklusive `CNAME` und `.nojekyll` (Weboberfläche: *Add file › Upload files*). `store/` und `README.md` können weggelassen werden.
3. *Settings › Pages*: Source „Deploy from a branch“, Branch `main`, Ordner `/ (root)`, speichern.
4. Im selben Bereich unter *Custom domain* `raumplan-app.de` eintragen und speichern.

**DNS beim Domain-Anbieter** (alte A-/AAAA-Einträge für `@` vorher löschen, z. B. eine „Parkseite“):

| Typ | Name | Wert |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |
| CNAME | www | `<dein-github-name>.github.io` |

**Danach**
5. Warten, bis GitHub unter *Settings › Pages* „DNS check successful“ meldet (Minuten bis einige Stunden), dann **Enforce HTTPS** anhaken. Das Zertifikat stellt GitHub kostenlos aus.
6. Empfohlen: Domain im GitHub-Konto verifizieren (*Profilbild › Settings › Pages › Add a domain*, dort steht ein TXT-Eintrag für den DNS). Das verhindert, dass jemand anderes die Domain mit einer eigenen Pages-Seite übernimmt.
7. In App Store Connect eintragen: Support `https://raumplan-app.de/support.html`, Marketing `https://raumplan-app.de/`, Datenschutz `https://raumplan-app.de/datenschutz.html`.

Grenzen von GitHub Pages (für diese Seite weit unterschritten): Seite höchstens 1 GB, etwa 100 GB Datenverkehr im Monat. Nicht erlaubt ist Pages vor allem als Hosting für Onlineshops oder kommerzielle Dienste; eine Info- und Supportseite zu einer kostenlosen App ist üblich.

Die Datenschutzerklärung nennt GitHub Pages schon als Hoster. Offen sind dort noch die zwei gelben Stellen (Übermittlungsgrundlage, Link zur Datenschutzerklärung von GitHub).

## 4. Vor dem Veröffentlichen prüfen

- Stimmen die Funktionen auf der Seite noch mit der App überein, nachdem sie auf den Geräten getestet wurde? Besonders: Vision-Pro-Funktionen, iCloud-Abgleich, Export-Formate.
- Ist die App wirklich ohne Werbung, Analyse und In-App-Käufe? Sonst stimmen Datenschutzerklärung, „Keine Daten erfasst“ und der Nicht-Händler-Status nicht mehr.
- Impressum und Datenschutz müssen auch in der App mit höchstens zwei Tipps erreichbar sein, z. B. als Links in der Hilfe auf diese Seiten.
- Keine Rechtsberatung: Die Texte folgen den üblichen Mustern für eine kostenlose Hobby-App ohne Datenerhebung. Bei Unsicherheit einmal mit einem Generator (z. B. eRecht24, Datenschutz-Generator.de) gegenprüfen.
