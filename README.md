# setup-dalamud

This action allows for cross-platform installing of [Dalamud](https://github.com/goatcorp/dalamud) branches in GitHub Actions pipelines. It uses `bash, curl, unzip` on UNIX-like systems and `Powershell, Invoke-WebRequest, and Expand-Archive` on Windows.

## Basic Usage

```yaml
- uses: Blooym/setup-dalamud@v1
  with:
    branch: release # Replace with 'stg' for staging builds 
```

## Configuration

The configuration options below can be passed under the `with:` key. 

From [action.yml](./action.yml)

```yaml
branch:
  description: "The branch name that should be installed. Use 'latest' for the stable branch."
  required: true
path-environment-variable:
  description: "The environment variable that final Dalamud installation path will be set under."
  required: true
  default: "DALAMUD_HOME"
distribution-source:
  description: "[Experimental] The source location for downloading Dalamud releases."
  required: true
  default: "https://goatcorp.github.io/dalamud-distrib"
```