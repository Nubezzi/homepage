<script>
    import '../App.css';
    import { fly } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';
    var isIn = false
    function actionWhenInViewport(e) {
    const observer = new IntersectionObserver(entries => {
        if(entries[0].isIntersecting) {
            isIn = true
        }else {
            isIn = false
        }
    });
    observer.observe(e);
    }

</script>

<div  class='scroll-content'>
    <div use:actionWhenInViewport>
        {#if isIn}
        <h2 transition:fly="{{delay: 50, duration: 600, x: 500, y: 0, opacity: 0, easing: cubicOut}}">About</h2>
        {/if}
    </div>
</div>