# Delete Full-Stack Preview Environment on K8s

Uses Open Source Uffizzi CLI `uffizzi preview delete` to delete on-demand, ephemeral test environment deployed onto your Kubernetes cluster.

## Inputs

### `id`

**Required** Deployment ID string

### `username`

Uffizzi username

### `project`

Uffizzi project slug

### `request-token`

Access token obtained from the GHA pipeline available as `ACTIONS_RUNTIME_TOKEN` in the pipeline environment. See example below.

### `request-token_url`

URL where the pipeline OIDC token can be requested from available as `ACTIONS_ID_TOKEN_REQUEST_URL` in the pipeline environment. See example below.

### `server`

URL of your Uffizzi installation

### `password`

Your Uffizzi password. Specify a GitHub Encrypted Secret and use it! See example below.

## Example usage
### Email and password login

```yaml
uses: UffizziCloud/delete-preview-action@v1
with:
  id: 'deployment-23'
  username: 'admin@uffizzi.com'
  server: 'https://app.uffizzi.com'
  project: 'default'
  password: ${{ secrets.UFFIZZI_PASSWORD }}
```

### OIDC token login

```yaml
delete-preview:
  name: "Delete Preview on Uffizzi"
  runs-on: ubuntu-20.04
  steps:
    - uses: actions/github-script@v6
      id: ci-job-token
      with:
        script: |
          const token = process.env['ACTIONS_RUNTIME_TOKEN']
          const runtimeUrl = process.env['ACTIONS_ID_TOKEN_REQUEST_URL']
          core.setOutput('request-token', token.trim())
          core.setOutput('request-token-url', runtimeUrl.trim())
    - uses: UffizziCloud/delete-preview-action@v1
      with:
        server: 'https://app.uffizzi.com'
        request-token: ${{ steps.ci-job-token.outputs.request-token }}
        request-token-url: ${{ steps.ci-job-token.outputs.request-token-url }}
        preview-id: 1
permissions:
  id-token: write
```
