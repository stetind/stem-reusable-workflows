## Reusable workflows

### Description
Reusable workflows with pre-defined GitHub actions.

* [Laravel CI actions](#Laravel-ci-actions)
* [Automated Releases](#Automated-Releases)
* [Sonar](#Sonar)


### Avoid executions
* [see the article](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs) 


### Laravel CI actions
An action that runs basic checks like 
* phpunit
* linting
* PhpStan
* Code duplication 
* etc

#### Example Usage:
Add it directly in a job of your workflow with this syntax:

* CI syntax

* TODO check if we can use the secret.GITHUB_TOKEN instead COMPOSER_ACCESS_TOKEN
*
```yaml
  job_name:
    uses: stetind/stem-reusable-workflows/.github/workflows/ci.yaml@main
    secrets:
      COMPOSER_ACCESS_TOKEN: ${{ secrets.COMPOSER_ACCESS_TOKEN }}
```
Where `COMPOSER_ACCESS_TOKEN` should be defined as a secret at the repository that calls the reusable workflow.

### Automated Releases

This action automatically creates draft releases (with associated tags) when triggered. 

Each draft release includes:
* All commits since the last release commit
* An automatically generated changelog based on the commit messages, grouped by [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) _type_

The release name and the accompanying tag are incremented in accordance with the [Semantic Versioning](https://semver.org/) specification, taking into account the commits _type_

##### Supported commit types / Version pumping

| Version increment | Reason                                                                                                                 |
|-------------------|------------------------------------------------------------------------------------------------------------------------|
| Patch             | Commit type is `fix`, `bugfix`, `perf`, `ref`, `refactor`, `test`, `tests`, `chore`, `ci`, `docs`, `build`.                                    |
| Minor             | Commit type is `feat`, `feature`.                                                                                           |
| Major             | Commit message includes **BREAKING CHANGE**.  <br/> Commit type contains **!** (`type(scope)!: message` or `type!: message`) |



#### Example Usage:

```yaml
name: 📖 Generate Release

on:
    workflow_run:
        workflows: [CI]
        types:
            - completed

jobs:
    generate-release:
        if: ${{ github.event.workflow_run.conclusion == 'success' }}
        uses: stetind/stem-reusable-workflows/.github/workflows/generate-release.yaml@main

```

### Sonar
```yaml
  job_name:
    uses: stetind/stem-reusable-workflows/.github/workflows/sonar.yaml@main
    secrets: inherit
```
* Sonar Secret Variable Requirements:
    * SONAR_TOKEN => the sonar project token

* Sonar extra configuration
  In order to be able to run the analysis, the repository must has, the `sonar-project.properties` file on root

example

```
sonar.organization=elearningindustry
sonar.projectKey={project key from sonar}
sonar.projectName={title}
sonar.projectVersion=1.0.0
sonar.sources=/*src*/
sonar.tests=/*test*/
# sonar.javascript.lcov.reportPaths=coverage/lcov.info
```
