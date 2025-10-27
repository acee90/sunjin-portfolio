<!-- https://codepen.io/snorkltv/pen/azodrxB -->

<script>
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { onMount } from 'svelte';

	// gsap.registerPlugin(ScrollTrigger);

	let container = $state();

	onMount(() => {
		gsap.set('li > span', { transformOrigin: '0 50%' });
		gsap.set('li:not(:first-of-type) span', { opacity: 0.2, scale: 0.8 });

		const tl = gsap
			.timeline()
			.to('li:not(:first-of-type) span', { opacity: 1, scale: 1, stagger: 0.5 })
			.to('li:not(:last-of-type) span', { opacity: 0.2, scale: 0.8, stagger: 0.5 }, 0);

		ScrollTrigger.create({
			trigger: container,
			pin: true,
			scrub: true,

			start: 'center center',
			endTrigger: 'li:last-of-type',
			end: 'center center',

			markers: true,
			animation: tl
		});
	});
</script>

<div class="test-container">
	<div class="spacer" style="height:80vh;">Scroll Down</div>

	<div class="cols2" bind:this={container}>
		<h1>hello</h1>
		<ul class="rotator">
			<li><span>Akapowl</span></li>
			<li><span>Jack</span></li>
			<li><span>Cassie</span></li>
			<li><span>Rodrigo</span></li>
			<li><span>Shaun</span></li>
			<li><span>Mitchel</span></li>
			<li><span>Craig</span></li>
			<li><span>SHRUG</span></li>
			<li><span>Carl</span></li>
			<li><span>Jonathan</span></li>
			<li><span>Sahil</span></li>
			<li><span>Zach</span></li>
			<li><span>Blake</span></li>
			<li><span>Diaco</span></li>
			<li><span>DIPSCOM</span></li>
		</ul>
	</div>

	<div class="spacer" style="height:80vh; margin-top:80px; margin-bottom:0">The Bottom</div>
	<div class="brand" style="background:black; text-align:center;">
		<a
			href="https://www.creativecodingclub.com/bundles/creative-coding-club?src=scrollsnapcdpn"
			target="_blank"
			><img src="https://assets.codepen.io/32887/logo-ill.svg" width="300" alt="" /></a
		>
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Saira+Extra+Condensed:wght@800&family=Staatliches&display=swap');

	.test-container {
		font-family: 'Saira Extra Condensed', sans-serif;
	}

	li {
		scroll-snap-align: center;
		padding-left: 0.2em;
	}

	.spacer {
		color: #2d2d3f;
		display: flex;
		align-items: center;
		justify-content: center;
		background: #eaf3fa;
		margin-bottom: 80px;
		font-size: 40px;
	}

	li {
		/* IMPORTANT FOR THE SNAPPING */
		scroll-snap-align: center;
		padding-left: 0.2em;
	}

	li > span {
		display: inline-block;
	}

	.cols2 {
		padding-left: 20px;
		display: flex;
		/* outline:1px solid green; */
	}

	h1,
	ul,
	li {
		margin: 0;
		font-weight: 800;
		text-transform: uppercase;
		letter-spacing: 0.06em;
		line-height: 1;
		font-size: clamp(30px, 8vw, 60px);
	}

	h1 {
		/* background:#c6e6ff; */
		flex-grow: 0;
		align-self: flex-start;
	}
	ul {
		list-style-type: none;
		padding-left: 0;
		/* outline: 1px solid blue; */
	}

	ul,
	h1,
	li {
		margin: 0;
		line-height: 1;
	}
</style>
