<script>
    import '../App.css';
    console.log("testi")
    import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
    import Home from '../components/home.svelte'
    import Logo from '../components/logo.svelte'
    import About from '../components/about.svelte'
    import Projects from '../components/projects.svelte'
    import Contact from '../components/contact.svelte'
    import photo from '../foregrounds/0.png'

    const layers = [1, 2, 3, 4, 5, 6, 7];

	let y, maxy, maxx;

</script>
<svelte:window bind:innerWidth={maxx} bind:innerHeight={maxy} bind:scrollY={y}/>
<body>
    <nav class="navbar">
        <a href="/">Home</a>
        <a href="/">About</a>
        <a href="/">Projects</a>
        <a href="/">Contact</a>
    </nav>  
      
      <div class="parallax-container">
          {#each layers as layer}
              <img
                  class='img-scroll'
                  style="transform: translate(0,{((layer * ((maxy/1080)*90)) - ((maxy/1080)*200) + (-y) * (layer/(layer + ((maxy/1080)*8))))}px);
                        filter: blur({0.5 + (y/400)}px);
                        z-index: {10 + layer}"
                  src="src/foregrounds/{layer}.png"
                  alt="parallax layer {layer}"
              >
          {/each}
          <Logo px={y} maxy={maxy} maxx={maxx}/>
          <Home px={y} maxy={maxy}/>
      </div>
      
       
      <div class="text">
      
          <div class="foreground">
              You have scrolled {y} pixels
          </div>
      </div>
</body>




