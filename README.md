# Schnellheim

Eine einzelne Seite fürs Handy: die nächsten Busse von **Tullnerfeld Bahnhof nach Judenau**,
mit Bussteig, Countdown, Verspätung und Ausfällen.

Kein Build, kein Server, keine Abhängigkeiten – alles steckt in `index.html`.

## Benutzen

`index.html` im Browser öffnen oder auf einen beliebigen Webserver legen.

Mit GitHub Pages: *Settings → Pages → Deploy from a branch → `main` / root*. Die Seite liegt
dann unter `https://teachers-petgoat.github.io/schnellheim/` und lässt sich am Handy zum
Home-Bildschirm hinzufügen. Achtung: Eine Pages-Seite ist öffentlich erreichbar.

## Einstellungen

Oben im Skript von `index.html` steht der Block `CONFIG`:

| Wert | Bedeutung |
|---|---|
| `from` | evaId der ÖBB-Abfahrtstafel (`8102059` = Tullnerfeld) |
| `dest` | Namensanfang oder evaId der Zielhaltestellen, mehrere mit Komma |
| `results` | Anzahl der fahrenden Busse (Standard 3) |
| `refreshSeconds` | Abstand der automatischen Aktualisierung |
| `platformMap` | Linie → Steig, falls die Tafel keinen Steig liefert, z. B. `{'410': 'C'}` |
| `charset` | bei kaputten Umlauten auf `''` stellen |

## URL-Schalter

- `?demo` – Beispieldaten (Linien und Steige sind erfunden)
- `?debug` – zeigt gefundene Zielhaltestellen und die Rohdaten der Tafel
- `?reset` – sucht die Zielhaltestellen neu (sie werden im Browser gemerkt)

## Datenquelle

Die Seite lädt die ÖBB-Abfahrtstafel (`fahrplan.oebb.at/bin/stboard.exe`) als Skript und
filtert mit `dirInput` auf Fahrten, die in Judenau halten. Die Nummern der Judenau-Haltestellen
holt sie einmalig über die ÖBB-Haltestellensuche. Schlägt die Suche fehl, zeigt sie alle Busse
der Tafel und weist in der Statuszeile darauf hin.

Das ist keine offiziell dokumentierte Schnittstelle; sie kann sich ohne Ankündigung ändern.

## Stand

Oberfläche und Auswertung sind gegen eine nachgebaute Antwort getestet, **noch nicht gegen die
echte ÖBB-Tafel**. Offen ist insbesondere:

- ob der Browser die Antwort der ÖBB als Skript annimmt,
- ob Busse auf der Tafel `8102059` stehen und einen Steig (Feld `tr`) haben,
- ob die Haltestellensuche und `dirInput` wie erwartet filtern.

`?debug` zeigt, was tatsächlich ankommt.
