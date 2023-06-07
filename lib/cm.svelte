<script>
    import { onMount, createEventDispatcher } from "svelte"
    import { writable } from "svelte/store"
    import cm from "codemirror"

    import "codemirror/lib/codemirror.css"

    export let options = {}
    export let value = ""

    const dispatch = createEventDispatcher()
    let container = null
    let input = null
    const inputValue = writable(value)

    export const editor = () => input

    $: value = $inputValue
    $: if ($inputValue !== value) {
        input.setValue(value)
    }
    $: inputValue.set(value)

    $: if (input !== null) {
        for (const [name, value] of Object.entries(options)) {
            input.setOption(name, value)
        }
    }

    const init = () => {
        input = cm(container, {})
        input.setSize("100%", "100%")
        requestAnimationFrame(
            () => {
                input.setValue(value)
                input.on(
                    "change",
                    () => $inputValue = input.getValue()
                )
            }
        )
        dispatch("ready", input)
    }
    onMount(init)
</script>

<div bind:this={container} {...$$restProps} />
