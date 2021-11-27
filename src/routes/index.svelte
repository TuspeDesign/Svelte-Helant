<script>
	import data from "../data.json";

	function parseHTML(e) {
		return e.replace(/\n/g, "<br />");
	}
</script>

{#if data}
	<section id="hero" class="relative">
		<div id="caption" class="grid">
			<div id="captionContent" class="self-center text-light">
				<h1>{data.site}</h1>
				<div class="content">{@html parseHTML(data.hero)}</div>
			</div>
		</div>

		<picture class="block">
			<source
				srcset="/hero-360.webp"
				media="(max-width:500px)"
				type="image/webp"
			/>
			<source
				srcset="/hero-360.jpg"
				media="(max-width:500px)"
				type="image/jpeg"
			/>
			<source
				srcset="/hero-768.webp"
				media="(max-width:768px)"
				type="image/webp"
			/>
			<source
				srcset="/hero-768.jpg"
				media="(max-width:768px)"
				type="image/jpeg"
			/>
			<source
				srcset="/hero.webp"
				media="(min-width:768px)"
				type="image/webp"
			/>
			<source
				srcset="/hero.webp"
				media="(min-width:768px)"
				type="image/webp"
			/>
			<img class="block" src="/hero.jpg" alt={data.photos.hero.alt} />
		</picture>

		<div id="action">
			<div id="actionContent" class="grid h-full container">
				<div class="content grid">
					<div class="self-center inline-block">
						<h3>{data.action.title}</h3>
						<span>{data.action.content}</span>
					</div>
				</div>
				<div class="button grid">
					<div class="self-center">
						<button>
							{data.action.button}
						</button>
					</div>
				</div>
			</div>
		</div>
	</section>

	<section id="services">
		<div id="servicesContent" class="container">
			<div class="title">
				<h2>{data.services.title}</h2>
				<div class="content">{data.services.content}</div>
			</div>

			<ul class="grid" aria-label="Palvelumme">
				{#each data.services.items as e}
					<li class="block">
						<h3>{e.title}</h3>
						<div class="content">{e.content}</div>
					</li>
				{/each}
			</ul>
		</div>
	</section>

	<section id="contact">
		<div id="contactContent" class="container grid">
			<div class="inner grid">
				<picture class="block">
					<source
						srcset={"/" + data.photos.contact.src + ".webp"}
						type="image/webp"
					/>
					<source
						srcset={"/" + data.photos.contact.src + ".jpg"}
						type="image/jpeg"
					/>
					<img
						class="block"
						src={"/" + data.photos.contact.src + ".jpg"}
						alt={data.photos.contact.alt}
					/>
				</picture>

				<div class="grid">
					<div class="self-center">
						<h3>{data.site}</h3>
						<div class="content">
							{data.contact.phone}<br />
							{data.contact.email}<br />
							{data.contact.street}<br />
							{data.contact.postal + " " + data.contact.area}
						</div>
					</div>
				</div>
			</div>

			<div id="contactMap">
				<iframe
					class="h-full"
					src={data.contact.map}
					title={data.contact.mapTitle}
				/>
			</div>
		</div>
	</section>

	<section id="reviews">
		<div id="reviewsContent" class="container">
			<div class="title">
				<h2>{data.clients.title}</h2>
			</div>

			<ul
				class="content"
				:aria-label={"Asiakaspalautetta yritykselle " + data.site}
			>
				{#each data.clients.items as e}
					<li class="inline-block">
						<div class="review">{@html parseHTML(e.content)}</div>
						<div class="reviewer">
							<span>{e.name}</span>
							{#if e.company}<span
									>{@html parseHTML(e.company)}</span
								>{/if}
						</div>
					</li>
				{/each}
			</ul>
		</div>
	</section>
{/if}

<footer id="creator" class="block">
	<a
		class="inline-block text-light"
		href="https://tuspe.com/"
		title="Tuspe Design - verkkosivustot ja verkkokaupat yritykselle"
		>Tuspe Design Oy</a
	>
</footer>
