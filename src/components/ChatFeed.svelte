<!-- src/components/ChatFeed.svelte -->

<script>
    import { writable } from 'svelte/store';
  
    const messages = writable([]); // store to hold the chat messages
  
    // function to add a new message to the chat
    function addMessage(message) {
      messages.update(msgs => [...msgs, message]);
    }
  </script>
  
  <style>
    /* component styles go here */
  
    .chat-messages {
        /* style for the chat messages list */
        list-style: none;
        margin: 0;
        padding: 0;
        border: 1px solid #ccc;
        background-color: #fff;
        height: 200px;
        overflow-y: auto;
    }

  
    .chat-message {
        /* style for each chat message */
        display: flex;
        align-items: center;
        padding: 8px;
        border-bottom: 1px solid #ccc;
    }   

    .chat-form {
        /* style for the chat form */
        display: flex;
        align-items: center;
        padding: 8px;
    }

    .chat-form input[type="text"] {
        /* style for the chat form input field */
        flex: 1;
        border: 1px solid #ccc;
        padding: 8px;
        font-size: 14px;
    }

    .chat-form button[type="submit"] {
        /* style for the chat form submit button */
        border: none;
        background-color: #4caf50;
        color: #fff;
        padding: 8px 16px;
        font-size: 14px;
        cursor: pointer;
    }

  </style>
  
  <!-- component template goes here -->
  
  <ul class="chat-messages">
    {#each $messages as message}
      <li class="chat-message">{message}</li>
    {/each}
  </ul>
  
  <form class="chat-form" on:submit|preventDefault={(e) => {
    const message = e.target.message.value;
    addMessage(message);
    e.target.message.value = '';
  }}>
    <input type="text" name="message" placeholder="Enter a message" />
    <button type="submit">Send</button>
  </form>
  