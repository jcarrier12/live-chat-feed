<!-- src/components/VideoEmbed.svelte -->

<script>
    // bind the type and videoId props to the videoType and videoId variables in the app state
    export const type = 'youtube';
    export let videoId = '';
  
    // get a reference to the iframe element
    let iframe;
  
    // callback function to handle messages from the iframe
    function handleMessage(event) {
      // check that the message is from the correct origin
      if (event.origin !== 'https://www.youtube.com') return;
  
      // parse the message data
      let data;
      try {
        data = JSON.parse(event.data);
      } catch (error) {
        console.error(error);
        return;
      }
  
      // handle the message based on its type
      switch (data.event) {
        case 'onReady':
          // the iframe is ready, send a message to load the video
          iframe.contentWindow.postMessage(
            JSON.stringify({
              event: 'command',
              func: 'loadVideoById',
              args: [videoId]
            }),
            'https://www.youtube.com'
          );
          break;
        case 'onError':
          // the iframe encountered an error, log the details
          console.error(data.info.code, data.info.message);
          break;
        default:
          // ignore other messages
          break;
      }
    }
  
    // add an event listener to handle messages from the iframe
    window.addEventListener('message', handleMessage);
  </script>
  
  <style>
    /* component styles go here */
  
    .video-embed {
      /* style for the video embed container */
      position: relative;
      width: 100%;
      height: 0;
      padding-bottom: 56.25%;
      border: 1px solid #ccc;
      background-color: #fff;
    }
  
    .video-embed iframe {
      /* style for the video iframe */
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: none;
    }
  </style>
  
  <!-- component template goes here -->
  
  <div class="video-embed">
    <!-- the iframe element -->
    <iframe
      src="https://www.youtube.com/embed/{videoId}"
      title="Video embed"
      frameborder="0"
      allow="autoplay; fullscreen"
      allowfullscreen
      bind:this={iframe}
    ></iframe>
  </div>
  
  
  