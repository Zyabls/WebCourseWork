<script>
  import { onMount } from 'svelte';
  let webampInstance;
  let currentTrackIndex = 0;

  onMount(() => {
    const script = document.createElement('script');
    script.src = 'https://unpkg.com/webamp@1.4.2/built/webamp.bundle.min.js';
    script.onload = () => {
      const webamp = new window.Webamp({
        initialTracks: [
          {
            metaData: {
              artist: "DJ Mike Llama",
              title: "Llama Whippin' Intro",
            },
            url: "https://cdn.jsdelivr.net/gh/captbaritone/webamp@43434d82cfe0e37286dbbe0666072dc3190a83bc/mp3/llama-2.91.mp3",
            duration: 5.322286,
          },
          {
            metaData: {
              title: "Heroines",
              artist: "DiabloфSwing Orchestra",
            },
            url: "https://raw.githubusercontent.com/captbaritone/webamp-music/4b556fbf/60_Tigres_-_11_-_Garage.mp3",
            duration: 322.612245,
          },
          {
            metaData: {
              title: "We Are Going To Eclecfunk Your Ass",
              artist: "Eclectek",
            },
            url: "https://raw.githubusercontent.com/captbaritone/webamp-music/4b556fbf/Eclectek_-_02_-_We_Are_Going_To_Eclecfunk_Your_Ass.mp3",
            duration: 190.093061,
          },
        ],
        onTrackChanged: (index) => {
          currentTrackIndex = index;
    
        },
      });

      webampInstance = webamp;
      webamp.renderWhenReady(document.getElementById("app"));
    };
    document.head.appendChild(script);
  });
</script>

<div id="app" style="height: 100vh">

</div>
