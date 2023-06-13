# Tests

> :warning: &nbsp; Das beschriebene Vorgehen zu den Testcases ist ein erster Entwurf. Details und Strukturen können jederzeit geändert oder angepasst werden.

Neben den [Unit- und e2e-Tests](https://github.com/av-dimag/ech-0160-dimag-ingest/actions/workflows/main.yml) sind wir auch auf standardisierte Tests von Seiten der User angewiesen.

Die einzelnen Testcases werden im Repository-spezifischen [Wiki](https://github.com/av-dimag/ech-0160-dimag-ingest/wiki) aufgelistet.

## Testcase-Beschreibung im Wiki

Der Titel der einzelnen Wiki-Seite sollte lediglich "T nn" (bspw. T 01) beinhaltet. Dies hilft uns, um einfach auf die einzelnen Testcases verlinken zu können. In [Issues](https://github.com/av-dimag/ech-0160-dimag-ingest/issues), wie auch in den [Discussions](https://github.com/av-dimag/ech-0160-dimag-ingest/discussions) reicht das Schreiben von [`T-01`](https://github.com/av-dimag/ech-0160-dimag-ingest/wiki/T-01) und der Link zum ersten Testcase wird automatisch gesetzt (ähnlich wie bspw. `#42`, um auf ein Issue, eine Discussion oder einen Pull Request zu verweisen). Leider funktionieren diese automatischen Verlinkungen nicht im Wiki selbst. Die andere Problematik ist, dass im Titel selbst kein "-" geschrieben werden kann, resp. wird dieser beim Speichern automatisch entfernt, ist aber bei der automatischen Verlinkung sehr wichtig!

Die Seite wird (wie bei Issues und Discussions) in [Markdown](https://www.markdownguide.org/) geschrieben.

```markdown
# [Name des Testcases]

## Beschreibung
<!-- kurze Beschreibung -->

## Erwartetes Ergebnis

1. Jeder Punkt
1. als Liste
1. aufführen

## Verweise auf Discussions

[#145](https://github.com/av-dimag/ech-0160-dimag-ingest/discussions/145)

## Verweise auf Issues

[#171](https://github.com/av-dimag/ech-0160-dimag-ingest/issues/171)

## Testergebnis (bei Erfolg)
<!-- evt. Screenshot hier einfügen -->

## Protokollierung

Die Protokollierung erfolgt über das [Discussion-Formular "Test Report"](https://github.com/av-dimag/ech-0160-dimag-ingest/discussions/new?category=test-report).
```

## Ablauf der Tests

Gemäss Beschreibung vorgehen und das erwartete Ergebnis überprüfen.

Im Repository <https://github.com/av-dimag/ech-0160-testdaten> befinden sich Test-SIPs (geordnet nach eCH-0160 Version), die verwendet werden können. Es empfiehlt sich aber auch, dass mit eigenen, richtigen Daten getestet wird, um unvorgesehenes besser abzufangen und zu korrigieren.

## Protokollierung in den Discussions

Die Tests werden innerhalb der Discussion in der Kategorie "Test Report" protokolliert. Dazu steht ein vorgefertigtes Formular zur Verfügung. Innerhalb dieser Kategorie auf "New Discussion" klicken oder folgendem Link folgen: <https://github.com/av-dimag/ech-0160-dimag-ingest/discussions/new?category=test-report>.

