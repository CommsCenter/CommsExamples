# Headers
Headers usually display a logo (desktop and mobile version), menu (desktop and mobile version), and conditionally the basket module or CTA button. Advanced headers feature multiple menus, custom sections or slots, search component, user profile and more.

`<hub-header-vendor-foo></hub-header-vendor-foo>`

## Mixin pckgHeader
 - computed
   - `slotElements` object (slot => elements)
   - `menus` object (slug => items)
   - `logos` object (device => logo)
   - `design` object (theme variables/settings)

## comms.json
`header` share type additional properties are:
 - `slots` - object with available slots in the Page builder

Updated `comms.json` looks like:
```
{
    ...
    "header": {
        "slots": {
            "left": "Left",
            "menu": "Menu",
            "right": "Right"
        }
    }
}
```

## Build
Follow classic build procedure as described [here](./../README.md).

## All headers
See [all headers on Hub](https://hub.comms.dev/)