# Agent Check: Teamcity

# Overview

This check watches for build-related events and sends them to Datadog.

Unlike most Agent checks, this one doesn't collect any metrics—just events.

# Installation

The Teamcity check is packaged with the Agent, so simply [install the Agent](https://app.datadoghq.com/account/settings#agent) on your Teamcity servers. If you need the newest version of the check, install the `dd-check-teamcity` package.

# Configuration

## Prepare Teamcity

Follow [Teamcity's documentation](https://confluence.jetbrains.com/display/TCD9/Enabling+Guest+Login) to enable Guest Login. 

Create a file `teamcity.yaml` in the Agent's `conf.d` directory:

```
init_config:

instances:
  - name: My Website
    server: teamcity.mycompany.com
#   server: user:password@teamcity.mycompany.com # if you set basic_http_authentication to true
#   basic_http_authentication: true # default is false
    build_configuration: MyWebsite_Deploy # the internal build ID of the build configuration you wish to track
#   host_affected: msicalweb6 # defaults to hostname of the Agent's host
#   is_deployment: true       # causes events to use the word 'deployment' in their messaging
#   ssl_validation: false     # default is true
#   tags:                     # add custom tags to events
#   - test
```

Add an item like the above to `instances` for each build configuration you want to track.

Restart the Agent to start collecting and sending Teamcity events to Datadog.

# Validation

Run the Agent's `info` subcommand and look for `teamcity` under the Checks section:

```
  Checks
  ======
    [...]

    teamcity
    -------
      - instance #0 [OK]
      - Collected 0 metrics, 3 events & 0 service checks

    [...]
```

# Compatibility

The teamcity check is compatible with all major platforms.
