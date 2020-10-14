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
If your component depends on some library, you'll need to create the standard `package.json`, install your dependencies, and create custom build with docker command above. Just make sure to add `comms-hub-dev` as dependency. This will install all dependencies needed to build the component.

## VueJS
Some mixins are available in all components (except custom components, as in examples):
 - `pckgTranslations`
   - exposes method `__(slug)`
 - `pckgCdn`
   - exposes method `cdn(url)` 

### Component mixins
Share mixins (such as `pckgItem` and `pckgList`) expose `settings(name)` method.

You can use vars in LESS by defining them in component's style tag:

`<template><div :style="{'--some-var': setting('key')}">...</div></template>`
   
### Translations
When you use the `pckgTranslations` mixin with `__` helper, you need to define at least English defaults. See example in [./headers/](./07_headers/). Translations will be registered under `hub.shareType.vendorName.shareIdentifier` namespace.

### Settings
You can add different settings to your shares. They must be defined in `comms.json` so they can be rendered in the Pagebuilder.

Custom properties need to be defined in `comms.json`. Available property types are `string`, `number`, `decimal`, `color`, `range`.

# ... zip ...
To share the share, you need to .zip the `comms.json` file and `build` directory.

Shares that do not need to be built (emails, microcontent, and documents) should be located in the root of the .zip file.

# ... and share.
Login to your [Comms Hub](https://hub.comms.dev) account and upload the .zip (max .zip file size is 5MB). We will validate `comms.json` file, .zip contents, and make it available to other users.