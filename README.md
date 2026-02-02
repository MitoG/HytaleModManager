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
1. If not present, create the `htmm.json` file in the `mods` folder

```json

{
    "notifyInLog"       : true,
    "notifyInChat"      : true,
    "notifyWithWebhooks": true,
    "webhooks"          : [
        { "type": "discord", "url": "https://discord.com/api/webhooks/123456789/abcdefghi" },
        {
            "type"       : "generic",
            "url"        : "https://webhook.site/73889e10-b951-4a1b-9950-a26c1dcdbe1b",
            "method"     : "POST",
            "fields"     : [ "mod", "file", "updateUrl", "lastCheck" ],
            "excludeMods": [ "ExampleMod" ]
        }
    ],
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
    ]
}


```


