# do-git-from-action

exploring how to do git from an github action

## actions/checkout

The checkout action is already authenticated, so you can do git stuff without fuss

> The auth token is persisted in the local git config. This enables your scripts to run authenticated git commands.
– https://github.com/actions/checkout#push-a-commit-using-the-built-in-token

## Github CLI

You can do repo admin via the preauthenticatred Github CLI in an action

> GitHub CLI is preinstalled on all GitHub-hosted runners. For each step that uses GitHub CLI, you must set an environment variable called GITHUB_TOKEN to a token with the required scopes.
>
> You can execute any GitHub CLI command. For example, this workflow uses the gh issue comment subcommand to add a comment when an issue is opened.
– https://docs.github.com/en/actions/guides/using-github-cli-in-workflows

## actions/github-script

You can write fancy, preauthenticated JavaScripts to do all sorts of things:

> This action makes it easy to quickly write a script in your workflow that uses the GitHub API and the workflow run context.
```
on:
  issues:
    types: [opened]

jobs:
  comment:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/github-script@v4
        with:
          script: |
            github.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: '👋 Thanks for reporting!'
            })
```
> Note that github-token is optional in this action, and the input is there in case you need to use a non-default token.
> By default, github-script will use the token provided to your workflow.
– https://github.com/actions/github-script