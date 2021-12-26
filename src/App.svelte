<script>
  // imports
  import Header from './UI/Header.svelte';
  import MeetupGrid from './Meetups/MeetupGrid.svelte';
  import EditMeetup from './Meetups/EditMeetup.svelte';
  import Button from './UI/Button.svelte';

  // temp meetup data
  let meetups = [
    {
      id: 1,
      title: 'Coding Bootcamp',
      subtitle: 'Learn to build a basic web app in a couple of hours',
      description:
        'In this bootcamp, we will have industry vets training you how to build a basic web app using on of the most popular frameworks.',
      imgUrl:
        'https://www.trilogyed.com/blog/wp-content/uploads/2018/05/columbia_coding_boot_camp2_brandon_colbert.jpg',
      location: 'Remote',
      contactEmail: 'codingcamp@test.com',
      isFavorite: false,
    },
    {
      id: 2,
      title: 'Keyboard Meetup',
      subtitle: 'Share and experience other keebs',
      description:
        'We are a group of keeb enthusiast looking to share and grow our custom keyboard community.',
      imgUrl:
        'https://switchandclick.com/wp-content/uploads/2020/10/IMG_7991-1-1024x683.webp',
      location: '123 Keeb Way, Raleigh, NC 27604',
      contactEmail: 'keebcom@test.com',
      isFavorite: false,
    },
    {
      id: 3,
      title: 'Pokemon Meet',
      subtitle: 'Come chat and see all things Pokemon',
      description:
        'Calling all Poke Trainers! Come show off your team and collection to prove why you are the very best!',
      imgUrl:
        'https://img.redbull.com/images/c_fill,g_auto,w_1060,h_707/q_auto,f_auto/redbullcom/2016/09/20/1331818966444_2/nostalgick%C3%BD-%C4%8Dtvrtek-10-zvl%C3%A1%C5%A1tn%C3%ADch-pok%C3%A9mon-her-pok%C3%A9mon-super-mystery-dungeon',
      location: '123 Poke Ct, Durham, NC 27777',
      contactEmail: 'Pokemonchamp@test.com',
      isFavorite: false,
    },
  ];

  // toggles edit state to show form
  let editMode = false;

  // adds a new meetup
  function addMeetup(e) {
    // extracts the data from the event and adds to a new meetup object
    const meetup = e.detail;

    const newMeetup = {
      id: Math.random().toString(),
      title: meetup.title,
      subtitle: meetup.subtitle,
      description: meetup.description,
      imgUrl: meetup.imgUrl,
      location: meetup.location,
      contactEmail: meetup.contactEmail,
    };

    // adds the new meet up to the spread meetup array and sets edit to false
    meetups = [newMeetup, ...meetups];
    editMode = false;
  }

  // cancel the meetup edit
  function cancelEdit() {
    editMode = false;
  }

  // toggle favorite
  function toggleFavorite(e) {
    // finds the meetup based on ID and t oggles isFavorite
    const id = e.detail;
    const updatedMeetup = { ...meetups.find((m) => m.id === id) };
    updatedMeetup.isFavorite = !updatedMeetup.isFavorite;

    // finds the meetup index and replaces with the updated meetup
    const meetupIndex = meetups.findIndex((m) => m.id === id);
    const updatedMeetups = [...meetups];
    updatedMeetups[meetupIndex] = updatedMeetup;
    meetups = updatedMeetups;
  }
</script>

<Header />
<main>
  <div class="meetup-controls edit">
    <Button
      caption={editMode ? 'x' : '+'}
      mode="circle"
      on:click={() => (editMode = !editMode)}
    />
  </div>
  {#if editMode}
    <EditMeetup on:save={addMeetup} on:cancel={cancelEdit} />
  {/if}
  <MeetupGrid {meetups} on:toggleFavorite={toggleFavorite} />
</main>

<style>
  main {
    margin-top: 5rem;
  }

  .meetup-controls {
    margin: 1rem;
  }

  .edit {
    font-size: 1.1rem;
    font-weight: bold;
  }
</style>
