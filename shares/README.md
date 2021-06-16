# Shares
Shares are everything that's available on the Hub - designs, components, .csv files, ... They all contain `comms.json` file with share definition, and `build/` directory with publicly available assets.

# Develop ...
For a hello world project, all you need to do is create a single file Vue component with template and script tags.

# ... build ...
Most shares need to be built. Docker image includes all dev dependencies for the build - npm, webpack, yarn and `node_modules` folder.

You can build your single file VueJS component with dev docker container. This will clear the last build, generate the `itemType.js` and `webpack.config.js` files, and build your component.

`$ docker run comms/dev-hub /path/to/dir/:/build/`

The command above will run a webpack build from `webpack.config.js`.

To automatically generate `webpack.config.js` and/or `list.js`, you can pass parameters `-e vendor=vendor -e type=type -e share=name.vue` (recommended).

You can pass the `--watch` and `-p 8080:8080` parameters to watch your files and autogenerate them during development. To view your result simply open `https://localhost:8080/`

If the `comms.json` file is already present, the script also validates it.

## Webpack
If your component depends on some library, you'll need to create the standard `package.json`, install your dependencies, and create custom build with docker command above. Just make sure to add `comms-hub-dev` package as dependency to install all dependencies needed to build the component.

`$ webpack --env.SHARE=unusual-header --env.SHARE_TYPE=header --env.SHARE_VENDOR=comms`

You can find generic `webpack.config.js` used in `comms/dev-hub` image in `./shares/00_shared/` directory.

## VueJS
Some mixins are available in all components (except custom components, as in examples):
 - `pckgTranslations`
   - exposes method `__(slug)`
 - `pckgCdn`
   - exposes method `cdn(url)` 

### Component mixins
Share mixins (`pckgItem`, `pckgList`, `pckgComponent`, `pckgLayout`, `pckgPage`) expose `settings(name)` method.

You can use vars in LESS by defining them in component's style tag:

`<template><div :style="{'--some-var': setting('key')}">...</div></template>`
   
### Translations
When you use the `pckgTranslations` mixin with `__` helper, you need to define at least English defaults. See example in [./headers/](./07_headers/). Translations will be registered under `hub.shareType.vendorName.shareIdentifier` namespace.

### Capabilities
Shares can require or define different capabilities:
 - items can require lists to have specific capabilities (such as `grid` or `no-grid`)
 - capabilities `contents`, `content` and `content: [...fields]` allow classic content to be connected with action
 - add `subactions` capability to allow component to have children
 - add `slots` capability to define available slots to put children in

### Content
You can create single-, two-, or multi-level structure with generic content. Content cannot be linked to page, layout or header - you can add subactions to slots.

Available fields:
 - `id` number
 - `created_at` datetime
 - `updated_at` datetime
 - `order` number
 - `title` string
 - `subtitle` string
 - `description` string (HTML)
 - `content` string (HTML)
 - `picture` string - relative url, use cdn(content.picture), or cdn(imageResize(content.picture, 'c', '200x200'))
 - `video` string - youtube or vimeo video
 - `icon` string - FA icon
 - `url` string - relative or absolute URL

## comms.json
Here's a minimum required version for your `comms.json` file. You need to create a Vendor and Share on the Hub to acquire their identifiers. The file will be validated on upload and all data must match to prevent errors.
```
{
    share: {
        vendor: "vendor-identifier", # your Vendor identifier on Hub
        type: "item", # one of allowed share types
        identifier: "share-identifier", # your Share identifier on Hub 
        version: "0.0.1",
    },
    entrypoint: "item-foo.js" # main .js file from your build
}
```

### Settings
You can add different settings to your shares. They must be defined in `comms.json` so they can be rendered in the Pagebuilder.

They are also available in templates under value `action.settings.someStyleSetting`.

Available property types are:
 - `text` - text, up to 255 characters
 - `html` - html, up to 1024 characters
 - `number` - negative or positive integer
 - `decimal` - decimal/float
 - `color` - hex color
 - `select:single` - dropdown with single select 
 - `select:multiple` - dropdown with multiple selects
 - `checkbox` - true or false
 - `unit` - define allowed units

Updated `comms.json` looks like:
```
{
    ...
    "settings": {
        "someStyleSetting": {
            "type": "select:single",
            "required": true,
            "default": "option-two",
            "options": {
                "option-one": "First style",
                "option-two": "Second style"
            }
        },
        "someWidthSetting": {
            "type": "unit",
            "required": true,
            "default": "2px",
            "settings": {
                "units": ["px", "rem"]
            }
        },
    }
}
```

# ... zip ...
To share the share, you need to .zip the `comms.json` file and `build` directory.

Shares that do not need to be built (emails, microcontent, and documents) should be located in the root of the .zip file.

# ... and share.
Login to your [Comms Hub](https://hub.comms.dev) account and upload the .zip (max .zip file size is 5MB). We will validate `comms.json` file, .zip contents, and make it available to other users.