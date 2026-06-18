# Vornamen von Neugeborenen in München — Datenvisualisierung

Interaktive Visualisierung der offiziellen Vornamensstatistik der Landeshauptstadt
München (Vornamen der Nulljährigen zum 31.12. des jeweiligen Jahres).

**Datenquelle:** [Open Data Portal München — Vornamen von Neugeborenen](https://opendata.muenchen.de/dataset/vornamen-von-neugeborenen)
· Statistisches Amt München · Lizenz CC BY 4.0.

## Nutzung

Einfach `index.html` im Browser öffnen — z. B. per Doppelklick oder über einen
lokalen Server:

```bash
python3 -m http.server 8000
# dann http://localhost:8000 aufrufen
```

Eine aktive Internetverbindung ist erforderlich, da die Daten beim Laden der
Seite **direkt und tagesaktuell** aus dem Open-Data-Portal geholt werden.

## Funktionsumfang

- **Überblick** – gestapelte Flächengrafik der gemeldeten Nennungen pro Jahr,
  aufgeteilt nach Mädchen/Jungen, plus Kennzahlen zum aktuellsten Jahrgang.
- **Top-Vornamen eines Jahrgangs** – die 25 häufigsten Namen je Jahr, umschaltbar
  nach Geschlecht, mit Jahres-Slider und „Abspielen"-Animation über alle Jahre.
- **Namens-Trend im Zeitverlauf** – Vornamen suchen und ihre Häufigkeit über die
  Jahre vergleichen, wahlweise als absolute Anzahl oder als Anteil (‰).

## Technik

Eine einzelne, abhängigkeitsfreie HTML-Datei (Vanilla JS, handgezeichnete
SVG-Charts). Die Datei ermittelt über die CKAN-API des Portals
(`/api/3/action/package_show`) automatisch alle jährlichen CSV-Ressourcen und
lädt sie zur Laufzeit. Dadurch erscheinen neue Jahrgänge automatisch, sobald die
Stadt sie veröffentlicht — ohne Änderung am Code.

Der CSV-Parser ist robust gegenüber den im Datensatz vorkommenden Formaten:
Trennzeichen `;` oder `,`, Groß-/Kleinschreibung der Spaltenköpfe sowie
Geschlechtsangaben als `m`/`w` oder `männlich`/`weiblich`.
