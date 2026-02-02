# HytaleModManager

This mod for Hytale checks if any installed mod can be updated to a newer version.

## Goals

- [ ] Check for updates to any mod installed on the server
- [ ] Notify via server logs, ingame notification, webhooks

## Limitiations

- Currently only works with CurseForge

## Roadmap

- Integrate other mod sites
- Make the mod configurable
  - Specify the url / mod site which should be checked
  
## Not currently planned

- Auto updates

## Installation

1. Download the latest release
2. Copy it into the `mods` folder of your Hytale server

## Configuration

- If not present, create the `htmm.json` file in the `mods` folder

### General configuration

| option | required | default | description |
| --- | --- | --- | --- |
| `notifyInLog` | no | false | writes a message in the server log |
| `notifyInGame` | no | false | uses `/notify` to make users aware of a new update |
| `notifyWithWebhooks` | no | false | calls the specified webhooks |
| `mods` | yes | | the mods to check for updates |
| `webhooks` | no | `[]` | which webhooks to call when an update is detected |

### Mods configuration

| option | required | default | description |
| --- | --- | --- | --- |
| `name` | no | | The name of the mod, used for notifications. If empty or not specified, `fileName` is used |
| `fileName` | yes | | the filename of the mod, only needs to be set once |
| `modUrl` | yes | | Where the mod is hosted, only supports [curseforge](https://www.curseforge.com) for now |

### Webhook configuration

| option | required | default | description |
| --- | --- | --- | --- |
| `type` | no | `generic` | can be `generic` or `discord` (always uses `POST`) |
| `url` | yes | | the webhook url |
| `method` | no | `GET` | `GET` or `POST` |
| `fields` | no | `[ "mod", "file", "url" ]` | the fields which will be included when the webhook method is `POST` |
| `excludeMods` | no | `[]` | Mods for which this webhook is not called |

### Example configuration

```json
{
    "notifyInLog"       : true,
    "notifyInGame"      : true,
    "notifyWithWebhooks": true,
    "mods"              : [
        {
            "name"    : "MultipleHUD",
            "fileName": "MultipleHUD-1.0.4.jar",
            "modUrl"  : "https://www.curseforge.com/hytale/mods/multiplehud"
        },
        {
            "name"    : "ExampleMod",
            "fileName": "ExampleMod-1.0.0.jar",
            "modUrl"  : "https://www.curseforge.com/hytale/mods/examplemod"
        }
    ],
    "webhooks"          : [
        { "url": "https://discord.com/api/webhooks/123456789/abcdefghi" },
        {
            "type"       : "generic",
            "url"        : "https://webhook.site/73889e10-b951-4a1b-9950-a26c1dcdbe1b",
            "method"     : "POST",
            "fields"     : [ "mod", "file", "url" ],
            "excludeMods": [ "ExampleMod" ]
        }
    ]
}
```
