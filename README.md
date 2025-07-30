# Useful_Git_actions

Dorny reporter
```
https://github.com/dorny/test-reporter
```

Semantic PR Check

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

Welcome message for contributors

```
name : Greetings

on:
  fork:
  push:
    branches: [main]
  issues:
    types: [opened]
  issue_comment:
    types: [created]
  pull_request_target:
    types: [opened]
  pull_request_review_comment:
    types: [created]

jobs:
  welcome:
    name: Welcome Step
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: EddieHubCommunity/gh-action-community/src/welcome@main
        with:
          github-token: ${{ secrets.github_token }}
          issue-message: "<h3>Hey! contributor, thank you for opening an Issue 🎉.</h3>"
          pr-message: "<h3>Hey! contributor, thank you for opening a Pull Request 🎉.</h3>"
          footer: "<h3>Thank you for contributing to the project 🚀</h3>"
```

Delete branch on pr merge
```
name: delete branch on close pr
on:
  pull_request:
    types: [closed]

jobs:
  delete-branch:
    runs-on: ubuntu-latest
    steps:
      - name: Delete merged branch
        uses: SvanBoxel/delete-merged-branch@1.4.3
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
Checkstyle validation
```
name: run checkstyle analysis

on:
  pull_request:
    branches:
      - main

jobs:
  checkstyle:
    runs-on: ubuntu-latest
    timeout-minutes: 15
    steps:
      - uses: actions/checkout@v4

      - name: Set up JDK 11
        uses: actions/setup-java@v3
        with:
          java-version: 11
          distribution: 'temurin'
          cache: maven

      - name: checkstyle validations
        run: mvn checkstyle:check
```
