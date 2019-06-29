<script>
    export let type = 'button';
    export let href = null;
    export let disabled = false;
    export let styleOption = 'default';
    export let color = 'default';

</script>

<style>

    button {
        padding: 8px 20px;
        border-radius: 5px;
        cursor: pointer;
        box-shadow: rgba(0, 0, 0, 0.26);
        border: 2px solid;
    }
    button.default {
        color: white;
        background-color: #e40763;
        border-color: #e40763;
    }

    button.default:hover {
        background-color: #c90657;
    }

    button:disabled {
        cursor: not-allowed;
        opacity: 0.7;
    }

    a.default {
        color:  #e40763;
        cursor: pointer;
    }

    button.outline {
        background-color: transparent;
        border-color: #c90657;
        color: #c90657;
    }

    button.outline:hover {
        background-color: #e40763;
        color: white;
    }

    button.default.outline {
        background-color: transparent;
        border-color: #c90657;
        color: #c90657;
    }

    button.default.outline:hover {
        background-color: #e40763;
        color: white;
    }

    button.success {
        background-color: #46b601;
        border-color: #46b601;
        color: white;

    }

    button.success:hover {
        background-color: #3d9a04;
        border-color: #3d9a04;
    }

    button.success.outline {
        background-color: transparent;
        border-color: #3d9a04;
        color: #3d9a04;
    }

    button.success.outline:hover {
        background-color: #3d9a04;
        color: white;
    }

</style>


{#if href}
    <a class="{styleOption}" on:click href="{href}"><slot /></a>
{:else}
    <button class="{styleOption} {color}" disabled={disabled} on:click type={type}><slot /></button>
{/if}

