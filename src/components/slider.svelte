<script>
    import '../App.css';
    import Visibility from '../components/visibility.svelte'
	import { fly } from 'svelte/transition';
	import { cubicOut, cubicIn } from 'svelte/easing';
    export var content;
    export var classname;
    export var num;

    function paljonko(percent) {
        console.log(percent)
    }

</script>

<Visibility classname={classname} num={num} let:percent let:unobserve let:intersectionObserverSupport>
    <div on:mouseenter={paljonko(percent)}></div>
    {#if percent > 60}
        <div>
            <div 
            on:mouseenter={paljonko(percent)} 
            in:fly={{duration: 1000, x: 500}}
            out:fly={{duration: 500, x: -500}} 
            use:unobserve
            
            >
                <svelte:component this={content}/>
            </div>
        </div>
    {/if}
</Visibility>