<script>

    import { createEventDispatcher, onMount } from 'svelte';

    import TextInput from '../UI/TextInput.svelte';
    import Button from '../UI/Button.svelte';
    import Modal from '../UI/Modal.svelte';

    onMount(() => {
        if (state !== 'update') {
            resetMeetup();
        }
    });

    const dispatch = createEventDispatcher();

    export let meetup = {};
    export let state = 'update';

    function resetMeetup() {
        meetup = {
            id: null,
            title: '',
            subtitle: '',
            description: '',
            imageUrl: '',
            address: '',
            contactEmail: '',
            favourite: false
        };
    }

</script>

<style>
    form {
        width: 100%;
    }
</style>

<Modal on:cancel title="Edit Meetup">
    <form>

        <TextInput
            id="title"
            label="Title"
            value={meetup.title}
            on:input={event => (meetup.title = event.target.value)}
        />
        <TextInput
            id="subtitle"
            label="Subtitle"
            value={meetup.subtitle}
            on:input={event => (meetup.subtitle = event.target.value)}
        />

        <TextInput
            id="address"
            label="Address"
            value={meetup.address}
            on:input={event => (meetup.address = event.target.value)}
        />

        <TextInput
            id="imageUrl"
            label="Image URL"
            value={meetup.imageUrl}
            on:input={event => (meetup.imageUrl = event.target.value)}
        />

        <TextInput
            inputType="email"
            id="email"
            label="Email"
            value={meetup.contactEmail}
            on:input={event => (meetup.contactEmail = event.target.value)}
        />

        <TextInput
            controlType="textarea"
            id="description"
            label="Description"
            value={meetup.description}
            on:input={event => (meetup.description = event.target.value)}
        />
    </form>
    <div slot="footer">
        <Button type="button" on:click="{() => {dispatch('save', meetup)}}">Save</Button>
        <Button styleOption="outline" on:click={() => {dispatch('cancel')}}>Cancel</Button>
    </div>
</Modal>
