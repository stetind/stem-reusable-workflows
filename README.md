## Reusable workflows

### Description
Reusable workflows with pre-defined GitHub actions.

### Usage
Add it directly in a job of your workflow with this syntax:
```yaml
  job_name:
    uses: stetind/stem-reusable-workflows/.github/workflows/ci.yaml@main
    secrets:
      COMPOSER_ACCESS_TOKEN: ${{ secrets.COMPOSER_ACCESS_TOKEN }}
```
Where `COMPOSER_ACCESS_TOKEN` should be defined as a secret at
the repository that calls the reusable workflow.
