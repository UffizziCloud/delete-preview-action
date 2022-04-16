# Delete Full-Stack Preview Environment on K8s

Uses Open Source Uffizzi CLI `uffizzi preview delete` to delete on-demand, ephemeral test environment deployed onto your Kubernetes cluster.

## Inputs

### `id`

**Required** Deployment ID string

### `username`

**Required** Uffizzi username

### `project`

**Required** Uffizzi project name

### `server`

URL of your Uffizzi installation

### `password`

Your Uffizzi password. Specify a GitHub Encrypted Secret and use it! See example below.

## Example usage

```yaml
uses: UffizziCloud/delete-preview-action@v1
with:
  id: 'deployment-23'
  username: 'admin@uffizzi.com'
  server: 'https://app.uffizzi.com'
  project: 'default'
  password: ${{ secrets.UFFIZZI_PASSWORD }}
```
