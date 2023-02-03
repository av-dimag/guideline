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

### Commit Message Format

```text
<type>(<scope>): <subject>
```

#### Type

Der Typ muss einer der folgenden sein:

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

#### Scope (optional)

Die Zuordnung zu einem Bereich (scope) ist optional. Es ist aber sinnvoll, wenn dieser auch gesetzt wird.

>
> :clipboard: Wir werden noch eine entsprechende Themenliste ausarbeiten.
>

Bisherige Scopes:

- workflow
- xml-converter
- ci/cd

#### Subject

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



### Add a label (optional)

This step is optional, since it has no impact on the release process anymore. However, adding at least one of the
corresponding labels to your PR will help quickly realize its purpose:

- **breaking**: breaking changes.
- **enhancement**: new feature.
- **bug**: a bug fix.
- **styling** update style (keine Änderung am produktiven Code).
- **documentation**: changes to the documentation.
- **testing**: all about tests: adding, refactoring tests (keine Änderung am produktiven Code).
- **refactor**: refactoring production code.
- **chore**: maintenance tasks (keine Änderung am produktiven Code).
- **dependencies**: update a dependency package version.

### Make a draft

Please [convert the pull request to draft](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request#converting-a-pull-request-to-a-draft)
as long it isn't ready for reviewing. As soon as the PR is [ready for review](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request#marking-a-pull-request-as-ready-for-review),
click on the corresponding button "Ready for review".

### Branch protection rules

The main branch of each repo (it's usually the `main` branch) is protected by the following rules:

- Require pull request reviews before merging
  - At least from one reviewer
- Require status checks to pass before merging
  - Require branches to be up-to-date before merging
  - Status checks e.g. tests defined in each repository's CI

When the PR is merged, the branch will be deleted automatically.

## Code Review

- Reviewers should pay attention to proper [PR title setting](#pr-title-format).

## General GitHub actions workflows (CI)

We use [GitHub actions](https://github.com/features/actions) to automate some processes.

### Run tests

With each push to GitHub, the tests of the repository are executed. Successful tests are needed to merge code into the
repository's main branch (s. [Branch protection rules](#branch-protection-rules)).

# Merge und Release

### Prepare release

We use [release-please-action](https://github.com/marketplace/actions/release-please-action) to prepare the next release.
This action script automates the CHANGELOG generation, the creation of GitHub releases, and version bumps. In doing so,
it creates a release PR which updates itself with each push into main branch following the commit messages. It's
important to use the defined rules from [above](#git-commit-guidelines) in all commits and in [PR titles](#pr-title-format).

### Create release

When we are ready to tag a release, simply merge the release PR. This will create a release on GitHub, builds the npm
package or the docker image and publishes on the corresponding platform.
