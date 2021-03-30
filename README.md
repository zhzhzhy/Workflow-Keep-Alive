# Workflow-Keep-Alive
**A Github action to keep Another Repo workflow alive**

1. Fork this repository
2. Create some sercets in your repository(Settings -> Secrets)
	- REST_TOKEN: Create a token with the permission ```admin:org, delete:packages, repo, user, workflow, write:packages``` in the access token, and then use the value of this token to create a sercet named REST_TOKEN in your repo
	- API_ADDRESS: Use this format:
```https://api.github.com/repos/{owner}/{repo}/actions/workflows/{workflow_id}/enable``` 
See Docs in [https://docs.github.com/cn/rest/reference/actions#enable-a-workflow](https://docs.github.com/cn/rest/reference/actions#enable-a-workflow)


