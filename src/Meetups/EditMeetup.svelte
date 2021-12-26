<script>
  // imports
  import { createEventDispatcher } from 'svelte';
  import TextInput from '../UI/TextInput.svelte';
  import Button from '../UI/Button.svelte';
  import Modal from '../UI/Modal.svelte';

  // variables and constants
  let title = '';
  let subtitle = '';
  let location = '';
  let contactEmail = '';
  let description = '';
  let imgUrl = '';

  // creates event dispatcher
  const dispatch = createEventDispatcher();

  // function to save the data from the form to the save dispatch event
  function submitForm() {
    dispatch('save', {
      title,
      subtitle,
      location,
      contactEmail,
      description,
      imgUrl,
    });
  }

  // dispatches cancel
  function cancel() {
    dispatch('cancel');
  }
</script>

<Modal title="Edit Meetup Data" on:cancel>
  <form on:submit|preventDefault={submitForm}>
    <TextInput
      id="title"
      label="Title"
      value={title}
      on:input={(e) => (title = e.target.value)}
    />
    <TextInput
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      on:input={(e) => (subtitle = e.target.value)}
    />
    <TextInput
      id="location"
      label="Location"
      value={location}
      on:input={(e) => (location = e.target.value)}
    />
    <TextInput
      id="imgUrl"
      label="Image URL"
      value={imgUrl}
      on:input={(e) => (imgUrl = e.target.value)}
    />
    <TextInput
      id="contactEmail"
      label="Email"
      type="email"
      value={contactEmail}
      on:input={(e) => (contactEmail = e.target.value)}
    />
    <TextInput
      id="description"
      label="Description"
      value={description}
      controlType="textarea"
      rows="3"
      on:input={(e) => (description = e.target.value)}
    />
  </form>
  <div slot="footer">
    <Button mode="outline" caption="Cancel" on:click={cancel} />
    <Button caption="Save" on:click={submitForm} />
  </div>
</Modal>

<style>
  form {
    width: 100%;
  }
</style>
