# Components

Custom components can be anything. They can be added to the page as normal action with pagebuilder.

Few examples:
 - counter
 - calendar
 - graph
 - game
 - slider

## Mixin `pckgComponent`
 - props:
  - `action` object
  - `content` object

## comms.json
`component` share type additional properties are:
 - `slots` - object with available slots in the Page builder

Updated `comms.json` looks like:
```
{
    ...
    "component": {
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
   
## All components
See [all components on Hub](https://hub.comms.dev/)