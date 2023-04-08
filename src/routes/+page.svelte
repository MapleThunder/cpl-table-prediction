<script lang="ts">
	import List from "./List.svelte";

	let items = [
		"Halifax Wanderers",
		"Atletico Ottawa",
		"York United",
		"Forge",
		"Valour",
		"Cavalry",
		"Pacific",
		"Vancouver",
	];

	function handleReorder(event) {
		items = event.detail;
	}
</script>

<main><List on:reorder={handleReorder} {items} /></main>

<style>
	main {
		max-width: 1000px;
		margin: 30px auto;
	}
</style>
