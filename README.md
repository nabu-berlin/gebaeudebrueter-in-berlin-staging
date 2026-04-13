# Gebäudebrüter in Berlin – Staging

Dieses Repository ist die Vorschau-Umgebung für GitHub Pages (Branch `main`, Ordner `docs/`).
Hier wird jede neu erzeugte Karte aus dem Generator zuerst veröffentlicht und manuell geprüft, bevor ein Live-Deploy erfolgt.

## Gesamtworkflow (Kurzüberblick)

1. Karte lokal im Generator erzeugen.
2. Ergebnis nach Staging kopieren und nach GitHub pushen.
3. Staging-Seite auf GitHub Pages manuell prüfen.
4. Bei Erfolg explizit in das Live-Repository deployen.

## Zielsetzung dieses Repos

- Sichere Zwischenstufe zwischen Generierung und Live-Anzeige.
- Nachvollziehbare Versionierung der Assets unter `docs/generated/<sha>/`.
- Schnelle manuelle Qualitätskontrolle vor Live-Freigabe.

## Funktionen / Struktur

- `docs/GebaeudebrueterMultiMarkers.html` – aktive Staging-Karte.
- `docs/generated/<sha>/assets/` – versionsierte JS/CSS-Assets je Build.
- GitHub Pages liest aus `main` + `docs`.

## Prozessschritte

### 1) Stage ausführen (im Generator-Repo)

```powershell
python scripts/run_full_pipeline.py --verbose stage
```

Ergebnis:

- `docs/GebaeudebrueterMultiMarkers.html` wird aktualisiert.
- Assets landen in `docs/generated/<sha>/assets/`.
- Commit `Update map <sha>` wird erstellt und nach `origin/main` gepusht.

### 2) Manuelle Kontrolle

- Öffne die Staging-Pages-URL.
- Prüfe Karte, Marker, Filter, Popups und UI.
- Nur bei erfolgreicher Prüfung Live-Freigabe starten.

## Handlungsanweisungen

- Bei Fehlern keinen Live-Deploy auslösen.
- Korrekturen im Generator vornehmen und erneut `stage` ausführen.
- Erst nach erfolgreicher Prüfung den zweiten Befehl `publish-live` verwenden.
