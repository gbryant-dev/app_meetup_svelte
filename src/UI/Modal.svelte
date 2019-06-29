<script>
    import Button from '../UI/Button.svelte';
    import { createEventDispatcher, onMount, onDestroy, beforeUpdate, afterUpdate } from 'svelte';

    const dispatch = createEventDispatcher();
    let agreed = false;
    let autoScroll = false;

    onMount(() => {
        console.log('onMount');
    });

    onDestroy(() => {
        console.log('onDestroy');
    });

    beforeUpdate(() => {
        console.log('beforeUpdate');
        autoScroll = agreed;
    });

    afterUpdate(() => {
        console.log('afterUpdate');
        if (autoScroll) {
            const modal = document.querySelector('.modal');
            modal.scrollTo(0, modal.scrollHeight);
        }
    });




</script>

<style>
    .backdrop {
        position: fixed;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
        background-color: #000;
        opacity: 0.6;
        z-index: 1;
    }

    .modal {
        position: fixed;
        top: 10vh;
        left: 0;
        right: 0;
        width: 60%;
        height: 15vh;
        padding: 1rem;
        z-index: 2;
        margin: 0 auto;
        background-color: white;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.26);
        border-radius: 4px;
        overflow-y: scroll;
    }

    .spacer {
        margin: 20px 2px;
        height: 2px;
        background-color: #eee;
    }

</style>


<div on:click="{() => dispatch('dismiss')}" class="backdrop"></div>
<div class="modal">
    <header>
        <slot name="header">
            <h2>Testing</h2>
        </slot>
    </header>
    <div class="spacer"></div>
    <div class="content"></div>
    <div class="disclaimer">
        <p>Before you close, you need to agree to our terms!</p>
        <Button on:click="{() => agreed = true}" caption="Agree" />
    </div>
    <footer>
        <slot name="footer" didAgree={agreed}>
            <Button
             caption="Check"
             on:click="{() => dispatch('normal')}"
             disabled={!agreed}
             />
        </slot>
        <Button
         on:click="{() => dispatch('cancel')}"
         caption="Cancel"
        />
    </footer>
</div>
