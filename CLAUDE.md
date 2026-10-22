# Tagwerk – Veröffentlichung auf GitHub Pages

Dieser Ordner enthält eine fertige Web-App (PWA). Es gibt keinen Build-Schritt: Die Dateien werden genau so veröffentlicht, wie sie hier liegen. Am Code muss nichts geändert werden.

## Update veröffentlichen (App ist schon online)

Wenn es in diesem Ordner schon ein Git-Repository gibt (`git status` funktioniert, `git remote -v` zeigt GitHub) und der Nutzer sagt „veröffentliche das Update“ oder „veröffentliche die App“:

1. `git status` zeigen und kurz sagen, welche Dateien sich geändert haben.
2. Veröffentlichen:
   ```
   git add index.html sw.js manifest.webmanifest icon-180.png icon-192.png icon-512.png CLAUDE.md ANLEITUNG.md
   git commit -m "Tagwerk Update"
   git push
   ```
3. Warten, bis GitHub Pages neu gebaut hat: alle 15 Sekunden `gh api repos/{owner}/tagwerk/pages/builds/latest --jq .status` abfragen, bis `built` erscheint.
4. Dem Nutzer sagen: App auf dem iPhone einmal schließen (aus dem App-Umschalter wischen) und neu öffnen, dann ist das Update da. Die Daten bleiben erhalten, die App übernimmt sie automatisch ins neue Format.

Die Cache-Version in `sw.js` ist bei mitgelieferten Updates bereits hochgezählt. Nichts am Code ändern.

## Erstveröffentlichung

Gibt es noch kein Repository, führe diese Schritte aus und erkläre jeden kurz auf Deutsch:

1. **Werkzeuge prüfen:** `git --version` und `gh --version`.
   - Fehlt `gh` unter Windows: `winget install --id GitHub.cli` (danach muss das Terminal evtl. neu gestartet werden).
   - Fehlt `git` unter Windows: `winget install --id Git.Git`.
   - Unter macOS: `brew install gh git`.
2. **Anmelden:** `gh auth status`. Wenn nicht angemeldet: den Nutzer bitten, `gh auth login` selbst im Terminal auszuführen (GitHub.com, HTTPS, im Browser anmelden), da dies interaktiv ist.
3. **Repository anlegen und hochladen** (im Ordner mit der index.html):
   ```
   git init -b main
   git add index.html sw.js manifest.webmanifest icon-180.png icon-192.png icon-512.png
   git commit -m "Tagwerk 1.0"
   gh repo create tagwerk --public --source=. --push
   ```
   Existiert `tagwerk` schon, den Nutzer fragen, ob das bestehende Repository aktualisiert oder ein anderer Name verwendet werden soll.
4. **GitHub Pages einschalten:**
   ```
   gh api -X POST repos/{owner}/tagwerk/pages -f "source[branch]=main" -f "source[path]=/"
   ```
   `{owner}` ist der GitHub-Benutzername (`gh api user --jq .login`). Ist Pages schon aktiv, kommt ein Fehler 409, das ist in Ordnung.
5. **Warten, bis die Seite online ist:** alle 15 Sekunden `gh api repos/{owner}/tagwerk/pages/builds/latest --jq .status` abfragen, bis `built` erscheint (meist 1–2 Minuten).
6. **Adresse ausgeben:** `gh api repos/{owner}/tagwerk/pages --jq .html_url` und dem Nutzer groß anzeigen.

## Danach dem Nutzer sagen

- Adresse auf dem iPhone in **Safari** öffnen → **Teilen → Zum Home-Bildschirm**.
- Die App ab dann nur über das Symbol öffnen. Safari und die Home-Bildschirm-App speichern getrennt.
- Die Daten bleiben nur auf dem iPhone. Das Repository enthält nur den Programmcode.

## Spätere Updates

Geänderte Dateien hier ablegen, dann:
```
git add -A && git commit -m "Update" && git push
```
Zusätzlich in `sw.js` die Zeile `const CACHE = 'tagwerk-v1';` hochzählen (v2, v3 …), damit das iPhone die neue Version sicher lädt. Die Daten auf dem iPhone bleiben bei Updates erhalten.
