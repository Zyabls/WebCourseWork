<script>
	import Typewriter from './Typewriter.svelte';
	import LaggyText from './LaggyText.svelte';
	import MusicPlayer from './MusicPlayer.svelte';
	import Winamp from './Winamp.svelte';
	const layers = [0, 1, 2, 3, 4, 5, 6, 7, 8];
	let currentTrackIndex = 0;

function updateCode(newCode) {
  code = newCode;
}

function handleTrackChange(event) {
  currentTrackIndex = event.detail.currentTrackIndex;
}

const handleImageClick = (i) => {

    gifPaths[currentTrackIndex] = gifPaths[5];
    setTimeout(() => {
      gifPaths[currentTrackIndex] = 'images/gifs/screen1.gif'; // Replace originalGifPath with the actual variable holding the original path
	  gifPaths = [
		'images/gifs/screen1.gif',
		'images/gifs/screen_face.gif',
		'images/gifs/screen_figure.gif',
		'images/gifs/screen_dance.gif',
		'images/gifs/screen_run.gif',
		'images/gifs/screen_error.jpg',
	]
    }, 1000); // 1000 milliseconds = 1 second
  };
	let y;

	let imagePaths = [
		'images/cropped_conputer.png',
        'images/err1.jpg',
		'images/err2.webp',
		'images/err3.jpg',
		'images/err4(sonic).jpg',
		'images/err5.webp',
		'images/err6.webp',
		'images/err7.webp',
		'images/err8.webp',
        
    ];
	let gifPaths = [
		'images/gifs/screen1.gif',
		'images/gifs/screen_face.gif',
		'images/gifs/screen_figure.gif',
		'images/gifs/screen_dance.gif',
		'images/gifs/screen_run.gif',
		'images/gifs/screen_error.gif',
	
	]
	let gifID = 0
// Загрузка файла при инициализации компонента
</script>

<svelte:window bind:scrollY={y} />
<title>223</title>
<body>
	
<div class="parallax-container">
	<div class="Music">
		<MusicPlayer bind:currentTrackIndex={currentTrackIndex} on:trackChange={handleTrackChange} />
		
	</div>
	
	<img src="images/winxpback.jpg" alt="Background"
	style="width: 2200px;height: 800px;">

	
	
	<!--Screen-->
	<img 
	
	style="transform: translate(0,{(y * gifID) / (gifID.length - 1)}px); 
	{currentTrackIndex === 0 ? 'width: 580px; height: 520px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
	{currentTrackIndex === 1 ? 'width: 539px; height: 520px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
	{currentTrackIndex === 2 ? 'width: 542px; height: 480px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
	{currentTrackIndex === 3 ? 'width: 540px;  height: 480px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
	{currentTrackIndex === 4 ? 'width: 540px;  height: 470px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
	{currentTrackIndex === 5 ? 'width: 520px;  height: 520px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
	{currentTrackIndex === 6 ? 'width: 520px;  height: 520px; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''})
	"
	src={gifPaths[currentTrackIndex]} 
	alt="">
	
	<div class="Winamp">
		<Winamp />
	</div>
	<!-- Errors and computer-->
	{#each layers as layer, i}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <img
  style="transform: translate(0,{(y * layer) / (layers.length - 1)}px); 
  {i === 0 ? 'width: 30%; height: auto; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); border-radius: 10px;' : ''}
  {i === 1 ? 'width: 12%; height: 12%; position: absolute; top: 20%; left: 70%;' : ''}
  {i === 2 ? 'width: 12%; height: 12%; position: absolute; top: 60%; left: 80%;' : ''}
  {i === 3 ? 'width: 12%; height: 12%; position: absolute; top: 20%; left: 20%;' : ''}
  {i === 4 ? 'width: 12%; height: 12%; position: absolute; top: 30%; left: 25%' : ''}
  {i === 5 ? 'width: 12%; height: 12%; position: absolute; top: 80%; left: 20%;' : ''}
  {i === 6 ? 'width: 12%; height: 12%; position: absolute; top: 40%; left: 15%;' : ''}
  {i === 7 ? 'width: 12%; height: 12%; position: absolute; top: 10%; left: 6%;' : ''}
  {i === 8 ? 'width: 12%; height: 12%; position: absolute; top: 70%; left: 90%;' : ''}"
  src={imagePaths[i]}
  alt="parallax layer {layer}"
  on:click={() => handleImageClick(i)}
/>
{/each}

</div>

<div class="text">
	<span style="opacity: {1 - Math.max(0, y / 40)}"></span>

	<div class="foreground">

			<div style="color: blue;">{y}<Typewriter y={y} /></div>
			
			<LaggyText />

			
			<!--<HackerTyper/> -->
		
			
	</div>
</div>


</body>

<style>

	@font-face {
	font-family: 'PerfectDOSVGA437';
	src: url('../fonts/perfectdosvga437.eot'); /* IE 9 Compatibility Mode */
	src: url('../fonts/perfectdosvga437.eot?#iefix') format('embedded-opentype'), /* IE < 9 */
		url('../fonts/perfectdosvga437.woff2') format('woff2'), /* Super Modern Browsers */
		url('../fonts/perfectdosvga437.woff') format('woff'), /* Firefox >= 3.6, any other modern browser */
		url('../fonts/perfectdosvga437.ttf') format('truetype'), /* Safari, Android, iOS */
		url('../fonts/perfectdosvga437.svg#perfectdosvga437') format('svg'); /* Chrome < 4, Legacy iOS */
}
.Winamp{
    position: fixed;
    bottom: 0;
    right: 0;
    margin: 20px;
    z-index: 9999; /* Устанавливает плеер поверх других элементов */
  }

	.parallax-container {
		position: fixed;
		width: 2400px;
		height: 712px;/* Adjust height as needed */
		left: 50%;
		transform: translate(-50%, 0);
		font-family: 'PerfectDOSVGA437';
	}
	

	.parallax-container img {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		will-change: transform;
	}

	.parallax-container img:last-child::after {
		content: '';
		position: absolute;
		width: 100%;
		height: 100%;
		background: rgb(45, 10, 13);
	}

	.text {
		position: relative;
		width: 100%;
		height: 220vh;
		color: rgb(61, 133, 228);
		text-align: left;
		padding: 4em 0.5em 0.5em 0.5em;
		box-sizing: border-box;
		pointer-events: none;
		font-family: 'PerfectDOSVGA437';
		font-size: 30px;
		overflow-wrap: break-word;
	}



	span {
		display: block;
		font-size: 1em;
		text-transform: uppercase;
		will-change: transform, opacity;
	}


		.foreground {
  position: absolute;
  top: 800px;
  left: 0;
  width: 100%;
  height: calc(90% - 1000px);
  padding: 50vh 0 0 0;
  font-family: 'PerfectDOSVGA437';
  text-decoration: none;
  display: inline-block;
  width: 100%;

  background-image: url('../images/gray_background.png');
  background-size: 100% auto; /* Stretch horizontally */
  background-repeat: no-repeat;
  background-color: rgb(192, 192, 192);


  
}
	

	:global(body) {
		margin: 0;
		padding: 0;
		background-color: rgb(192, 192, 192);
	}

</style>

