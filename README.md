# sync-forks

Sync every fork repo in a GitHub organization with its upstream, using the
[`merge-upstream`](https://docs.github.com/en/rest/branches/branches#sync-a-fork-branch-with-the-upstream-repository)
API (via `gh repo sync`). A repo is only synced if its name contains `pattern`
and it is a fork; on merge-upstream failure it retries with `gh repo sync --force`.

## Inputs

| Name | Required | Default | Description |
|---|---|---|---|
| `github-token` | yes | — | Token with repo access, used as `GH_TOKEN` for `gh` CLI |
| `org` | no | `github.repository_owner` | Organization to scan |
| `pattern` | no | `--` | Substring a repo name must contain to be treated as a syncable fork |

## Outputs

| Name | Description |
|---|---|
| `all-repo-names` | Comma-separated names of every repo in the org (fork or not) |
| `synced` | Number of forks successfully synced |
| `total` | Number of forks matched by `pattern` |

## Usage

```yaml
- name: Sync forks
  id: sync
  uses: farfarfun-action/sync-forks@v1
  with:
    github-token: ${{ secrets.ACTION_GITHUB_TOKEN }}
```
