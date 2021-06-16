# Pages
Prefer to build some really custom pages that go above and beyond the page builder? You can build custom page with slots that are populated from the pagebuilder. 

## Mixin pckgPage
 - $router?
 - $route?
 - routeParams? (as "resolved?")

## comms.json
`Page` share type does additional properties are:
 - `slots` - object with available slots in the Page builder
 - `resolve` - array with parameters resolved in the url - `packet`, `offer`, `category`, `unit`, `gallery`, `news`

Updated `comms.json` looks like:
```
{
    ...
    "page": {
        "slots": {
            "content": "Content",
            "header": "Header",
            "footer": "Footer"
        },
        "resolve": ["packet"]
    }
}
```

## Build
Follow classic build procedure as described [here](./../README.md).
   
## All pages
See [all pages on Hub](https://hub.comms.dev/)