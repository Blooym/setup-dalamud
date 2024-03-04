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

## Usage in MSBuild

Add the following to your .csproj or .targets file, replacing any existing definitions of DalamudLibPath property.

<PropertyGroup>
  <DalamudLibPath Condition="$([MSBuild]::IsOSPlatform('Windows'))">$(appdata)\XIVLauncher\addon\Hooks\dev\</DalamudLibPath>
  <DalamudLibPath Condition="$([MSBuild]::IsOSPlatform('Linux'))">$(HOME)/.xlcore/dalamud/Hooks/dev/</DalamudLibPath>
  <DalamudLibPath Condition="$([MSBuild]::IsOSPlatform('OSX'))">$(HOME)/Library/Application Support/XIV on Mac/dalamud/Hooks/dev/</DalamudLibPath>
  <DalamudLibPath Condition="$(DALAMUD_HOME) != ''">$(DALAMUD_HOME)/</DalamudLibPath>
</PropertyGroup>

You will now be able to use the DALAMUD_HOME environment variable to override the default DalamudLibPath when it's set.
