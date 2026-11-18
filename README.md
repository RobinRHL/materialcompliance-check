# Compliance-Check Werkstoffe

Lokale Web-App zur Prüfung von Werkstoffen auf **REACH/SVHC**, **RoHS**, **California Proposition 65** und **TSCA**.
Werkstoff eingeben (z. B. `1.4301`), Ergebnis je Verordnung ablesen – inklusive passender RoHS-Ausnahme und Begründung.

Eine einzige HTML-Datei, kein Server, keine Installation. Alle Daten bleiben im Browser.

## Funktionen

- **Prüfung je Werkstoff**: SVHC (> 0,1 %, Art. 33 REACH), RoHS Anhang II inkl. automatischer Zuordnung der Bleiausnahmen 6(a)-I / 6(b) / 6(c) nach Delegierter RL (EU) 2025/2364, Prop 65 (jeder Gehalt, mit Toxizitätsart), TSCA §6(h) PBT-Stoffe, SNUR/Consent-Order-Hinweise, PFAS-Hinweis für Fluorpolymere
- **Mehrere Werkstoffe auf einmal** und **Übersicht aller Werkstoffe** mit Filter, Sortierung und CSV-Export
- **Werkstoffe bearbeiten und anlegen** – auch per Copy & Paste aus IMDS, Datenblatt oder Excel, mit CAS-Prüfziffernkontrolle
- **Listen aktualisieren per Drag & Drop**: neue ECHA-, OEHHA- und TSCA-Dateien hineinziehen, alles wird neu bewertet
- **Eigene Werkstoff-Datenbank** über die Excel-Vorlage (`Werkstoff-Datenbank_neutral.xlsx`) oder ERP-Exporte importieren

## Nutzung

1. `index.html` herunterladen und im Browser öffnen (Chrome, Edge, Firefox).
2. Werkstoff-Nr. oder Name eingeben → **Prüfen**.
3. Neue Regulierungslisten unter **Daten aktualisieren** hineinziehen:
   - SVHC: [ECHA Candidate List](https://echa.europa.eu/candidate-list-table) (Excel-Export)
   - Prop 65: [OEHHA Proposition 65 List](https://oehha.ca.gov/proposition-65/proposition-65-list) (Excel)
   - TSCA: [EPA TSCA Inventory](https://www.epa.gov/tsca-inventory/how-access-tsca-inventory) (CSV)

Für den Import wird einmalig die Bibliothek SheetJS von cdnjs geladen (Internet nötig). Die Prüfung selbst funktioniert offline.

## Enthaltene Daten

| Daten | Stand |
|---|---|
| ECHA-Kandidatenliste (SVHC) | 04.02.2026 |
| OEHHA Proposition 65 List | 31.07.2026 |
| EPA TSCA Inventory (Stoffe mit SNUR/Order/§6-Regel) | 07/2026 |
| Werkstoff-Datenbank | 72 Werkstoffe: Stähle, Edelstähle, Aluminium, Kupfer- und Zinklegierungen nach EN-Normen, generische Kunststoffe/Elastomere |

### Methodik der Werkstoff-Datenbank
- Metalle: Zusammensetzung nach EN-Norm. Legierungselemente mit Bereich → Mittelwert; Elemente mit Höchstwert → Höchstwert; **Blei und Cadmium immer Höchstwert** (Worst Case); Basis-Element als Rest.
- Kunststoffe/Elastomere: nur Grundpolymer. Additive, Farbmittel, Weichmacher und Flammschutzmittel sind **nicht** erfasst – die App zeigt diese Werkstoffe daher als „kein Befund im Grundpolymer“ und nicht als konform.

## Grenzen

- Die Bewertung ist nur so gut wie die hinterlegte Zusammensetzung. Reale Chargen können abweichen (Werkszeugnis 3.1 maßgeblich).
- Prop 65: Bewertet wird das Vorkommen gelisteter Stoffe, nicht die tatsächliche Exposition. Formbeschränkte Einträge (z. B. TiO₂, Carbon Black nur als lungengängiger Staub) sind per Schalter einstellbar.
- RoHS-Ausnahmen nach Grundmetall; Sonderfälle (z. B. 6(a)-II feuerverzinkt) werden nicht automatisch erkannt.
- Durchgestrichene (gestrichene) Prop-65-Einträge werden beim Import nicht erkannt.

**Keine Rechtsberatung.** Die Ergebnisse ersetzen keine fachliche Prüfung und keine Lieferantenerklärung.

## Datenquellen und Lizenz

- Source: European Chemicals Agency, https://echa.europa.eu/ – Candidate List of substances of very high concern
- California Office of Environmental Health Hazard Assessment (OEHHA), Proposition 65 List
- U.S. Environmental Protection Agency, TSCA Chemical Substance Inventory

Code: MIT-Lizenz (siehe `LICENSE`). Die enthaltenen Regulierungslisten unterliegen den Nutzungsbedingungen der jeweiligen Behörde.
