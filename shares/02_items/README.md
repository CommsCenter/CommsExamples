# Items
Item components accepts content as a parameter and prints them.

## Mixin pckgSmartItem
Provides basic properties for all templates.
 - props
   - `content` object -> data.`myContent`
   - `action` -> data.`myAction`
   - `index` number
   - `settings` object
 - data
   - `tpl` string
   - `myAction` object
   - `myContent` object
 - computed
   - `templateClass` + `magicTemplateClass` string
   - `contents` array

## Build
Follow classic build procedure as descripted [here](./../README.md).
   
## All items
See [all items on Hub](https://hub.comms.dev/)