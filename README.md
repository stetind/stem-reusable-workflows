## Reusable workflows

### Description
Reusable workflows with pre-defined GitHub actions.

### Usage
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
Where `COMPOSER_ACCESS_TOKEN` should be defined as a secret at
the repository that calls the reusable workflow.

* Sonar syntax
```yaml
  job_name:
    uses: stetind/stem-reusable-workflows/.github/workflows/sonar.yaml@main
    secrets: inherit
```
* Sonar Secret Variable Requirements:
  * SONAR_TOKEN => the sonar project token


### Avoid executions
* [see the article](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs) 