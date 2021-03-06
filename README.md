# Automated Branch Pull Requests

This action will open a pull request to the repository default branch (or otherwise specified)
whenever a branch with some prefix (can be empty, will lead to executuon for all branches) is pushed to.
The idea is that you can set up some workflow that pushes content to branches of the repostory,
and you would then want this push reviewed for merged.

Here is an example of what to put in your `.github/main.workflow` file to
trigger the action.

```
# workflow auto-pr
workflow "auto-pr" {
  resolves = ["create-pr"]
  on = "push"
}

action "create-pr" {
  uses = "smartinspereira/auto-create-pr-action@master"
  secrets = ["GITHUB_TOKEN"]
  env = {
    BRANCH_PREFIX = ""
    # BASE_BRANCH = ""
    # PULL_REQUEST_TITLE = ""
    # PULL_REQUEST_BODY = ""
    PULL_REQUEST_DRAFT = "true"
  }
}
```

Environment variables include:

  - **BRANCH_PREFIX**: the prefix to filter to. If the branch doesn't start with the prefix, it will be ignored
  - **BASE_BRANCH**: the branch to issue the pull request to. Defaults to the repositores default branch (optional)
  - **PULL_REQUEST_BODY**: the body for the pull request (optional)
  - **PULL_REQUEST_TITLE**: the title for the pull request  (optional)
  - **PULL_REQUEST_DRAFT**: should the pull request be a draft PR? (optional; unset defaults to `false`)
