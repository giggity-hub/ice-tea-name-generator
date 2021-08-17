
<script>
import { elasticOut, bounceIn, backIn, backOut, expoIn, cubicIn, cubicOut } from 'svelte/easing';




    function spin(node, { duration }) {
		return {
			duration,
			css: t => {
				const eased = cubicOut(t);

				return `transform: rotate(${eased*360}deg)`
			}
		};
	}
</script>



<div class="backdrop">
    <div class="comic-dots"></div>
    <div in:spin={{duration: 5000}}  class="gradient">
</div>




</div>

<style>
    .backdrop{
        background: var(--primary);
        background: radial-gradient(circle, white 0%, black 100%);
        height: 100vh;
        width: 100vw;
    }

    .comic-dots{
        height: 100vh;
        width: 100vw;
       
        background: var(--primary);
		background-image: url('/image.jpg');
		background-size: contain;
		background-blend-mode: darken;
        opacity: 1;

        mix-blend-mode: darken;
    }

    .gradient{
		height: 400vh;
		width: 400vw;

		top: -150vh;
		left: -150vw;
	
		position: fixed;
		background: 
			radial-gradient(circle, var(--secondary) 3%, rgba(0,0,0,.0) 20%),
			radial-gradient(circle, rgba(0,0,0,0) 0%, var(--primary) 30%),
			repeating-conic-gradient(rgba(0,0,0,0) 0 9deg, var(--secondary) 9deg 18deg);

	}
    @media only screen and (max-width: 1000px) {
        .comic-dots {
            background-size: cover;
        }
    }
</style>