<script lang="ts">
	// Props
	/** Exposes parent props to this component. */
	export let parent: any;

	// Stores
	import { getModalStore } from '@skeletonlabs/skeleton';
	const modalStore = getModalStore();

	// Form Data
	const index = $modalStore[0].meta.index;
	const data = $modalStore[0].meta.data;

	// We've created a custom submit function to pass the response and close the modal.
	function onFormSubmit(): void {
		if ($modalStore[0].response) $modalStore[0].response({index, data});
		modalStore.close();
	}

	// Base Classes
	const cBase = 'card p-4 w-modal shadow-xl space-y-4';
	const cHeader = 'text-2xl font-bold';
	const cForm = 'border border-surface-500 p-4 space-y-4 rounded-container-token';
</script>
{#if $modalStore[0]}
	<div class="modal-example-form {cBase}">
		<header class={cHeader}>Editing field {index}</header>
		<!-- Enable for debugging: -->
		<form class="modal-form {cForm}">
			<label class="label">
				<span>Example Data:</span>
				<input class="input" type="text" bind:value={data.example} placeholder="Enter example data..." />
			</label>
		</form>
		<!-- prettier-ignore -->
        <footer class="modal-footer {parent.regionFooter}">
            <button class="btn variant-filled" on:click={parent.onClose}>Cancel</button>
            <button class="btn variant-filled-primary" on:click={onFormSubmit}>Submit Form</button>
        </footer>
	</div>
{/if}