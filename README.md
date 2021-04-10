# When
This action is to be used with a workflow run for a push event with the pull number in the
commit message ( matches on #*pullnumber*)

# Behaviour
Will create comment/s in pull request and / or associated issues

# Inputs

## Comment
Provide the comment with the comment input

## Controlling where to add comment

Comments can be created in the pull request and / or associated issues - control with addTo.

## Related issues

The remaining inputs control the discovery of the pull request associated issues.

There are 4 ways that associated issues can be specified.
### Common

All 4 use the inputs closeWords and caseSensitive as part of their matching.  

Close words defaults to the close words used by github to automatically close an issue from a pull request.
### Pull request and commits

In the pull request itself - control with usePullTitle and usePullBody.

In the pull request commits - control with useCommitMessages.

The pull request title, pull request body and commit messages will match against *closeWord* #123

### Branch name

Control with useBranch, branchIssueWords and branchDelimiters.


The branch name will match *closeWord* *delimiter* *branchIssueWord* *delimiter* *issuenumber* e.g - fix-issue-123



# Example workflow yaml
```
name: add comment on push
on:
  push

jobs:
  add-comment-on-push:
    name: add comment to pull and issues
    runs-on: windows-2019
    steps:
      - name: add comment to issues
        uses: tonyhallett/addCommentToPullAndIssuesFromPushAction@v1.0.0
        env:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
            comment: 'fix merged'
            addTo: issues
```
      

