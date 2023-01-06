<!-- src/components/VideoEmbed.svelte -->

<script>

  // bind the type and videoId props to the videoType and videoId variables in the app state
  export let type = 'youtube';
  export let videoId = '';
  // build the embed URL for the selected video
  let embedUrl = '';
  if (type === 'youtube') {
    embedUrl = `https://www.youtube.com/embed/${videoId}`;
  } else if (type === 'twitch') {
    embedUrl = `https://player.twitch.tv/?video=v${videoId}`;
  }
  // add a console log statement to verify that the embedUrl variable is being set correctly
  console.log(`embedUrl: ${embedUrl}`);
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
    {#if embedUrl}
      {console.log(`embedUrl: ${embedUrl}`)}
      <iframe src={embedUrl} title="Video embed" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
    {/if}
  </div>
  
  