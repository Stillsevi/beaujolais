# Beaujolais – Infoseite

Statische Infoseite über das Weinbaugebiet Beaujolais, mit Schwerpunkt Beaujolais Nouveau und Lyon. Eine HTML-Datei, keine Abhängigkeiten.

## Lokal ansehen

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Veröffentlichen mit GitHub Pages

1. Auf GitHub ein neues Repository anlegen (z. B. `beaujolais`), **ohne** README/.gitignore.
2. Lokal verbinden und hochladen:
   ```bash
   git remote add origin https://github.com/<benutzername>/beaujolais.git
   git push -u origin main
   ```
   Alternativ mit der GitHub-CLI: `gh repo create beaujolais --public --source=. --push`
3. Auf GitHub: Settings → Pages → Source «Deploy from a branch», Branch `main`, Ordner `/ (root)`.
4. Nach ein bis zwei Minuten ist die Seite unter `https://<benutzername>.github.io/beaujolais/` erreichbar.

Hinweis: GitHub Pages ist bei kostenlosen Konten nur für **öffentliche** Repositories verfügbar.

## Schriften

Geist und Newsreader (SIL Open Font License), lokal in `fonts/`, Lizenztexte dort.

## Quellen

Siehe Footer der Seite, u. a. Hugh Johnson / Jancis Robinson: *Der Weinatlas*, S. 66–68.
