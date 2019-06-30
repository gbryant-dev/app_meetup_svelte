<script>
    import Header from './UI/Header.svelte';
    import MeetupGrid from './Meetups/MeetupGrid.svelte';
    import MeetupEdit from './Meetups/MeetupEdit.svelte';
    import TextInput from './UI/TextInput.svelte';
    import Button from  './UI/Button.svelte';
    import Modal from './UI/Modal.svelte';


    let editMode = false;
    let editState = 'update';

    let meetup = {
        id: null,
        title: '',
        subtitle: '',
        description: '',
        imageUrl: '',
        address: '',
        contactEmail: '',
        favourite: false
    };

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that will teach you how to code',
            imageUrl: 'https://www.birminghamupdates.com/wp-content/uploads/2018/10/Screen-Shot-2018-10-17-at-10.28.03.png',
            address: '27th Nerd Road, 32523 New York',
            contactEmail: 'code@test.com',
            favourite: false
        },
        {
            id: 'm2',
            title: 'Swim Together',
            subtitle: 'Let\'s go for some swimming',
            description: 'We will simply swim some rounds',
            imageUrl: 'http://learntoswim.pk/wp-content/uploads/2018/06/LOGOFINAL.png',
            address: '27th Nerd Road, 32523 New York',
            contactEmail: 'swim@test.com',
            favourite: false
        },

    ];


    function createMeetup() {
        editMode = true;
        editState = 'new';
    }

    function addMeetup(event) {
        console.log('Adding meetup', event.detail);
        let newMeetup = event.detail;
        let index = meetups.findIndex(m => m.id === newMeetup.id);
        if (index !== -1) {
            console.log('Meetup already exists!');
            meetups[index] = newMeetup;
            editMode = false;
        } else {
            console.log('New meetup!');
            meetup.id = Math.random().toString();
            meetups = [...meetups, newMeetup];
            editMode = false;
        }

    }

    function toggleEdit(event) {
        meetup = event.detail.meetupToEdit;
        editMode = true;
        editState = 'update';
        console.log('Editing!', meetup);
    }

    function cancelEdit () {
        editMode = false;
    }


</script>

<style>
    main {margin-top: 5rem;}

    .center {
        display: flex;
        justify-content: center;
        margin: 1rem 0;
    }
</style>

<Header />

<main>

    {#if editMode}
        <MeetupEdit
            {meetup}
            state={editState}
            on:save="{addMeetup}"
            on:cancel="{cancelEdit}"
            />
    {/if}

    {#if !editMode}
        <div class="center">
            <Button on:click={createMeetup}>Add New Meetup</Button>
        </div>
    {/if}

    <MeetupGrid on:edit={toggleEdit} {meetups} />
    <!-- <MeetupGrid on:edit={(event) => {toggleEdit(event)}} {meetups} /> -->

</main>


