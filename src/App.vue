<template>
	<section id="hero" class="relative">
		<div id="caption" class="grid">
			<div id="captionContent" class="self-center">
				<h1>{{ data.site }}</h1>
				<div v-html="parseHTML(data.hero)" class="content" />
			</div>
		</div>

		<Photo :name="data.photos.hero.src" :alt="data.photos.hero.alt" />

		<div id="action">
			<div id="actionContent" class="grid h-full container">
				<div class="content grid">
					<div class="self-center inline-block">
						<h3>{{ data.action.title }}</h3>
						<span>{{ data.action.content }}</span>
					</div>
				</div>
				<div class="button grid">
					<div class="self-center">
						<button>
							{{ data.action.button }}
						</button>
					</div>
				</div>
			</div>
		</div>
	</section>

	<section id="services">
		<div id="servicesContent" class="container">
			<div class="title">
				<h2>{{ data.services.title }}</h2>
				<div class="content">{{ data.services.content }}</div>
			</div>

			<ul class="grid" aria-label="Palvelumme">
				<li
					v-for="(e, i) in data.services.items"
					:key="i"
					class="block"
				>
					<h3>{{ e.title }}</h3>
					<div class="content">{{ e.content }}</div>
				</li>
			</ul>
		</div>
	</section>

	<section id="contact">
		<div id="contactContent" class="container grid">
			<div class="inner grid">
				<Photo
					:name="data.photos.contact.src"
					:alt="data.photos.contact.alt"
				/>
				<div class="grid">
					<div class="self-center">
						<h3>{{ data.site }}</h3>
						<div class="content">
							{{ data.contact.phone }}<br />
							{{ data.contact.email }}<br />
							{{ data.contact.street }}<br />
							{{ data.contact.postal + " " + data.contact.area }}
						</div>
					</div>
				</div>
			</div>

			<div id="contactMap">
				<iframe
					class="h-full"
					:src="data.contact.map"
					:title="data.contact.mapTitle"
				/>
			</div>
		</div>
	</section>

	<section id="reviews">
		<div id="reviewsContent" class="container">
			<div class="title">
				<h2>{{ data.clients.title }}</h2>
			</div>

			<ul
				class="content"
				:aria-label="`Asiakaspalautetta yritykselle ${data.site}`"
			>
				<li
					v-for="(e, i) in data.clients.items"
					:key="i"
					class="inline-block"
				>
					<div class="review" v-html="parseHTML(e.content)" />
					<div class="reviewer">
						<span>{{ e.name }}</span>
						<span v-if="e.company" v-html="parseHTML(e.company)" />
					</div>
				</li>
			</ul>
		</div>
	</section>
</template>

<script>
	import json from "./data.json";
	import Photo from "./components/img.vue";
	export default {
		name: "App",
		components: {
			Photo,
		},
		data() {
			return {
				data: json,
			};
		},
		methods: {
			parseHTML(e) {
				return e.replace(/\n/g, "<br />");
			},
		},
	};
</script>

