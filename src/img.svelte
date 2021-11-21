<script>
	export let name;
	export let alt = "";
</script>

<picture class="block">
	<source srcset={"/" + name + ".webp"} type="image/webp" />
	<source srcset={"/" + name + ".jpg"} type="image/jpeg" />
	<img class="block" src={"/" + name + ".jpg"} {alt} />
</picture>
