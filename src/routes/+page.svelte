<script>
    import '../App.css';
    import { onMount, tick } from 'svelte';
    import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
    import Home from '../components/home.svelte'
    import Logo from '../components/logo.svelte'
    import About from '../components/about.svelte'
    import Projects from '../components/projects.svelte'
    import Contact from '../components/contact.svelte'
    import kuva1 from '../lib/assets/1.png'
    import kuva2 from '../lib/assets/2.png'
    import kuva3 from '../lib/assets/3.png'
    import kuva4 from '../lib/assets/4.png'
    import kuva5 from '../lib/assets/5.png'
    import kuva6 from '../lib/assets/6.png'
    import kuva7 from '../lib/assets/7.png' 
    const kuvat = [kuva1, kuva2, kuva3, kuva4, kuva5, kuva6, kuva7];
    const layers = [1, 2, 3, 4, 5, 6, 7];
    var about = false
    var projects = false
    var contact = false
    let bodyHeight;
    let y, realy, maxy, maxx, currY, contentHeight, parallaxHeight, navHeight, bodyY;
    $: {y = Math.round(realy)}
    $:{
        currY = y / (bodyHeight - maxy) * 10
        console.log(y)
    }
    $:{
        if(y >= (parallaxHeight + (0 - (maxy / 5))) && y <= (parallaxHeight + (maxy - 2*(maxy / 5)))){
            about = true
        }else {
            about = false
        }
    }
    $:{
        if(y >= (parallaxHeight + (maxy - 2*(maxy / 5)))  && y <= (parallaxHeight + (2*maxy - 2*(maxy / 5)))){
            projects = true
        }else {
            projects = false
        }
    }
    $:{
        if(y >= (parallaxHeight + (2*maxy - 2*(maxy / 5)))){
            contact = true
        }else {
            contact = false
        }
    }

    function scrollIntoView({ target }) {
		const el = document.querySelector(target.getAttribute('href'));
		if (!el) return;
        el.scrollIntoView({
        behavior: 'smooth',
        block: 'center'
        });
    }

    onMount(() => {
        bodyHeight = document.body.scrollHeight
		console.log(`nav: ${navHeight}, parallax: ${parallaxHeight}, cont: ${contentHeight}, screensize: ${maxy}`)
        bodyHeight = navHeight + parallaxHeight + contentHeight
	})

</script>
<svelte:window bind:innerWidth={maxx} bind:outerHeight={maxy} bind:scrollY={realy}/>
<body>
    <nav bind:clientHeight={navHeight} class="navbar">
        <a href="#section-1" on:click|preventDefault={scrollIntoView}>Home</a>
        <a href="#section-2" on:click|preventDefault={scrollIntoView}>About</a>
        <a href="#section-3" on:click|preventDefault={scrollIntoView}>Projects</a>
        <a href="#section-4" on:click|preventDefault={scrollIntoView}>Contact</a>
    </nav>  
      
      <div id="section-1" bind:clientHeight={parallaxHeight} class="parallax-container">
          {#each layers as layer}
              <img
                  class='img-scroll'
                  style="transform: translate(0,{((layer * ((maxy/1080)*90)) - ((maxy/1080)*200) + (-y) * (layer/(layer + ((maxy/1080)*8))))}px);
                        filter: blur({0.5 + (y/400)}px);
                        z-index: {10 + layer}"
                  src={kuvat[layer-1]}
                  alt="parallax layer {layer}"
              >
          {/each}
          <Logo px={y} maxy={maxy} maxx={maxx}/>
          <Home px={y} maxy={maxy}/>
      </div>
      
       
      <div bind:clientHeight={contentHeight} class="text">
          <div class="foreground">
            <About isIn={about} />
            <Projects isIn={projects} />
            <Contact isIn={contact} />
          </div>
      </div>
</body>




