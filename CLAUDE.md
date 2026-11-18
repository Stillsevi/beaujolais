# CLAUDE.md – Beaujolais-Infoseite

Anleitung für Claude Code zur Arbeit an diesem Repository.

## Projekt

Statische Infoseite über das Weinbaugebiet Beaujolais (Beaujolais Nouveau, Lyon & Beaujolais, Trauben, Appellationen, 10 Crus, Lagen, Weinstil, Produzenten, Traditionen, Orte, Essen & Wein, Trends, Glossar). Veröffentlichung über **GitHub Pages**.

## Struktur

```
/
├── index.html   # Die gesamte Seite: HTML, CSS (im <style>) und JS (im <script>)
├── fonts/       # Geist + Newsreader Light (WOFF2, OFL-Lizenzen), selbst gehostet
├── README.md    # Kurzbeschreibung und Anleitung GitHub Pages
├── .nojekyll    # GitHub Pages ohne Jekyll ausliefern
└── CLAUDE.md    # Diese Datei
```

## Grundprinzipien

- **Mobile first – verbindlich.** Die Seite wird primär für Smartphones gebaut und nach oben erweitert (Details siehe Abschnitt «Mobile first»).
- **Eine Datei, keine Abhängigkeiten.** Kein Framework, kein Build-Schritt, keine externen Fonts, CDNs oder Bilder-Hotlinks. CSS und JS bleiben inline in `index.html`. Einzige Ausnahme: die selbst gehosteten Schriften in `fonts/`.
- **Sprache: Deutsch (Schweiz).** `lang="de-CH"`, **kein «ß», immer «ss»**. Guillemets «…» statt „…“. Französische Fachbegriffe kursiv oder mit Akzenten korrekt (Chénas, Régnié, Moulin-à-Vent).
- **Eigene Formulierungen.** Keine Textpassagen aus Quellen kopieren; Fakten paraphrasieren und die Quelle im Footer verlinken.
- **Barrierearm.** Semantisches HTML, `aria-label` auf SVG und Navigation, ausreichender Kontrast in Light und Dark Mode.

## Mobile first

Basis-CSS = Smartphone (≈ 360–400 px). Grössere Bildschirme werden **nur über `min-width`-Media-Queries** ergänzt, nie umgekehrt.

- **Breakpoints:** `@media (min-width: 640px)` (Tablet) und `@media (min-width: 960px)` (Desktop). Keine `max-width`-Queries für das Layout.
- **Layout:** Standard ist einspaltig. Mehrspaltige Grids (`.g2`, `.g3`, `.mapbox`, Glossar) erst ab Breakpoint aktivieren.
- **Typografie:** Fliesstext mind. 16–17 px, Überschriften mit `clamp()` skalieren. Zeilenlänge auf grossen Screens begrenzen (`--maxw`).
- **Touch:** Klickflächen mind. 44 × 44 px (Navigation, Links in Karten). Keine Inhalte, die nur per Hover erreichbar sind.
- **Navigation:** Die Sticky-Nav scrollt auf Mobile horizontal; sie darf nicht umbrechen und keinen Inhalt verdecken (Anker-Sprungziele mit `scroll-margin-top` versehen).
- **Tabellen:** immer in `<div class="tbl">` (horizontal scrollbar). Wenn eine Tabelle auf Mobile unlesbar wird, lieber als Karten-Liste darstellen.
- **Grafiken:** SVG mit `viewBox` und `width:100%`, Beschriftungen auf 400 px Breite lesbar halten.
- **Performance:** keine grossen Bilder; falls doch Bilder nötig sind, `loading="lazy"`, `width`/`height` setzen und moderne Formate (WebP/AVIF) verwenden.
- **Prüfung bei jeder Änderung:** zuerst bei 375 px Breite kontrollieren, danach 768 px und 1200 px, jeweils in Light und Dark Mode. Kein horizontales Scrollen der ganzen Seite.

## Design-System

- Farben ausschliesslich über CSS-Variablen in `:root` (z. B. `--gamay`, `--accent`, `--granite`, `--stone`, `--saone`). Dark-Mode-Werte im Block `@media (prefers-color-scheme: dark)` mitpflegen.
- Schriften (Typografie von website-sevi übernommen): `--serif` = Newsreader Light (300) für Überschriften, `--sans` = Geist (400, 600 nur für Fettschrift) für Fliesstext. Grössen nur über die Tokens `--fs-display`, `--fs-h2`, `--fs-title`, `--fs-text`, `--fs-small` (Desktop-Werte ab 640 px); Zeilenhöhen `--lh-*`, Laufweiten `--ls-*`.
- Wiederverwendbare Bausteine: `.card`, `.grid.g2` / `.grid.g3`, `.callout`, `.tag`, `.tbl` (scrollbarer Tabellen-Wrapper), `.pyramid` / `.tier`.

## Abschnitte & Anker

Jeder Abschnitt ist eine `<section id="…">` und hat einen Eintrag in `<nav class="toc">`. Bestehende IDs nicht umbenennen (externe Links):

`nouveau`, `lyon`, `lage`, `trauben`, `appellationen`, `crus`, `lagen`, `stil`, `produzenten`, `traditionen`, `orte`, `essen`, `trends`, `glossar`

Neuen Abschnitt hinzufügen = Section + Nav-Eintrag + ggf. Quellen im Footer.

## Besondere Elemente

- **Karte (`svg.map`):** schematisch, nicht massstabsgetreu. Crus sind nummeriert von Nord (1 Saint-Amour) nach Süd (10 Côte de Brouilly). Beim Verschieben von Labels darauf achten, dass sie die Saône-Linie (x ≈ 285–315) nicht überlappen.
- **Nouveau-Countdown (`#countdown`, im Hero):** JS berechnet automatisch den 3. Donnerstag im November des laufenden bzw. nächsten Jahres; bis 30 Tage danach zeigt er «ist da». Kein Jahr hart codieren.
- **Reihenfolge:** Nouveau und Lyon stehen bewusst als erste Abschnitte direkt nach dem Hero.
- **Quellenangaben aus dem Weinatlas:** inline als `<p class="src">` mit Link auf `#q-weinatlas` im Footer.

## Lokale Vorschau

```bash
python3 -m http.server 8000
# dann http://localhost:8000 öffnen
```

Nach Änderungen in den DevTools (Gerätemodus) zuerst bei 375 px prüfen, dann 768 px und 1200 px – jeweils auch im Dark Mode.

## Jährliche Aktualisierung (Checkliste)

- [ ] «Stand: …» im Footer anpassen
- [ ] Datum der Sarmentelles de Beaujeu im Abschnitt `traditionen`
- [ ] Status der Premier-Cru-Anträge (Fleurie, Brouilly, Moulin-à-Vent) im Abschnitt `lagen`
- [ ] Kennzahlen im Hero (Rebfläche, Gamay-Anteil) und im Abschnitt `trends`
- [ ] Produzentenliste auf Generationswechsel/Umbenennungen prüfen
- [ ] Alle Links in der Quellenliste testen

## Deployment

GitHub → Settings → Pages → Source: Branch `main`, Ordner `/ (root)`. Jede Änderung auf `main` ist nach kurzer Zeit live.

## Commits

Kurze, deutschsprachige Commit-Messages im Imperativ, z. B. `Premier-Cru-Status aktualisieren` oder `Abschnitt Jahrgänge ergänzen`.
