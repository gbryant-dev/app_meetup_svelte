<script>
    export let controlType = 'input';
    export let inputType = 'text';
    export let id;
    export let label;
    export let rows = 0;
    export let value;

</script>

<style>

    input, textarea {
        width: 100%;
        /* border-color: #e40763; */
        outline: none;
        border-bottom: 3px solid lightgray;
    }

    input:focus, textarea:focus {
        transition: ease-in 0.25s;
        border-bottom: 3px solid #e40763;
    }


    label {
        display: block;
        margin-bottom: 0.5rem;
        width: 100%;
    }

    .form-control {
        padding: 0.5rem 0;
        width: 100%;
        margin: 0.25rem 0;
    }

</style>

<div class="form-control">
    <label for="{id}">{label}</label>
    {#if controlType === 'textarea'}
        <textarea rows="{rows}" id="{id}" value={value} on:input />
    {:else}
        <input type="{inputType}" id="{id}" value={value} on:input>
    {/if}
</div>
