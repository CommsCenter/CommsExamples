# Layouts
Every page is by in the default layout component `pckg-app` with html attribute `data-frontend`.
Default layout renders 3 positions (`header`, `content` and `footer`) while custom layouts can add more positions (such as `sidebar`).

<pckg-app data-frontend></pckg-app>

## Mixin pckgLayout
Provides basic properties for all templates.
 - computed
   - `groupedActions` array
   - `groupedRootElements` object

## comms.json
`layout` share type additional properties are:
 - `slots` - object with available slots in the Page builder

Updated `comms.json` looks like:
```
{
    ...
    "layout": {
        "slots": {
            "header": "Header",
            "content": "Content",
            "footer": "Footer",
            "sidebar": "Sidebar"
        }
    }
}
```

## Build
Follow classic build procedure as described [here](./../README.md).
   
## All layouts
See [all layouts on Hub](https://hub.comms.dev/)