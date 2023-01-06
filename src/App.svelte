<script>
	import ChatFeed from './components/ChatFeed.svelte';
	import VideoEmbed from './components/VideoEmbed.svelte';
	import VideoSelector from './components/VideoSelector.svelte';
  
	// declare the videoType and videoId stores at the top level of the component
	let videoType = 'youtube';
	let videoId = '';
  
	// callback function to handle the form submission
	function handleSubmit({ type, id }) {
	  // update the type and videoId values in the app state
	  videoType = type;
	  videoId = id;
	}
  </script>
  
  <style>
	/* styles for the app go here */
  </style>
  
  <VideoSelector on:submit={handleSubmit} />
  <VideoEmbed type={videoType} videoId={videoId} />
  <ChatFeed />
  