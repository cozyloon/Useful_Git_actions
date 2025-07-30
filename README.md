# Useful_Git_actions

https://github.com/amannn/action-semantic-pull-request
```
name: "Semantic PR Check"

on:
  pull_request:
    types: [opened, edited]

permissions:
  pull-requests: read

jobs:
  main:
    name: Validate PR title
    runs-on: ubuntu-latest
    steps:
      - uses: amannn/action-semantic-pull-request@v5.5.3
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          subjectPattern: ^([A-Za-z0-9]+-\d+|\bNOJIRA\b)\s*(\|\s*)?.+
          types: |
            fix
            feat
            style
            docs
            refactor
            test
```


