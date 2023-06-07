# Svelte CodeMirror (cm-svelte)

Simple binding for CodeMirror 5 (I'm not a fan of the API for 6) so that
editors can be dropped into a page quickly and easily.

## Usage
```svelte
<script>
    import CodeMirror from "@axel668/cm-svelte"
</script>

<CodeMirror bind:value {options} />
```
> Your Svelte build configuration will need to support importing css files
> (something like rollup-plugin-import-css) in order to use this component.

### Props
- #### value
    The text in the editor. Supports binding and reactivity.
- #### options
    The CodeMirror [options](https://codemirror.net/5/doc/manual.html#config).
    Changes to the options object will be applied to the editor even after
    initial setup.
- #### $$restProps
    Any props passed to the component other than `options` and `value` are
    passed to the container element as is, so styling can be done in any way.

### Keybindings, Themes, Modes
Codemirror 5 is a dependency of this library, so it will always be installed
along side it. In order to use keybinds, themes, or modes other than the
default, they need to be imported into the project so that only what is listed
is included in the build, instead of dozens of themes and language modes that
are not in use. The imports do not need to do anything with the imported value;
everything should work with plain script imports.

```js
import "codemirror/mode/javascript/javascript.js"
import "codemirror/keymap/sublime.js"
import "codemirror/theme/the-matrix.css"
```
