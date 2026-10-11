# Tilgungsrechner

Ein Tilgungsrechner für Annuitätendarlehen in einer einzigen HTML-Datei, ohne Abhängigkeiten. Er zeigt den monatlichen Tilgungsplan bis zum Ende der Sollzinsbindung. Tatsächliche und fiktive Änderungen des Tilgungssatzes sowie Sondertilgungen lassen sich einplanen.

## Nutzung

`index.html` im Browser öffnen. Chrome oder Edge werden empfohlen, siehe [Speichern](#speichern).

### Vertragsdaten

| Feld | Bedeutung |
| --- | --- |
| Darlehensteil = Berechnungskapital | Darlehensbetrag in € |
| Valuta | Auszahlung bzw. Kreditbeginn. Ab hier läuft auch die Sollzinsbindung. |
| Anfangsdatum | Fälligkeitsmonat der ersten Zins- und Tilgungsrate |
| Sollzins p.a. | Gebundener Sollzinssatz |
| Anfangstilgung p.a. | Tilgungssatz bezogen auf das Berechnungskapital |
| Sollzinsbindung | Laufzeit in Jahren ab Valuta |
| Zins- und Tilgungsrate neu | Optional: die Rate laut Vertrag. Leer = Berechnungskapital × (Zins + Tilgung) ÷ 12 |

Zwischen Valuta und Anfangsdatum wird nur die **Zinsrate** fällig, also keine Tilgung.

### Tilgungsplan

Der Plan hat die Spalten Fälligkeitsmonat, Gesamtleistung (Abbuchung), Zins- und verw. Kosten, Tilgung und Restschuld. Er endet mit der Restschuld zum Ende der Sollzinsbindung oder früher mit der vollständigen Tilgung. Optional lassen sich Jahressummen einblenden.

### Änderungen

Jede Änderung legt fest:

- ab welchem Fälligkeitsmonat sie gilt,
- optional einen neuen Tilgungssatz. Die neue Rate ist dann Berechnungskapital × (Sollzins + neuer Tilgungssatz) ÷ 12.
- optional eine Sondertilgung. Sie wird nach der Monatsrate verrechnet.

Eine Änderung ist entweder **tatsächlich** und gehört damit zum Ist-Plan, oder **fiktiv** als Gedankenspiel, das mit dem Ist-Plan verglichen wird. Für jede Änderung wird angezeigt, wie sich Zinsen gesamt, Zinsen bis zum Ende der Zinsbindung und die Laufzeit verändern. Grundlage ist jeweils der Plan mit allen früheren Änderungen. Die Sollzinsbindung wird durch Änderungen nicht verlängert.

## Speichern

Kredite bekommen einen Namen und werden als `<Name>.json` gespeichert:

- **Chrome und Edge:** Beim ersten Speichern wählst du den Ordner aus, in dem `index.html` liegt. Danach erscheinen alle gespeicherten Kredite in der Auswahlliste. Dafür wird die File System Access API genutzt.
- **Andere Browser:** Über „JSON herunterladen“ und „JSON-Datei öffnen“.

Die aktuelle Eingabe bleibt zusätzlich im Browser (localStorage) erhalten.

> Gespeicherte Kredit-Dateien (`*.json`) sind per `.gitignore` von der Versionsverwaltung ausgeschlossen.

## Rechenannahmen

- Zinsen nach 30/360: Restschuld × Sollzins ÷ 12 pro Monat, auf den Cent gerundet. Im Valutamonat werden die Zinsen nur anteilig berechnet.
- Eine Rate pro Monat, fällig im jeweiligen Fälligkeitsmonat.
- Für Volltilgung, Zinsen gesamt und Laufzeit gilt: Der Sollzins bleibt auch nach Ende der Zinsbindung gleich.

Die Ergebnisse sind unverbindlich. Maßgeblich ist der Tilgungsplan der Bank.

## Lizenz

[MIT](LICENSE)
