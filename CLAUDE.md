# E-Mail-Checker („Pix & fertig“)

Statische Single-File-Webanwendung (`index.html`) zum Prüfen von E-Mail-Adressen aus Excel,
dazu Impressum (`impressum.html`) und Datenschutzhinweis (`datenschutz.html`).
Live unter **https://hannespix.github.io/email-checker/** (GitHub Pages).

## Dateien

- `index.html` – die komplette Anwendung (kein Build, keine Abhängigkeiten, keine externen Ressourcen),
  unten mit Fußzeile und Links auf Impressum und Datenschutz
- `impressum.html` – Impressum im Look der Anwendung. Die Angaben entsprechen dem Impressum von pix-el.de
  (Repo `hannespix/pix-el`, `src/App.jsx`, `ImpressumContent`). Ändern sich Name, Anschrift oder E-Mail,
  alle Stellen anpassen: `impressum.html`, `datenschutz.html` (Abschnitt „Verantwortlich“) und pix-el.de.
- `datenschutz.html` – Datenschutzhinweis im selben Look. Er beschreibt die aktuelle Funktionsweise:
  keine Cookies, kein Speichern im Browser, keine Netzwerkzugriffe, keine nachgeladenen Inhalte,
  Hosting über GitHub Pages. Stimmt das nach einem Update nicht mehr, muss der Text angepasst werden.
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
3. **Fußzeile erhalten.** Bringt das Update eine neue `index.html` ohne Links auf `impressum.html`
   und `datenschutz.html` mit, die Fußzeile wieder einsetzen (siehe „Fußzeile“ unten).
   `impressum.html` und `datenschutz.html` bleiben, wie sie sind.
4. **Datenschutz prüfen.** Die neue `index.html` nach `localStorage`, `sessionStorage`, `indexedDB`,
   `document.cookie`, `fetch(`, `XMLHttpRequest`, `sendBeacon`, `WebSocket` und externen URLs in
   `src`/`href` durchsuchen. Taucht davon etwas neu auf, `datenschutz.html` anpassen und im Bericht darauf hinweisen.
5. **Commit & Push** des Branches.
6. **Pull Request gegen `main`** erstellen und **sofort mergen** (Merge-Commit).
   Nicht auf Review warten – der Merge ist ausdrücklich beauftragt.
7. **Deployment prüfen.** Der Merge startet den Workflow „Deploy to GitHub Pages“ (Actions).
   Lauf beobachten, bis er grün ist. Bei Fehlern das Job-Log lesen, beheben, erneut mergen.
8. **Live-Check.** `https://hannespix.github.io/email-checker/`, `…/impressum.html` und `…/datenschutz.html`
   abrufen und sicherstellen, dass die neue Version ausgeliefert wird (z. B. anhand einer geänderten Stelle im HTML).
9. **Kurz berichten:** PR-Nummer, Merge-Commit, Workflow-Status, Live-URL.

## Fußzeile

Die Fußzeile steckt in `index.html` an zwei Stellen. Fehlt sie nach einem Update, beides wieder einfügen.
`impressum.html` und `datenschutz.html` haben dieselbe Fußzeile; dort trägt der Link auf die
jeweils eigene Seite zusätzlich `aria-current="page"`.

- **CSS** direkt vor der ersten `@media`-Regel im `<style>`-Block:

  ```css
  /* ---------- Fußzeile mit Impressum und Datenschutz ---------- */
  body { min-height: 100vh; }
  /* Bei kurzem Inhalt sitzt die Leiste am unteren Fensterrand, sonst am Seitenende. */
  .fuss { position: sticky; top: 100vh; background: var(--lcd-3); color: var(--lcd-0); border-top: 4px solid var(--lcd-0); }
  .fuss::before {
    content: ""; position: absolute; inset: 0; pointer-events: none;
    background: linear-gradient(rgba(15, 56, 15, .08) 1px, transparent 1px) 0 0 / 100% 4px,
                linear-gradient(90deg, rgba(15, 56, 15, .08) 1px, transparent 1px) 0 0 / 4px 100%;
  }
  .fuss .wrap { position: relative; display: flex; flex-wrap: wrap; justify-content: space-between; align-items: baseline; gap: .5rem 1.5rem; padding-top: 1rem; padding-bottom: 1.1rem; font: 400 20px/1 var(--pixel); }
  .fuss nav { display: flex; flex-wrap: wrap; gap: .5rem 1.5rem; }
  .fuss a { color: inherit; font-weight: 400; text-decoration-thickness: 2px; text-underline-offset: 3px; }
  .fuss a:hover { background: var(--lcd-4); }
  .fuss a[aria-current="page"] { text-decoration: none; }
  ```

- **HTML** direkt nach `</main>`:

  ```html
  <footer class="fuss">
    <div class="wrap">
      <span>Pix &amp; fertig</span>
      <nav aria-label="Rechtliches">
        <a href="impressum.html">Impressum</a>
        <a href="datenschutz.html">Datenschutz</a>
      </nav>
    </div>
  </footer>
  ```

## Deployment-Details

- Pages-Quelle ist „GitHub Actions“. Der Workflow läuft bei jedem Push auf `main` und manuell per `workflow_dispatch`.
- Das gesamte Repo-Root wird als Site-Artefakt hochgeladen (`.git` und `.github` ausgenommen).
- Sicherheitsnetz: Fehlt in `index.html` der Verweis auf `impressum.html` oder `datenschutz.html`, ergänzt
  der Workflow für dieses Deployment eine schlichte Fußzeile mit beiden Links und meldet eine Warnung.
  Das Repo bleibt dabei unverändert; die richtige Fußzeile gehört trotzdem in `index.html` (Schritt 3 oben).
- Sonst gibt es keinen Build-Schritt: Was im Repo liegt, wird 1:1 veröffentlicht.
