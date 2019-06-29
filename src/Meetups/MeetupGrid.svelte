<script>
    import MeetupItem from './MeetupItem.svelte';
    export let meetups;
</script>

<style>

    #meetups {
        width: 80%;
        margin: 2rem auto;
    }

    section {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr;
        grid-gap: 1rem;
    }

    @media (min-width: 768px) {
        section {
            grid-template-columns: repeat(2, 1fr);
        }
    }

</style>

<section id="meetups">
    {#each meetups as meetup (meetup.id)}
        <MeetupItem on:edit {meetup}
        />

    {/each}
    <!-- <slot name="edit" editedMeetup={editing}></slot> -->
</section>


