<script lang="ts">
	import { getModalStore, type ModalSettings } from "@skeletonlabs/skeleton";
	import EditModal from "./EditModal.svelte";

	let dataArray = [
		{example: "test"},
		{example: "test2"},
		{example: "test3"},
		{example: "test4"},
		{example: "test5"}
	]
	const modalStore = getModalStore();
	function updateArrayData(response: { data: {example: string}, index: number}) {
		dataArray[response.index] = response.data;
	}

	const modalSettings: ModalSettings = {
		component: {
			ref: EditModal
		},
		type: "component",
		response: updateArrayData
	}
</script>

<div class="flex flex-col">
	{#each dataArray as data, index}
		<button class="btn variant-filled max-w-xs" on:click={() => {modalStore.trigger({...modalSettings, meta: { data, index}})}}>Edit Example {data.example} at index {index}</button>
	{/each}
</div>