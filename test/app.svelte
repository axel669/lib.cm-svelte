<script>
    import {
        Text,
        wsx
    } from "@axel669/zephyr"

    import CodeMirror from "../main.mjs"

    import "codemirror/mode/javascript/javascript.js"
    import "codemirror/keymap/sublime.js"
    import "codemirror/theme/the-matrix.css"

    import testCode from "./test-code.mjs"

    let value = testCode
    $: console.log(value)
    const ready = (evt) => {
        const editor = evt.detail
        window.editor = editor
    }

    window.test = (text) => {
        value = text
    }

    const options = {
        lineNumbers: true,
        keyMap: "sublime",
        mode: "javascript",
        theme: "the-matrix",
    }
</script>

<svelte:body use:wsx={{ theme: "tron", "@app": true }} />

<CodeMirror
    ws-x="w[480px] h[640px]"
    {options}
    on:ready={ready}
    bind:value
    class="test"
/>
