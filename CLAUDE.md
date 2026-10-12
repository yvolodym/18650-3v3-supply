# CLAUDE.md

Hinweise für Claude Code in diesem Repository.

## Projekt

KiCad-10-Projekt: 18650-Akku → stabile 3,3 V (TP4056-Ladung, DW01A/FS8205A-Schutz,
MT3608-Boost auf ~4,0 V, AP2112K-3.3-LDO). Details und Stückliste: `README.md`.

## Dateien

- `Akku_3V3_Versorgung.kicad_sch` – Schaltplan (S-Expression, Hauptdatei)
- `Akku_3V3_Versorgung.kicad_pcb` – Platine, aktuell noch leer
- `Akku_3V3_Versorgung.kicad_pro` – Projekteinstellungen
- `Akku3V3.kicad_sym` – projektlokale Symbolbibliothek
- `sym-lib-table` – bindet die Bibliothek über `${KIPRJMOD}` ein

## Regeln

- KiCad-Dateien sind S-Expressions. Bei Bearbeitung von Hand Klammerstruktur und UUIDs
  erhalten; keine UUIDs duplizieren. Größere Änderungen lieber in KiCad selbst machen.
- Vor dem Bearbeiten prüfen, ob KiCad das Projekt geöffnet hat (`~*.lck`) – sonst
  überschreibt KiCad die Änderungen beim nächsten Speichern.
- Neue Symbole in `Akku3V3.kicad_sym` ablegen, nicht in globalen Bibliotheken.
- Lokale/temporäre Dateien (`*.kicad_prl`, `*.lck`, Backups) und Fertigungsdaten
  (Gerber, Bohrdaten, CSV) werden nicht eingecheckt (`.gitignore`).
- Schaltplan-Notizen und Dokumentation auf Deutsch.
- Bei Wertänderungen (z. B. R6/R7 für Boost-Spannung) die Notiztexte im Schaltplan
  und `README.md` mit anpassen.

## Prüfen (falls kicad-cli verfügbar)

```sh
kicad-cli sch erc Akku_3V3_Versorgung.kicad_sch
kicad-cli pcb drc Akku_3V3_Versorgung.kicad_pcb
```
