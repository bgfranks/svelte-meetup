<script>
  // imports
  import MeetupItem from './MeetupItem.svelte';

  // props
  export let meetups;
</script>

<section id="meetups">
  {#each meetups as meetup}
    <MeetupItem
      id={meetup.id}
      title={meetup.title}
      subtitle={meetup.subtitle}
      description={meetup.description}
      location={meetup.location}
      contactEmail={meetup.contactEmail}
      imgUrl={meetup.imgUrl}
      isFavorite={meetup.isFavorite}
    />
  {/each}
</section>

<style>
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
