# OBS Video Timer Dock

A free custom browser dock for OBS Studio that automatically detects which video (media source) is playing in the active scene and shows the **elapsed time, remaining time and a progress bar** live. Click a source to select it and pause or resume it right from the dock.

**Quick start:** In OBS go to **Docks → Custom Browser Docks**, add a name and paste this URL: `https://vidiverse.github.io/obs-media-info/`. No download needed.

**Requirements:** OBS Studio 28 or newer with the obs-websocket server enabled (**Tools → obs-websocket Settings**). Click the gear icon in the dock to enter host (default `localhost`), port (default `4455`) and password if set.

**Features:** automatic media source detection in the active scene, live countdown, pause/resume for the selected source, auto-reconnect, remembered connection settings (optional), collapsible settings panel, single HTML file without dependencies.

**Limitations:** media sources inside nested scenes or groups are not detected. Supported types: media source (`ffmpeg_source`) and VLC video source (`vlc_source`).

**License:** MIT. This project is not affiliated with or endorsed by the OBS Project.

Keywords: OBS Studio, media source timer, video countdown, remaining time, browser dock, obs-websocket, livestream.

---

## Deutsch

### OBS Video-Timer-Dock

Ein Custom Browser Dock für OBS Studio, das automatisch erkennt, welches Video (Medienquelle) gerade in der aktiven Szene läuft, und die verstrichene sowie verbleibende Zeit live anzeigt.

**Version:** v0.8
**Entwickelt für:** JungleCraft Livestreams
**Erstellt von:** Junglecraft Social-Media-Team

## Funktionen

- Erkennt automatisch alle Medienquellen (Video/VLC-Quelle) in der aktuell aktiven Programm-Szene
- Zeigt pro Quelle Status (Läuft/Pause), verstrichene Zeit, verbleibende Zeit und einen Fortschrittsbalken
- Reagiert live auf Szenenwechsel, Sichtbarkeits-Änderungen und Start/Stopp des Videos
- Quelle per Klick auf die jeweilige Karte auswählbar, darunter kleine Pause-/Weiter-Steuerung für die gewählte Quelle
- Verbindet sich automatisch neu, falls OBS neu startet oder die Verbindung abbricht
- Verbindungseinstellungen (Host/Port/Passwort) sind über ein Zahnrad-Symbol ein- und ausblendbar

## Voraussetzungen

- OBS Studio 28 oder neuer (obs-websocket ist ab Version 28 bereits eingebaut)
- obs-websocket-Server in OBS aktiviert: **Werkzeuge → obs-websocket-Einstellungen**

## Installation

Keine Datei herunterladen nötig – einfach die gehostete URL direkt in OBS einbinden:

1. In OBS: **Docks → Benutzerdefinierte Browser-Docks**
2. Namen vergeben und als URL eintragen:
   ```
   https://vidiverse.github.io/obs-media-info/
   ```
3. Erstellen klicken – das Dock erscheint

## Einrichtung im Dock

1. Zahnrad-Symbol ⚙ oben rechts anklicken, um die Verbindungseinstellungen einzublenden
2. Host (Standard: `localhost`), Port (Standard: `4455`) und ggf. das obs-websocket-Passwort eintragen
3. **Verbinden** klicken

> Läuft OBS auf einem anderen Rechner als der Dock-Browser, muss statt `localhost` die IP-Adresse des OBS-Rechners eingetragen werden, und Port 4455 muss in der Firewall freigegeben sein.

## Bekannte Einschränkungen

- Medienquellen in verschachtelten Szenen oder Gruppen werden aktuell nicht erkannt, nur Quellen direkt in der aktiven Szene
- Unterstützt Medienquellen vom Typ `ffmpeg_source` (Medienquelle) und `vlc_source` (VLC-Video-Quelle)

## Lizenz

MIT, siehe [LICENSE](LICENSE). Dieses Projekt steht in keiner Verbindung zum OBS Project.

## Versionshistorie

- **v0.8** – Die ganze Karte ist zuverlässig klickbar (Auswahl reagiert sofort beim Drücken, auch während das Video läuft)
- **v0.7** – Verbindungsdaten (inkl. Passwort) werden auf Wunsch gespeichert, kein erneutes Eingeben nach OBS-Neustart
- **v0.6** – Schreibweise des Team-Credits korrigiert (Junglecraft Social-Media-Team)
- **v0.5** – Quellenauswahl erfolgt jetzt per Klick auf die Karte statt über ein Dropdown
- **v0.4** – Dropdown zur Quellenauswahl, darunter kleine Pause-/Weiter-Steuerung oberhalb der Versionsanzeige
- **v0.3** – Versionsnummer und Credits in der Fußzeile ergänzt
- **v0.2** – Verbindungseinstellungen standardmäßig ausgeblendet, über Zahnrad-Symbol ein-/ausblendbar
- **v0.1** – Erste Version: automatische Erkennung laufender Medienquellen, Live-Anzeige von verstrichener/verbleibender Zeit
