<script lang="ts">
	// import { onMount } from "svelte";
	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();

	export let items: string[];

	function dragStart(event, index) {
		event.dataTransfer.setData("text/plain", index);
	}

	function dragOver(event: DragEvent) {
		event.preventDefault();
	}

	function drop(event, index) {
		const draggedIndex = event.dataTransfer.getData("text/plain");
		const item = items[draggedIndex];
		items.splice(draggedIndex, 1);
		items.splice(index, 0, item);
		dispatch("reorder", items);
	}
</script>

<ul>
	{#each items as item, index}
		<li
			draggable="true"
			on:dragstart={(event) => dragStart(event, index)}
			on:dragover={dragOver}
			on:drop={(event) => drop(event, index)}
		>
			<span class="table-position pos-{index}">{index + 1}</span>
			<span class="team-name">{item}</span>
		</li>
	{/each}
</ul>

<style>
	ul {
		list-style-type: none;
		margin: 0;
		padding: 0;
		width: fit-content;
	}

	li {
		border: 1px solid #ccc;
		margin-bottom: -1px;
		display: grid;
		grid-template-columns: 30px auto;
	}

	li > span {
		padding: 10px;
	}

	span.table-position {
		height: 100%;
		border-right: 1px solid #ccc;
	}

	.pos-0,
	.pos-1,
	.pos-2,
	.pos-3,
	.pos-4 {
		background-color: rgb(3, 98, 3);
	}
	.pos-5,
	.pos-6,
	.pos-7 {
		background-color: rgb(155, 14, 14);
	}
</style>
