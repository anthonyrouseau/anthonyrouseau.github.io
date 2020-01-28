<script>
	import { Content } from '../content.js';
	import ContactSection from './ContactSection.svelte';
	import AboutSection from './AboutSection.svelte';
	import EducationSection from './EducationSection.svelte';
	import ProjectSection from './ProjectSection.svelte';
	import TechSection from './TechSection.svelte';
	import Cover from './Cover.svelte';
	import { quintOut } from 'svelte/easing';
	import { crossfade } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	let projects = Content.projects;
	let about = Content.about;
	let education = Content.education;
	let tech = Content.tech;
	let contact = Content.contact;
	let width;
	$: shouldCover = width >= 1200;

	let sections = [
		{
			key: "contact",
			section: ContactSection,
			data: contact,
			titles: {main: "Anthony Rouseau", sub: "Contact Info"}
		},
		{
			key: "about",
			section: AboutSection,
			data: about,
			titles: {main: "About Me"}
		},
		{
			key: "education",
			section: EducationSection,
			data: education,
			titles: {main: "Education"}
		},
		{
			key: "projects",
			section: ProjectSection,
			data: projects,
			titles: {main: "Projects"}
		},
		{
			key: "tech",
			section: TechSection,
			data: tech,
			titles: {main: "Tech Skills"}
		}
	];

	let original = sections.slice()
	$: if (!shouldCover){
		sections = original;
		document.body.classList.add("no-fun")
	}else{
		document.body.classList.remove("no-fun")
	}

	let positionMapping = ["mc", "tl", "tr", "br", "bl"]

	function swapPositions(index) {
		let copy = sections.slice();
		copy[0] = sections[index];
		copy[index] = sections[0];
		sections = copy;
	}

	const [send, receive] = crossfade({
		fallback(node, params) {
			const style = getComputedStyle(node);
			const transform = style.transform === 'none' ? '' : style.transform;

			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`
			};
		}
	});

	function flipAndScale(node, {from, to}, params) {
		const style = getComputedStyle(node);
		const transform = style.transform === 'none' ? '' : style.transform;
		const difX = from.width - node.clientWidth;
		const difY = from.height - node.clientHeight;
		const dx = (from.left - to.left);
		const dy = (from.top - to.top);

		const d = Math.sqrt(dx * dx + dy * dy);

		const {
			delay = 0,
			duration = (d) => Math.sqrt(d) * 50,
			easing = quintOut
		} = params;
		let factor;
		if (difX > 0) {
			factor = 1.66
		}else{
			factor = 0.6
		}

		return {
			delay,
			duration: duration(d),
			easing,
			css: (t, u) => `transform: ${transform} translate(${u * (dx + difX/2)}px, ${u * (dy + difY/2)}px) scale(${-(factor) * t * t + t + factor });`
		};

	}
</script>

<svelte:window bind:innerWidth={width}/>
<main>
	{#if shouldCover}
		<div class="background-layer"></div>
	{/if}
	{#each sections as section, index (section.key)}
		<div 
			class={`content loc-${positionMapping[index]}`}
			in:receive="{{key: section.key}}"
			out:send="{{key: section.key}}"
			animate:flipAndScale
		>
			{#if shouldCover && index !== 0}
			<Cover titles={section.titles} swap={() => swapPositions(index)}/>
			{:else}
			<svelte:component this={section.section} {...section.data} />
			{/if}
		</div>
	{/each}
</main>

<style>
	main {
		height: 100vh;
		width: 100vw;
		display: grid;
		grid-template-columns: auto;
		grid-template-rows: auto;
		overflow-y: scroll;
	}
	.content {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		height: 30vh;
		width: 100%;
		padding: 2% 5%;
		text-align: center;
		overflow-y: scroll;
		font-size: 1.5vw;
		-ms-overflow-style: none;
		font-size: 2vw;
		
	}
	.content::-webkit-scrollbar{
		display: none;
	}
	.loc-mc {
		position: relative;
		height: 30vh;
		overflow-y: scroll;
		background-image: url(https://images.unsplash.com/photo-1534190760961-74e8c1c5c3da?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1500&q=80);
		background-position: center -1vh;
		background-attachment: fixed;
		background-repeat: no-repeat;
		background-size: 100% auto;
		box-shadow: 0 3px 5px 3px #a9a9a9;
		font-size: 2vw;
	}
	.loc-br {
		min-height: 40vh;
	}
	.no-fun {
		animation: none !important;
		transition: none !important;
	}
	@media only screen and (min-width: 576px){
		.loc-mc {
			height: 50vh;
			background-position: center -5vh;
		}
	}
	@media only screen and (min-width: 768px){
		.loc-mc {
			height: 40vh;
			background-position: center -5vh;
		}
	}
	@media only screen and (min-width: 992px) {
	}
	@media only screen and (min-width: 1200px) {
		main {
			padding: 1vh 1vw;
			height: 98vh;
			width: 98vw;
			grid-template-columns: repeat(11, 1fr);
			grid-template-rows: repeat(11, 1fr);
			grid-template-areas: 
				"tl tl tl . tc tc tc . tr tr tr"
				"tl tl tl . tc tc tc . tr tr tr"
				"tl tl tl . tc tc tc . tr tr tr"
				". . . mc mc mc mc mc . . . "
				"ml ml ml mc mc mc mc mc mr mr mr "
				"ml ml ml mc mc mc mc mc mr mr mr "
				"ml ml ml mc mc mc mc mc mr mr mr "
				". . . mc mc mc mc mc . . . "
				"bl bl bl . bc bc bc . br br br"
				"bl bl bl . bc bc bc . br br br"
				"bl bl bl . bc bc bc . br br br"
		}
		.background-layer {
			height: 100%;
			width: 100%;
			position: fixed;
			top: 0;
			left: 0;
			background-image: url(https://images.unsplash.com/photo-1534190760961-74e8c1c5c3da?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1500&q=80);
			background-size: 100% 100%;
			filter: blur(3px);
			-webkit-filter: blur(3px);
			z-index: 0;
		}
		.content {
			position: relative;
			height: 100%;
			width: 100%;
			border-radius: 1em;
			opacity: 1;
		}
		.loc-tr {
			grid-area: tr;
		}
		.loc-tl {
			grid-area: tl;
		}
		.loc-mc {
			grid-area: mc;
			z-index: 1000;
			background: none;
			box-shadow: none;
			background-color: rgba(255,255,255,.7);
		}
		.loc-br {
			grid-area: br;
			min-height: 0;
		}
		.loc-bl {
			grid-area: bl;
		}
	}
</style>