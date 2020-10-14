# Lists
List components accepts contents as a parameter and prints their `itemComponent` in a loop.

## Mixin pckgSmartList
Provides basic properties in templates.
 - props
   - `contents` array
   - `action` -> data.`myAction`
 - data
   - `myAction` object
   - `capabilities` objects
 - computed
   - `content` object
   - `subcontents` array
   - `subactions` array
   - `templateClass` string
   - `hasMediaGrid` bool
   - `mediaGridClass` string

## Build
Follow classic build procedure as descripted [here](./../README.md).

## Default lists
 - `bootstrap` - bootstrap v2 - col-xx-yy
 - `grid` - by number of items or width
 - `no-grid` - item defines elements row/column flow

## All lists
See [all lists on Hub](https://hub.comms.dev/)