# Versioning (Next SemVers)

Compute the next `major`, `minor`, and `patch` versions from a given SemVer string (`WyriHaximus/github-action-next-semvers`).

## Inputs
- `version` *(required)* — e.g. `1.2.3`, `v1.2.3`, or `1.2.3-alpha`
- `strict` (default: `"true"`) — if `"false"`, pads missing segments with `.0`

## Outputs
Given `1.2.3`:
- `major`: `2.0.0` | `v_major`: `v2.0.0`
- `minor`: `1.3.0` | `v_minor`: `v1.3.0`
- `patch`: `1.2.4` | `v_patch`: `v1.2.4`

*(For pre-releases like `1.2.3-alpha`, `patch` becomes `1.2.3`.)*

## Example
```yaml
- uses: actions/checkout@v4

- name: Get previous tag
  id: previoustag
  uses: WyriHaximus/github-action-get-previous-tag@v1
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

- name: Get next semver versions
  id: semvers
  uses: WyriHaximus/github-action-next-semvers@v1
  with:
    version: ${{ steps.previoustag.outputs.tag }}

- name: Use next patch version
  run: echo "Next patch is ${{ steps.semvers.outputs.v_patch }}"
```
