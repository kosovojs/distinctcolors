<script>
	export let colors;
</script>

<div>
	<div class="colors">
		<div class="color-block">
			<div class="color-box">Main</div>
			<div class="color-box">Darker</div>
			<div class="color-box">Lighter</div>
		</div>
		{#each colors as { main, darker, lighter }, i}
			<div class="color-block">
				<div class="color-box" style={`background-color: ${main.rgb}; color: ${main.whiteText ? 'white' : 'black'}`}>{main.name}</div>
				<div class="color-box" style={`background-color: ${darker.rgb}; color: ${darker.whiteText ? 'white' : 'black'}`}>{darker.name}</div>
				<div class="color-box" style={`background-color: ${lighter.rgb}; color: ${lighter.whiteText ? 'white' : 'black'}`}>{lighter.name}</div>
			</div>
		{/each}
	</div>
</div>

<style>
	.colors {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
	}

	.color-box {
		padding: 15px;
		width: 100px;
	}

	.color-block:not(:last-child) {
		margin-bottom: 1.5rem;
	}
</style>
