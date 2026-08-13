# Simpli AI Hub installieren

Der Hub ist ein Fenster mit Reitern: links die Projekte, rechts die Monday-Aufgaben,
in der Mitte laufen die Claude-Sessions. Ein Klick auf ein Projekt holt es von GitHub
und startet Claude darin.

## 0. Einladung annehmen

Vorab kommt eine Mail von GitHub mit der Einladung in die Organisation
**Simpli-bot**. Diese zuerst annehmen — ohne sie bleibt die Projektliste im
Hub leer, weil sie direkt von GitHub kommt.

## 1. Vorher installieren

Drei Programme müssen auf dem Rechner sein. Alle drei sind kostenlos.

| Programm | Wozu | Woher |
|---|---|---|
| **Claude Code** | die eigentliche Arbeit | https://claude.com/product/claude-code |
| **GitHub CLI** (`gh`) | Anmeldung bei GitHub, Projekte herunterladen | https://cli.github.com |
| **Git** | kommt meist mit der GitHub CLI mit | https://git-scm.com/download/win |

Prüfen, ob alles da ist: PowerShell öffnen und nacheinander eingeben.

```powershell
claude --version
gh --version
git --version
```

Antwortet eines davon mit „ist nicht als Befehl erkannt", fehlt es noch.

## 2. Setup starten

### Der kurze Weg: Claude machen lassen

Wer Claude Code schon nutzt, kopiert **diese eine Zeile** in eine Session:

```
Installiere mir den Simpli AI Hub auf diesem Windows-Rechner: lade das neueste Release aus dem öffentlichen Repo restriden/simpli-ai-hub-releases herunter (gh release download --repo restriden/simpli-ai-hub-releases --pattern "SimpliAIHub-Setup-*.exe"), führe die Datei still mit dem Schalter /S aus und prüfe danach, dass die Verknüpfung "Simpli AI Hub" auf dem Desktop liegt — sag mir Bescheid, wenn es fertig ist.
```

Es muss **eine einzige Zeile** bleiben: jeder Umbruch wäre in Claude Code ein
Enter, und der Auftrag ginge halb fertig ab.

Claude lädt dann das Release (rund 108 MB) und installiert es still. Fertig ist
es, sobald die Verknüpfung **Simpli AI Hub** auf dem Desktop liegt.

### Der Weg von Hand

Den Installer gibt es unter
[**Releases**](https://github.com/restriden/simpli-ai-hub-releases/releases/latest)
— dort die Datei `SimpliAIHub-Setup-….exe` herunterladen (rund 108 MB) und
doppelt anklicken.

Windows zeigt dabei einmalig ein blaues Fenster:
„Der Computer wurde durch Windows geschützt".

Das ist **kein Fehler** — es erscheint bei jedem Programm ohne gekauftes
Signaturzertifikat. So geht es weiter:

1. Auf **„Weitere Informationen"** klicken
2. Auf **„Trotzdem ausführen"** klicken

Danach fragt das Setup nur noch nach dem Zielordner. Ab dem zweiten Start
kommt die Meldung nicht wieder.

## 3. Beim ersten Start mit GitHub verbinden

Im Hub links unter **Projekte** steht zunächst nur „Mit GitHub verbinden".

1. Darauf klicken — es öffnet sich ein Reiter mit `gh auth login`
2. Die Fragen im Reiter beantworten:
   - **GitHub.com**
   - **HTTPS**
   - Anmelden mit dem Browser (`Y`)
   - Den angezeigten Code im Browser eingeben
3. Zurück im Hub auf **„Erneut prüfen"** klicken

Jetzt kennt der Hub die eigenen Repos.

## 4. Projekte auswählen

Auf **„Repos verwalten"** klicken. Die Liste zeigt alles, worauf der eigene
GitHub-Zugang Zugriff hat.

- Haken setzen bei den Projekten, an denen gearbeitet wird
- **„Übernehmen"** — sie stehen ab sofort links in der Sidebar
- **„lokal"** heißt: liegt schon auf dem Rechner.
  **„wird geklont"**: wird beim ersten Klick heruntergeladen.

Fehlt ein Projekt in der Liste, ist der GitHub-Zugang dafür noch nicht
freigeschaltet — dann bei Tim melden.

## 5. Arbeiten

Klick auf ein Projekt in der Sidebar:

1. lädt es bei Bedarf nach `C:\Users\<Name>\Projects\<projekt>` herunter
2. öffnet einen Reiter und startet Claude darin
3. schickt `/morning`, damit Claude den letzten Stand kennt

Ein vorhandener Ordner wird nur geöffnet, nie überschrieben.

**Nützlich:**

- `Strg` + `Tab` — zwischen Reitern wechseln, `Alt` + `1…9` springt direkt
- `Strg` + `Shift` + `T` neuer Reiter, `Strg` + `Shift` + `W` schließen
- `Strg` + `Shift` + `Leertaste` — Diktat, spricht statt tippt
- Doppelklick auf den Reiternamen benennt ihn um
- Leuchtet ein Reiter gelb, ist Claude dort fertig und wartet

## Updates

Gibt es eine neue Fassung, erscheint oben rechts im Hub ein orangener Knopf
**„Update x.y.z"**. Ein Klick zeigt, was die Version bringt — geladen und
installiert wird erst auf Zuruf. Wer gerade mitten in einer Session steckt,
klickt einfach auf **„Später"**; der Knopf bleibt.

## Wo liegen die Einstellungen?

Unter `%APPDATA%\simpli-ai-hub`:

- `config.json` — die Knöpfe der Sidebar (der Knopf „Buttons bearbeiten" öffnet sie)
- `repos.json` — welche Projekte angehakt sind
- `monday-cache.json` — die zuletzt geladenen Aufgaben

Zum Zurücksetzen den Hub schließen, die jeweilige Datei löschen und neu starten.

## Wenn etwas klemmt

| Problem | Ursache |
|---|---|
| Sidebar ist leer | `config.json` beschädigt — Datei löschen, Hub neu starten |
| „GitHub CLI fehlt" | `gh` ist nicht installiert (Schritt 1) |
| Projekt-Liste bleibt leer | im Dialog auf **⟳ Neu laden** klicken |
| Monday-Aufgaben leer | dafür braucht es einen Monday-Zugang — bei Tim melden |
| Diktat reagiert nicht | Windows muss dem Hub das Mikrofon erlauben (Einstellungen → Datenschutz → Mikrofon) |
| Mikrofon-Knopf bleibt grau | Beim **ersten** Diktat lädt der Hub einmalig das Sprachmodell (548 MB) nach. Der Fortschritt steht im Fenstertitel; danach ist es dauerhaft da und übersteht auch Updates |
