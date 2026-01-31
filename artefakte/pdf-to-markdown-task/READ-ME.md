---
title: "PDF → Markdown Task (Basis)"
date: 2026-01-31
---

# PDF → Markdown Task (Basis)

Ein Basis-Task meines Obsidian-Plugins: Er nimmt **eine PDF**, schickt sie an ein LLM und legt die **Antwort als Markdown-Datei daneben** ab.

Das Ziel ist nicht “Chat”. Das Ziel ist **Transformation**: Aus einem schwer durchsuchbaren Dokument wird ein bearbeitbares, versionierbares Artefakt.

---

## Warum ich das gebaut habe

PDFs sind für Menschen okay, für Workflows schlecht:  
Suchen ist mühsam, Weiterverarbeitung ist brüchig, Kontext landet in Köpfen statt in Dateien.

Ich will den Inhalt als Markdown **neben** der Quelle haben, damit:
- ich im Vault normal suchen/querverlinken kann,
- Inhalte in Notizen/Tasks weiterfließen,
- Änderungen nachvollziehbar bleiben (Git/History).

---

## Single Responsibility (wichtig)

Dieser Task hat **eine** Verantwortung:

> **PDF rein → Markdown raus.**

Er hat **nichts** mit einem “ASK Task” zu tun (Frage stellen, Q&A, Interpretation).  
Q&A ist ein eigener Task, mit eigener Verantwortung und eigener Fehlerklasse.

---

## Input / Output

**Input**
- Eine PDF-Datei im Vault

**Output**
- Eine Markdown-Datei direkt daneben, z. B.  
  `Rechnung_2026-01.pdf` → `Rechnung_2026-01.md`

Optional (empfohlen): Frontmatter im Output für Nachvollziehbarkeit:
- `source`: Pfad zur PDF
- `created`: Timestamp
- `model`: Model-ID
- `hash`: Hash der PDF (für “ist noch aktuell?”)

---

## Ablauf (high level)

1. PDF wird geladen
2. Inhalt wird an ein LLM übergeben
3. LLM liefert Markdown/Text zurück
4. Plugin speichert Ergebnis als `*.md` neben der PDF

---

## Guardrails (damit es stabil bleibt)

- **Kein Q&A, keine Interpretation:** Der Task soll nicht “schlau” sein, sondern verlässlich.
- **Nachvollziehbarkeit > Schönheit:** Lieber rohes, aber korrektes Markdown als hübsche Fantasie.
- **Fehler sichtbar machen:** Wenn Extraktion scheitert, wird das im Output protokolliert (statt still zu schlucken).

---

## Status

Das ist ein **Basis-Task**, den ich als Fundament für weitere Workflows nutze (Suche, Verlinkung, spätere Query-Tasks).

Wenn du das nachbauen willst: Details folgen, sobald der Task stabil genug ist, dass andere ihn ohne Support-Hölle nutzen können.

