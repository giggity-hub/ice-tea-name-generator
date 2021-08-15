<script>
import { onMount } from "svelte";
import pickRandom from 'pick-random';

	export let name;
	
	let dirTea;

	let adjectives;
	let foods;

	function timeout(ms) {
    	return new Promise(resolve => setTimeout(resolve, ms));
	}

	function generateTeaName(){
		let adj = pickRandom(adjectives);
		let food = pickRandom(foods);

		dirTea = adj + " " + food
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
</script>

<main>
	<button on:click={generateTeaName} >Generate Dir-Tea</button>
	<div>{dirTea}</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>