# Multiple Jira Transition
Transition Multiple Jira issues

Forked from the original jira transition action [gajira-transition](https://github.com/atlassian/gajira-transition) repository
Updated to add support to transition multiple Jira issues per job
> ##### Only supports Jira Cloud. Does not support Jira Server (hosted)

## Usage

> ##### Note: this action requires [Jira Login Action](https://github.com/marketplace/actions/jira-login)

![Issue Transition](../assets/example.gif?raw=true)

Example transition action:

```yaml
- name: Transition issue
  uses: ./
  with:
    issueList: ./jiras-completed.txt
    transition: "Released to Production"
```

The `issueList` parameter is a file containing a list of one or more Jira keys to transition (for an example see `jiras-completed.txt`)

```yaml
on:
  push

name: Test Transition Issue

jobs:
  test-transition-issue:
    name: Transition Issue
    runs-on: ubuntu-latest
    steps:
    - name: Login
      uses: atlassian/gajira-login@master
      env:
        JIRA_BASE_URL: ${{ secrets.JIRA_BASE_URL }}
        JIRA_USER_EMAIL: ${{ secrets.JIRA_USER_EMAIL }}
        JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}
        
    - name: Create new issue
      id: create
      uses: atlassian/gajira-create@master

    - name: Transition issue
      uses: ./
      with:
        issueList: ./jiras-completed.txt
        transition: "In Progress"
```
----
## Action Spec:

### Environment variables
- None

### Inputs
- `issueList` (required) - file containing a list of issue keys to perform a transition on
- `transition` - Case insensetive name of transition to apply. Example: `Cancel` or `Accept`
- `transitionId` - transition id to apply to an issue

### Outputs
- None