<style>
	@font-face {
		font-family: montserrat;
		src: url("/montserrat-light-webfont.woff2") format("woff2"),
			url("/montserrat-light-webfont.woff") format("woff");
		font-weight: 300;
		font-style: normal;
		font-display: swap;
	}
	@font-face {
		font-family: montserrat;
		src: url("/montserrat-bold-webfont.woff2") format("woff2"),
			url("/montserrat-bold-webfont.woff") format("woff");
		font-weight: 700;
		font-style: normal;
		font-display: swap;
	}

	:root {
		--blue: rgb(0, 108, 141);
		--white: #fff;
		--light: rgba(255, 255, 255, 0.87);
	}
	body {
		font: 300 16px montserrat, Verdana;
		color: #333;
		line-height: 1.5;
	}
	html,
	body,
	ul,
	h1,
	#action h3,
	#reviews h2,
	#contact h3 {
		margin: 0;
	}
	h1,
	h2,
	h3 {
		font-weight: 700;
	}
	h1,
	h2 {
		line-height: 1.2;
	}
	#services h3 {
		font-size: 1.2rem;
	}
	#contact h3 {
		font-size: 1rem;
	}
	ul {
		padding: 0;
	}
	h1,
	h2 {
		font-size: clamp(2rem, 2.4rem, 8vw);
	}
	a,
	h2 {
		color: var(--blue);
	}
	.title,
	#services li {
		text-align: center;
	}
	.title {
		max-width: 640px;
		margin: 0 auto 3rem;
	}
	h1,
	#services h2,
	#services h3,
	.review {
		margin: 0 0 15px;
	}
	section:not(#hero) {
		padding: 3rem 1.5rem;
	}
	.container {
		margin-left: auto;
		margin-right: auto;
	}
	.container:not(#actionContent) {
		max-width: 1200px;
	}
	.block {
		display: block;
	}
	.inline-block {
		display: inline-block;
	}
	.grid {
		display: grid;
	}
	.self-center {
		align-self: center;
	}
	#hero {
		height: 100vh;
	}
	#caption,
	#hero picture {
		height: 85vh;
	}
	#action {
		height: 15vh;
		background-color: var(--blue);
	}
	#caption {
		position: absolute;
		top: 0;
		left: 0;
		background-color: rgba(0, 0, 0, 0.4);
	}
	#action,
	#caption h1 {
		color: var(--white);
	}
	#caption .content {
		color: var(--light);
	}
	html,
	body,
	#caption,
	#hero img {
		width: 100vw;
		overflow-x: hidden;
	}
	#hero img,
	.h-full {
		height: 100%;
	}
	#hero img,
	iframe {
		object-fit: cover;
	}
	iframe {
		width: 100%;
		border: 0;
	}
	#captionContent {
		margin-left: 10vw;
		max-width: 600px;
	}
	#actionContent {
		max-width: 700px;
		gap: 2rem;
	}
	#actionContent button {
		border: 0;
		color: var(--white);
		background: #ea7d00;
		padding: 15px 40px;
		font-size: 1.2rem;
		text-transform: uppercase;
		border-radius: 10px;
	}
	#services ul,
	#contactContent {
		gap: 2.5rem;
	}
	#contactContent .inner {
		gap: 1.2rem;
	}
	#services li .content {
		font-size: 0.9rem;
	}
	#contact img {
		border-radius: 50%;
	}
	#reviews {
		background-color: #f2f2f2;
	}
	#reviews li {
		background-color: var(--white);
		border: 1px solid #999;
		border-radius: 10px;
		padding: 25px;
		-webkit-box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, 0.15);
		-moz-box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, 0.15);
		box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, 0.15);
	}
	img {
		max-width: 100%;
	}
	@media screen and (min-width: 550px) and (max-width: 1100px) {
		#services ul {
			grid-template-columns: repeat(2, 1fr);
		}
	}
	@media screen and (min-width: 750px) {
		#contactContent {
			grid-template-columns: 400px 1fr;
		}
		#contactContent .inner {
			grid-template-columns: 170px 1fr;
		}
		#actionContent {
			grid-template-columns: 1fr 1fr;
		}
		#action .content {
			text-align: right;
		}
	}
	@media screen and (min-width: 550px) and (max-width: 1100px) {
		#services ul {
			grid-template-columns: repeat(2, 1fr);
		}
	}
	@media screen and (min-width: 1000px) {
		#reviews ul {
			width: 100%;
			-moz-column-count: 2;
			-moz-column-gap: 20px;
			-moz-column-width: 12vw;
			-webkit-column-count: 2;
			-webkit-column-gap: 15px;
			-webkit-column-width: 12vw;
			column-count: 2;
			column-gap: 15px;
			column-width: 12vw;
			margin-bottom: -1rem;
		}
		#reviews li {
			margin-bottom: 1rem;
		}
	}
	@media screen and (min-width: 1100px) {
		#services ul {
			grid-template-columns: repeat(4, 1fr);
		}
	}
</style>
