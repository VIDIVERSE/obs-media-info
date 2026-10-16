# CLAUDE.md

Projektkontext und Arbeitsregeln für Claude in diesem Repository.

## Projekt

OBS Video-Timer-Dock: ein Custom Browser Dock für OBS Studio, das über obs-websocket (v5, ab OBS 28 eingebaut) automatisch erkennt, welche Medienquelle in der aktiven Programm-Szene läuft, und verstrichene sowie verbleibende Zeit live anzeigt. Ausgewählte Quellen lassen sich pausieren und fortsetzen.

- Entwickelt für JungleCraft Livestreams
- Erstellt vom Junglecraft Social-Media-Team
- Live-URL (GitHub Pages): https://vidiverse.github.io/obs-media-info/

## Dateistruktur

- `index.html`: die komplette Anwendung (HTML, CSS und JavaScript in einer Datei, keine externen Abhängigkeiten). GitHub Pages liefert sie von `main` aus.
- `README.md`: Nutzerdokumentation (Englisch oben, Deutsch darunter) inklusive Versionshistorie.
- `LICENSE`: MIT-Lizenz (JungleCraft).
- `llms.txt`: maschinenlesbare Kurzbeschreibung für KI-Systeme.
- `CLAUDE.md`: diese Datei.

## Verbindliche Regeln

1. **Versionsnummer bei jeder Änderung erhöhen.** Die Version steht im Footer von `index.html` (`<span class="version">vX.Y</span>`), über den Credits. Zusätzlich `README.md` anpassen: Zeile `**Version:**` (deutscher Teil) und neuer Eintrag in der Versionshistorie (neueste oben). Englischen Abschnitt bei Funktionsänderungen mitpflegen.
2. **Footer-Text beibehalten:**
   - `vX.Y`
   - `Entwickelt für JungleCraft Livestreams`
   - `erstellt von Junglecraft Social-Media-Team`
3. **Sprache der Oberfläche: Deutsch.** Antworten an den Nutzer ebenfalls auf Deutsch.
4. **Eine einzige Datei, keine externen Skripte, Fonts oder CDNs.** Das Dock muss auch offline im OBS-Browser (Chromium/CEF) laufen.
5. **Kein `localStorage`/`sessionStorage`.** Zustand bleibt im Arbeitsspeicher.
6. **Keine Secrets committen.** Das obs-websocket-Passwort wird nur im Dock eingegeben und nie gespeichert. Zugriffstokens gehören nie in Dateien oder Commit-Nachrichten.

## Verhalten der Oberfläche (nicht versehentlich ändern)

- Verbindungseinstellungen (Host, Port, Passwort) sind standardmäßig eingeklappt und über das Zahnrad-Symbol ein-/ausblendbar.
- Quellen werden per **Klick auf die Karte** ausgewählt (nicht per Dropdown). Erneuter Klick hebt die Auswahl auf.
- Die Buttons **Pause** und **Weiter** stehen zentriert direkt über der Versionsanzeige und sind nur aktiv, wenn eine Quelle ausgewählt und die Verbindung steht.
- Angezeigt werden nur Medienquellen (`ffmpeg_source`, `vlc_source`), die in der aktuellen Programm-Szene aktiviert sind und den Status Läuft oder Pause haben.

## Technische Eckpunkte

- Protokoll: obs-websocket v5 über rohes `WebSocket`, Authentifizierung per SHA-256 (`crypto.subtle`), Event-Subscriptions `2047`.
- Genutzte Requests: `GetCurrentProgramScene`, `GetSceneItemList`, `GetMediaInputStatus`, `TriggerMediaInputAction`.
- Genutzte Events: `CurrentProgramSceneChanged`, `SceneItemEnableStateChanged`, `SceneItemCreated`, `SceneItemRemoved`, `MediaInputPlayback*`.
- Zeitangaben von obs-websocket sind Millisekunden. Zwischen den Abfragen (1 Sekunde) wird die Anzeige lokal interpoliert.
- Verbindung baut sich bei Abbruch alle 3 Sekunden automatisch neu auf.

## Bekannte Einschränkungen

- Medienquellen in verschachtelten Szenen oder Gruppen werden nicht erkannt.

## Design

Dunkles Theme passend zu OBS. Farben als CSS-Variablen in `:root` (`--live` für Rot/Aktiv, `--pause` für Amber). Zeitwerte in Monospace, sonst Systemschrift. Keine Großbuchstaben-Labels, Beschriftungen in normaler Schreibweise.
