<template>
	<picture v-if="name && alt" class="block">
		<source :srcset="`/${name}.webp`" type="image/webp" />
		<source :srcset="`/${name}.jpg`" type="image/jpeg" />
		<img class="block" :src="`/${name}.jpg`" :alt="alt" />
	</picture>
</template>

<script>
	export default {
		name: "Photo",
		props: {
			name: {
				type: String,
				default: null,
			},
			alt: {
				type: String,
				default: null,
			},
		},
	};
</script>