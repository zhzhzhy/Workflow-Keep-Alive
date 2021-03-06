# Workflow-Keep-Alive
[![Run](https://github.com/zhzhzhy/Workflow-Keep-Alive/actions/workflows/main.yml/badge.svg)](https://github.com/zhzhzhy/Workflow-Keep-Alive/actions/workflows/main.yml)<br>

**A Github action to keep Another Repo workflow alive after 60days inactive**<br>

### Steps:

1. Fork this repository
2. Create some sercets in your repository(Settings -> Secrets)
	- `REST_TOKEN`: Create a token with the permission ```admin:org, delete:packages, repo, user, workflow, write:packages``` in the access token, and then use the value of this token to create a sercet named REST_TOKEN in your repo
	- `API_ADDRESS`: Use this format:
```https://api.github.com/repos/{owner}/{repo}/actions/workflows/{workflow_id}/enable```<br>
You can replace `workflow_id` with the workflow file name. For example, you could use `main.yaml`<br>
See Docs in [https://docs.github.com/cn/rest/reference/actions#enable-a-workflow](https://docs.github.com/cn/rest/reference/actions#enable-a-workflow)
3. Run github action again,check if the workflow in another repo is enabled.

**Notice:** This workflow could be disabled by Github after 60 Days inactive.
**To wake up mutually,YOU MUST Do** above steps in the target repo's workflow again,then add following Github Action after `step:`<br>
```
    - name: curl
      id: enable_workflow
      env:
        REST_TOKEN: ${{ secrets.REST_TOKEN }}
        API_ADDRESS: ${{ secrets.API_ADDRESS }}
      run: |
        echo "Enable Workflow Start..."
        curl -X PUT -H "Authorization: token $REST_TOKEN" "$API_ADDRESS"
        echo "Finished"
```
And cron timer after `on:`<br>
```
schedule:
    - cron: 00 00 * * *
```
Run github action and check if this repo workflow is enabled.


