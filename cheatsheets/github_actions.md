# Github actions cheatsheet

- [Configuring and managing workflows](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow) from actions docs
- [Syntax](https://help.github.com/en/actions/reference/workflow-syntax-for-github-actions)
- [Github Actions Documentation](https://help.github.com/en/actions)

## Examples

### Python

Build to a matrix of Python versions.

```yaml
name: Python package

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      max-parallel: 4
      matrix:
        python-version: [3.6, 3.X]

    steps:
      - uses: actions/checkout@v1
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v1
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: make dev-install
      - name: Check formatting.
        run: make format
      - name: Lint with Pylint.
        run: make lint
```

## Pushing

Applies to pushes on master and branches, even if no PR.

```yaml
on: push
```

This comes from the docs but doesn't seem to add much from above.

```yaml
on: [push, pull_request]
```

Or trigger on Pull Request only. 

```yaml
on: pull_request
```
This is useful if you enforce checks passing in repo branch rules, which also means that PRs are needed and commits cannot be made to master directly.

This could be useful to avoid doing a check when pushing to a feature branch without a Pull Request. Assuming that is will rerun checks on pushes to the PR - to be confirmed.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0OTcxODMzOF19
-->