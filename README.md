# OBS Video-Timer-Dock

Ein Custom Browser Dock für OBS Studio, das automatisch erkennt, welches Video (Medienquelle) gerade in der aktiven Szene läuft, und die verstrichene sowie verbleibende Zeit live anzeigt.

**Version:** v0.3
**Entwickelt für:** JungleCraft Livestreams
**Erstellt von:** JungleCraft Social Media Team

## Funktionen

- Erkennt automatisch alle Medienquellen (Video/VLC-Quelle) in der aktuell aktiven Programm-Szene
- Zeigt pro Quelle Status (Läuft/Pause), verstrichene Zeit, verbleibende Zeit und einen Fortschrittsbalken
- Reagiert live auf Szenenwechsel, Sichtbarkeits-Änderungen und Start/Stopp des Videos
- Verbindet sich automatisch neu, falls OBS neu startet oder die Verbindung abbricht
- Verbindungseinstellungen (Host/Port/Passwort) sind über ein Zahnrad-Symbol ein- und ausblendbar

## Voraussetzungen

- OBS Studio 28 oder neuer (obs-websocket ist ab Version 28 bereits eingebaut)
- obs-websocket-Server in OBS aktiviert: **Werkzeuge → obs-websocket-Einstellungen**

## Installation

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

## Versionshistorie

- **v0.3** – Versionsnummer und Credits in der Fußzeile ergänzt
- **v0.2** – Verbindungseinstellungen standardmäßig ausgeblendet, über Zahnrad-Symbol ein-/ausblendbar
- **v0.1** – Erste Version: automatische Erkennung laufender Medienquellen, Live-Anzeige von verstrichener/verbleibender Zeit
