<!-- src/components/VideoSelector.svelte -->

<script>
    import { createEventDispatcher } from 'svelte';
  
    // create the submit event dispatcher
    const dispatch = createEventDispatcher();
  
    // bind the videoId variable to the input field using a two-way binding
    let videoId = '';
    let type = 'youtube';
  
    // handle the form submission
    function handleSubmit(event) {
  // add a console log statement to verify that the function is being called
  console.log('handleSubmit called');
  // prevent the default form submission behavior
  event.preventDefault();
  // dispatch the submit event with the selected video type and ID
  dispatch('submit', { type, videoId });
}
  </script>
  
<style>
    /* component styles go here */
  


.video-selector form select {
  /* style for the video type select field */
  margin-right: 0.5rem;
  padding: 0.25rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  appearance: none;
  -webkit-appearance: none;
}

.video-selector form input[type="text"] {
  /* style for the video ID input field */
  margin-right: 0.5rem;
  padding: 0.25rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  width: 200px;
}

.video-selector form button[type="submit"] {
  /* style for the submit button */
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  color: #fff;
  background-color: #007bff;
  cursor: pointer;
}

  </style>
  
  <!-- component template goes here -->
  
  <form on:submit={handleSubmit}>
    <!-- dropdown menu to select the video type -->
    <select bind:value={type}>
      <option value="youtube">YouTube</option>
      <option value="twitch">Twitch</option>
    </select>
    <!-- input field to enter the video ID -->
    <input type="text" bind:value={videoId} placeholder="Enter video ID" />
    <!-- submit button -->
    <button type="submit">Go</button>
  </form>
  