<script>
    import '../App.css';
    import { fly } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';
    export var isIn = false

</script>

<div id="section-2" class='scroll-content'>
    {#if isIn}
        <h2 transition:fly="{{delay: 50, duration: 600, x: 500, y: 0, opacity: 0, easing: cubicOut}}">About</h2>
        <p transition:fly="{{delay: 200, duration: 600, x: 500, y: 0, opacity: 0, easing: cubicOut}}" >
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed nec pretium tellus. Nam ac nibh orci. 
            Sed tempus, nibh ac dapibus dignissim, lorem leo gravida dui, vitae commodo dolor quam vitae lacus. Praesent vestibulum massa eget sapien cursus vulputate. 
            Nam rhoncus tellus nibh. Praesent interdum mattis eros at dictum. Etiam at porta odio. Ut vitae laoreet tortor. Proin convallis gravida orci, a lobortis justo finibus nec. 
            Donec consectetur quam at pharetra facilisis. Nulla tempor at sapien in vehicula.
        </p>
    {/if}
</div>