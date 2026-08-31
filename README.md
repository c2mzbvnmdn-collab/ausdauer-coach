# Ausdauer-Coach

Ein KI-Trainingspartner für Ausdauersport (Laufen, Trail, Ultra, Radfahren), umgesetzt als System-Prompt für **Claude** – ehrlich beratend statt Ja-Sager, datenbasiert und mit Gedächtnis über Strava und Notion.

**→ [Coach einrichten](https://c2mzbvnmdn-collab.github.io/ausdauer-coach/)** &nbsp;·&nbsp; **[Updates für Bestandsnutzer](https://c2mzbvnmdn-collab.github.io/ausdauer-coach/update.html)**

Aktueller Stand: **v1.3**

## Was ist das?

Kein fertiger Bot zum Installieren, sondern eine Anweisung (Prompt), die Claude in einen spezialisierten Ausdauer-Coach verwandelt. Er plant Training rückwärts vom Wettkampf, denkt Kraft/Mobilität und Fueling mit, zieht echte Einheiten aus Strava und merkt sich alles in Notion. Er widerspricht, wenn etwas unklug ist, statt zu beschwichtigen.

## Nutzung

1. Die **[Einrichtungs-Seite](https://c2mzbvnmdn-collab.github.io/ausdauer-coach/)** öffnen und den vier Schritten folgen (~10 Minuten): Prompt kopieren → Strava verbinden → Notion verbinden → loslegen. Auch mit Claude Free nutzbar (mit kleinen Abstrichen).
2. Schon eingerichtet und es gibt eine neue Version? Über die **[Update-Seite](https://c2mzbvnmdn-collab.github.io/ausdauer-coach/update.html)** die eigene Version wählen – sie liefert **nur die neuen Änderungen** als Modul zum Einfügen. Der Coach geht sie einzeln mit dir durch (übernehmen/anpassen/überspringen).

Einrichtung und Updates laufen über die Website. Daneben gibt es das **Komplettpaket als Markdown-Dokument** – die eigenständige Gesamtfassung zum Lesen, Teilen und Archivieren. Ein PDF wird nicht mehr gepflegt.

## Aufbau des Repos

Statische GitHub-Pages-Seite: kein Build, keine Abhängigkeiten, kein Backend.

| Datei | Zweck |
|---|---|
| `index.html` | Grund-Einrichtung inklusive des vollständigen, kopierbaren Coach-Prompts. **Der Prompt lebt ausschließlich hier** – das ist die Quelle der Wahrheit. |
| `update.html` | Update-Seite für Bestandsnutzer. Trägt im `<script>` den `RELEASES`-Block mit den versionierten Prompt-Änderungen. |
| `README.md` | Dieses Dokument: Übersicht und Änderungshistorie (kanonisches Zuhause des Changelogs). |
| `Ausdauer-Coach_Komplettpaket_vX_Y.md` | Eigenständiges Gesamtdokument (Prompt + Anleitung + Updates + Changelog) zum Lesen/Teilen. Trägt die Versionsnummer im Dateinamen. |

## Pflege bei neuen Versionen (Maintainer)

1. Prompt in `index.html` ändern, die `# VERSION`-Zeile und die Footer-Version hochsetzen.
2. Nur bei **prompt-wirksamen** Änderungen: passenden Eintrag im `RELEASES`-Array in `update.html` ergänzen (`kind: "replace"` mit `find`/`replaceWith`, oder `kind: "add"` mit `addText`) und dort `LATEST` sowie `VERSION_BLOCK` aktualisieren. Reine Website-/Doku-Änderungen gehören **nicht** ins Modul (höchstens als `info`-Zeile) – sonst bekommt der Nutzer Text zum Einfügen, der in keinen Prompt gehört.
3. Changelog unten ergänzen.
4. Der `# VERSION`-Block muss in `index.html` und der `VERSION_BLOCK` in `update.html` **identisch** sein. Ebenso die alte/neue Textfassung eines `replace`-Deltas exakt so, wie sie im Prompt steht.
5. Fest verdrahtete URL: Die Adresse der Update-Seite steht im `# VERSION`-Block und in `update.html`. Bei Repo-Umbenennung beide nachziehen.

Die Versionsnummer bedeutet für Nutzer „ich habe alle Änderungen bis hier gesehen und entschieden" – nicht „exakter Prompt-Stand". Eine abgelehnte Änderung setzt die Version trotzdem hoch und taucht nicht erneut auf; wer sie später doch will, lässt das Update ab einer früheren Version noch einmal laufen.

## Änderungshistorie

**v1.3 · August 2026**
- **Update-System für Bestandsnutzer:** Der Prompt trägt jetzt einen `# VERSION`-Block – der Coach kennt seinen Stand. Neue, separate **Update-Seite** (`update.html`) liefert versioniert nur die jeweils neuen Prompt-Änderungen als Modul, das der Coach einzeln mit dem Nutzer durchgeht (übernehmen/anpassen/überspringen).
- Grund-Seite verlinkt dezent auf die Update-Seite.
- **PDF-Ausgabe eingestellt.** Das Paket wird als Website (Einrichtung + Updates), README und Markdown-Komplettdokument geführt; die Änderungshistorie liegt kanonisch in dieser README.

**v1.2 · August 2026**
- Prompt/ROLLE geschärft: Andere Sportarten werden weiterhin nicht geplant, ihre **Belastung** (Ermüdung, Regeneration, Verletzungsrisiko) fließt aber jetzt ausdrücklich in die Steuerung von Lauf und Rad ein.
- Notion-Struktur entdoppelt: Teil 3 auf einen Kurzüberblick eingedampft (volle Struktur + Gym-Log-Tabelle stehen nur noch im Prompt als verbindlicher Fassung).
- Sofort-Start-Hinweis konsolidiert: nur noch eine ausführliche Stelle, sonst ein Verweis.
- Website: „Assistent" → „Coach" vereinheitlicht; Triathlon-Hinweis entfernt (Fokus bleibt Laufen & Radfahren).

**v1.1 · August 2026**
- Hinweis ergänzt: Die Connector-Einrichtung (Strava/Notion) läuft über claude.ai im Browser, **nicht** über die Desktop-App.

**v1.0 · August 2026 – Erste vollständige Ausgabe**
- System-Prompt komplett: Onboarding mit Ziel + Datum zuerst; stehende Regeln (Datum-/Wetter-Abruf, Effort vor Pace, Progression, Fueling); Nutzungsmodi; Übernahme geplanter Einheiten & Pläne aus anderen Quellen; Notion-Struktur direkt im Prompt.
- Eigene Bausteine: Kraft & Mobilität; Ausrüstungsberatung (inkl. Prüfung der aktuellen Verfügbarkeit, Laufschuh-/Laufanalyse-Hinweis, Wettkampf-Pflichtausrüstung); Gesundheits-Leitplanken.
- Ton-Varianten (Berater & unterstützend), kinderleichte Einrichtung, Abschnitt „Chat neu starten", Abschnitt „Geht das mit Claude Free?".
- Ausgeliefert in drei Formaten: Website, PDF und Markdown (PDF seit v1.3 eingestellt; Markdown wird fortgeführt).

---

*Diese Vorlage ist ein Startpunkt – Struktur, Ton und Regeln lassen sich frei anpassen. Der Coach ersetzt keine medizinische, physiotherapeutische oder ärztliche Beratung.*
