# autosquash@v1

This action enables automatic squash commits on pull requests when the repository has 'automatic merging' enabled.

To add this action use the following workflow:

```yaml
name: autosquash
on:
  pull_request:
    types:
      - opened
      - synchronized
      - reopened
      - edited
      - labeled
      - unlabeled
      - ready_for_review
jobs:
  autosquash:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: theoremlp/autosquash@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          pull-request-number: ${{ github.event.pull_request.number }}
          squash-commit-title: "${{ github.event.pull_request.title }} (#${{ github.event.pull_request.number }})"
          squash-commit-message: "${{ github.event.pull_request.body }}"
```
