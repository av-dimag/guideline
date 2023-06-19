# Wie sehen die Abläufe auf Github aus?

> :warning: &nbsp; Das Dokument ist im Aufbau und daher noch nicht vollständig!

Unsere Software steht unter der Git Versions Kontrolle. Dazu verwenden wir [GitHub](https://github.com/av-dimag). Hier wird hauptsächlich ein Ingest-Vorbereitungstool für den eCH-0160 Standard entwickelt:

[![ech-0160-dimag-ingest](https://img.shields.io/github/v/release/av-dimag/ech-0160-dimag-ingest?include_prereleases&label=eCH-0160-DIMAG-Ingest)](https://github.com/av-dimag/ech-0160-dimag-ingest)

Das Vorgehen bei der Entwicklung ist stets dasselbe. Wir folgen den Empfehlungen von [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow):

1. [Neuen Branch von "main" erstellen](#branch).
1. [Commits schreiben](#commits).
1. [Pull Request öffnen](#pull-request).
1. [Code Review durchführen](#code-review).
1. [Branch in `main` mergen](#merge-und-release)

## Sprache

Ich schlage vor, dass die Benennung des Branchs und der Commits in Englisch geschrieben werden.

## Branch

Branch werden anhand von Issues erstellt. Nachdem jemandem ein Issue zugewiesen wurde, kann über den Link `Create a branch` im jeweiligen Issue schnell ein Branch erstellt und darin gearbeitet werden. Die Benennung des Branchs erfolgt aus dem Titel des Issues, kann aber auch bereits ähnlich der späteren PR-Commit-Message (s. [commits](#commit-message-format)) erfolgen.

Ich kann mir ein System vorstellen, das mit dem Änderungstyp (feat, fix, chore, etc.) beginnt und durch einen Schrägstrich `/` von der restlichen Bezeichnung getrennt wird. Danach folgt der Bereich (scope) und eine kurzer Betreff (subject); alles in kebab-case mit Bindestrich "-".

Der [**Issue** #24](https://github.com/av-dimag/ech-0160-dimag-ingest/issues/24) ist ein Feature Request und hat den folgenden Titel: `feat [workflow]: Startseite mit Ladezone`

Der **Branch** würde dann wie folgt aussehen: `feat/workflow-landingpage`

Und, um es vorwegzunehmen, der spätere **Titel des PRs** sollte wie eine **Commit Message** geschrieben sein. In diesem Beispiel lautet dieser dann: `feat(workflow): Landingpage with drop zone`

>
> :clipboard: Hier kommt später auch die Thematik Codespace hinzu.
>

## Commits

Um eine einheitliche Lesbarkeit zu garantieren, insbesondere im Zusammenhang mit den Releases, den Versionen (s. [SemVer](https://semver.org/)) und den Changelogs, müssen die Commit-Nachrichten strikten Regeln folgen. Wir halten uns an [Conventional Commit messages](https://www.conventionalcommits.org/), die folgendes Format vorgeben:

### Format eines Commits

```text
<type>(<scope>): <subject>
```

#### Typ (type)

Der Typ muss einer der Folgenden sein:

- **fix**: bei Bug fixes. Ein solcher Commit ändert die Version auf Ebene **patch**
- **feat**: bei neuen Features. Ein solcher Commit ändert die Version auf Ebene **minor**.
- **refactor**: wenn der Code oder die Struktur aufgeräumt/reorganisert wird. Ein solcher Commit ändert die Version auf Ebene **patch**.
- **feat!**, **fix!**, **refactor!**, etc.: Im Falle eines Breaking Changes wird das Ausrufzeichen verwendet. Ein solcher Commit ändert die Version auf Ebene **major**.
  :warning: Es ist wichtig, dass das Ausrufezeichen vor dem Doppelpunkt steht; z.Bsp. `feat!: <subject>` oder `feat(workflow)!: <subject>`
- **docs**: Änderungen an der Dokumentation (keine Änderung am produktiven Code).
- **chore**: Wartungsarbeiten bspw. Github Actions o.ä. (keine Änderung am produktiven Code).
- **style**: Design Updates (keine Änderung am produktiven Code).
- **test**: Alles rund um Tests; auch im Fall von Test-Refactoring (keine Änderung am produktiven Code).

Die ersten vier Punkte dieser Liste haben einen Einfluss auf die Versionsnummer und werden in den Release Notes aufgeführt.

#### Bereich (scope; optional)

Die Zuordnung zu einem Bereich (scope) ist optional. Es ist aber sinnvoll, wenn dieser auch gesetzt wird.

>
> :clipboard: Wir werden noch eine entsprechende Themenliste ausarbeiten.
>

Bisherige Scopes:

- workflow
- xml-converter
- ci/cd

#### Betreff (subject)

Der Betreff (subject) beinhaltet eine knappe Beschreibung der Änderung:

- man verwendet den englischen *Imperativ*: "change" nicht "changed" oder "changes"
- Der erste Buchstabe wird *klein geschrieben*
- Am Ende steht *kein Punkt*

## Pull Request

### Titel und Beschreibung

Ein Pull Request entspricht in der Regel mindestens einem Issue oder einer User Story. Da wir für die Versionierung und die Releases die [release-please-action](https://github.com/marketplace/actions/release-please-action) verwenden, ist es sehr wichtig, dass der PR Titel korrekt geschrieben wird. Der Titel wird für die Commit Message des Merges übernommen. Deshalb muss er, wie unter [Commits](#commits) definiert, entsprechend geschrieben werden; s. auch das Beispiel unter [Branch](#branch).
Wird der Titel falsch geschrieben, wird der PR später nicht im Changelog oder in den Release Notes aufgelistet!

In der Beschreibung wird immer der zugehörige Issue verlinkt. Dazu wird eines der [Github-Schlüsselwörter](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/using-keywords-in-issues-and-pull-requests) `resolves`, `closes` etc. gefolgt von der Issue Nummer.

```text
resolves #42
```

In diesem Beispiel wird der Issue Nr. 42 mit dem PR beidseitig verknüpft und nach dem Merge ebenfalls automatisch geschlossen.

### Label (optional)

Das Setzen eines Labels ist optional, ist aber sicher hilfreich beim Sortieren und Auffinden bestimmter Pull Requests. Im Release Prozess hat es jedenfalls keinen Einfluss mehr.

- **breaking**: Breaking Changes.
- **enhancement**: Neue Features.
- **bug**: Bug fixes.
- **styling** Style resp. Design Updates (keine Änderung am produktiven Code).
- **documentation**: Änderungen an der Dokumentation.
- **testing**: Alles mit Tests (keine Änderung am produktiven Code).
- **refactor**: Simples Überarbeiten des Codes.
- **chore**: Wartungsarbeiten, insbesondere Github betreffend (CI/CD) (keine Änderung am produktiven Code).
- **dependencies**: Updates von Paketversionen.

### Entwurf

Bitte [konvertiere den Pull Request zu einem Entwurf](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request#converting-a-pull-request-to-a-draft)
so lange dieser nicht parat für den Review ist. Sobald dies der Fall ist, wird der [Entwurfsstatus wieder entfernt](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request#marking-a-pull-request-as-ready-for-review),
klicke dazu auf die entsprechende Schaltfäche: "Ready for review".

### Geschützter Branch

Der Hauptbranch `main` in jedem Repository ist geschützt. Folgende Regeln müssen vor einem Merge eingehalten werden:

- Mindestens ein Code Review wird benötigt
- Status Checks:
  - Branch muss von Seiten `main` aktualisiert sein
  - Test- und Build-Prozess in den Github Actions (CI/CD) müssen erfolgreich sein

Nach dem Mergen wird der entsprechende Branch automatisch gelöscht.

### Code Review

- Ein Reviewers soll neben dem Code, der Funktionalität auch die [PR Titel Einstellungen](#titel-und-beschreibung) prüfen, damit [Release-Please](#release-vorbereiten) einwandfrei funktioniert.

## GitHub Actions (CI/CD)

Wir benutzen [GitHub Actions](https://github.com/features/actions), um automatisch Tests, Releases und das Deployment durchzuführen.

### Tests

Mit jedem Push nach GitHub werden "Builds" und Tests ausgeführt. Diese müssen erfolgreich durchlaufen, bevor neuer Code in den Hauptbranch gemergt werden kann (s. [Geschützter Branch](#geschützter-branch)).

### Release vorbereiten

Wir benutzen [release-please-action](https://github.com/marketplace/actions/release-please-action), um einen Release vorzubereiten. Dieses GH Action Skript erstellt automatisch die `CHANGELOG.md`-Datei, macht Releases und setzt die korrekte Versionsnummer z.B. im `package.json`. Release-Please arbeitet in zwei Schritten: Zuerst erstellt resp. aktualisiert die Action nach jedem Merge in den Hauptbranch einen sogenannten Release-PR. Wenn dieser PR dann gemergt wird, erstellt die Action einen Release-Tag und bildet daraus den Release selbst.
Um einen sauberen Ablauf und übersichtliche Release Notes zu gewährleisten, ist das Beachten der oben erwähnten [Commit-Regeln](#commits) in den [PR Titeln](#titel-und-beschreibung) zwindend notwendig.

### Release erstellen

Sobald wir für einen neuen Release bereit sind, wird der Release PR durchgesehen (Review) und daraufhin zusammengeführt (merge). Dadurch wird automatisch der entsrpechende Release publiziert und das Produkt innert kürzester Zeit bereitgestellt. Der Download wird dem [Release angehängt](https://github.com/av-dimag/ech-0160-dimag-ingest/releases/latest).
