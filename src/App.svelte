<script>
	import distinctColors from 'distinct-colors';
	import chroma from 'chroma-js';
	import ColorBlock from './ColorBlock.svelte';
	import Colornames from './Colornames.svelte';

	let colors;
	let colorCount = 25;
	$: mainColorString = colors.map((c) => c.main.name);

	const useWhiteText = (color) => {
		return chroma.contrast('black', color) < 4.5;
	};

	const colorPresets = {
		main: ['#2f4f4f', '#2e8b57', '#191970', '#8b0000', '#808000', '#ff0000', '#ff8c00', '#ffd700', '#ba55d3', '#00ff7f', '#0000ff', '#f08080', '#adff2f', '#ff00ff', '#1e90ff', '#dda0dd', '#ff1493', '#f5deb3', '#87cefa', '#7fffd4'],
		lesscolors: ['#191970', '#006400', '#ff0000', '#ffd700', '#00ff00', '#00ffff', '#ff00ff', '#ffb6c1'],
	};

	const colorData = (color) => ({
		name: color.name(),
		rgb: color.css(),
		whiteText: useWhiteText(color),
	});

	const formatColors = (palette) => {
		return palette.map((color) => {
			const clr = typeof color === 'string' ? chroma(color) : color;
			return {
				main: colorData(clr),
				darker: colorData(clr.darken(1.5)),
				lighter: colorData(clr.brighten(1.5)),
			};
		});
	};

	const generateColors = () => {
		var palette = distinctColors({ count: colorCount });
		colors = formatColors(palette);
	};

	generateColors();
</script>

<main class="container">
	<h2>Random colors</h2>
	<ColorBlock {colors} />
	<Colornames colors={mainColorString} />
	<input type="number" bind:value={colorCount} min="2" max="50" /> Number of colors
	<button type="button" class="btn btn-primary" on:click={generateColors}>Generate</button>

	<h2>Pregenerated sets</h2>
	<div class="accordion" id="accordionExample">
		<div class="accordion-item">
			<h2 class="accordion-header" id="headingOne">
				<button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
					20 colors (using {' '} <a href="https://mokole.com/palette.html">mokole</a>)
				</button>
			</h2>
			<div id="collapseOne" class="accordion-collapse collapse show" aria-labelledby="headingOne" data-bs-parent="#accordionExample">
				<div class="accordion-body">
					<ColorBlock colors={formatColors(colorPresets.main)} />
					<Colornames colors={colorPresets.main} />
				</div>
			</div>
		</div>
		<div class="accordion-item">
			<h2 class="accordion-header" id="headingTwo">
				<button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
					8 colors (using {' '} <a href="https://mokole.com/palette.html">mokole</a>)
				</button>
			</h2>
			<div id="collapseTwo" class="accordion-collapse collapse" aria-labelledby="headingTwo" data-bs-parent="#accordionExample">
				<div class="accordion-body">
					<ColorBlock colors={formatColors(colorPresets.lesscolors)} />
					<Colornames colors={colorPresets.lesscolors} />
				</div>
			</div>
		</div>
	</div>

	<h2>Other color generator tools</h2>
	<ul>
		<li><a href="https://colorbrewer2.org/">Color Brewer</a></li>
		<li><a href="https://medialab.github.io/iwanthue/">i want hue</a></li>
		<li><a href="https://mokole.com/palette.html">Visually Distinct Colors Generator</a></li>
		<li><a href="http://tristen.ca/hcl-picker/">Colorpicker for data</a></li>
		<li><a href="http://vis4.net/palettes/">Chroma.js Color Palette Helper</a></li>
	</ul>
</main>

<style>
	main {
		margin: 0 auto;
	}
</style>
