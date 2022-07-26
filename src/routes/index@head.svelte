<script>
	import { each } from 'svelte/internal';
</script>

<main>
	{#await fetch('https://fakestoreapi.com/products') then response}
		{#await response.json() then list}
			{#each list as { title, id, category, description, image, price, rating }}
				<div class="product card" data-id={id}>
					<img class="image" src={image} alt="" />
					<div class="title">{title}</div>
					<div class="price">{price}$</div>
					<button>Add to Cart</button>
				</div>
			{/each}
			{console.log(list)}
		{/await}
	{/await}
</main>

<style lang="scss">
	main {
		display: flex;
		flex-wrap: wrap;
		gap: 50px;
		// justify-content: center;
		padding: 30px 50px;
	}
	.product {
		&.card {
			.image {
				height: 100px;
				width: 100px;
			}
			.title {
				text-align: center;
			}
			button {
				padding: 0.2em 0.3em;
				border: 1px solid gray;
				border-radius: 3px;
				background-color: transparent;
				align-self: flex-end;
				cursor: pointer;
			}
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			align-items: flex-start;
			width: 250px;
			height: 270px;
			// background-color: rgba(128, 128, 128, 0.3);
			box-shadow: 0px 0px 4px 0.2px;
			padding: 20px;
			border-radius: 5px;
		}
	}
</style>
