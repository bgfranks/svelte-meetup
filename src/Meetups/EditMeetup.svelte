<script>
  // imports
  import meetupsStore from './meetups-store';
  import { createEventDispatcher } from 'svelte';
  import TextInput from '../UI/TextInput.svelte';
  import Button from '../UI/Button.svelte';
  import Modal from '../UI/Modal.svelte';
  import { isEmpty, isValidEmail, isValidHttpUrl } from '../Helpers/validation';

  // variables and constants
  let title = '';
  let subtitle = '';
  let location = '';
  let contactEmail = '';
  let description = '';
  let imgUrl = '';

  // creates event dispatcher
  const dispatch = createEventDispatcher();

  // binds data to the validation functions
  $: titleValid = !isEmpty(title);
  $: subtitleValid = !isEmpty(subtitle);
  $: locationValid = !isEmpty(location);
  $: emailValid = isValidEmail(contactEmail);
  $: descValid = !isEmpty(description);
  $: imgValid = isValidHttpUrl(imgUrl);
  $: formIsValid =
    titleValid &&
    subtitleValid &&
    locationValid &&
    emailValid &&
    descValid &&
    imgValid;

  // function to save the data from the form to the save dispatch event
  function submitForm() {
    const newMeetup = {
      title: title,
      subtitle: subtitle,
      description: description,
      imgUrl: imgUrl,
      location: location,
      contactEmail: contactEmail,
    };

    // adds the new meet up to the meetup store and sets edit to false
    meetupsStore.addMeetup(newMeetup);
    dispatch('save');
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
      valid={titleValid}
      errMsg="Please enter a valid title"
      on:input={(e) => (title = e.target.value)}
    />
    <TextInput
      id="subtitle"
      label="Subtitle"
      value={subtitle}
      valid={subtitleValid}
      errMsg="Please enter a valid subtitle"
      on:input={(e) => (subtitle = e.target.value)}
    />
    <TextInput
      id="location"
      label="Location"
      value={location}
      valid={locationValid}
      errMsg="Please enter a valid location"
      on:input={(e) => (location = e.target.value)}
    />
    <TextInput
      id="imgUrl"
      label="Image URL"
      value={imgUrl}
      valid={imgValid}
      errMsg="Please enter a valid image URL"
      on:input={(e) => (imgUrl = e.target.value)}
    />
    <TextInput
      id="contactEmail"
      label="Email"
      type="email"
      value={contactEmail}
      valid={emailValid}
      errMsg="Please enter a valid email address"
      on:input={(e) => (contactEmail = e.target.value)}
    />
    <TextInput
      id="description"
      label="Description"
      value={description}
      valid={descValid}
      errMsg="Please enter a valid meetup description"
      controlType="textarea"
      rows="3"
      on:input={(e) => (description = e.target.value)}
    />
  </form>
  <div slot="footer">
    <Button mode="outline" caption="Cancel" on:click={cancel} />
    <Button caption="Save" on:click={submitForm} disabled={!formIsValid} />
  </div>
</Modal>

<style>
  form {
    width: 100%;
  }
</style>
