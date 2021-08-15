<script lang="ts">
    export let value: any
    export let label = ""
    export let name = ""
    let type: "text" | "number" | "email" | "password" = "text"

    const handleInput = (e) => value = (e.target as HTMLInputElement).value
</script>

<div>
    <label for={name}>
        {label}
     </label>     
    <input id={name} {type} class={`p-2 border rounded-lg ${$$props.class}`} value={value} on:input={handleInput}>
</div>
