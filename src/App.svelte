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
    editMode = false;
  }

  // cancel the meetup edit
  function cancelEdit() {
    editMode = false;
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
  <MeetupGrid meetups={$meetupsStore} />
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
