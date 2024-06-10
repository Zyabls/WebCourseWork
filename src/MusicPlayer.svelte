<!-- MinimalistPlayer.svelte -->
<script>
  import { onMount } from 'svelte';
  
  import Typewriter from './Typewriter.svelte';
  let y=0;
  export let currentTrackIndex = 0;
  let isPlaying = false;
  let volume = 1.0;
  let audio;

  let tracks = [
    { title: 'Screen 1', src: 'music/1.mp3' },
    { title: 'Screen 2', src: 'music/1.mp3' },
    { title: 'Screen 3', src: 'music/1.mp3' },
    { title: 'Screen 4', src: 'music/1.mp3' },
    { title: 'Screen 5', src: 'music/1.mp3' }
  ];

  function playTrack(index) {
    currentTrackIndex = index;
    playAudio();
  }

  function playAudio() {
    isPlaying = true; // Update play state
    audio = new Audio(tracks[currentTrackIndex].src);
    audio.volume = volume;
    audio.play();
    audio.onended = () => {
      nextTrack();
    };
  }

  function pauseAudio() {
    isPlaying = false; // Update play state
    audio.pause();
  }

  function nextTrack() {
  pauseAudio(); // Stop the current audio playback
  currentTrackIndex = (currentTrackIndex + 1) % tracks.length;
  playAudio(); // Start playing the next track
  setContext('currentTrackIndex', currentTrackIndex);

  y = 5000;  
  setContext('y', y);
 
}

function previousTrack() {
  pauseAudio(); // Stop the current audio playback
  currentTrackIndex = (currentTrackIndex - 1 + tracks.length) % tracks.length;
  playAudio(); // Start playing the previous track
  setContext('currentTrackIndex', currentTrackIndex);

  y = 5000;  
  setContext('y', y);
}

  onMount(() => {
    audio = new Audio(tracks[currentTrackIndex].src);
    audio.volume = volume;
    audio.onended = () => {
      nextTrack();
    };
  });

  // Add additional functionality for volume control, etc.
</script>

<style>
  .minimalist-player {
    display: flex;
    align-items: center;
    justify-content: center;
    width:45%; /* Adjust size as needed */
    height: 52%; 
    position: relative;
    z-index: 1;
  }
  .minimalist-player button {
    background-color: transparent;
    border: none;
    margin: 0 10px;
    cursor: pointer;
  }
  .minimalist-player img {
    width: 30px; /* Adjust size as needed */
    height: 30px; /* Adjust size as needed */

  filter: saturate(100%) brightness(100%) hue-rotate(240deg);

  }
  .typewriter-wrapper {
    /* Adjust the margin as needed */
    display: flex;
    
    justify-content: center;
    width: 45%; /* Adjust size as needed */
    height: 30%; 
    position: relative;
    z-index: 1;
    font-size: 20px;
  }
</style>

<div class="minimalist-player">
  <button on:click={previousTrack}>
    <img src="images/player/icons8-перейти-в-начало-32.png" alt="Previous">
  </button>
  
  <button on:click={nextTrack}>
    <img src="images/player/icons8-перейти-в-начало-32.png" style="transform: scaleX(-1);" alt="Next">
  </button>
</div>
<svelte:window bind:scrollY={y} />
{#if currentTrackIndex !== undefined}
  <div class="typewriter-wrapper">
    <Typewriter text={tracks[currentTrackIndex].title} isPlayer={true} y={y}/>
  </div>
{/if}