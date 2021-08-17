<script>
import CanSvg from "./CanSvg.svelte";
import Fitty from "./Fitty.svelte";

export let text;

export let noOutline = false;
let newColors = []

export let primary;
export let secondary;

import colors from './css-colors';

let i = 0;
$: color = colors[i];

function nextColor(){
	i++
	console.log(color);
}

function delColor(){
	newColors.push(color)
	console.log(newColors);
}
</script>



<div class="can-container">
	<CanSvg {primary} {secondary}/>

	<div class="text-overlay grid ">
		<div class="grid-item mid">
			<span class="text primary">
				<Fitty {text} />
			</span>
		</div>
	
		<div class="grid-item bottom">
			<span class="text secondary">
				Dirt Tea
			</span>
		</div>
	</div>

</div>

<!-- <div class="shosh">
	<button on:click={nextColor} >Next color</button>
	<button on:click={delColor}>Take</button>
</div> -->


<style>
	.shosh{
		z-index: 3000;
		position: fixed;
	}
	.text-overlay{
		top: 0;
		left: 0;
		position: absolute;
		display: grid;
		grid-template-rows: 1fr 2fr 1fr;
		grid-template-columns: auto;
		grid-template-areas: 
			"top"
			"mid"
			"bottom";
		width: 100%;
		height: 100%;
		/* background: black; */
	}




	.can-container{
		position: relative;
		width: 400px;
		height: auto;
		display: flex;
		align-items: center;
		/* background: green; */
		max-width: 70vw;
	}

	.text{
		font-family: 'Comic Neue';
		font-weight: bold;
		color: white;
		font-size: 80px;
		width: 100%;
		text-align: center;
		opacity: .9;
		/* line-height: 0; */

	}

	.grid-item{
		display: flex;

		justify-content: center;
		align-items: center;
		width: 100%;
		height: 100%;
		min-width: 0;
		min-height: 0;

		padding-left: 30px;
		padding-right: 30px;
	}


	.grid-item.mid{
		grid-area: mid;
		/* background: orange; */
		/* background: blue; */
	}
	.grid-item.bottom{
		grid-area: bottom;
		/* flex-direction: column;
		justify-content: flex-start;
		background: purple; */
		align-items: flex-start;
		/* background: blue; */
	}

	.text.primary{

		/* -webkit-text-stroke: 2px black; */
		/* background: orange; */
		/* background: green; */

	}
	.text.secondary{
		font-size: 30px;
		/* background: red; */
		/* background: purple; */
	}




</style>