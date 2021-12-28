<script>
  // imports
  import meetupsStore from './Meetups/meetups-store';
  import Header from './UI/Header.svelte';
  import MeetupGrid from './Meetups/MeetupGrid.svelte';
  import EditMeetup from './Meetups/EditMeetup.svelte';
  import Button from './UI/Button.svelte';

  // toggles edit state to show form
  let editMode = false;

  // adds a new meetup
  function addMeetup(e) {
    // extracts the data from the event and adds to a new meetup object
    const meetup = e.detail;

    const newMeetup = {
      title: meetup.title,
      subtitle: meetup.subtitle,
      description: meetup.description,
      imgUrl: meetup.imgUrl,
      location: meetup.location,
      contactEmail: meetup.contactEmail,
    };

    // adds the new meet up to the meetup store and sets edit to false
    meetupsStore.addMeetup(newMeetup);
    editMode = false;
  }

  // cancel the meetup edit
  function cancelEdit() {
    editMode = false;
  }

  // toggle favorite
  function toggleFavorite(e) {
    const id = e.detail;
    meetupsStore.toggleFavorite(id);
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
  <MeetupGrid meetups={$meetupsStore} on:toggleFavorite={toggleFavorite} />
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
