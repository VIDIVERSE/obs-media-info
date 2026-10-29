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
5. **`localStorage` nur für die Verbindungsdaten** (Schlüssel `jc-obs-video-timer`, nur wenn „Verbindungsdaten merken" aktiv ist, immer mit try/catch). Sonst bleibt Zustand im Arbeitsspeicher.
6. **Keine Secrets committen.** Das obs-websocket-Passwort wird nie im Repo gespeichert, nur optional im lokalen Browser-Speicher des Nutzers. Zugriffstokens gehören nie in Dateien oder Commit-Nachrichten.

## Verhalten der Oberfläche (nicht versehentlich ändern)

- Verbindungseinstellungen (Host, Port, Passwort) sind standardmäßig eingeklappt und über das Zahnrad-Symbol ein-/ausblendbar.
- Quellen werden per **Klick auf die Karte** ausgewählt (nicht per Dropdown). Erneuter Klick hebt die Auswahl auf.
- Unten, direkt über der Versionsanzeige, steht der Steuerbereich: oben eine Spulleiste (Schieberegler für die ausgewählte Quelle), darunter zentriert **−10 s**, **Pause**, **Weiter**, **+10 s**. Aktiv nur, wenn eine Quelle ausgewählt und die Verbindung steht; Spulleiste und ±10 s zusätzlich nur, solange das Video läuft oder pausiert ist. Die Spulleiste liegt bewusst außerhalb der Karten, weil diese alle 200 ms neu gezeichnet werden.
- Angezeigt werden nur Medienquellen (`ffmpeg_source`, `vlc_source`), die in der aktuellen Programm-Szene aktiviert sind und den Status Läuft oder Pause haben.

## Technische Eckpunkte

- Protokoll: obs-websocket v5 über rohes `WebSocket`, Authentifizierung per SHA-256 (`crypto.subtle`), Event-Subscriptions `2047`.
- Genutzte Requests: `GetCurrentProgramScene`, `GetSceneItemList`, `GetMediaInputStatus`, `TriggerMediaInputAction`, `SetMediaInputCursor` (Spulen, Millisekunden).
- Genutzte Events: `CurrentProgramSceneChanged`, `SceneItemEnableStateChanged`, `SceneItemCreated`, `SceneItemRemoved`, `MediaInputPlayback*`.
- Zeitangaben von obs-websocket sind Millisekunden. Zwischen den Abfragen (1 Sekunde) wird die Anzeige lokal interpoliert.
- Verbindung baut sich bei Abbruch alle 3 Sekunden automatisch neu auf. Bei Close-Code 4009 (Authentifizierung fehlgeschlagen) kein Reconnect, stattdessen werden die Einstellungen geöffnet.

## Bekannte Einschränkungen

- Medienquellen in verschachtelten Szenen oder Gruppen werden nicht erkannt.

## Design

Dunkles Theme passend zu OBS. Farben als CSS-Variablen in `:root` (`--live` für Rot/Aktiv, `--pause` für Amber). Zeitwerte in Monospace, sonst Systemschrift. Keine Großbuchstaben-Labels, Beschriftungen in normaler Schreibweise.
