<script>
  import Header from './UI/Header.svelte';
  import MeetupGrid from './Meetups/MeetupGrid.svelte';

  const meetups = [
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
    },
  ];
</script>

<Header />
<main>
  <MeetupGrid {meetups} />
</main>

<style>
  main {
    margin-top: 5rem;
  }
</style>
