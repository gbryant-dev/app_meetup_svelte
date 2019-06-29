<script>
    import Button from '../UI/Button.svelte';
    import Badge from '../UI/Badge.svelte';
    import { createEventDispatcher } from 'svelte';

    export let meetup;

    const dispatch = createEventDispatcher();


</script>

<style>

article {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    border-radius: 5px;
    background: white;
    margin: 1rem;
}

header, .content, footer {
    padding: 1rem;
}

.content {
    height: 4rem;
}

.image {
    width: 100%;
    height: 14rem;
  }

.image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}


p {
    font-size: 1.25rem;
    margin: 0;
}

div {
    text-align: right;
}

h1 {
    font-size: 1.25rem;
    margin: 0.5rem 0;
    font-family: "Roboto Slab", sans-serif;
}


</style>


<article>
    <header>
        <h1>
            {meetup.title}
            {#if meetup.favourite}
                <Badge>FAVOURITE</Badge>
            {/if}
        </h1>
        <h2>{meetup.subtitle}</h2>
        <p>{meetup.address}</p>
    </header>
    <div class="image">
        <img src="{meetup.imageUrl}" alt="{meetup.title}">
    </div>
    <div class="content">
    <p>{meetup.description}</p>
    </div>
    <footer>
        <Button href="mailto:{meetup.contactEmail}">Contact</Button>
        <Button>Show Details</Button>
        <Button
         styleOption="outline"
         color="{meetup.favourite ? 'default' : 'success'}"
         on:click="{_ => (meetup.favourite = !meetup.favourite)}"
         >
         {meetup.favourite ? 'Unfavourite' : 'Favourite'}
         </Button>
         <Button on:click={() => {dispatch('edit', {meetupToEdit: meetup})}}>Edit</Button>
    </footer>
</article>
