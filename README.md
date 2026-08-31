# Ausdauer-Coach

Ein KI-Trainingspartner für Ausdauersport (Laufen, Trail, Ultra, Radfahren), umgesetzt als System-Prompt für **Claude** – ehrlich beratend statt Ja-Sager, datenbasiert und mit Gedächtnis über Strava und Notion.

**→ [Coach einrichten](https://c2mzbvnmdn-collab.github.io/ausdauer-coach/)** &nbsp;·&nbsp; **[Updates für Bestandsnutzer](https://c2mzbvnmdn-collab.github.io/ausdauer-coach/update.html)**

Aktueller Stand: **v1.1**

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

### Versionsschema

Format `MAJOR.MINOR[.PATCH]`. Ab v1.1 gilt:

- **MINOR** (z. B. 1.5 → 1.6): spürbare Verhaltensänderung – neue oder geänderte Regeln, neuer Abschnitt, neues Feature.
- **PATCH** (z. B. 1.5 → 1.5.1): Verfeinerung, Klarstellung, Wortlaut, Doku-Anpassung, kleiner Tweak an bestehendem Verhalten.
- **MAJOR** (→ 2.0): nur bei grundlegendem Umbau des Konzepts.

So steigen die Nummern langsamer. Die gesamte Entwicklung nach der Erstausgabe wurde bewusst zu **einem** Release v1.1 zusammengefasst (nichts wurde vorher über das Update-System ausgeliefert). Bestehende Labels (v1.0, v1.1) bleiben ab jetzt unverändert – die Update-Seite ordnet Nutzer über genau diese Nummern zu, nachträgliches Umbenennen würde den Abgleich brechen. Die Vergleichslogik (`cmp` in `update.html`) kommt mit dreiteiligen Nummern bereits klar; bei einem Patch einfach die neue Nummer als Dropdown-Option ergänzen und `LATEST` setzen.

## Änderungshistorie

**v1.1 · August 2026**
- **Update-System für Bestandsnutzer:** `# VERSION`-Block im Prompt (der Coach kennt seinen Stand) plus separate **Update-Seite** (`update.html`), die versioniert nur neue Prompt-Änderungen als Modul liefert – der Coach geht sie einzeln mit dem Nutzer durch (übernehmen/anpassen/überspringen). Grund-Seite verlinkt dezent dorthin.
- **Andere Sportarten:** Der Coach fragt im Onboarding aktiv danach (Art, Häufigkeit, Intensität), plant sie nicht, rechnet ihre Belastung (Ermüdung, Regeneration, Verletzungsrisiko) aber in Lauf und Rad ein und bietet das an. Ausdauer-Aktivitäten bietet er an, aus Strava zu ziehen; nicht ausdauerbezogene beschreibt der Nutzer selbst.
- **Dokumentation & Konsistenz:** Notion-Struktur entdoppelt, Sofort-Start konsolidiert, „Assistent" → „Coach" vereinheitlicht, Triathlon-Hinweis entfernt (Fokus bleibt Laufen & Radfahren).
- **Web-only:** PDF-Ausgabe eingestellt; das Paket läuft als Website (Einrichtung + Updates), README (kanonische Änderungshistorie) und Markdown-Komplettdokument. Versionsschema festgelegt (MAJOR.MINOR.PATCH).
- Hinweis: Connector-Einrichtung (Strava/Notion) läuft über claude.ai im Browser, **nicht** über die Desktop-App.

**v1.0 · August 2026 – Erste vollständige Ausgabe**
- System-Prompt komplett: Onboarding mit Ziel + Datum zuerst; stehende Regeln (Datum-/Wetter-Abruf, Effort vor Pace, Progression, Fueling); Nutzungsmodi; Übernahme geplanter Einheiten & Pläne aus anderen Quellen; Notion-Struktur direkt im Prompt.
- Eigene Bausteine: Kraft & Mobilität; Ausrüstungsberatung (inkl. Prüfung der aktuellen Verfügbarkeit, Laufschuh-/Laufanalyse-Hinweis, Wettkampf-Pflichtausrüstung); Gesundheits-Leitplanken.
- Ton-Varianten (Berater & unterstützend), kinderleichte Einrichtung, Abschnitt „Chat neu starten", Abschnitt „Geht das mit Claude Free?".
- Ursprünglich in drei Formaten ausgeliefert (Website, PDF, Markdown); PDF seit v1.1 eingestellt.

---

*Diese Vorlage ist ein Startpunkt – Struktur, Ton und Regeln lassen sich frei anpassen. Der Coach ersetzt keine medizinische, physiotherapeutische oder ärztliche Beratung.*
