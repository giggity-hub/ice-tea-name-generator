<script>
import { onMount } from "svelte";
import pickRandom from 'pick-random';
import { elasticOut, bounceIn, backIn, backOut, expoIn, cubicIn, cubicOut } from 'svelte/easing';
import Header from "./Header.svelte";
import Fitty from "./Fitty.svelte";
import SodaCan from "./SodaCan.svelte";
import colors from './Colors';
import { fade, fly } from 'svelte/transition';
import Backdrop from "./Backdrop.svelte";

	// <a href="https://www.vecteezy.com/free-vector/soda-can-vector-free">Soda Can Vector Free Vectors by Vecteezy</a>
	// <a href="https://www.vecteezy.com/free-vector/decorative">Decorative Vectors by Vecteezy</a>
	// https://www.vecteezy.com/vector-art/2176448-red-comic-zoom-with-lines-dots-and-white-elements-vector
	export let name;
	
	let dirTea = "Dirt Tea";
	

	let adjectives;
	let foods;

	let primary = "red";
	let secondary = "orange";

	function timeout(ms) {
    	return new Promise(resolve => setTimeout(resolve, ms));
	}

	function generateTeaName(){
		let adj = pickRandom(adjectives);
		let food = pickRandom(foods);

		dirTea = adj + " " + food

		primary = pickRandom (colors);
		secondary = pickRandom(colors);

	}

	onMount(async () => {
		adjectives = await 	fetch('https://raw.githubusercontent.com/giggity-hub/ice-tea-name-generator/main/Jupyter%20Notebook/NEG_ADJ_EN.txt')
			.then(res => res.text())
			.then(text => text.split("\n"))

		foods = await 	fetch('https://raw.githubusercontent.com/giggity-hub/ice-tea-name-generator/main/Jupyter%20Notebook/Food_Filtered.txt')
			.then(res => res.text())
			.then(text => text.split("\n"))
			.then(words => words.map(word => word.replace("_", " ")))

		console.log(adjectives);



	})





	

	function grow(node, { duration }) {
		return {
			duration,
			css: t => {
				const eased = backOut(t);
				const rotation = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${rotation*360}deg);
					color: hsl(
						${~~(t * 360)},
						${Math.min(100, 1000 - 1000 * t)}%,
						${Math.min(50, 500 - 500 * t)}%
					);`
			}
		};
	}



</script>

<main style="--primary: {primary}; --secondary: {secondary}" >
	<!-- <Header/> -->
	
	{#key dirTea}


	<div class="content">
		
		<div in:grow={{duration:800}} >

			<SodaCan {primary} {secondary} text={dirTea} />
		</div>
	</div>

	<Backdrop/>

	{/key}
	
	<button class="generate-tea-btn" on:click={generateTeaName} >Generate Tea</button>
		
	
	
	
</main>

<style>

	main{
		display: flex;
		align-items: center;
		justify-content: center;

		width: 100%;
		height: 100%;
	}

	.generate-tea-btn{
		position: fixed;
		z-index: 300;
		background: var(--secondary);
		padding: 10px;
		bottom: 20px;
		font-size: 50px;
		color: white;
		border-radius: 2px;
		border: 7px solid black;
		/* border-bottom: none;
		box-shadow: 7px 7px 0px 4px green; */
	}

	@media only screen and (max-width: 600px) {
		.generate-tea-btn {
			font-size: 30px;
		}
	}


	.content{
		position: fixed;
		z-index: 2;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100vw;
		height: 100vh;
	}

</style>