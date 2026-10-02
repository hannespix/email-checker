# E-Mail-Checker („Pix & fertig“)

Statische Single-File-Webanwendung (`index.html`) zum Prüfen von E-Mail-Adressen aus Excel.
Live unter **https://hannespix.github.io/email-checker/** (GitHub Pages).

## Dateien

- `index.html` – die komplette Anwendung (kein Build, keine Abhängigkeiten, keine externen Ressourcen)
- `.nojekyll` – verhindert eine Jekyll-Verarbeitung durch Pages
- `lizenzen/OFL-Jersey-10.txt` – Lizenz der eingebetteten Schrift „Jersey 10“
- `README.md` – Beschreibung für Nutzer
- `.github/workflows/deploy-pages.yml` – Deployment auf GitHub Pages

## Update-Workflow – bei jedem Update genau so vorgehen

Der Repo-Inhaber liefert Updates als ZIP (z. B. `pix-und-fertig.zip`) oder als einzelne Dateien.
Dann ohne Rückfrage diesen Ablauf durchführen:

1. **Entpacken.** Die Dateien aus dem ZIP-Ordner (z. B. `pix-und-fertig/`) gehören ins **Repo-Root**,
   nicht in einen Unterordner. Bestehende Dateien werden ersetzt.
2. **Feature-Branch.** Nie direkt auf `main` arbeiten. Branch von `main` abzweigen, Dateien einspielen.
   Enthält das README wieder den Platzhalter `https://BENUTZERNAME.github.io/pix-und-fertig/`,
   durch `https://hannespix.github.io/email-checker/` ersetzen.
3. **Commit & Push** des Branches.
4. **Pull Request gegen `main`** erstellen und **sofort mergen** (Merge-Commit).
   Nicht auf Review warten – der Merge ist ausdrücklich beauftragt.
5. **Deployment prüfen.** Der Merge startet den Workflow „Deploy to GitHub Pages“ (Actions).
   Lauf beobachten, bis er grün ist. Bei Fehlern das Job-Log lesen, beheben, erneut mergen.
6. **Live-Check.** `https://hannespix.github.io/email-checker/` abrufen und sicherstellen, dass die
   neue Version ausgeliefert wird (z. B. anhand einer geänderten Stelle im HTML).
7. **Kurz berichten:** PR-Nummer, Merge-Commit, Workflow-Status, Live-URL.

## Deployment-Details

- Pages-Quelle ist „GitHub Actions“. Der Workflow läuft bei jedem Push auf `main` und manuell per `workflow_dispatch`.
- Das gesamte Repo-Root wird als Site-Artefakt hochgeladen (`.git` und `.github` ausgenommen).
- Es gibt keinen Build-Schritt: Was im Repo liegt, wird 1:1 veröffentlicht.
