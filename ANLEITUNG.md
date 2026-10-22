# Tagwerk aufs iPhone bringen

Die App muss einmal im Internet liegen, damit Safari sie öffnen kann. Deine Daten bleiben trotzdem nur auf deinem iPhone, sie werden nie hochgeladen. Am einfachsten und kostenlos geht das mit GitHub Pages.

## 1. Dateien hochladen (einmalig, ca. 10 Minuten, am besten am PC)

Mit Claude Code geht es automatisch: Ordner in VS Code öffnen und Claude Code sagen „Veröffentliche die App“. Die Schritte stehen in CLAUDE.md. Von Hand geht es so:

1. Konto anlegen auf **github.com** (kostenlos).
2. Oben rechts **+ → New repository**. Name: `tagwerk`. Auf **Public** lassen. **Create repository**.
3. Auf der neuen Seite **uploading an existing file** antippen.
4. Alle Dateien aus dem Ordner `tagwerk` ins Browserfenster ziehen (index.html, sw.js, manifest.webmanifest, die drei icon-Dateien). Nicht den Ordner selbst, sondern die Dateien darin. **Commit changes**.
   - Auf dem iPhone: Die ZIP-Datei in der Dateien-App antippen, dann wird sie entpackt.
5. Im Repository **Settings → Pages**. Bei *Branch* **main** und **/(root)** wählen, **Save**.
6. Nach ein bis zwei Minuten steht oben die Adresse, etwa `https://deinname.github.io/tagwerk/`.

## 2. Auf den Home-Bildschirm legen

1. Die Adresse in **Safari** öffnen.
2. **Teilen-Symbol → Zum Home-Bildschirm**.
3. Ab jetzt nur noch über das Symbol auf dem Home-Bildschirm öffnen.

Wichtig: Safari und die Home-Bildschirm-App haben getrennte Speicher. Was du in Safari einträgst, siehst du in der App nicht. Also direkt die App benutzen.

## 3. Daten sichern

Unter **Mehr → Backup sichern** speicherst du eine Datei in der Dateien-App (oder iCloud Drive). Mit **Backup laden** holst du sie zurück, zum Beispiel auf einem neuen iPhone. Ein Backup alle paar Wochen reicht.

## Updates

Wenn du neue Dateien hochlädst (gleicher Weg wie oben, alte Dateien werden ersetzt), holt sich die App das Update beim nächsten oder übernächsten Öffnen. Deine Daten bleiben dabei erhalten.
