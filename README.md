# Escape 3D: Das Labor von Prof. Quotientia

3D-Escape-Room für die 1. Oberstufe (Sek, Zyklus 3) zu Brüchen, Dezimalzahlen, Prozent-Schreibweise, Modellen (Kreis-, Strecken-, Balkenmodell, Bruchbilder), Kehrwert sowie Erweitern & Kürzen.

- Läuft im Browser (iPad/Safari ab iPadOS 16.4, Chrome, Edge) – eine einzige Datei `index.html`, keine Installation.
- Jedes neue Spiel erzeugt neue Rätselzahlen und einen eigenen 6-stelligen Türcode.
- Alle Rätsel sind im Kopf lösbar.
- Zwei Schwierigkeitsgrade: **Grundlegend** (4 Bücher, Noten bis Achtel, 4 Gläser, Bruchbild 10×10) und **Erweitert** (6 Bücher, Noten bis Sechzehntel, 6 Gläser, Bruchbild 12×12).
- Spielzeit 30–80 Minuten (Standard 40), Strafzeiten für Tipps und Fehleingaben einstellbar.
- Lehrpersonen-Bereich (🎓) mit PIN – Lösungsweg für das Spiel auf dem jeweiligen Gerät.

## LearningView
Die Anwendung unterstützt die [Embed-API von LearningView](https://learningview.org/embed-api.php). Wird sie in LearningView eingebettet, erkennt sie den Modus selbst:

| Modus | Verhalten |
|---|---|
| `student` | Spielstand wird bei LearningView gespeichert (statt lokal) und beim Öffnen wiederhergestellt. Das Ergebnis wird als Prozentwert gemeldet: gelöste Rätsel von 7, nach dem Ausbrechen 100 %. |
| `studentReview` | Einzelansicht für die Lehrperson: Kennzahlen, Lösungsweg des jeweiligen Spiels und begehbarer Raum – **nur lesen**, Eingaben verändern den Spielstand nicht. |
| `class` | Klassenübersicht mit Fortschritt, Zeit, Tipps, Fehlversuchen und Status aller Lernenden (nach Freigabe der Klassendaten). |
| `preview` | Raum spielbar, ohne zu speichern. |

Ausserhalb von LearningView wird der Spielstand wie bisher im Browser (`localStorage`) gesichert.

### Einbetten per Webadresse oder als hochgeladene Datei?
Beides ist möglich. Für direkt eingebettete Webseiten nennt die Dokumentation `getEmbedContext`, `getClassAnswerData`, `getClassStudents`, `getSelectedStudent` und `setDialogSize`; ob `saveAnswerData`/`getAnswerData` dort ebenfalls bedient werden, ist nicht dokumentiert. Die Anwendung kommt mit beidem zurecht:

- Sie sichert den Spielstand im Spielmodus zusätzlich lokal im Browser und lädt ihn von dort, wenn LearningView keinen Stand liefert. Das Spiel geht also nie verloren.
- Im Lehrpersonen-Bereich (🎓) steht zuoberst eine Statuszeile: Modus, Anzahl bestätigter Übertragungen und der letzte Fehler. Damit lässt sich in zwei Minuten prüfen, ob die Einbettung per Webadresse auch die Antwortdaten speichert.
- Wird das Speichern nicht bestätigt, bleibt die Klassenübersicht leer; dann die Datei `index.html` als HTML-Aufgabe hochladen.

Hinweise:
- Speichervorgänge laufen nacheinander mit mindestens 2 Sekunden Abstand und warten auf die Bestätigung; Fehler werden den Lernenden angezeigt.
- Klassendaten werden nur nach Freigabe durch die Lehrperson übertragen; während der Freigabe zeigt die Anwendung einen Wartehinweis.
- Im Lehrpersonen-Modus entfällt die PIN, weil LearningView die Ansicht bereits schützt.

## Dateien
- `index.html` – spielbereite Version (Three.js eingebettet)
- `quelle/escape-quelle.html` – lesbarer Quelltext (lädt Three.js r160 per Import-Map)
