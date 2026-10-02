# Pix & fertig – Pix’ E-Mail-Checker

E-Mail-Adressen aus Excel prüfen, typische Tippfehler korrigieren und die Adressen je Beruf als BCC-Liste für Outlook kopieren.

**Direkt im Browser nutzen:** https://hannespix.github.io/email-checker/

## So funktioniert es

1. Excel-Datei (.xlsx oder .csv) hineinziehen oder Zellen aus Excel einfügen. Die Spalten für Beruf und E-Mail werden erkannt und lassen sich umstellen.
2. Die Adressen werden auf ihr Format geprüft. Eindeutige Fehler (Leerzeichen, `web,de`, `(at)`, `mailto:`) werden automatisch bereinigt, vermutete Tippfehler (`gmial.com`, `tonline.de`, `hotmail.con`) als Vorschlag angezeigt.
3. Je Beruf entsteht eine BCC-Liste ohne Dubletten, die sich mit einem Klick kopieren lässt.

Geprüft wird nur das Format. Ob ein Postfach tatsächlich existiert, zeigt erst der Versand.

## Datenschutz

Das Tool ist eine einzelne HTML-Datei ohne Server und ohne Nachladen von Inhalten. Die Daten werden ausschließlich im Browser verarbeitet und nicht übertragen oder gespeichert. Die Datei funktioniert auch heruntergeladen und offline.

## Lizenzen

Eingebettete Schrift „Jersey 10“: Copyright 2023 The Soft Type Project Authors, SIL Open Font License 1.1 – siehe [`lizenzen/OFL-Jersey-10.txt`](lizenzen/OFL-Jersey-10.txt).
