<script>
	import { onMount } from 'svelte';
	import '../App.css';

	let canvas;
	export var px = 10
	export var maxy;
	export var maxx;
	var scale = 1
	$: {
		if(maxx < 500) {
			scale = maxx / 500
		}
	}
	
	onMount(() => {
		const ctx = canvas.getContext('2d');
		let frame;

		(function loop() {
			frame = requestAnimationFrame(loop);

			const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);

			for (let p = 0; p < imageData.data.length; p += 4 ){
				const i = p / 4;
				const x = i % canvas.width;
				const y = i / canvas.height >>> 0;

				const t = window.performance.now();

				const r = 0 + (128 * x / canvas.width) + (64 * Math.sin(t / 400));
				const g = 64 + (128 * y / canvas.height) + (64 * Math.cos(t / 500));
				const b = 200;

				imageData.data[p + 0] = r;
				imageData.data[p + 1] = g;
				imageData.data[p + 2] = b;
				imageData.data[p + 3] = 255;
			}

			ctx.putImageData(imageData, 0, 0);
		}());

		return () => {
			cancelAnimationFrame(frame);
		};
	});
</script>
<canvas
	style="transform: translate(0,{(-0*(maxy/1080) + (-px / (70*(maxy/1080) / Math.log(px))))}px) rotate({45 + px/15}deg) scale({scale});
	--scale: {scale}"
	class='logo'
	bind:this={canvas}
	width={100}
	height={100}
></canvas>


