<script>
	import { onMount } from "svelte";
	export let apiKEY;
	// const apiKEY = "c8d240cd165a450b9a480bb6d6b0bd93";
	const dataUrl = `https://newsapi.org/v2/everything?q=javascript&sortBy=publishedAt&apiKey=${apiKEY}`;
	let items = [];
	const fetchData = async () => {
		const response = await fetch(dataUrl);
		const data = await response.json();
		console.log(data);
		items = data["articles"];
	};

	onMount(fetchData());
</script>

<h1>Daily News</h1>

<div class="container">
	{#each items as item}
		<div class="card">
			<img src={item.urlToImage} alt='news'/>
			<div class="card-body">
				<h3>{item.title}</h3>
				<p>{item.description}</p>
				<a href={item.url}>Read</a>
			</div>
		</div>
	{/each}
</div>

<style>
	h1 {
		color: purple;
		font-family: "kalam";
	}
	.container {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(305px, 1fr));
		grid-gap: 15px;
	}
	.container > .card img {
		max-width: 100%;
	}
</style>
