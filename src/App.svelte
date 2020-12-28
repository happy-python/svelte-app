<script>
	import { cards } from "./store";
	import AddCard from "./AddCard.svelte";
	import CardList from "./CardList.svelte";
</script>

<style>
</style>

<main>
	{#each $cards as card, i}
		<CardList index={i} {...card} />
	{/each}
	<AddCard />
</main>
